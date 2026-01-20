
I am using the branch `casiano`.

## Installing the tools and building the book site

First, I have installed dart version 3.10.7:

```sh
➜  craftinginterpreters git:(casiano) ✗ dart --version
Dart SDK version: 3.10.7 (stable) (Tue Dec 23 00:01:57 2025 -0800) on "macos_x64"
```
and then I tried `make get` for the Makefile of the munificent/craftinginterpreters repository. I assume it get the tools needed for building the book, but:

```
➜  craftinginterpreters git:(casiano) ✗ make get
Resolving dependencies... 
The lower bound of "sdk: '>2.11.0 <3.0.0'" must be 2.12.0'
or higher to enable null safety.

The current Dart SDK (3.10.7) only supports null safety.

For details, see https://dart.dev/null-safety
make: *** [get] Error 65
```

So I asked ChatGPT:

How can I fix this error?  Shall I install a lower version of dart? How?

The answer is in [/docs/make-get-old-dart.chatgpt.md](/docs/make-get-old-dart.chatgpt.md).

I followed the [first approach using `brew`](/docs/make-get-old-dart.chatgpt.md#option-a-using-homebrew-simplest-on-macos) (Ask ChatGPT for your OS if you need help) and installed dart version 2.19.6:

```sh
➜  craftinginterpreters git:(casiano) ✗ dart --version
Dart SDK version: 2.19.6 (stable) (Tue Mar 28 13:41:04 2023 +0000) on "macos_x64"
```

After that I've got the dependencies with:

```sh
➜  craftinginterpreters git:(casiano) ✗ make get
  ╔════════════════════════════════════════════════════════════════════════════╗
  ║ The Dart tool uses Google Analytics to report feature usage statistics     ║
  ║ and to send basic crash reports. This data is used to help improve the     ║
  ║ Dart platform and tools over time.                                         ║
  ║                                                                            ║
  ║ To disable reporting of analytics, run:                                    ║
  ║                                                                            ║
  ║   dart --disable-analytics                                                 ║
  ║                                                                            ║
  ╚════════════════════════════════════════════════════════════════════════════╝

Resolving dependencies... (1.5s)
  archive 2.0.13 (4.0.7 available)
  args 1.6.0 (2.7.0 available)
  async 2.4.1 (2.13.0 available)
  charcode 1.1.3 (1.4.0 available)
  cli_repl 0.2.0+1 (0.2.3 available)
  collection 1.14.12 (1.19.1 available)
  convert 2.1.1 (3.1.2 available)
  crypto 2.1.5 (3.0.7 available)
  glob 1.2.0 (2.1.3 available)
  http 0.12.1 (1.6.0 available)
  http_parser 3.1.4 (4.1.2 available)
  image 2.1.19 (4.7.2 available)
  js 0.6.1+1 (0.7.2 available)
  markdown 2.1.3 (7.3.0 available)
  matcher 0.12.6 (0.12.18 available)
  meta 1.1.8 (1.18.0 available)
  mime_type 0.3.0 (1.0.1 available)
  mustache_template 1.0.0+1 (2.0.3 available)
  node_interop 1.1.1 (2.2.0 available)
  node_io 1.1.1 (2.3.0 available)
  package_config 1.9.3 (2.2.0 available)
  path 1.7.0 (1.9.1 available)
  pedantic 1.9.0 (1.11.1 available)
  petitparser 3.0.4 (7.0.1 available)
  pool 1.4.0 (1.5.2 available)
  quiver 2.1.3 (3.2.2 available)
  sass 1.26.5 (1.97.2 available)
  shelf 0.7.5 (1.4.2 available)
  source_maps 0.10.9 (0.10.13 available)
  source_span 1.7.0 (1.10.1 available)
  stack_trace 1.9.3 (1.12.1 available)
  stream_channel 2.0.0 (2.1.4 available)
  stream_transform 1.2.0 (2.1.1 available)
  string_scanner 1.0.5 (1.4.1 available)
  term_glyph 1.1.0 (1.2.2 available)
  tuple 1.0.3 (2.0.2 available)
  typed_data 1.1.6 (1.4.0 available)
  watcher 0.9.7+15 (1.2.1 available)
  xml 4.5.1 (6.6.1 available)
Got dependencies!
```

Then I followed the section "Building Stuff" in [README.md](/README.md#building-stuff). Here is the markdown:

````markdown
### Building

Once you've got that setup, try:

```sh
$ make
```

If everything is working, that will generate the site for the book as well as
compiling the two interpreters clox and jlox. You can run either interpreter
right from the root of the repo:

```sh
$ ./clox
$ ./jlox
```
````

No errors were found. 

```sh
➜  craftinginterpreters git:(casiano) ✗ make
Compiling Dart snapshot...
Info: Compiling without sound null safety!
Dart 3 will only support sound null safety, see https://dart.dev/null-safety
- site/index.css
- site/style.css
✓ Crafting Interpreters (14 words)
✓ Dedication (23 words)
✓ Acknowledgements (309 words)
✓ Table of Contents (14 words)
✓ I. Welcome (140 words)
  ✓ 1. Introduction (3913 words)
  ✓ 2. A Map of the Territory (5181 words)
  ✓ 3. The Lox Language (6595 words)
✓ II. A Tree-Walk Interpreter (185 words)
  ✓ 4. Scanning (7193 words, 294 loc)
  ✓ 5. Representing Code (7758 words, 169 loc)
  ✓ 6. Parsing Expressions (7546 words, 169 loc)
  ✓ 7. Evaluating Expressions (5546 words, 138 loc)
  ✓ 8. Statements and State (10223 words, 202 loc)
  ✓ 9. Control Flow (5481 words, 122 loc)
  ✓ 10. Functions (7976 words, 180 loc)
  ✓ 11. Resolving and Binding (7787 words, 231 loc)
  ✓ 12. Classes (9559 words, 235 loc)
  ✓ 13. Inheritance (5130 words, 98 loc)
✓ III. A Bytecode Virtual Machine (161 words)
  ✓ 14. Chunks of Bytecode (9236 words, 225 loc)
  ✓ 15. A Virtual Machine (7176 words, 142 loc)
  ✓ 16. Scanning on Demand (7238 words, 332 loc)
  ✓ 17. Compiling Expressions (8025 words, 248 loc)
  ✓ 18. Types of Values (5847 words, 143 loc)
  ✓ 19. Strings (6520 words, 164 loc)
  ✓ 20. Hash Tables (10058 words, 192 loc)
  ✓ 21. Global Variables (6006 words, 177 loc)
  ✓ 22. Local Variables (5667 words, 138 loc)
  ✓ 23. Jumping Back and Forth (7504 words, 165 loc)
  ✓ 24. Calls and Functions (11683 words, 295 loc)
  ✓ 25. Closures (12775 words, 226 loc)
  ✓ 26. Garbage Collection (10960 words, 213 loc)
  ✓ 27. Classes and Instances (4785 words, 134 loc)
  ✓ 28. Methods and Initializers (10076 words, 196 loc)
  ✓ 29. Superclasses (5556 words, 95 loc)
  ✓ 30. Optimization (10253 words, 72 loc)
✓ Backmatter (61 words)
  ✓ A1. Appendix I (614 words)
  ✓ A2. Appendix II (1611 words, 341 loc)
Built 207,252 words and 5,336 lines of code (232,385 total words) in 1.04 seconds
      cc c/chunk.c                                -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/compiler.c                             -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/debug.c                                -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/main.c                                 -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/memory.c                               -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/object.c                               -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/scanner.c                              -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/table.c                                -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/value.c                                -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc c/vm.c                                   -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
      cc build/clox                               -std=c99 -Wall -Wextra -Werror -Wno-unused-parameter -O3 -flto
   javac java/com/craftinginterpreters/tool/GenerateAst.java          -Werror
   javac java/com/craftinginterpreters/lox/AstPrinter.java            -Werror
   javac java/com/craftinginterpreters/lox/Environment.java           -Werror
   javac java/com/craftinginterpreters/lox/Expr.java                  -Werror
   javac java/com/craftinginterpreters/lox/Interpreter.java           -Werror
   javac java/com/craftinginterpreters/lox/Lox.java                   -Werror
   javac java/com/craftinginterpreters/lox/LoxCallable.java           -Werror
   javac java/com/craftinginterpreters/lox/LoxClass.java              -Werror
   javac java/com/craftinginterpreters/lox/LoxFunction.java           -Werror
   javac java/com/craftinginterpreters/lox/LoxInstance.java           -Werror
   javac java/com/craftinginterpreters/lox/Parser.java                -Werror
   javac java/com/craftinginterpreters/lox/Resolver.java              -Werror
   javac java/com/craftinginterpreters/lox/Return.java                -Werror
   javac java/com/craftinginterpreters/lox/RuntimeError.java          -Werror
   javac java/com/craftinginterpreters/lox/Scanner.java               -Werror
   javac java/com/craftinginterpreters/lox/Stmt.java                  -Werror
   javac java/com/craftinginterpreters/lox/Token.java                 -Werror
   javac java/com/craftinginterpreters/lox/TokenType.java             -Werror
➜  craftinginterpreters git:(casiano) ✗ ls -tr
LICENSE   README.md book      java      note      test      docs      build
Makefile  asset     c         jlox      site      util      tool      clox
```

## Running the interpreters

The C version is `clox` and the Java version is `jlox` (See [test/assignment/associativity.lox example](/test/assignment/associativity.lox)):

```
➜  craftinginterpreters git:(master) ./clox test/assignment/associativity.lox 
c
c
c
```


```
➜  craftinginterpreters git:(casiano) ✗ ./jlox test/assignment/associativity.lox 
c
c
c
```

## Building the book site

We can build the book site with:

```sh
➜  craftinginterpreters git:(casiano) make book
- site/index.css
- site/style.css
✓ Crafting Interpreters (14 words)
✓ Dedication (23 words)
✓ Acknowledgements (309 words)
...
✓ Backmatter (61 words)
  ✓ A1. Appendix I (614 words)
  ✓ A2. Appendix II (1611 words, 341 loc)
Built 207,252 words and 5,336 lines of code (232,385 total words) in 1.17 seconds
```
But it is much better to do `make serve` to have a local server with live reload:

```sh
➜  craftinginterpreters git:(casiano) ✗ make serve
- site/index.css
- site/style.css
✓ Crafting Interpreters (14 words)
✓ Dedication (23 words)
✓ Acknowledgements (309 words)
✓ Table of Contents (14 words)
✓ I. Welcome (140 words)
  ✓ 1. Introduction (3913 words)
  ✓ 2. A Map of the Territory (5181 words)
  ✓ 3. The Lox Language (6595 words)
✓ II. A Tree-Walk Interpreter (185 words)
  ✓ 4. Scanning (7193 words, 294 loc)
  ✓ 5. Representing Code (7758 words, 169 loc)
  ✓ 6. Parsing Expressions (7546 words, 169 loc)
  ✓ 7. Evaluating Expressions (5546 words, 138 loc)
  ✓ 8. Statements and State (10223 words, 202 loc)
  ✓ 9. Control Flow (5481 words, 122 loc)
  ✓ 10. Functions (7976 words, 180 loc)
  ✓ 11. Resolving and Binding (7787 words, 231 loc)
  ✓ 12. Classes (9559 words, 235 loc)
  ✓ 13. Inheritance (5130 words, 98 loc)
✓ III. A Bytecode Virtual Machine (161 words)
  ✓ 14. Chunks of Bytecode (9236 words, 225 loc)
  ✓ 15. A Virtual Machine (7176 words, 142 loc)
  ✓ 16. Scanning on Demand (7238 words, 332 loc)
  ✓ 17. Compiling Expressions (8025 words, 248 loc)
  ✓ 18. Types of Values (5847 words, 143 loc)
  ✓ 19. Strings (6520 words, 164 loc)
  ✓ 20. Hash Tables (10058 words, 192 loc)
  ✓ 21. Global Variables (6006 words, 177 loc)
  ✓ 22. Local Variables (5667 words, 138 loc)
  ✓ 23. Jumping Back and Forth (7504 words, 165 loc)
  ✓ 24. Calls and Functions (11683 words, 295 loc)
  ✓ 25. Closures (12775 words, 226 loc)
  ✓ 26. Garbage Collection (10960 words, 213 loc)
  ✓ 27. Classes and Instances (4785 words, 134 loc)
  ✓ 28. Methods and Initializers (10076 words, 196 loc)
  ✓ 29. Superclasses (5556 words, 95 loc)
  ✓ 30. Optimization (10253 words, 72 loc)
✓ Backmatter (61 words)
  ✓ A1. Appendix I (614 words)
  ✓ A2. Appendix II (1611 words, 341 loc)
Built 207,252 words and 5,336 lines of code (232,385 total words) in 1.14 seconds
Serving at http://localhost:8000
```
Then you visit `http://localhost:8000` in your browser to see the book site. If you modify any markdown file 
in folder `book/`, the site is automatically rebuilt and you can refresh the browser to see the changes.

## Visual Studio Code Syntax Highlighting

There are several VS Code extensions for Lox syntax highlighting. I have installed the one by [dberezin](https://marketplace.visualstudio.com/items?itemName=dberezin.lox-language).

<img src="/docs/images/syntax-highlighting.lox.png" alt="Lox syntax highlighting in VS Code" width="600"/>

## Instructions for Reading these notes

We open with our IDE the file with the markdown for the corresponding chapter or section, 
for instance if we are reading chapter 3, open in your editor the file [book/the-lox-language.md](/book/the-lox-language.md), run your book server `make serve` and visit 
your book server at the corresponding section URL, in this example will visit http://localhost:8000/the-lox-language.html.

Being at the root of the project, [once we have built the C interpreter](/docs/README.md), we run:

```sh
➜  craftinginterpreters git:(casiano) ✗ export PATH=$PATH:`pwd`
➜  examples git:(casiano) ✗ clox
> print(2+3);
5
> ^D
```

## Reading Chapter 3: The Lox Language

Se file [/docs/reading/chapter-3-the-lox-language/README.md](/docs/reading/chapter-3-the-lox-language).