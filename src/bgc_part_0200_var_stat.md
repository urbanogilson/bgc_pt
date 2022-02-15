<!-- Beej's guide to C

# vim: ts=4:sw=4:nosi:et:tw=72
-->

<!-- # Variables and Statements -->

# Variáveis e Declarações

> _"It takes all kinds to make a world, does it not, Padre?"_ \
> _"So it does, my son, so it does."_
>
> ---Pirate Captain Thomas Bartholomew Red to the Padre, Pirates

<!-- There sure can be lotsa stuff in a C program. -->

Com certeza pode haver muitas coisas em um programa C.

<!-- Yup. -->

Sim.

<!-- And for various reasons, it'll be easier for all of us if we classify
some of the types of things you can find in a program, so we can be
clear what we're talking about. -->

E por várias razões, será mais fácil para todos nós se classificarmos alguns dos tipos de coisas que você pode encontrar em um programa, para que possamos ter clareza do que estamos falando.

<!-- ## Variables -->

## Variáveis

<!-- It's said that "variables hold values". But another way to think about
it is that a variable is a human-readable name that refers to some data
in memory. -->

Diz-se que "variáveis guardam valores". Mas outra maneira de pensar sobre isso é que uma variável é um nome legível por humanos que se refere a algum dado na memória.

<!-- We're going to take a second here and take a peek down the rabbit hole
that is pointers. Don't worry about it. -->

Vamos tirar um segundo aqui e dar uma olhada na toca do coelho que são os ponteiros. Não se preocupe com isso.

<!-- You can think of memory as a big array of bytes^[A "byte" is an 8-bit
binary number. Think of it as an integer that can only hold the values
from 0 to 255, inclusive.] Data is stored in this "array"^[I'm seriously
oversimplifying how modern memory works, here. But the mental model
works, so please forgive me.]. If a number is larger than a single byte,
it is stored in multiple bytes. Because memory is like an array, each
byte of memory can be referred to by its index. This index into memory
is also called an _address_, or a _location_, or a _pointer_. -->

Você pode pensar na memória como um grande array de bytes^[Um "byte" é um número binário de 8 bits. Pense nisso como um número inteiro que só pode conter os valores de 0 a 255, inclusive.] Os dados são armazenados neste "array"^[Estou simplificando seriamente como a memória moderna funciona aqui. Mas o modelo mental funciona, então por favor me perdoe.]. Se um número for maior que um único byte, ele será armazenado em vários bytes. Como a memória é como um array, cada byte de memória pode ser referenciado por seu índice. Esse índice na memória também é chamado de _endereço_, ou uma _localização_, ou um _ponteiro_.

<!-- When you have a variable in C, the value of that variable is in memory
_somewhere_, at some address. Of course. After all, where else would it
be? But it's a pain to refer to a value by its numeric address, so we
make a name for it instead, and that's what the variable is. -->

Quando você tem uma variável em C, o valor dessa variável está na memória em _algum lugar_, em algum endereço. Claro. Afinal, onde mais seria? Mas é difícil se referir a um valor por seu endereço numérico, então, em vez disso, criamos um nome para ele, e é isso que a variável é.

<!-- The reason I'm bringing all this up is twofold: -->

A razão pela qual estou trazendo tudo isso é dupla:

<!-- 1. It's going to make it easier to understand pointer variables
   later---they're variables that hold the address of other variables!
2. Also, it's going to make it easier to understand pointers later. -->

1 - Isso tornará mais fácil entender as variáveis de ponteiro mais tarde --- elas são variáveis que guardam o endereço de outras variáveis!
2 - Além disso, tornará mais fácil entender os ponteiros mais tarde.

<!-- So a variable is a name for some data that's stored in memory at some
address. -->

Portanto, uma variável é um nome para alguns dados armazenados na memória em algum endereço.

<!-- ### Variable Names -->

### Nomes de Variáveis

<!-- You can use any characters in the range 0-9, A-Z, a-z, and underscore
for variable names, with the following rules: -->

Você pode usar qualquer caractere no intervalo 0-9, A-Z, a-z e underscore para nomes de variáveis, com as seguintes regras:

<!-- * You can't start a variable with a digit 0-9.
* You can't start a variable name with two underscores.
* You can't start a variable name with an underscore followed by a
  capital A-Z. -->

* Você não pode iniciar uma variável com um dígito 0-9.
* Você não pode iniciar um nome de variável com dois underscores.
* Você não pode iniciar um nome de variável com um underscore seguido de A-Z maiúsculo.

<!-- For Unicode, just try it. There are some rules in the spec in §D.2 that
talk about which Unicode codepoint ranges are allowed in which parts of
identifiers, but that's too much to write about here and is probably
something you'll never have to think about anyway. -->

Para Unicode, apenas tente. Existem algumas regras na especificação em §D.2 que fala sobre quais intervalos de codepoints Unicode são permitidos em quais partes dos identificadores, mas isso é muito para escrever aqui e provavelmente é algo que você nunca terá que pensar de qualquer maneira.

<!-- ### Variable Types -->

### Tipos de variáveis

<!-- Depending on which languages you already have in your toolkit, you might
or might not be familiar with the idea of types. But C's kinda picky
about them, so we should do a refresher. -->

Dependendo de quais linguagens você já possui em seu kit de ferramentas, você pode ou não estar familiarizado com a ideia de tipos. Mas C é meio exigente com eles, então devemos fazer uma atualização.

<!-- Some example types, some of the most basic: -->

Alguns tipos de exemplo, alguns dos mais básicos:

<!-- |Type|Example|C Type|
|:---|------:|:-----|
|Integer|`3490`|`int`|
|Floating point|`3.14159`|`float`|
|Character (single)|`'c'`|`char`|
|String|`"Hello, world!"`|`char *`^[Read this as "pointer to a char" or "char pointer". "Char" for character. Though I can't find a study, it seems anecdotally most people pronounce this as "char", a minority say "car", and a handful say "care". We'll talk more about pointers later.]| -->

|Tipo|Exemplo|Tipo C|
|:---|------:|:-----|
|Inteiro|`3490`|`int`|
|Ponto flutuante|`3.14159`|`float`|
|Caractere (único)|`'c'`|`char`|
|String|`"Olá, mundo!"`|`char *`^[Leia isso como "ponteiro para um caractere" ou "ponteiro de caractere". "Char" para o caractere. Embora eu não consiga encontrar um estudo, parece que a maioria das pessoas pronuncia isso como "char", uma minoria diz "car" e um punhado diz "care". Falaremos mais sobre ponteiros mais tarde.]|

<!-- C makes an effort to convert automatically between most numeric types
when you ask it to. But other than that, all conversions are manual,
notably between string and numeric. -->

C faz um esforço para converter automaticamente entre a maioria dos tipos numéricos quando você solicita. Mas fora isso, todas as conversões são manuais, principalmente entre string e numérico.

<!-- Almost all of the types in C are variants on these types. -->

Quase todos os tipos em C são variantes desses tipos.

<!-- Before you can use a variable, you have to _declare_ that variable and
tell C what type the variable holds. Once declared, the type of variable
cannot be changed later at runtime. What you set it to is what it is
until it falls out of scope and is reabsorbed into the universe. -->

Antes de poder usar uma variável, você precisa declarar essa variável e informar a C que tipo a variável contém. Uma vez declarado, o tipo de variável não pode ser alterado posteriormente em tempo de execução. O que você define é o que é até que saia do escopo e seja reabsorvido no universo.

<!-- Let's take our previous "Hello, world" code and add a couple variables
to it: -->

Vamos pegar nosso código anterior "Olá Mundo!" e adicionar algumas variáveis a ele:

``` {.c .numberLines}
#include <stdio.h>

int main(void)
{
    int i;    // Mantém números inteiros com sinal, e.g. -3, -2, 0, 1, 10
    float f;  // Mantém números de ponto flutuante com sinal, e.g. -3.1416

    printf("Olá Mundo!\n");  // Ah, abençoada familiaridade
}
```

<!-- There! We've declared a couple of variables. We haven't used them yet,
and they're both uninitialized. One holds an integer number, and the
other holds a floating point number (a real number, basically, if you
have a math background). -->

Lá! Declaramos algumas variáveis. Ainda não as usamos, e ambas não foram inicializadas. Uma contém um número inteiro e a outra contém um número de ponto flutuante (um número real, basicamente, se você tiver experiência em matemática).

<!-- Uninitialized variables have indeterminate value^[Colloquially, we say
they have "random" values, but they aren't truly---or even
pseudo-truly---random numbers.]. They have to be initialized or else you
must assume they contain some nonsense number. -->

Variáveis não inicializadas têm valor indeterminado^[Coloquialmente, dizemos que elas têm valores "aleatórios", mas não são números verdadeiros---ou mesmo pseudo-verdadeiros---números aleatórios.]. Eles precisam ser inicializados ou então você deve assumir que eles contêm algum número sem sentido.

<!-- > This is one of the places C can "get you". Much of the time, in my
> experience, the indeterminate value is zero... but it can vary from
> run to run! Never assume the value will be zero, even if you see it
> is. _Always_ explicitly initialize variables to some value before you
> use them^[This isn't strictly 100% true. When we get to learning about
> static storage duration, you'll find the some variables are
> initialized to zero automatically. But the safe thing to do is always
> initialize them.]. -->

> Este é um dos lugares onde C pode "pegar você". Na maioria das vezes, na minha experiência, o valor indeterminado é zero... mas pode variar de execução para execução! Nunca assuma que o valor será zero, mesmo que você veja que é. _Sempre_ inicialize explicitamente as variáveis com algum valor antes de usá-las^[Isso não é estritamente 100% verdadeiro. Quando aprendermos sobre a duração do armazenamento estático, você descobrirá que algumas variáveis são inicializadas em zero automaticamente. Mas o mais seguro a se fazer é sempre inicializá-las.].

<!-- What's this? You want to store some numbers in those variables? Insanity! -->

O que é isso? Você quer armazenar alguns números nessas variáveis? Insanidade!

<!-- Let's go ahead and do that: -->

Vamos em frente e fazer isso:

``` {.c .numberLines}
int main(void)
{
    int i;

    i = 2; // Atribua o valor 2 na variável i

    printf("Olá Mundo!\n");
}
```

<!-- Killer. We've stored a value. Let's print it. -->

Feito. Armazenamos um valor. Vamos imprimir.

<!-- We're going to do that by passing _two_ amazing arguments to the
`printf()` function. The first argument is a string that describes what
to print and how to print it (called the _format string_), and the
second is the value to print, namely whatever is in the variable `i`. -->

Faremos isso passando _dois_ argumentos incríveis para a função `printf()`. O primeiro argumento é uma string que descreve o que imprimir e como imprimir (chamado de _string de formatação_), e o segundo é o valor a ser impresso, ou seja, o que estiver na variável `i`.

<!-- `printf()` hunts through the format string for a variety of special
sequences which start with a percent sign (`%`) that tell it what to
print. For example, if it finds a `%d`, it looks to the next parameter
that was passed, and prints it out as an integer. If it finds a `%f`, it
prints the value out as a float. If it finds a `%s`, it prints a string. -->

`printf()` procura através da string de formatação uma variedade de sequências especiais que começam com um sinal de porcentagem (`%`) que informam o que imprimir. Por exemplo, se encontrar um `%d`, ele procura o próximo parâmetro que foi passado e o imprime como um inteiro. Se encontrar um `%f`, imprime o valor como um float. Se encontrar um `%s`, imprime uma string.

<!-- As such, we can print out the value of various types like so: -->

Como tal, podemos imprimir o valor de vários tipos assim:

``` {.c .numberLines}
#include <stdio.h>

int main(void)
{
    int i = 2;
    float f = 3.14;
    char *s = "Hello, world!";  // char * ("ponteiro para char") é o tipo string

    printf("%s  i = %d and f = %f!\n", s, i, f);
}
```

<!-- And the output will be: -->

E a saída será:

``` {.default}
Hello, world!  i = 2 e f = 3.14!
```

<!-- In this way, `printf()` might be similar to various types of format
strings or parameterized strings in other languages you're familiar
with. -->

Dessa forma, `printf()` pode ser semelhante a vários tipos de string de formatação ou strings parametrizadas em outras linguagens com as quais você está familiarizado.

<!-- ### Boolean Types -->

### Tipos booleanos

<!-- C has Boolean types, true or false? -->

C tem tipos booleanos, verdadeiro ou falso?

<!-- 1! -->

1!

<!-- Historically, C didn't have a Boolean type, and some might argue it
still doesn't. -->

Historicamente, C não tinha um tipo booleano, e alguns podem argumentar que ainda não tem.

<!-- In C, `0` means "false", and non-zero means "true". -->

Em C, `0` significa "falso" e diferente de zero significa "verdadeiro".

<!-- So `1` is true. And `-37` is true. And `0` is false. -->

Então `1` é verdadeiro. E `-37` é verdadeiro. E `0` é falso.

<!-- You can just declare Boolean types as `int`s: -->

Você pode simplesmente declarar tipos booleanos como `int`s:

``` {.c}
int x = 1;

if (x) {
    printf("x é verdadeiro!\n");
}
```

<!-- If you `#include <stdbool.h>`, you also get access to some symbolic
names that might make things look more familiar, namely a `bool` type
and `true` and `false` values: -->

Se você `#include <stdbool.h>`, você também terá acesso a alguns nomes simbólicos que podem tornar as coisas mais familiares, ou seja, um tipo `bool` e valores `true` e `false`:

``` {.c .numberLines}
#include <stdio.h>
#include <stdbool.h>

int main(void) {
    bool x = true;

    if (x) {
        printf("x é verdadeiro!\n");
    }
}
```

<!-- But these are identical to using integer values for true and false.
They're just a facade to make things look nice. -->

Mas estes são idênticos ao uso de valores inteiros para verdadeiro e falso.
Eles são apenas uma fachada para tornar as coisas bonitas.

<!-- ## Operadores e Expressões {#operators} -->

## Operadores e Expressões {#operators}

<!-- C operators should be familiar to you from other languages. Let's blast
through some of them here. -->

Os operadores do C devem ser familiares para você em outros linguagens. Vamos explodir através de alguns deles aqui.

<!-- (There are a bunch more details than this, but we're going to do enough
in this section to get started.) -->

(Há muito mais detalhes do que isso, mas faremos o suficiente nesta seção para começar.)


<!-- ### Arithmetic -->

### Aritméticos

<!-- Hopefully these are familiar: -->

Espero que estes sejam familiares:

``` {.c}
i = i + 3; // Operadores de adição (+) e atribuição (=), adiciona 3 a i
i = i - 8; // Subtração, subtrair 8 de i
i = i * 9; // Multiplicação
i = i / 2; // Divisão
i = i % 5; // Módulo (resto da divisão)
```

<!-- There are shorthand variants for all of the above. Each of those lines
could more tersely be written as: -->

Existem variantes abreviadas para todos os itens acima. Cada uma dessas linhas poderia ser escrita mais concisamente como:

``` {.c}
i += 3;  // O mesmo que "i = i + 3", adiciona 3 a i
i -= 8;  // O mesmo que "i = i - 8"
i *= 9;  // O mesmo que "i = i * 9"
i /= 2;  // O mesmo que "i = i / 2"
i %= 5;  // O mesmo que "i = i % 5"
```

<!-- There is no exponentiation. You'll have to use one of the `pow()`
function variants from `math.h`. -->

Não há exponenciação. Você terá que usar uma das variantes da função `pow()` da `math.h`.

<!-- Let's get into some of the weirder stuff you might not have in your
other languages! -->

Vamos entrar em algumas das coisas mais estranhas que você pode não ter em suas outras linguagens!

<!-- ### Ternary Operator -->

### Operador Ternário

C also includes the _ternary operator_. This is an expression
whose value depends on the result of a conditional embedded in it.

C também inclui o _operador ternário_. Esta é uma expressão cujo valor depende do resultado de uma condicional incorporada a ela.

``` {.c}
// Se x > 10, adicione 17 a y. Caso contrário, adicione 37 a y.

y += x > 10? 17: 37;
```

<!-- What a mess! You'll get used to it the more you read it. To help out a
bit, I'll rewrite the above expression using `if` statements: -->

Que bagunça! Você vai se acostumar com isso quanto mais você lê-lo. Para ajudar um pouco, vou reescrever a expressão acima usando instruções `if`:

``` {.c}
// Esta expressão:

y += x > 10? 17: 37;

// é equivalente às seguintes instruções:

if (x > 10)
    y += 17;
else
    y += 37;
```

<!-- Compare those two until you see each of the components of the ternary
operator. -->

Compare esses dois até ver cada um dos componentes do operador ternário.

<!-- Or, another example that prints if a number stored in `x` is odd or
even: -->

Ou outro exemplo que imprime se um número armazenado em `x` for ímpar ou par:

``` {.c}
printf("O número %d é %s.\n", x, x % 2 == 0? "par": "ímpar")
```

<!-- The `%s` format specifier in `printf()` means print a string. If the
expression `x % 2` evaluates to `0`, the value of the entire ternary
expression evaluates to the string `"even"`. Otherwise it evaluates to
the string `"odd"`. Pretty cool! -->

O especificador de formato `%s` no `printf()` significa imprimir uma string. Se a expressão `x % 2` for avaliada como `0`, o valor de toda a expressão ternária será avaliado como a string `"par"`. Caso contrário, ele será avaliado como a string `"ímpar"`. Muito legal!

<!-- It's important to note that the ternary operator isn't flow control like
the `if` statement is. It's just an expression that evaluates to a value. -->

É importante notar que o operador ternário não é controle de fluxo como a instrução `if`. É apenas uma expressão que avalia um valor.

<!-- ### Pre-and-Post Increment-and-Decrement -->

### Pré-e-Pós-Incremento e Decremento

Now, let's mess with another thing that you might not have seen.

Agora, vamos mexer com outra coisa que você pode não ter visto.

These are the legendary post-increment and post-decrement operators:

Estes são os lendários operadores de pós-incremento e pós-decremento:

``` {.c}
i++;        // Adicione um a i (pós-incremento)
i--;        // Subtraia um de i (pós-decremento)
```

Very commonly, these are just used as shorter versions of:

Muito comumente, eles são usados apenas como versões mais curtas de:

``` {.c}
i += 1;        // Adiciona um a i
i -= 1;        // Subtrai um de i
```

<!-- but they're more subtly different than that, the clever scoundrels. -->

mas eles são mais sutilmente diferentes do que isso.

<!-- Let's take a look at this variant, pre-increment and pre-decrement: -->

Vamos dar uma olhada nesta variante, pré-incremento e pré-decremento:

``` {.c}
++i;        // Adicione um a i (pré-incremento)
--i;        // Subtraia um de i (pré-decremento)
```

<!-- With pre-increment and pre-decrement, the value of the variable is
incremented or decremented _before_ the expression is evaluated. Then
the expression is evaluated with the new value. -->

Com pré-incremento e pré-decremento, o valor da variável é incrementado ou decrementado _antes_ da expressão ser avaliada. Em seguida, a expressão é avaliada com o novo valor.

<!-- With post-increment and post-decrement, the value of the expression is
first computed with the value as-is, and _then_ the value is incremented
or decremented after the value of the expression has been determined. -->

Com pós-incremento e pós-decremento, o valor da expressão é calculado primeiro com o valor como está, e _então_ o valor é incrementado ou decrementado após o valor da expressão ter sido determinado.

<!-- You can actually embed them in expressions, like this: -->

Você pode realmente incorporá-los em expressões, assim:

``` {.c}
i = 10;
j = 5 + i++;  // Calcula 5 + i, _então_ incrementa i

printf("%d, %d\n", i, j);  // Imprime 11, 15
```

<!-- Let's compare this to the pre-increment operator: -->

Vamos comparar isso com o operador de pré-incremento:

``` {.c}
i = 10;
j = 5 + ++i;  // Incrementa i, _então_ calcula 5 + i

printf("%d, %d\n", i, j);  // Imprime 11, 16
```

<!-- This technique is used frequently with array and pointer access and
manipulation. It gives you a way to use the value in a variable, and
also increment or decrement that value before or after it is used. -->

Essa técnica é usada frequentemente com acesso e manipulação de arrays e ponteiros. Ele fornece uma maneira de usar o valor em uma variável e também aumentar ou diminuir esse valor antes ou depois de ser usado.

<!-- But by far the most common place you'll see this is in a `for` loop: -->

Mas, de longe, o lugar mais comum que você verá é em um loop `for`:

``` {.c}
for (i = 0; i < 10; i++)
    printf("i is %d\n", i);
```

<!-- But more on that later. -->

Mas mais sobre isso mais tarde.

<!-- ### The Comma Operator -->

### O operador de vírgula

<!-- This is an uncommonly-used way to separate expressions that will run
left to right: -->

Esta é uma maneira incomum de separar expressões que serão executadas da esquerda para a direita:

``` {.c}
x = 10, y = 20;  // Primeiro atribui 10 a x, depois 20 a y
```

<!-- Seems a bit silly, since you could just replace the comma with a
semicolon, right? -->

Parece um pouco bobo, já que você poderia substituir a vírgula por um ponto e vírgula, certo?

``` {.c}
x = 10; y = 20;  // Primeiro atribui 10 a x, depois 20 a y
```

<!-- But that's a little different. The latter is two separate expressions,
while the former is a single expression! -->

Mas isso é um pouco diferente. O último é duas expressões separadas, enquanto o primeiro é uma única expressão!

<!-- With the comma operator, the value of the comma expression is the value
of the rightmost expression: -->

Com o operador de vírgula, o valor da expressão de vírgula é o valor da expressão mais à direita:

``` {.c}
x = 1, 2, 3;

printf("x is %d\n", x);  // Imprime 3, porque 3 está mais à direita na lista de vírgulas
```

<!-- But even that's pretty contrived. One common place the comma operator is
used is in `for` loops to do multiple things in each section of the
statement: -->

Mas mesmo isso é bastante artificial. Um lugar comum em que o operador de vírgula é usado é em loops `for` para fazer várias coisas em cada seção da instrução:

``` {.c}
for (i = 0, j = 10; i < 100; i++, j++)
    printf("%d, %d\n", i, j);
```

<!-- We'll revisit that later. -->

Voltaremos a isso mais tarde.

<!-- ### Conditional Operators -->

### Operadores condicionais

<!-- For Boolean values, we have a raft of standard operators: -->

Para valores booleanos, temos uma série de operadores padrão:

``` {.c}
a == b; // Verdadeiro se a for equivalente a b
a != b; // Verdadeiro se a não for equivalente a b
a < b;  // Verdadeiro se a for menor que b
a > b;  // Verdadeiro se a for maior que b
a <= b; // Verdadeiro se a for menor ou igual a b
a >= b; // Verdadeiro se a for maior ou igual a b
```

<!-- Don't mix up assignment `=` with comparison `==`! Use two equals to
compare, one to assign. -->

Não confunda atribuição `=` com comparação `==`! Use dois iguais para comparar, um para atribuir.

<!-- We can use the comparison expressions with `if` statements: -->

Podemos usar as expressões de comparação com instruções `if`:

``` {.c}
if (a <= 10)
    printf("Success!\n");
```

<!-- ### Boolean Operators -->

### Operadores booleanos

<!-- We can chain together or alter conditional expressions with Boolean
operators for _and_, _or_, and _not_. -->

Podemos encadear ou alterar expressões condicionais com operadores booleanos _and_, _or_ e _not_.

|Operador|Significado booleano|Significado booleano (Inglês)|
|:------:|:-------------:|:-------------:|
|`&&`|e|and|
|`||`|ou|or|
|`!`|não|not|

<!-- An example of Boolean "and": -->

Um exemplo de booleano "and":

``` {.c}
// Faça algo se x menor que 10 e y maior que 20:

if (x < 10 && y > 20)
    printf("Fazendo algo!\n");
```

<!-- An example of Boolean "not": -->

Um exemplo de booleano "not":

``` {.c}
if (!(x < 12))
    printf("x não é menor que 12\n");
```

<!-- `!` has higher precedence than the other Boolean operators, so we have
to use parentheses in that case. -->

`!` tem maior precedência do que os outros operadores booleanos, então temos que usar parênteses nesse caso.

<!-- Of course, that's just the same as: -->

Claro, isso é exatamente o mesmo que:

``` {.c}
if (x >= 12)
    printf("x não é menor que 12\n");
```

<!-- but I needed the example! -->

mas eu precisava do exemplo!

<!-- ### The `sizeof` Operator {#sizeof-operator} -->

### O operador `sizeof` {#sizeof-operator}

<!-- This operator tells you the size (in bytes) that a particular variable
or data type uses in memory. -->

Este operador informa o tamanho (em bytes) que uma determinada variável ou tipo de dados usa na memória.

<!-- More particularly, it tells you the size (in bytes) that the _type of a
particular expression_ (which might be just a single variable) uses in
memory. -->

Mais especificamente, ele informa o tamanho (em bytes) que o _tipo de uma determinada expressão_ (que pode ser apenas uma única variável) usa na memória.

<!-- This can be different on different systems, except for `char` and its
variants (which are always 1 byte). -->

Isso pode ser diferente em sistemas diferentes, exceto para `char` e suas variantes (que são sempre de 1 byte).

<!-- And this might not seem very useful now, but we'll be making references
to it here and there, so it's worth covering. -->

E isso pode não parecer muito útil agora, mas faremos referências a ele aqui e ali, então vale a pena cobrir.

<!-- Since this computes the number of bytes needed to store a type, you
might think it would return an `int`. Or... since the size can't be
negative, maybe an `unsigned`? -->

Como isso calcula o número de bytes necessários para armazenar um tipo, você pode pensar que retornaria um `int`. Ou... já que o tamanho não pode ser negativo, talvez um `unsigned`?

<!-- But it turns out C has a special type to represent the return value from
`sizeof`. It's `size_t`, pronounced "_size tee_"^[The `_t` is short for
`type`.]. All we know is that it's an unsigned integer type that can
hold the size in bytes of anything you can give to `sizeof`. -->

Mas acontece que C tem um tipo especial para representar o valor de retorno de `sizeof`. É `size_t`, pronunciado "_size tee_"^[O `_t` é a abreviação de `type`.]. Tudo o que sabemos é que é um tipo inteiro sem sinal que pode conter o tamanho em bytes de qualquer coisa que você possa dar a `sizeof`.

<!-- `size_t` shows up a lot of different places where counts of things are
passed or returned. Think of it as a value that represents a count. -->

`size_t` mostra muitos lugares diferentes onde as contagens de coisas são passadas ou retornadas. 
Pense nisso como um valor que representa uma contagem.

<!-- +You can take the `sizeof` a variable or expression: -->

Você pode pegar o `sizeof` de uma variável ou expressão:

``` {.c}
int a = 999;

// %zu é o especificador de formato para o tipo size_t

printf("%zu\n", sizeof a);      // Imprime 4 no meu sistema
printf("%zu\n", sizeof(2 + 7)); // Imprime 4 no meu sistema
printf("%zu\n", sizeof 3.14);   // Imprime 8 no meu sistema

// // Se você precisar imprimir valores negativos de size_t, use %zd
```

<!-- Remember: it's the size in bytes of the _type_ of the expression, not
the size of the expression itself. That's why the size of `2+7` is the
same as the size of `a`---they're both type `int`. We'll revisit this
number `4` in the very next block of code... -->

Lembre-se: é o tamanho em bytes do _type_ da expressão, não o tamanho da expressão em si. É por isso que o tamanho de `2+7` é o mesmo que o tamanho de `a`---ambos são do tipo `int`. Revisitaremos este número `4` no próximo bloco de código...

<!-- ...Where we'll see you can take the `sizeof` a type (note the
parentheses are required around a type name, unlike an expression): -->

...Onde veremos que você pode pegar o `sizeof` de um tipo (observe que os parênteses são necessários em torno de um nome de tipo, diferente de uma expressão):

``` {.c}
printf("%zu\n", sizeof(int));   // Imprime 4 no meu sistema
printf("%zu\n", sizeof(char));  // Imprime 1 em todos os sistemas
```

<!-- It's important to note that `sizeof` is a _compile-time_
operation^[Except for with variable length arrays---but that's a story
for another time.]. The result of the expression is determined entirely
at compile-time, not at runtime. -->

É importante notar que `sizeof` é uma operação em _tempo de compilação_^[Exceto para arrays de comprimento variável---mas isso é uma história para outra hora.]. O resultado da expressão é determinado inteiramente em tempo de compilação, não em tempo de execução.

<!-- We'll make use of this later on. -->

Faremos uso disso mais adiante.

<!-- ## Flow Control -->

## Controle de fluxo

<!-- Booleans are all good, but of course we're nowhere if we can't control
program flow. Let's take a look at a number of constructs: `if`, `for`,
`while`, and `do-while`. -->

Booleanos são bons, mas é claro que não estamos em lugar nenhum se não podemos controlar o fluxo do programa. Vamos dar uma olhada em várias construções: `if`, `for`, `while` e `do-while`.

<!-- First, a general forward-looking note about statements and blocks of
statements brought to you by your local friendly C developer: -->

Primeiro, uma nota prospectiva geral sobre declarações e blocos de declarações trazidos a você por seu desenvolvedor C local amigável:

<!-- After something like an `if` or `while` statement, you can either put a single
statement to be executed, or a block of statements to all be executed in
sequence. -->

Depois de algo como uma instrução `if` ou `while`, você pode colocar uma única instrução para ser executada ou um bloco de instruções para que todas sejam executadas em sequência.

<!-- Let's start with a single statement: -->

Vamos começar com uma única declaração:

``` {.c}
if (x == 10) printf("x é 10\n");
```

<!-- This is also sometimes written on a separate line. (Whitespace is largely
irrelevant in C---it's not like Python.) -->

Às vezes, isso também é escrito em uma linha separada. (Espaço em branco é amplamente irrelevante em C---não é como Python.)

``` {.c}
if (x == 10)
    printf("x é 10\n");
```

<!-- But what if you want multiple things to happen due to the conditional?
You can use squirrelly braces to mark a _block_ or _compound statement_. -->

Mas e se você quiser que várias coisas aconteçam devido à condição?
Você pode usar chaves para marcar um _bloco_ ou _declaração composta_.

``` {.c}
if (x == 10) {
    printf("x é 10\n");
    printf("E isso também acontece quando x é 10\n");
}
```

<!-- It's a really common style to _always_ use squirrelly braces even if
they aren't necessary: -->

É um estilo muito comum usar _sempre_ chaves mesmo que não sejam necessárias:

``` {.c}
if (x == 10) {
    printf("x é 10\n");
}
```

<!-- Some devs feel the code is easier to read and avoids errors like this
where things visually look like they're in the `if` block, but actually
they aren't. -->

Alguns desenvolvedores acham que o código é mais fácil de ler e evita erros como este, onde as coisas parecem visualmente que estão no bloco `if`, mas na verdade não estão.

``` {.c}
// EXEMPLO DE "ERRO"

if (x == 10)
    printf("Isso acontece se x for 10\n");
    printf("Isso acontece SEMPRE\n"); // Surpresa!! Incondicional!
```

<!-- `while` and `for` and the other looping constructs work the same way as
the examples above. If you want to do multiple things in a loop or after
an `if`, wrap them up in squirrelly braces. -->

`while` e `for` e as outras construções de loop funcionam da mesma forma que os exemplos acima. Se você quiser fazer várias coisas em um loop ou depois de um `if`, envolva-as em chaves.

<!-- In other words, the `if` is going to run the one thing after the `if`.
And that one thing can be a single statement or a block of statements. -->

Em outras palavras, o `if` vai executar a única coisa após o `if`.
E essa coisa pode ser uma única instrução ou um bloco de instruções.

### The `if`-`else` statement {#ifstat}

### A instrução `if`-`else` {#ifstat}

<!-- We've already been using `if` for multiple examples, since it's likely
you've seen it in a language before, but here's another: -->

Já usamos `if` para vários exemplos, pois é provável que você já tenha visto isso em uma outra linguagem antes, mas aqui está outro:

``` {.c}
int i = 10;

if (i > 10) {
    printf("Sim, i é maior que 10.\n");
    printf("E isso também será impresso se i for maior que 10.\n");
}

if (i <= 10) printf("i é menor ou igual a 10.\n");
```

<!-- In the example code, the message will print if `i` is greater than 10,
otherwise execution continues to the next line. Notice the squirrley
braces after the `if` statement; if the condition is true, either the
first statement or expression right after the if will be executed, or
else the collection of code in the squirlley braces after the `if` will
be executed. This sort of _code block_ behavior is common to all
statements. -->

No código de exemplo, a mensagem será impressa se `i` for maior que 10, caso contrário, a execução continua para a próxima linha. Observe as chaves após a instrução `if`; se a condição for verdadeira, a primeira instrução ou expressão logo após o if será executada, ou então a coleção de código nas chaves após o `if` será executada. Esse tipo de comportamento de _bloco de código_ é comum a todas as instruções.

<!-- Of course, because C is fun this way, you can also do something if the
condition is false with an `else` clause on your `if`: -->

Claro, porque C é divertido dessa maneira, você também pode fazer algo se a condição for falsa com uma cláusula `else` em seu `if`:

``` {.c}
int i = 99;

if (i == 10)
    printf("i é 10!\n");
else {
    printf("i definitivamente não é 10.\n");
    printf("O que me irrita um pouco, francamente.\n");
}
```

<!-- And you can even cascade these to test a variety of conditions, like
this: -->

E você pode até mesmo cascateá-los para testar uma variedade de condições, como esta:

``` {.c}
int i = 99;

if (i == 10)
    printf("i é 10!\n");

else if (i == 20)
    printf("i é 20!\n");

else if (i == 99) {
    printf("é 99! Meu favorito\n");
    printf("Não posso dizer o quanto estou feliz.\n");
    printf("Realmente.\n");
}
    
else
    printf("i é um número maluco que nunca ouvi falar.\n");
```

<!-- Though if you're going that route, be sure to check out the
[`switch`](#switch-statement) statement for a potentially better
solution. The catch is `switch` only works with equality comparisons
with constant numbers. The above `if`-`else` cascade could check
inequality, ranges, variables, or anything else you can craft in a
conditional expression. -->

No entanto, se você estiver seguindo esse caminho, verifique a instrução [`switch`](#switch-statement) para uma solução potencialmente melhor. O problema é que `switch` só funciona com comparações de igualdade com números constantes. A cascata `if`-`else` acima pode verificar desigualdade, intervalos, variáveis ou qualquer outra coisa que você possa criar em uma expressão condicional.

<!-- ### The `while` statement {#whilestat} -->

### A instrução `while` {#whilestat}

<!-- `while` is your average run-of-the-mill looping construct. Do a thing while a condition
expression is true. -->

`while` é sua construção de loop comum. Faça algo enquanto uma expressão de condição for verdadeira.

<!-- Let's do one! -->

Vamos fazer um!

``` {.c}
// Imprime a seguinte saída:
//
//   i agora é 0!
//   i agora é 1!
//   [ mais do mesmo entre 2 e 7 ]
//   agora tenho 8!
//   agora tenho 9!

i = 0;

while (i < 10) {
    printf("i agora é %d!\n", i);
    i++;
}

printf("Tudo pronto!\n");
```

<!-- That gets you a basic loop. C also has a `for` loop which would have
been cleaner for that example. -->

Isso lhe dá um loop básico. C também tem um loop `for` que seria mais limpo para esse exemplo.

<!-- A not-uncommon use of `while` is for infinite loops where you repeat
while true: -->

Um uso não incomum de `while` é para loops infinitos onde você repete while true:

``` {.c}
while (1) {
    printf("1 é sempre verdadeiro, então isso se repete para sempre.\n");
}
```


<!-- ### The `do-while` statement {#dowhilestat} -->

### A instrução `do-while` {#dowhilestat}

<!-- So now that we've gotten the `while` statement under control, let's take
a look at its closely related cousin, `do-while`. -->

Então agora que temos o comando `while` sob controle, vamos dar uma olhada em seu primo relacionado, `do-while`.

<!-- They are basically the same, except if the loop condition is false on
the first pass, `do-while` will execute once, but `while` won't execute
at all. In other words, the test to see whether or not to execute the
block happens at the _end_ of the block with `do-while`. It happens at
the _beginning_ of the block with `while`. -->

Eles são basicamente os mesmos, exceto se a condição do loop for falsa na primeira passagem, o `do-while` será executado uma vez, mas o `while` não será executado. Em outras palavras, o teste para ver se deve ou não executar o bloco acontece no _final_ do bloco com `do-while`. Isso acontece no _início_ do bloco com `while`.

<!-- Let's see by example: -->

Vejamos por exemplo:

``` {.c}
// Usando uma instrução while:

i = 10;

// isso não é executado porque i não é menor que 10:
while(i < 10) {
    printf("while: i é %d\n", i);
    i++;
}

// Usando a instrução do-while:

i = 10;

// isso é executado uma vez, porque a condição do loop não é verificada
// até que o corpo do loop seja executado:

do {
    printf("do-while: i is %d\n", i);
    i++;
} while (i < 10);

printf("Tudo pronto!\n");
```

<!-- Notice that in both cases, the loop condition is false right away. So in
the `while`, the loop fails, and the following block of code is never
executed. With the `do-while`, however, the condition is checked _after_
the block of code executes, so it always executes at least once. In this
case, it prints the message, increments `i`, then fails the condition,
and continues to the "All done!" output. -->

Observe que em ambos os casos, a condição de loop é falsa imediatamente. Portanto, no `while`, o loop falha e o bloco de código a seguir nunca é executado. Com o `do-while`, entretanto, a condição é verificada _depois_ que o bloco de código é executado, então ele sempre executa pelo menos uma vez. Nesse caso, ele imprime a mensagem, incrementa `i`, falha a condição e continua para "Tudo pronto!".

<!-- The moral of the story is this: if you want the loop to execute at least
once, no matter what the loop condition, use `do-while`. -->

A moral da história é esta: se você quiser que o loop seja executado pelo menos uma vez, não importa qual seja a condição do loop, use `do-while`.

<!-- All these examples might have been better done with a `for` loop. Let's
do something less deterministic---repeat until a certain random number
comes up! -->

Todos esses exemplos poderiam ter sido melhor feitos com um loop `for`. Vamos fazer algo menos determinístico---repetir até que um certo número aleatório apareça!

``` {.c .numberLines}
#include <stdio.h>   // Para printf
#include <stdlib.h>  // Para rand

int main(void)
{
    int r;

    do {
        r = rand() % 100; // Obter um número aleatório entre 0 e 99
        printf("%d\n", r);
    } while (r != 37);    // Repita até 37 aparecer
}
```

<!-- Side note: did you run that more than once? If you did, did you notice
the same sequence of numbers came up again. And again. And again? This
is because `rand()` is a pseudorandom number generator that must be
_seeded_ with a different number in order to generate a different
sequence. Look up the [`srand()`](#man-srand) function for more details. -->

Nota lateral: você executou isso mais de uma vez? Se você fez, você notou que a mesma sequência de números apareceu novamente. E de novo. E de novo? Isso ocorre porque `rand()` é um gerador de números pseudoaleatórios que deve ser _seeded_ (semeado) com um número diferente para gerar uma sequência diferente. Procure a função [`srand()`](#man-srand) para mais detalhes.

<!-- ### The `for` statement {#forstat} -->

### A instrução `for` {#forstat}

<!-- Welcome to one of the most popular loops in the world! The `for` loop! -->

Bem-vindo a um dos loops mais populares do mundo! O laço `for`!

<!-- This is a great loop if you know the number of times you want to loop in
advance. -->

Este é um ótimo loop se você souber o número de vezes que deseja fazer o loop com antecedência.

<!-- You could do the same thing using just a `while` loop, but the `for`
loop can help keep the code cleaner. -->

Você pode fazer a mesma coisa usando apenas um loop `while`, mas o loop `for` pode ajudar a manter o código mais limpo.

<!-- Here are two pieces of equivalent code---note how the `for` loop is just
a more compact representation: -->

Aqui estão dois pedaços de código equivalente---note como o loop `for` é apenas uma representação mais compacta:

``` {.c}
// Imprime números entre 0 e 9, inclusive...

// Usando a instrução while:

i = 0;
while (i < 10) {
    printf("i é %d\n", i);
    i++;
}

// Faça exatamente a mesma coisa com um loop for:

for (i = 0; i < 10; i++) {
    printf("i é %d\n", i);
}
```

<!-- That's right, folks---they do exactly the same thing. But you can see
how the `for` statement is a little more compact and easy on the eyes.
(JavaScript users will fully appreciate its C origins at this point.) -->

Isso mesmo, pessoal---eles fazem exatamente a mesma coisa. Mas você pode ver como a instrução `for` é um pouco mais compacta e agradável aos olhos. (Os usuários de JavaScript irão apreciar plenamente suas origens C neste momento.)

It's split into three parts, separated by semicolons. The first is the
initialization, the second is the loop condition, and the third is what
should happen at the end of the block if the loop condition is true. All
three of these parts are optional.

Está dividido em três partes, separadas por ponto e vírgula. A primeira é a inicialização, a segunda é a condição de loop e a terceira é o que deve acontecer no final do bloco se a condição de loop for verdadeira. Todas essas três partes são opcionais.

``` {.c}
for (inicialize as coisas; faça um loop se isso for verdade; faça isso após cada loop)
```

<!-- Note that the loop will not execute even a single time if the loop
condition starts off false. -->

Observe que o loop não será executado nem uma única vez se a condição do loop começar como falsa.

<!-- > **`for`-loop fun fact!**
>
> You can use the comma operator to do multiple things in each clause of
> the `for` loop!
>
> ``` {.c}
> for (i = 0, j = 999; i < 10; i++, j--) {
>     printf("%d, %d\n", i, j);
> }
> ``` -->

> **`for`-loop fato divertido!**
>
> Você pode usar o operador vírgula para fazer várias coisas em cada cláusula
> do loop `for`!
>
> ``` {.c}
> for (i = 0, j = 999; i < 10; i++, j--) {
>     printf("%d, %d\n", i, j);
> }
> ```

<!-- An empty `for` will run forever: -->

Um `for` vazio será executado para sempre:

``` {.c}
for(;;) {  // "para sempre"
    printf("Vou imprimir isso de novo e de novo e de novo\n");
    printf("por toda a eternidade até a morte por calor do universo.\n");

    printf("Ou até você pressionar CTRL-C.\n");
}
```

<!-- ### The `switch` Statement {#switch-statement} -->

### A instrução `switch` {#switch-statement}

<!-- Depending on what languages you're coming from, you might or might not
be familiar with `switch`, or C's version might even be more restrictive
than you're used to. This is a statement that allows you to take a
variety of actions depending on the value of an integer expression. -->

Dependendo de quais linguagens você está vindo, você pode ou não estar familiarizado com o `switch`, ou a versão do C pode até ser mais restritiva do que você está acostumado. Esta é uma instrução que permite que você execute uma variedade de ações dependendo do valor de uma expressão inteira.

<!-- Basically, it evaluates an expression to an integer value, jumps to the
`case` that corresponds to that value. Execution resumes from that
point. If a `break` statement is encountered, then execution jumps out
of the `switch`. -->

Basicamente, ele avalia uma expressão para um valor inteiro, pula para o `case` que corresponde a esse valor. A execução recomeça a partir desse ponto. Se uma instrução `break` for encontrada, então a execução salta do `switch`.

<!-- Let's do an example where the user enters a number of goats and we print
out a gut-feel of how many goats that is. -->

Vamos fazer um exemplo onde o usuário digita um número de cabras e nós imprimimos uma intuição de quantas cabras são.

``` {.c .numberLines}
#include <stdio.h>

int main(void)
{
    int goat_count;

    printf("Digite uma contagem de cabras: ");
    scanf("%d", &goat_count);       // Ler um inteiro do teclado

    switch (goat_count) {
        case 0:
            printf("Você não tem cabras.\n");
            break;

        case 1:
            printf("Você tem uma única cabra.\n");
            break;

        case 2:
            printf("Você tem um par de cabras.\n");
            break;

        default:
            printf("Você tem uma infinidade genuína de cabras!\n");
            break;
    }
}
```

<!-- In that example, if the user enters, say, `2`, the `switch` will jump to
the `case 2` and execute from there. When (if) it hits a `break`, it
jumps out of the `switch`. -->

Nesse exemplo, se o usuário digitar, digamos, `2`, o `switch` pulará para o `case 2` e será executado a partir daí. Quando (se) atinge um `break`, ele salta para fora do `switch`.

<!-- Also, you might see that `default` label there at the bottom. This is
what happens when no cases match. -->

Além disso, você pode ver esse rótulo `default` na parte inferior. Isso é o que acontece quando nenhum caso coincide.

<!-- Every `case`, including `default`, is optional. And they can occur in
any order, but it's really typical for `default`, if any, to be listed
last. -->

Cada `case`, incluindo `default`, é opcional. E eles podem ocorrer em qualquer ordem, mas é realmente típico que `default`, se houver, seja listado por último.

<!-- So the whole thing acts like an `if`-`else` cascade: -->

Então a coisa toda age como uma cascata `if`-`else`:

``` {.c}
if (goat_count == 0)
    printf("Você não tem cabras.\n");
else if (goat_count == 1)
    printf("Você tem uma única cabra.\n");
else if (goat_count == 2)
    printf("Você tem um par de cabras.\n");
else
    printf("Você tem uma infinidade genuína de cabras!\n");
```

<!-- With some key differences: -->

Com algumas diferenças importantes:

<!-- * `switch` is often faster to jump to the correct code (though the spec
  makes no such guarantee).
* `if`-`else` can do things like relational conditionals like `<` and
  `>=` and floating point and other types, while `switch` cannot. -->

* `switch` é muitas vezes mais rápido para pular para o código correto (embora a especificação não faça tal garantia).
* `if`-`else` pode fazer coisas como condicionais relacionais como `<` e `>=` e ponto flutuante e outros tipos, enquanto `switch` não pode.

<!-- There's one more neat thing about switch that you sometimes see that is
quite interesting: _fall through_. -->

Há mais uma coisa interessante sobre o switch que você às vezes vê que é bastante interessante: _fall through_.

<!-- Remember how `break` causes us to jump out of the switch? -->

Lembra como `break` nos faz pular para fora do switch?

<!-- Well, what happens if we _don't_ `break`? -->

Bem, o que acontece se nós _não_ `quebrarmos`?

<!-- Turns out we just keep on going into the next `case`! Demo! -->

Acontece que continuamos indo para o próximo `caso`! Demonstração!

``` {.c}
switch (x) {
    case 1:
        printf("1\n");
        // Fall through!
    case 2:
        printf("2\n");
        break;
    case 3:
        printf("3\n");
        break;
}
```

<!-- If `x == 1`, this `switch` will first hit `case 1`, it'll print the `1`,
but then it just continues on to the next line of code... which prints
`2`! -->

Se `x == 1`, este `switch` atingirá primeiro o `case 1`, ele imprimirá o `1`, mas então apenas continua para a próxima linha de código... que imprime `2`!

<!-- And then, at last, we hit a `break` so we jump out of the `switch`. -->

E então, finalmente, acertamos um `break`, então saímos do `switch`.

<!-- if `x == 2`, then we just hit the `case 2`, print `2`, and `break` as
normal. -->

se `x == 2`, então nós apenas acertamos no `case 2`, imprimimos `2` e `break` normalmente.

<!-- Not having a `break` is called _fall through_. -->

Não ter um `break` é chamado de _fall through_.

<!-- ProTip: _ALWAYS_ put a comment in the code where you intend to fall
through, like I did above. It will save other programmers from wondering
if you meant to do that. -->

Dica: _SEMPRE_ coloque um comentário no código onde você pretende o _fall through_, como eu fiz acima. Isso evitará que outros programadores se perguntem se você pretendia fazer isso.

<!-- In fact, this is one of the common places to introduce bugs in C
programs: forgetting to put a `break` in your `case`. You gotta do it if
you don't want to just roll into the next case^[This was considered
such a hazard that the designers of the Go Programming Language made
`break` the default; you have to explicitly use Go's `fallthrough`
statement if you want to fall into the next case.]. -->

Na verdade, este é um dos lugares comuns para introduzir bugs em programas C: esquecer de colocar um `break` no seu `case`. Você tem que fazer isso se não quiser apenas passar para o próximo caso^[Isto foi considerado um perigo tão grande que os designers da linguagem de programação Go tornaram `break` o padrão; você tem que usar explicitamente a declaração `fallthrough` do Go se quiser cair no próximo caso.].

<!-- Earlier I said that `switch` works with integer types---keep it that
way. Don't use floating point or string types in there. One loophole-ish
thing here is that you can use character types because those are
secretly integers themselves. So this is perfectly acceptable: -->

Anteriormente eu disse que `switch` funciona com tipos inteiros---mantenha assim. Não use ponto flutuante ou tipos de string lá. Uma brecha aqui é que você pode usar tipos de caracteres porque eles são secretamente inteiros. Então isso é perfeitamente aceitável:

``` {.c}
char c = 'b';

switch (c) {
    case 'a':
        printf("É 'a'!\n");
        break;

    case 'b':
        printf("É 'b'!\n");
        break;

    case 'c':
        printf("É 'c'!\n");
        break;
}
```

<!-- Finally, you can use `enum`s in `switch` since they are also integer
types. But more on that in the `enum` chapter. -->

Finalmente, você pode usar `enum`s em `switch` já que eles também são tipos inteiros. Mas mais sobre isso no capítulo `enum`.