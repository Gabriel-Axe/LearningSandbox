---
layout: post
draft: false
title:  "Note Taking as a Thinking Tool"
---

One of the hardest things to manage in life is knowledge, since there is too many things to learn out there and too many things that call our attention. 

And perhaps, even learning a single subject deeply or well enough to be considered an "expert" can be hard, considering that the more deep the knowledge is, the more people had to learn to get there. You can't engineer a rocket after learning basic arithmetic.

If you asked me, the biggest problem I found in my learning journey is relying on my limited mind.

Sorry if this feels "once I understood the weakness of my flesh", but even if you have not ADHD, learning in a way that works with our brain is not the easiest thing to stumble into, let alone learn.

The way I was "conditioned" to learn is to simply read a book, and read again if I had doubts. Just read it and do the exercises and you will be fine. Either you get it, or you don't get it. And if you don't get it, you are a dum dum.

Sure, that works on a math book that has 3 paragraphs explaining how to divide and some problems right after, but once you are reading a operating systems or a networks book, that ain' gonna work lil bro.

And with great learning demands (university), comes great solutions. Behold, my current note taking (and knowledge management) system.

### Note Taking as a Thinking Tool

In the past, I have seen note taking as a storage tool, perhaps even a summarization one, that only forgetful people needed.

It just so happens that nowdays I'm the most forgetful person in every room.

But note taking is not just for knowledge storage, but also for self-learning, idea generation and a easy bit of production for those who consume too much.

Maybe you ever heard of the Feymann techinique if you ever become interested in learning before.

In short, it's a techinique where you learning by teaching and helping others. And it just so happens that in note taking, you are writing stuff down to help someone else: yourself.

The reason it works is because it forces you to see where you explanation is lacking, and to strentghen what you already know, explaning in a simple matter. After all, like Einstein said:

> [!QUOTE] If you can't explain it simply, you don't understand it well enough

To learn effectively is to know the subject deeply, and to know the subject deeply is to know how to explain it's essence, and notes encourage that philosophy given that you trim stuff down, your notes will be a mess and hard to read, which is a common thing when you are having many ideias per day.

Fortunately, there is a way to mitigate that, to left your notes in pristine qualities while continuing to aquire new ideias.

And the forgeting to do something does not apply only for complex machinery or abstract math. How many programmers joke about having to search how to create a list?

### Fleeting Notes

Ideias come and go, but the ones that survive make it through the short term memory incinerator.

Far too many ideias drown in the sea of thoughts and distractions. To learn effectively is to not let ideias escape.

To store ideas I have, books I read or organize annotations I use what is commonly called "fleeting notes". These notes are a mess, and have a bit of everything: links, tables, code blocks, book excerpts... 

The purpose is not to read them, but to store them until I have time and interest in working on that piece of knowledge.

Besides, for better use of your notes, keeping their tidy and concise is a must, and so storing fleeting notes separate from permanent notes is a pretty good pratice.

As a means of example, a small snippet of what a fleeting note may look like:

`note_taking_-_proc.md`
```md
#### Parents

Todo note possui conexão apenas com os seus "parents", pais.

Por exemplo, [[Machine_Learning]] possui conexões com:

- "[[Programing]]"
- "[[Computer_Science]]"

No entanto, muitos destes possuem conexões com [[Math]], porém [[Machine_Learning]] não é algo que se compôe/se constrói diretamente da [[Math|matemática]], mas de assuntos próximos/compostos diretamente da [[Math|matemática]].

#### Snippets

### Benefícios de *Sufixos*:

+ Todas as anotações ficam localizadas na mesma pasta, no root da vault, facilitando encontrar anotações em sistemas de busca não recursivos
+ É possível encontrar todas as anotações que recorrem um tema em comum fácilmente apenas pelo primeiro nome
+ Fácil de começar e de mudar pra outra opção

### Malefícios de *Sufixos*:

- Pode ser ser relativamente não agradavel estéticamente quando lendo a anotação
```

Yea, not the brightest tool in the shed.

Once I do have the time and interest, I refine them until they come about in a note such as this:

`Content_Creation.md`
```md
Eu priorizo projetos por meio de PMD:

- Paixão, o quão gostado é esse assunto para quem gosta
- Mainstream, o quão popular esse assunto é
- Dificuldade, o quão díficil é fazer sobre este assunto

| Valor | Paixão | Mainstream | Dificuldade |
| --------------- | --------------- | --------------- | --------------- |
| 1 | Pessoas que gostam gostam MUITO       | Literal todo mundo conhece | Muito fácil            |
| 2 | É bastante popular entre quem conhece | Bastante conhecido         | Fácil                  |
| 3 | Não é lá, tão amado assim             | Cult                       | Complicado             |
| 4 | Ninguém se importa com isso         | 0 pessoas sabem o que é    | Mais dificil impossivel|

Também categorizo idéias em quais canais de comunicação público este projeto:
- A: ambos
- B: blog apenas
- V: video apenas
- D: não sei

Isto gera um artefato como este:

- a123 - Exemplo de projeto
```

### Zettelkasten

There are also those that like to use it to distilate confusing and abstract ideias, not much different as one does from their emotions into a journal. ([[2026-06-05-note-taking#Zettelkasten]])

I would like to highlight one last thing before we end.

To cut to the chase, there is a style of note taking where you link ideas, much like Wikipedia, and this can help in many ways, such as connecting 2 pieces of knowledge, make shorter notes and even organize them.

In case the name is of interest, such style is called Zettelkasten.

Say you have a lisp note:

```md
Lisp é uma das linguagens mais antigas do mundo. [[Lisp]] ~é~ costumava ser a linguagem mais popular para programação de [[Artificial_Inteligence]].

Lisp é capaz de criar novas linguagens para solucionar um problema, além de ser um dos poucos linguagens com flexibilidade de definir e manipular programas e dados.
```

Considering that Lisp has concepts that are used extensively in compilers, artificial inteligence (I think) and virtual machines (again, I think), you could create links to those subects to Lisp.

Anoter example:

`Systems.md`
```md
### Lazy over Eager

Perdão pelo inglês americano, mas aqui empresto conceitos da [[Computer_Science|ciência da computação]], especificamente [[Programing_Terms#Lazy]] e [[Computer_Science#Eager]].

Um sistema "lazy" é aquele onde recursos, incluindo tempo, energia e [[Cognitive_Power|poder cognitivo]] não são gastos a toa, ou sequer necessários para utilizar o sistema (bem, talvez tempo seja uma exceção).
```

This style of note taking is already well supported by the mainstream note apps that exist nowdays, like [Obsidian](https://obsidian.md/), One Note and even Notion, among some open source alternatives, like [Trilium](https://triliumnotes.org/).
