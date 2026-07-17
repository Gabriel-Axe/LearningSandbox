---
layout: post
draft: true
title: 'To be Decided'
---

Springboot is a pain in the ass to use.

There, I said it.

I hate Springboot.

The fact is, that most of the hate that is given to Java, should instead be aimed at Springboot, and I'll stand by this fact. Not opnion, fact.

Here's why.

## Tooling Dependence

First off, if there is one thing you will be recieved with when asking advice on starting with this damnmed framework, it will be:

- "Install a IDE"

This normally is standard advice, in like, 90% of the projects and framework, but generally, that is not necessary. 

Springboot is different. Of course it is. Why else would it have so many jobs? Because no one wants to deal with it. Well, no one didn't want, before this AI crazy, where language still mattered.

Coming back to the IDE, the main reason to Springboot being... workable, with a IDE, it's because of...

> Runtime... programing? idk the word

Yes, youg read it right. Java, the language oftypes and OOP and all the nice things, can be runtime depended, just like Python or Javascript.

Do you realize how much of a issue just that is?

In Springboot, you have code such as this:

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByEmail(String email);
}
```

This is suposed to find a user by email. You can think of the code above like the one bellow:

```python
tipo = s \
       .query(TipoAnimal) \
       .where(TipoAnimal.id == animal.tipo_animal_id) \
       .first()
```

Oh, wait a second, why did I had to send a simpler example? Maybe because... **The framework is dependent on the literal function name**?

Yes, that's right, in Springboot, there are, in some cases, that you use interfaces that their function is used by their name.

Let me ask this small little question: **WHY**?

Was it too hard to make like flask (the other "get this object by this data" code)? Does the price of making it this... abomination?

This. This is why Springboot requires a IDE. Implicit programing. The moment that I typed that findBy was the moment I want to throw my laptop out the window and live as a farmer.

Unfortunately I don't have the money for neither finance a farm, nor do I have some land or property to let alone start one, so by all means, let's go right ahead.

## Memory Constraints

To play the devil's advocate, granted, this can be a issue with java (and all the tooling related to it). Apparently Java, and it's cooler brother C#, can be configured into using less memory, more eficient data structures and memory usage, and some other niceties. And apparently Java vm is a gorilla butt of default settings (compared to C#), buuut... it's there. 

But it still doesn't excuse the fact that, since it requires a IDE, and proper IDE's are expensive, that's half of your memory in your computer just to EDIT the damn thing.

And don't even get me started on the browser... It's almost like you HAVE to have firefox (or zen in my case) and suspend almost every tab in order to, idk, use postman in case you are a skill issue, or are testing the frontend to your "fullstack project".

And brother, let me tell you the stack traces. Oh dear Lord, look at those stack traces. You can almost write the bible of Java from jut the stack traces printed from missing a l in that `findByEmail`.

Ok, maybe... it wasn't that much that I hated about Springboot. Maybe, the perfect framework doesn't exist. Maybe the perfect tool was the friends we make along the way. Exactly. Make your friends write Springboot for you, then open a startup. Then use venture captalist money to drive off the competition. Then loby the government. Then cause mass mental health issues. Then in your death bed, rewrite everything in rust. It's genious. And blazingly fast.
