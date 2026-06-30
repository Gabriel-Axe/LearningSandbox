---
layout: post
draft: false
title:  "My Experience with Go"
---

Go is a really minimal language, that combine things from the low level of [C](), together with some concepts of higher levels, such as [Python] or [Java], to essentially create a language that stays out of your way as much as possible, while not sacrificing much in terms of performance, or even aiding with that.

I'll not talk about the basics of the language here, since, I guess this is not a tutorial, but I'll show some stuff that is particulary interesting for me (don't worry, it will be like, 3 or 4).

## Structs

Go, much like C, and I think, [C], and other languages, makes usage of structs. Structs are a way to hold related data together, and perhaps take advantage of the concept of locality in cache from the hardware, but I'm not sure yet.

```go
type player struct {
    ID   int    
    Name string 
    Team []*Unit
}
```

In any case, there's not much to talk about it alone, since structs for me only become really powerful (as a begginer of what, 3 or 4 days of Go?) once you combine them with [[2026-06-02-go#Interfaces]].

## Interfaces

Interfaces are, just like in every other programing language that has interfaces, a way to define a contract. Speaking in human readable way, it is a mean to say "here is what you have to give to me, here is what I give you". 

Anyone (like a class) that implements the interface, is guaranteed to use/take the parameters (things you give) and give you the result (things you get), hence why dynamic languages don't have interfaces.

In Go, this is an interface:

```go
type Effect interface {
	Apply(target *Unit, attacker *Unit, attack *Attack) error
}
```

This interface is used by any effect (stuff like fire, cold, weak...), and has just 1 function (for now): apply the effect. From there, I think you can deduce the rest.

In any case, once we have both a struct and a interface, we can combine both to make scalable and readable code such as this (as I hope as I paste this):

```go
func (p FreezeEffect) Apply(target *Unit, attacker *Unit, attack Attack) error {

	err := DeductMana(attacker, &attack)
	if err != nil {
		return  err
	}

	target.Effects = append(target.Effects, StatusEffect{
		Type: "freeze",
		Slowdown: p.Slowdown,
		Duration: p.Turns,
	})
	return  nil
}
```

## HTTP

Go is concise, and that is reflected on how much you need to make a HTTP server (as in, use the builtin libraries to make a server with endpoints, not built it from scratch...):

```go
func main() {

	http.HandleFunc("/ping", pong)
	http.HandleFunc("/game/start", HandleGameStart)
	http.HandleFunc("/game/status", HandleGetGameStatus)
	http.HandleFunc("/game/turn/pass", HandlePassTurn)
    // [...]
}
```

`http.HandleFunc`, combined with a function such as:

```go
func HandleGameStart(w http.ResponseWriter, req *http.Request) {

	if currentGame != nil {
		fmt.Fprintf(w, `{"error": "Game already begun"}`)
		return
	}

	currentGame = QuickGameSetup()
	json.NewEncoder(w).Encode(currentGame)
}
```

Is all that you need to make to make a endpoint.

## Testing

This one is the last one I would like to show.

In Go, tests are located in files such as `combat_test.go` for `combat.go`, and contain code such as this:

```go
func TestToggleDefend(t *testing.T) {
	g := QuickGameSetup()
	logGameState(t, g)
    // [...]
	t.Logf("Defender health after: %d", d.Health)
    if before == after {
        t.Fatalf("health didn't change: before=%d, after=%d", before, after)
    }
}
```

And then, you input:

```bash
go test -v
```

And get:

```txt
=== RUN   TestApplyEffect
    effects_test.go:11: Turn: 1
    effects_test.go:11: Attacker[0]: health=70, defending=false
[...]
2026/05/26 18:45:53 Processing effects
2026/05/26 18:45:53 Advancing turn
2026/05/26 18:45:53 Swapping attacker and defender
2026/05/26 18:45:53 Recharging mana
[...]
--- PASS: TestApplyEffect (0.00s)
=== RUN   TestManaUsage
[...]
--- PASS: TestManaUsage (0.00s)
=== RUN   TestRecharge
[...]
--- PASS: TestRecharge (0.00s)
PASS
ok      wand_rpg        0.002s
```

And that's all I wanted to show, for now, about the language itself. As I develop the project, I'll be updating this with some interesting things I ffound while creating it.

Really love when my programing language comes with stuff builtin and I don't have to question my sanity and my IDE if it's me or if the builders of the testing library have done something wrong, if the language tooling is genuinely bad or even all 3 ([like some languages](https://www.java.com/en/)).
