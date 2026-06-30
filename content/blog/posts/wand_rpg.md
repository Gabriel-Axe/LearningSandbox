---
title: "My RPG Backend with Go"
draft: false
---

In the last few days, I have been working on a personal project, not that far-fetched for a begginer in a programming language: a backend server for a RPG game. 

However, this one is... if not good or special, it is certainly is inovative.

To cut to the chase, I made a RPG based in one of my favorite games, [Noita](https://store.steampowered.com/app/881100/Noita/). The project can be found [here](https://github.com/Gabriel-Axe/Wand_RPG).

Anyway, let's begin.

## Context

In Noita, you are a wizard that uses wands to become death, destroyer of worlds.

And yourself.

{{< youtube jtxxuAjIQ9s >}}

The main magic of the game is that spells can be combined into ever more powerful spells. 

For example, you can take a simple spell that behaves like a magical arrow, and combine with the chainsaw spell. The chainsaw spell reduces the time between spells in the wand.

The result is a wand that behaves like a tommy gun. Now the wand goes brrrrrrr.

{{< youtube G1zvPQlqV50 >}}

Add enough time, patience and luck, and you go from this:

{{< youtube fI6eXnvOLgQ >}}

To annihilation on a stick:

{{< youtube gngbu8yEtiQ >}}

And that's just the tip of the iceberg (that I'm creative enough to make). There are thousands of ways to break this game.

## Why Go

First off, because it's simple. While I do find a bit nice the OOP aproach, I find there are too many ways to build something that is a nightmare to maintain, or even expand without exploding in complexity, oh and I say this when talking about C#. 

I won't even dare to touch Java because, 90% of the available jobs with it are based on Springboot, and I tried my fair share of Springboot, and trust me as a low-end laptop neovim dev: I never want to touch Springboot ever again.

And I could use Python or Javascript, or even Typescript. Then again, I could also stab my hands with a fork, given how frequently and undecisive I'm with my data structures, leading to lots of refactors, which these 2 (except Typescript) are not friendly towards, specially given how complex is the vision motivating the project.

Perhaps I could also have tried my hand on something more experimental, like Elixir, or maybe Haskell, maybe even Lua given it can do web stuff, but I didn't, because of the benefits Go brings to the table.

tldr: I like Go.

First off, I want a job, if my rambling about Java may not have made this clear, and as time goes on, Go becomes a increasingly demanded language, at least in my vision.

The second reason, and this one is techinical, is that Go is optmized for the kinda stuff we are looking towards, particulary the fact it's designed with first class concurrency, meaning it can run many threads and communicate within then with a ease other languages do not have acess to. That is a particulary important thing when you want to eventually make a server and have many games undergoing at the same time.

And the final reason, it's simple, really simple. There aren't many reasons to do things, like with OOP based langs, which means there are less ways to shoot your future self or reduce analysis paralisis, and it's really easy to read the code once you know the language. I read horror stories about inheritance and God forbid, obscure language features. If there is one thing does well, is that it doesn't try to sound genius, it just try to not look dumb

But enough talk, let's talk about my piece of appreciation for this game, perhaps you could even call a fangame.

## The Design

The project is a turn-based RPG where being a mage ~is~ will be extremely broken, essentially a pokemon with sprinkles of Noita.

Currently it has this structure:

```
.
├── attacks.go
├── combat.go
├── combat_structs.go
├── combat_test.go
├── coverage.out
├── effects.go
├── effects_structs.go
├── effects_test.go
├── go.mod
├── http.go
├── http_structs.go
├── interfaces.go
├── items.go
├── items_structs.go
├── items_test.go
├── main.go
├── modifier.go
├── README.md
└── utils.go
```

But that's kinda boring, so to cut to the chase, there are 3 things I want to share with you, these 3 being the most hard, most interesting, and most time consuming parts of the project as of the commit `b626d08`. These 3 things being the Groups, the Modifiers and the Wands.

## The Groups

Do you know that moment in games where you are cornered 5 to 1, and you somehow scapes? Happens all the time in Noita.

However, developing a positioning system in a RPG is a... let's say, not "beginner-friendly".

Because of my severe skill issues, combined to my stubborness into not developing any kind of graphic or UI for this game until absolutely needed (or developing the game "headless"ly), I came up with a system that allows for both abstracting that kinda situation into a turn-based RPG *and* allows for more interations with the probable future systems of the game.

This is the struct of the units (summarized):

```go
type Unit struct {
    // ...
    Health int
    MaxMana int
    ManaPool int
    Team *Team
    Group *Group
    IsDefending bool
    // ...
}
```

Every unit must belong to at least 1 group.

A group is nothing more then a possible conglomerate of units in space. In short, it says where units are relative to each other without having to create a complex system of location in a turn-based RPG, like a hexagonal map.

```go
type Group struct {
	Units []*Unit
}
```

For example, you have group A with 3 units and group B with 5. All units of A are near each other, and so are units of B to other units of B, but every unit of A is far from the units of B.

It's a simple system, but it seems to work relatively well for what I need now.

This implementation allows for 2 things: creating a distance data for attack ranges and allow attacks to damage more then 1 unit without doing arbitrary RNG shenanigans and as such, attacks are more then just "cut" and "apply poison".

```go
type AttackRange int
const (
	RangeShort AttackRange = iota
	RangeLong
	RangeBoth
)

// ...

func CalculateFinalDamage(attacker *Unit, defender *Unit, attackRange AttackRange, attack_damage int) int {
    // ...
    switch attackRange {
        case RangeShort:
            if attacker.Group != defender.Group {
                final_damage = (final_damage * 50) / 100
            }
        default:
            break
    }
    // ...
}
```

## The Modifiers

Modifiers are the direct equivalent to Noita modifiers. They modify how a spell is delivered or perhaps, what happens after, allowing for spells to behave in  much more interesting ways then just applying it on a friend or damaging a foe. 

You could have a modifier that when applied, pass it's effects to the whole group while the "host" is alive, or you could have an modifier that makes "chain" attacks, or even an modifier that duplicates it's spells.

```go
type Modifier interface {
	Apply(attack *Attack) []*Attack
	GetDescription() string
}

func (m *DuplicateModifier) Apply(attack *Attack) []*Attack {
	attack.PopModifier()
	clone := attack.Clone()

	return []*Attack{attack, clone}
}
```

This is a incomplete system, and if not designed correctly, extremely broken, but certainly, a fun one. Aside from making the game really fun and a mess to balance, it's also really ambiguous, since many modifiers could also be argued to be a status effect (stuff like burning, freezing), and the same for the other way around.

## The Wands

And last but not least, the star of the show.

Let's start with wands. They are suposed to be items that amplify a mage capability, enabling him to use spells much stronger then the ones he can do by hand, and in that sense, this struct allows for such a design:

```go
type Wand struct {
	Item
	Spells []Attack
	ManaCost int
}
```

Previously, I put mana in the wand, so that the spell used the wand mana, but that would allow for any unit to use magic, so instead I added a `ManaCost` atribute that tracks the total price of the spell, following the design decision of wands amplifying mages power as well.

Another thing I would like to point is that, as stated previously, wands are, or are suposed to, be the only way to use modifiers.

But at the moment, modifiers are part of attack, so theorically every attack could have a modifier, but as time goes on, I'll create a dedicated struct for spells, so that it is easier to make support spells like healing or invisibility.

## Final Words

I hope this project of mine, if hasn't made you interested in Noita or complex magic systems, at least remind you that programming is as much of an art process as painting is.

This whole endeavor started with a question of "could I", and so did many of humanity's wonders. And would you look at this, although I'm still starting out, it's actually kinda working, but alas, there's still a lot more work to do, like testing the system manually instead of relying on unit testing to see if it's actually fun and not just works as intended.

In any case, hope to see you soon.
