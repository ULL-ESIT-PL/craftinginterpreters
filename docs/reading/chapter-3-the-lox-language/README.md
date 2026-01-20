# Reading Chapter 3: The Lox Language

## Instructions

We open the file with the markdown for chapter 3 [book/the-lox-language.md](/book/the-lox-language.md) and visit http://localhost:8000/the-lox-language.html.

Being at the root of the project, [once we have built the C interpreter](/docs/README.md), we run:

```sh
➜  craftinginterpreters git:(casiano) ✗ export PATH=$PATH:`pwd`
➜  examples git:(casiano) ✗ clox
> print(2+3);
5
> ^D
```

## Hello, Lox! 3.1

Read Section [3.1](https://craftinginterpreters.com/the-lox-language.html#hello-lox).

See [docs/reading/chapter-3-the-lox-language/examples/hello.lox](/docs/reading/chapter-3-the-lox-language/examples/hello.lox)

```
➜  examples git:(casiano) ✗ clox hello-world.lox
Hello, world!
```

See also how the comment in the book at [/book/the-lox-language.md](https://raw.githubusercontent.com/ULL-ESIT-PL/craftinginterpreters/refs/heads/casiano/book/the-lox-language.md) is [rendered on the right side](https://craftinginterpreters.com/the-lox-language.html#hello-lox), and the source markdown:

````markdown
Here's your very first taste of <span name="salmon">Lox</span>:

<aside name="salmon">

Your first taste of Lox, the language, that is. I don't know if you've ever had
the cured, cold-smoked salmon before. If not, give it a try too.

</aside>
```` 

The word **lox** also means a type of cured, cold-smoked salmon, very common in Jewish / American cuisine,
often eaten on bagels with cream cheese

## A High-Level Language 3.2

Read Section [3.2](https://craftinginterpreters.com/the-lox-language.html#a-high-level-language).

I found the comment 

> Lox’s approach to scoping hews closely to Scheme. 

See [docs/reading/chapter-3-the-lox-language/schemescoping-versus-javascriptscoping.chatgpt.md](/docs/reading/chapter-3-the-lox-language/schemescoping-versus-javascriptscoping.chatgpt.md) for an explanation by ChatGPT of the difference between JavaScript scoping and Scheme scoping.

## Expressions 3.4

## Comparison and equality 3.4.2

```sh
➜  examples git:(casiano) clox operator/comparison.lox                                
true
false
false
true
true
false
false
false
true
false
true
true
false
false
false
false
true
true
true
true
```

## Functions 3.80

### Closures 3.8.1

Curious, the aside about closures and Landin:

````markdown
<aside name="closure">

Peter J. Landin coined the term "closure". Yes, he invented damn near half the
terms in programming languages. Most of them came out of one incredible paper,
"[The Next 700 Programming Languages][svh]".

[svh]: https://homepages.inf.ed.ac.uk/wadler/papers/papers-we-love/landin-next-700.pdf

In order to implement these kind of functions, you need to create a data
structure that bundles together the function's code and the surrounding
variables it needs. He called this a "closure" because it *closes over* and
holds on to the variables it needs.

</aside>
````

Landin introduces the term "closure" in his 1966 paper ["The Mechanical Evaluation of Expressions"](https://jhc.sjtu.edu.cn/~yutingwang/files/fp/landin-1964.pdf) (not in "The Next 700 Programming Languages", which came later in 1966).
The following excerpt from the paper describes the concept of closure:

> ### Mechanical evaluation

> In order to mechanize the above rule, we represent an environment by a list-structure made up of name-value pairs. There is a function designated by location such that if `E*` is this structure and `X` is an identifier then
>
>`locationE*X`
>
> denotes the selector that selects the value of X from `E*`.
>
> So if `E*` represents the environment `E` then the following
>equation holds:
>
> `valEX = locationE*XE*`.
>
> We shall not bother below to distinguish between `E` and `E*`.
>
> Also we represent the value of a lambda-expression by a bundle of information called a "**closure**," comprising the lambda-expression and the environment relative to which it was evaluated. We must therefore arrange that such
a bundle is correctly interpreted whenever it has to be applied to some argument. More precisely:
>
> a **closure** has an *environment part* which is a list whose two items are:
>
>* (1) an environment
>* (2) an identifier or list of identifiers,
>
>and a *control part* which consists of a list whose sole item is an `AE`.
>
>The value relative to E of a lambda-expression X is represented
>by the closure denoted by
>`constructclosure((E, bvX), unitlist(bodyX))`.

The function `val`is defined in a previous pragraph

> - R1. If `X` is an identifier, `valEX` is `EX`;
> - (R2. appears below);
> - R3. If `X` is a combination, `valEX` can be found by first subjecting both its operator and operand to `valE`, and then applying the result of the former to the result of the latter.

## 3.9 Classes

See [examples/class/breakfast.lox](/docs/reading/chapter-3-the-lox-language/examples/class/breakfast.lox)

```sh
➜  examples git:(casiano) ✗ clox class/breakfast.lox
Breakfast
Enjoy your bacon and toast, Dear Reader.
Eggs a-fryin'!
Enjoy your ham and English muffin, Noble Reader.
How about a Bloody Mary?
Cola!
```