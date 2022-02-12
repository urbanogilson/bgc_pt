<!-- Beej's guide to C

# vim: ts=4:sw=4:nosi:et:tw=72
-->

<!-- # Hello, World! -->

# Olá Mundo!

<!-- ## What to Expect from C -->

## O que esperar da linguagem C

> _"Where do these stairs go?"_ \
> _"They go up."_
>
> ---Ray Stantz and Peter Venkman, Ghostbusters

<!-- C is a low-level language. -->

C é uma linguagem de baixo nível.


<!-- It didn't used to be. Back in the day when people carved punch cards out
of granite, C was an incredible way to be free of the drudgery of
lower-level languages like [flw[assembly|Assembly_language]]. -->

Não costumava ser. Na época em que as pessoas esculpiam cartões perfurados em granito, C era uma maneira incrível de se livrar do trabalho penoso das linguagens de nível mais baixo como [flw[assembly|Assembly_language]].

<!-- But now in these modern times, current-generation languages offer all
kinds of features that didn't exist in 1972 when C was invented. This
means C is a pretty basic language with not a lot of features. It can do
_anything_, but it can make you work for it. -->

Mas agora, nestes tempos modernos, as linguagens da geração atual oferecem todos os tipos de recursos que não existiam em 1972, quando C foi inventado. Isso significa que C é uma linguagem bastante básica com poucos recursos. Ele pode fazer _qualquer coisa_, mas pode fazer você trabalhar para isso.

<!-- So why would we even use it today? -->

Então, por que usaríamos isso hoje?

<!-- * As a learning tool: not only is C a venerable piece of computing
  history, but it is connected to the bare metal in
  a way that present-day languages are not. When you learn C, you learn
  about how software interfaces with computer memory at a low level.
  There are no seatbelts. You'll write software that crashes, I assure
  you. And that's all part of the fun! -->

* Como uma ferramenta de aprendizado: C não é apenas uma peça venerável da história da computação, mas está conectado ao [flw[bare metal|Bare_machine]] de uma forma que as linguagens atuais não são.
  Quando você aprende C, você aprende sobre como o software interage com a memória do computador em um nível baixo.
  Não há cintos de segurança. Você escreverá um software que trava, garanto. E tudo isso faz parte da diversão!

<!-- * As a useful tool: C still is used for certain applications, such as
  building [flw[operating systems|Operating_system]] or in [flw[embedded
  systems|Embedded_system]]. (Though the
  [flw[Rust|Rust_(programming_language)]] programming language is eyeing
  both these fields!) -->

* Como uma ferramenta útil: C ainda é usado para certas aplicações, como construção de [flw[sistemas operacionais|Operating_system]] ou em [flw[sistemas embarcados|Embedded_system]]. (Embora a linguagem de programação [flw[Rust|Rust_(programming_language)]] esteja de olho nesses dois campos!)

<!-- If you're familiar with another language, a lot of things about C are
easy. C inspired many other languages, and you'll see bits of it in Go,
Rust, Swift, Python, JavaScript, Java, and all kinds of other languages.
Those parts will be familiar. -->

Se você estiver familiarizado com outra linguagem, muitas coisas sobre C são fáceis. C inspirou muitas outras linguagens, e você verá partes dele em Go, Rust, Swift, Python, JavaScript, Java e todos os outros tipos de linguagens. Essas partes serão familiares.

<!-- The one thing about C that hangs people up is _pointers_. Virtually
everything else is familiar, but pointers are the weird one. The concept
behind pointers is likely one you already know, but C forces you to be
explicit about it, using operators you've likely never seen before. -->

A única coisa sobre C que trava as pessoas são os _ponteiros_. Praticamente todo o resto é familiar, mas os ponteiros säo os estranhos. O conceito por trás de ponteiros é provavelmente um que você já conhece, mas C força você a ser explícito sobre isso, usando operadores que você provavelmente nunca viu antes.

<!-- It's especially insidious because once you [flw[_grok_|Grok]] pointers, they're suddenly easy. But up until that moment, they're slippery eels. -->

É especialmente traiçoeiro porque uma vez que você entende os ponteiros, eles de repente se tornam fáceis. Mas até esse momento, eles são enguias escorregadias.

<!-- Everything else in C is just memorizing another way (or sometimes the
same way!) of doing something you've done already. Pointers are the
weird bit. And, arguably, even pointers are variations on a theme you're
probably familiar with. -->

Todo o resto em C é apenas memorizar outra maneira (ou às vezes da mesma maneira!) de fazer algo que você já fez. Ponteiros são a parte estranha. E, sem dúvida, até os ponteiros são variações de um tema com o qual você provavelmente está familiarizado.

<!-- So get ready for a rollicking adventure as close to the core of the
computer as you can get without assembly, in the most influential
computer language of all time^[I know someone will fight me on that,
but it's gotta be at least in the top three, right?]. Hang on! -->

Então prepare-se para uma aventura divertida o mais próximo possível do interior do computador sem o desmontar, na linguagem de computador mais influente de todos os tempos^[Eu sei que alguém vai brigar comigo sobre isso, mas tem que estar pelo menos entre as três primeiras, certo?]. Aguarde!


<!-- ## Hello, World! -->

## Olá Mundo!

<!-- This is the canonical example of a C program. Everyone uses it. (Note
that the numbers to the left are for reader reference only, and are not
part of the source code.) -->

Este é o exemplo canônico de um programa C. Todo mundo usa. (Observe que os números à esquerda são apenas para referência do leitor e não fazem parte do código-fonte.)

<!-- ``` {.c .numberLines}
/* Hello world program */

#include <stdio.h>

int main(void)
{
    printf("Hello, World!\n");  // Actually do the work here
}
``` -->

``` {.c .numberLines}
/* programa Olá mundo */

#include <stdio.h>

int main(void)
{
    printf("Olá mundo!\n");  // Na verdade, o trabalho acontece aqui
}
```

<!-- We're going to don our long-sleeved heavy-duty rubber gloves, grab a
scalpel, and rip into this thing to see what makes it tick. So, scrub
up, because here we go. Cutting very gently... -->

Vamos colocar nossas luvas de borracha de manga comprida para serviço pesado, pegar um bisturi e rasgar essa coisa para ver o que faz funcionar. Então, prepare-se, porque aqui vamos nós. Cortando com muita delicadeza...

<!-- Let's get the easy thing out of the way: anything between the digraphs
`/*` and `*/` is a comment and will be completely ignored by the
compiler. Same goes for anything on a line after a `//`. This allows you
to leave messages to yourself and others, so that when you come back and
read your code in the distant future, you'll know what the heck it was
you were trying to do. Believe me, you will forget; it happens. -->

Vamos tirar a coisa fácil do caminho: qualquer coisa entre os dígrafos `/*` e `*/` é um comentário e será completamente ignorado pelo compilador. O mesmo vale para qualquer coisa em uma linha após um `//`.
Isso permite que você deixe mensagens para si mesmo e para os outros, para que, quando você voltar e ler seu código em um futuro distante, saiba o que diabos estava tentando fazer. Acredite, você vai esquecer; acontece.

<!-- Now, what is this `#include`? GROSS! Well, it tells the C Preprocessor
to pull the contents of another file and insert it into the code right
_there_. -->

Agora, o que é esse `#include`? BRUTO! Bem, ele diz ao Pré-processador do C para extrair o conteúdo de outro arquivo e inseri-lo no código _ali mesmo._.

<!-- Wait---what's a C Preprocessor? Good question. There are two
stages^[Well, technically there are more than two, but hey, let's
pretend there are two---ignorance is bliss, right?] to compilation: the
preprocessor and the compiler. Anything that starts with pound sign, or
"octothorpe", (`#`) is something the preprocessor operates on before the
compiler even gets started. Common _preprocessor directives_, as they're
called, are `#include` and `#define`. More on that later. -->

Espere---o que é um pré-processador C? Boa pergunta. Existem dois estágios^[Bem, tecnicamente há mais de dois, mas ei, vamos fingir que há dois---a ignorância é uma benção, certo?] na compilação: o pré-processador e o compilador. Qualquer coisa que comece com o jogo da velha, ou "octótropo", (`#`) é algo que o pré-processador opera antes mesmo de o compilador ser iniciado. As _diretivas do pré-processador_ comuns, como são chamadas, são `#include` e `#define`. Mais sobre isso mais tarde.

<!-- Before we go on, why would I even begin to bother pointing out that a
pound sign is called an octothorpe? The answer is simple: I think the
word octothorpe is so excellently funny, I have to gratuitously spread
its name around whenever I get the opportunity. Octothorpe. Octothorpe,
octothorpe, octothorpe. -->

Antes de continuarmos, por que eu começaria a me incomodar em apontar que o sinal do jogo da velha é chamado de octótropo? A resposta é simples: eu acho que a palavra octótropo é tão excelentemente engraçada que tenho que espalhar seu nome gratuitamente sempre que tenho a oportunidade. Octótropo. octótropo, octótropo, octótropo.

<!-- So _anyway_. After the C preprocessor has finished preprocessing
everything, the results are ready for the compiler to take them and
produce [flw[assembly code|Assembly_language]], [flw[machine
code|Machine_code]], or whatever it's about to do. Machine code is the
"language" the CPU understands, and it can understand it _very rapidly_.
This is one of the reasons C programs tend to be quick. -->

Então _de qualquer forma_. Depois que o pré-processador terminar de pré-processar tudo, os resultados estarão prontos para o compilador pegá-los e produzir [flw[código assembly|Assembly_language]], [flw[código de máquina|Machine_code]], ou o que estiver prestes a fazer. O código de máquina é a "linguagem" que a CPU entende e pode entendê-la _muito rapidamente_. Esta é uma das razões pelas quais os programas C tendem a ser rápidos.

<!-- Don't worry about the technical details of compilation for now; just
know that your source runs through the preprocessor, then the output of
that runs through the compiler, then that produces an executable for you
to run. -->

Não se preocupe com os detalhes técnicos da compilação por enquanto; apenas saiba que seu código fonte passa pelo pré-processador, então a saída dele passa pelo compilador, então isso produz um executável para você executar.

<!-- What about the rest of the line? What's `<stdio.h>`? That is what is
known as a _header file_. It's the dot-h at the end that gives it away.
In fact it's the "Standard I/O" (`stdio`) header file that you will grow
to know and love. It gives us access to a bunch of I/O
functionality^[Technically, it contains preprocessor directives and
function prototypes (more on that later) for common input and output
needs.]. For our demo program, we're outputting the string "Hello,
World!", so we in particular need access to the `printf()` function to
do this. The `<stdio.h>` file gives us this access.  Basically, if we
tried to use `printf()` without `#include <stdio.h>`, the compiler would
have complained to us about it. -->

E o resto da linha? O que é `<stdio.h>`? Isso é o que é conhecido como _arquivo de cabeçalho_. É o ponto-h no final que o entrega.
Na verdade, é o arquivo de cabeçalho "Standard I/O" (`stdio`) que você conhecerá e amará. Ele nos dá acesso a várias funcionalidades de I/O^[Tecnicamente, contém diretivas do pré-processador e protótipos de função (mais sobre isso depois) para necessidades comuns de entrada e saída.].
Para o nosso programa de demonstração, estamos produzindo a cadeia de caracteres "Olá mundo!", então, em particular, precisamos de acesso à função `printf()` para fazer isso. O arquivo `<stdio.h>` nos dá esse acesso.
Basicamente, se tentássemos usar `printf()` sem `#include <stdio.h>`, o compilador teria reclamado conosco sobre isso.

<!-- How did I know I needed to `#include <stdio.h>` for `printf()`? Answer:
it's in the documentation. If you're on a Unix system, `man 3 printf`
and it'll tell you right at the top of the man page what header files
are required. Or see the reference section in this book. `:-)` -->

Como eu sabia que precisava do `#include <stdio.h>` para acessar `printf()`? Resposta: está na documentação. Se você estiver em um sistema Unix, `man 3 printf` e ele lhe dirá logo no topo da página do manual quais arquivos de cabeçalho são necessários. Ou veja a seção de referência neste livro. `:-)`

<!-- Holy moly. That was all to cover the first line! But, let's face it, it
has been completely dissected. No mystery shall remain! -->

Santo Deus. Isso foi tudo para cobrir a primeira linha! Mas, convenhamos, foi completamente dissecado. Nenhum mistério permanecerá!

<!-- So take a breather...look back over the sample code. Only a couple easy
lines to go. -->

Então, respire... olhe para o código de exemplo. Apenas algumas linhas fáceis para entender.

<!-- Welcome back from your break! I know you didn't really take a break; I
was just humoring you. -->

Bem-vindo de volta da sua pausa! Eu sei que você realmente não fez uma pausa; Eu só estava brincando com você.

<!-- The next line is `main()`. This is the definition of the function
`main()`; everything between the squirrelly braces (`{` and `}`) is part
of the function definition. -->

A próxima linha é `main()`. Esta é a definição da função `main()`; tudo entre colchetes (`{` `}`) faz parte da definição da função.

<!-- (How do you _call_ a different function, anyway? The answer lies in the
`printf()` line, but we'll get to that in a minute.) -->

(Como você _chama_ uma função diferente, afinal? A resposta está na linha `printf()`, mas chegaremos a isso em um minuto.)

<!-- Now, the main function is a special one in many ways, but one way stands
above the rest: it is the function that will be called automatically
when your program starts executing. Nothing of yours gets called before
`main()`. In the case of our example, this works fine since all we want
to do is print a line and exit. -->

Agora, a função main é especial de muitas maneiras, mas uma delas está acima das outras: é a função que será chamada automaticamente quando seu programa começar a ser executado. Nada seu é chamado antes de `main()`. No caso do nosso exemplo, isso funciona bem, pois tudo o que queremos fazer é imprimir uma linha e encerrar.

<!-- Oh, that's another thing: once the program executes past the end of
`main()`, down there at the closing squirrelly brace, the program will
exit, and you'll be back at your command prompt. -->

Ah, tem outra coisa: uma vez que o programa é executado após o final de `main()`, lá embaixo na chave de fechamento, o programa será encerrado e você estará de volta a linha de comando.

<!-- So now we know that that program has brought in a header file,
`stdio.h`, and declared a `main()` function that will execute when the
program is started. What are the goodies in `main()`? -->

Então agora sabemos que esse programa trouxe um arquivo de cabeçalho, `stdio.h`, e declarou uma função `main()` que será executada quando o programa for iniciado. Quais são os brindes no `main()`?

<!-- I am so happy you asked. Really! We only have the one goodie: a call to
the function `printf()`. You can tell this is a function call and not a
function definition in a number of ways, but one indicator is the lack
of squirrelly braces after it. And you end the function call with a
semicolon so the compiler knows it's the end of the expression. You'll
be putting semicolons after almost everything, as you'll see. -->

Estou tão feliz que você perguntou. Mesmo! Nós só temos um brinde: uma chamada para a função `printf()`. Você pode dizer que isso é uma chamada de função e não uma definição de função de várias maneiras, mas um indicador é a falta de chaves depois dela. E você termina a chamada da função com um ponto e vírgula para que o compilador saiba que é o fim da expressão. Você colocará ponto e vírgula depois de quase tudo, como verá.

<!-- You're passing one argument to the function `printf()`: a string to be
printed when you call it. Oh, yeah---we're calling a function! We rock!
Wait, wait---don't get cocky. What's that crazy `\n` at the end of the
string? Well, most characters in the string will print out just like
they are stored. But there are certain characters that you can't print
on screen well that are embedded as two-character backslash codes. One
of the most popular is `\n` (read "backslash-N") that corresponds to the
_newline_ character. This is the character that causes further printing
to continue at the beginning of the next line instead of the current.
It's like hitting return at the end of the line. -->

Você está passando um argumento para a função `printf()`: uma cadeia de caracteres a ser impressa quando você a chama. Ah, sim---estamos chamando uma função! Nós arrasamos! Espere, espere---não fique arrogante. O que é aquele `\n` maluco no final da cadeia de caracteres? Bem, a maioria dos caracteres na cadeia serão impressos exatamente como estão armazenados.
Mas há certos caracteres que você não pode imprimir bem na tela que são incorporados como códigos de barra invertida de dois caracteres. Um dos mais populares é `\n` (leia "barra N") que corresponde ao caractere _nova linha_. Este é o caractere que faz com que a impressão continue no início da próxima linha em vez da atual.
É como apertar o retorno (enter) no final da linha.

<!-- So copy that code into a file called `hello.c` and build it. On a
Unix-like platform (e.g. Linux, BSD, Mac, or WSL), from the command line
you'll build with a command like so: -->

Então copie esse código em um arquivo chamado `hello.c` e compile-o. Em uma plataforma do tipo Unix (por exemplo, Linux, BSD, Mac ou WSL), a partir da linha de comando, você compilará com um comando assim:

``` {.zsh}
gcc -o hello hello.c
```

<!-- (This means "compile `hello.c`, and output an executable called
`hello`".) -->

(Isso significa "compilar `hello.c` e gerar um executável chamado `hello`".)

<!-- After that's done, you should have a file called `hello` that you can
run with this command: -->

Feito isso, você deve ter um arquivo chamado `hello` que pode ser executado com este comando:

``` {.default}
./hello
```

<!-- (The leading `./` tells the shell to "run from the current directory".) -->

(O `./` inicial diz ao shell para "executar a partir do diretório atual".)

<!-- And see what happens: -->

E veja o que acontece:

<!-- ``` {.default}
Hello, World! 
``` -->

``` {.default}
Olá mundo!
```

<!-- It's done and tested! Ship it! -->

Está feito e testado! Publique!

<!-- ## Compilation Details -->

## Detalhes da compilação

<!-- Let's talk a bit more about how to build C programs, and what happens
behind the scenes there. -->

Vamos falar um pouco mais sobre como construir programas em C e o que acontece nos bastidores.

<!-- Like other languages, C has _source code_. But, depending on what
language you're coming from, you might never have had to _compile_ your
source code into an _executable_. -->

Como outras linguagens, C tem _código-fonte_. Mas, dependendo de qual linguagem você está vindo, talvez você nunca precise _compilar_ seu código-fonte em um _executável_.

<!-- Compilation is the process of taking your C source code and turning it
into a program that your operating system can execute. -->

Compilação é o processo de pegar seu código-fonte C e transformá-lo em um programa que seu sistema operacional pode executar.

<!-- JavaScript and Python devs aren't used to a separate compilation step at
all--though behind the scenes it's happening! Python compiles your
source code into something called _bytecode_ that the Python virtual
machine can execute. Java devs are used to compilation, but that
produces bytecode for the Java Virtual Machine. -->

Os desenvolvedores de JavaScript e Python não estão acostumados a uma etapa de compilação separada--embora nos bastidores isso esteja acontecendo! Python compila seu código-fonte em algo chamado _bytecode_ que a máquina virtual Python pode executar. Os desenvolvedores Java estão acostumados com compilação, mas isso produz bytecode para a máquina virtual do Java.

<!-- When compiling C, _machine code_ is generated. This is the 1s and 0s
that can be executed directly and speedily by the CPU. -->

Ao compilar C, é gerado _código de máquina_. Estes são os 1s e 0s que podem ser executados diretamente e rapidamente pela CPU.

<!-- > Languages that typically aren't compiled are called _interpreted_
> languages. But as we mentioned with Java and Python, they also have a
> compilation step. And there's no rule saying that C can't be
> interpreted. (There are C interpreters out there!) In short, it's a
> bunch of gray areas. Compilation in general is just taking source code
> and turning it into another, more easily-executed form. -->

> As linguagens que normalmente não são compiladas são chamadas de linguagens _interpretadas_. Mas, como mencionamos com Java e Python, eles também têm uma etapa de compilação. E não há nenhuma regra dizendo que C não pode ser interpretado. (Existem interpretadores de C por aí!) Resumindo, é um monte de áreas cinzentas. A compilação em geral é apenas pegar o código-fonte e transformá-lo em outra forma mais fácil de executar.

<!-- The C compiler is the program that does the compilation. -->

O compilador C é o programa que faz a compilação.

<!-- As we've already said, `gcc` is a compiler that's installed on a lot of
[flw[Unix-like operating systems|Unix]]. And it's commonly run from the
command line in a terminal, but not always. You can run it from your
IDE, as well. -->

Como já dissemos, `gcc` é um compilador que é instalado em muitos [flw[sistemas operacionais do tipo Unix|Unix]]. E geralmente é executado a partir da linha de comando em um terminal, mas nem sempre. Você também pode executá-lo a partir do seu IDE.

<!-- So how do we do command line builds? -->

Então, como fazemos compilações a partir da linha de comando?

<!-- ## Building with `gcc` -->

## Compilando com `gcc`

<!-- If you have a source file called `hello.c` in the current directory, you
can build that into a program called `hello` with this command typed in
a terminal: -->

Se você tem um arquivo fonte chamado `hello.c` no diretório atual, você pode compilar isso em um programa chamado `hello` com este comando digitado em um terminal:

``` {.zsh}
gcc -o hello hello.c
```

<!-- The `-o` means "output to this file"^[If you don't give it an output
filename, it will export to a file called `a.out` by default---this
filename has its roots deep in Unix history.]. And there's `hello.c` at
the end, the name of the file we want to compile. -->

O `-o` significa "saída para este arquivo"^[Se você não fornecer um nome de arquivo de saída, ele será exportado para um arquivo chamado `a.out` por padrão---este nome de arquivo tem suas raízes profundas na história Unix.]. E há `hello.c` no final, o nome do arquivo que queremos compilar.

<!-- If your source is broken up into multiple files, you can compile them
all together (almost as if they were one file, but the rules are
actually more complex than that) by putting all the `.c` files on the
command line: -->

Se seu código fonte estiver dividido em vários arquivos, você pode compilá-los todos juntos (quase como se fossem um arquivo, mas as regras são realmente mais complexas do que isso) colocando todos os arquivos `.c` na linha de comando:

``` {.zsh}
gcc -o awesomegame ui.c characters.c npc.c items.c
```

<!-- and they'll all get built together into a big executable. -->

e todos eles serão integrados em um grande executável.

<!-- That's enough to get started---later we'll talk details about multiple
source files, object files, and all kinds of fun stuff. -->

Isso é o suficiente para começar---mais tarde falaremos detalhes sobre vários arquivos de origem, arquivos de objeto e todos os tipos de coisas divertidas.

<!-- ## Building with `clang` -->

## Compilando com `clang`

<!-- On Macs, the compiler isn't `gcc`---it's `clang`. But a wrapper is also
installed so you can run `gcc` and have it still work. -->

Em Macs, o compilador não é `gcc`---é `clang`. Mas um wrapper também é instalado para que você possa executar o `gcc` e ainda funcionar.

<!-- ## Building from IDEs -->

## Compilando a partir de IDEs

<!-- If you're using an _Integrated Development Environment_ (IDE), you
probably don't have to build from the command line.  -->

Se você estiver usando um _Ambiente de Desenvolvimento Integrado_ (IDE), provavelmente não precisará compilar a partir da linha de comando.

<!-- With Visual Studio, `CTRL-F7` will build, and `CTRL-F5` will run. -->

Com o Visual Studio, `CTRL-F7` irá compilar e `CTRL-F5` irá executar.

<!-- With VS Code, things are more complex, but you can hit `F5` to run via 
the debugger. (You'll have to install the C/C++ Extension.) -->

Com o VS Code, as coisas são mais complexas, mas você pode pressionar `F5` para executar através do depurador. (Você terá que instalar a extensão C/C++.)

<!-- With XCode, you can build with `COMMAND-B` and run with `COMMAND-R`. To
get the command line tools, Google for "XCode command line tools" and
you'll find instructions for installing them. -->

Com o XCode, você pode compilar com `COMMAND-B` e executar com `COMMAND-R`. Para obter as ferramentas de linha de comando, pesquise no Google por "XCode command line tools" e você encontrará instruções para instalá-las.

<!-- For getting started, I encourage you to also try to build from the
command line---it's history! -->

Para começar, encorajo você a também tentar construir a partir da linha de comando --- é história!

<!-- ## C Versions -->

## Versões da Linguagem C

<!-- C has come a long way over the years, and it had many named version
numbers to describe which dialect of the language you're using. -->

C percorreu um longo caminho ao longo dos anos, e tinha muitos números de versão nomeados para descrever qual dialeto da linguagem você está usando.

<!-- These generally refer to the year of the specification. -->

Geralmente se referem ao ano da especificação.

<!-- The most famous are C89, C99, C11, and C2x. We'll focus on the latter in this book. -->

Os mais famosos são C89, C99, C11 e C2x. Vamos nos concentrar neste último neste livro.

<!-- But here's a more complete table: -->

Mas aqui está uma tabela mais completa:

<!-- |Version|Description|
|-----|--------------|
|K&R C|1978, the original. Named after Brian Kernighan and Dennis Ritchie. Ritchie designed and coded the language, and Kernighan co-authored the book on it. You rarely see original K&R code today. If you do, it'll look odd, like Middle English looks odd to modern English readers.|
|**C89**, ANSI C, C90|In 1989, the American National Standards Institute (ANSI) produced a C language specification that set the tone for C that persists to this day. A year later, the reins were handed to the International Organization for Standardization (ISO) that produced the identical C90.|
|C95|A rarely-mentioned addition to C89 that included wide character support.|
|**C99**|The first big overhaul with lots of language additions. The thing most people remember is the addition of `//`-style comments. This is the most popular version of C in use as of this writing.|
|**C11**|This major version update includes Unicode support and multi-threading. Be advised that if you start using these language features, you might be sacrificing portability with places that are stuck in C99 land. But, honestly, 1999 is getting to be a while back now.|
|C17, C18|Bugfix update to C11. C17 seems to be the official name, but the publication was delayed until 2018. As far as I can tell, these two are interchangeable, with C17 being preferred.|
|C2x|What's coming next! Expected to eventually become C21.| -->

|Versão|Descrição|
|-----|--------------|
|K&R C|1978, o original. Nomeado após Brian Kernighan e Dennis Ritchie. Ritchie projetou e codificou a linguagem, e Kernighan foi co-autor do livro sobre ela. Você raramente vê o código K&R original hoje. Se você fizer isso, vai parecer estranho, como o Português antigo parece estranho para os leitores do Português moderno.|
|**C89**, ANSI C, C90|Em 1989, o American National Standards Institute (ANSI) produziu uma especificação de linguagem C que deu o tom para o C que persiste até hoje. Um ano depois, as rédeas foram entregues à Organização Internacional de Normalização (ISO) que produziu o C90 idêntico.|
|C95|Uma adição raramente mencionada ao C89 que incluía amplo suporte a caracteres.|
|**C99**|A primeira grande reformulação com muitas adições na linguagem. A coisa que a maioria das pessoas lembra é a adição de comentários no estilo `//`. Esta é a versão mais popular de C em uso até o momento em que este livro foi escrito.|
|**C11**|Esta atualização de versão principal inclui suporte a Unicode e multi-threading. Esteja ciente de que, se você começar a usar esses recursos da linguagem, poderá sacrificar a portabilidade com lugares que estão presos na terra C99. Mas, honestamente, 1999 está ficando para atrás agora.|
|C17, C18|Atualização de correção de bug para C11. C17 parece ser o nome oficial, mas a publicação foi adiada até 2018. Até onde eu sei, esses dois são intercambiáveis, sendo C17 o preferido.|
|C2x|O que vem a seguir! Espera-se que eventualmente se torne C21.|

<!-- You can force GCC to use one of these standards with the `-std=` command
line argument. If you want it to be picky about the standard, add
`-pedantic`. -->

Você pode forçar o GCC a usar um desses padrões com o argumento de linha de comando `-std=`. Se você quer ser exigente quanto ao padrão, adicione `-pedantic`.

<!-- For example: -->

Por exemplo:

``` {.zsh}
gcc -std=c11 -pedantic foo.c
```

<!-- For this book, I compile programs for C2x with all warnings set: -->

Para este livro, compilei programas para C2x com todos os avisos definidos:

``` {.zsh}
gcc -Wall -Wextra -std=c2x -pedantic foo.c
```
