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

## Hello, Lox! 

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