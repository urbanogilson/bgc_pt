<!-- Beej's guide to C

# vim: ts=4:sw=4:nosi:et:tw=72
-->

<!-- No hyphenation -->
[nh[scalbn]]
[nh[scalbnf]]
[nh[scalbnl]]
[nh[scalbln]]
[nh[scalblnf]]
[nh[scalblnl]]
<!-- Can't do things that aren't letters
[nh[atan2]]
[nh[atan2f]]
[nh[atan2l]]
-->
[nh[lrint]]
[nh[lrintf]]
[nh[lrintl]]
[nh[llrint]]
[nh[llrintf]]
[nh[llrintl]]
[nh[lround]]
[nh[lroundf]]
[nh[lroundl]]
[nh[llround]]
[nh[llroundf]]
[nh[llroundl]]

<!-- # Foreword -->

# Prefácio

<!-- No point in wasting words here, folks, let's jump straight into the C
code: -->

Não vale a pena desperdiçar palavras aqui, pessoal, vamos direto para o código em C:

``` {.c}
E((ck?main((z?(stat(M,&t)?P+=a+'{'?0:3:
execv(M,k),a=G,i=P,y=G&255,
sprintf(Q,y/'@'-3?A(*L(V(%d+%d)+%d,0)
```

<!-- And they lived happily ever after. The End. -->

E eles viveram felizes para sempre. Fim.

<!-- What's this? You say something's still not clear about this whole C
programming language thing? -->

O que é isso? Você diz que algo ainda não está claro sobre toda essa coisa de linguagem de programação C?

<!-- Well, to be quite honest, I'm not even sure what the above code does.
It's a snippet from one of the entries in the 2001 [fl[International
Obfuscated C Code Contest|https://www.ioccc.org/]], a wonderful
competition wherein the entrants attempt to write the most unreadable C
code possible, with often surprising results. -->

Bem, para ser bem honesto, nem eu tenho certeza do que o código acima faz.
Este é um trecho de uma das entradas no [fl[Concurso Internacional de Código C Ofuscado|https://www.ioccc.org/]] de 2001, uma competição maravilhosa em que os participantes tentam escrever o código C mais ilegível possível, com resultados muitas vezes surpreendentes.

<!-- The bad news is that if you're a beginner in this whole thing, all C
code you see probably looks obfuscated! The good news is, it's not
going to be that way for long. -->

A má notícia é que, se você é iniciante nessa coisa toda, todo o código C que você vê provavelmente parece ofuscado! A boa notícia é que não vai ser assim por muito tempo.

<!-- What we'll try to do over the course of this guide is lead you from complete and utter sheer lost confusion on to the sort of enlightened bliss that can only be obtained though pure C programming. Right on. -->

O que vamos tentar fazer ao longo deste guia é levá-lo da completa e absoluta confusão perdida para o tipo de felicidade iluminada que só pode ser obtida através da programação C pura. Pode apostar.

<!-- ## Audience -->

## Público

<!-- This guide assumes that you've already got some programming knowledge
under your belt from another language, such as
[flw[Python|Python_(programming_language)]],
[flw[JavaScript|JavaScript]], [flw[Java|Java_(programming_language)]],
[flw[Rust|Rust_(programming_language)]],
[flw[Go|Go_(programming_language)]],
[flw[Swift|Swift_(programming_language)]], etc.
([flw[Objective-C|Objective-C]] devs will have a particularly easy time
of it!) -->

Este guia pressupõe que você já tenha algum conhecimento em outra linguagem programação, como 
[flw[Python|Python_(programming_language)]],
[flw[JavaScript|JavaScript]],
[flw[Java|Java_(programming_language)]],
[flw[Rust|Rust_(programming_language)]],
[flw[Go|Go_(programming_language)]],
[flw[Swift|Swift_(programming_language)]], etc.
(Desenvolvedores [flw[Objective-C|Objective-C]] terão um jornada particularmente fácil!!)
 
<!-- We're going to assume you know what variables are, what loops do, how
functions work, and so on. -->

Estamos assumindo que você saiba o que são variáveis, o que os laços de repetição fazem, como as funções funcionam e assim por diante.

<!-- If that's not you for whatever reason the best I can hope to provide is
some pastey entertainment for your reading pleasure. The only thing I
can reasonably promise is that this guide won't end on a
cliffhanger... or _will_ it? -->

Se esse não for o seu caso por quaisquer que sejam os motivos, o melhor que posso oferecer é algum entretenimento pálido para o seu prazer de leitura. A única coisa que posso razoavelmente prometer é que este guia não terminará em um *cliffhanger*... ou será que vai?

<!-- ## Platform and Compiler -->

## Plataforma e compilador

<!-- I'll try to stick to Plain Ol'-Fashioned [flw[ISO-standard C|ANSI_C]].
Well, for the most part. Here and there I might go crazy and start
talking about [flw[POSIX|POSIX]] or something, but we'll see. -->

Vou tentar manter o simples e estiloso [flw[padrão ISO C|ANSI_C]].
Bem, para a maioria. Aqui e ali eu posso enlouquecer e começar a falar sobre [flw[POSIX|POSIX]] ou algo assim, mas vamos ver.

<!-- **Unix** users (e.g. Linux, BSD, etc.) try running `cc` or `gcc` from
the command line--you might already have a compiler installed. If you
don't, search your distribution for installing `gcc` or `clang`. -->

Usuários de **Unix** (e.g. Linux, BSD, etc.) tentem executar `cc` ou `gcc` a partir da linha de comando--talvez você já tenha um compilador instalado.
Se você não tiver, procure por sua distribuição para instalar `gcc` ou `clang`.

<!-- **Windows** users should check out [fl[Visual Studio
Community|https://visualstudio.microsoft.com/vs/community/]]. Or, if
you're looking for a more Unix-like experience (recommended!), install
[fl[WSL|https://docs.microsoft.com/en-us/windows/wsl/install-win10]] and
`gcc`. -->

Usuários do **Windows** devem conferir a [fl[Comunidade do Visual Studio|https://visualstudio.microsoft.com/vs/community/]].
Ou, se você estiver procurando por uma experiência mais parecida com o Unix (recomendado!), instale [fl[WSL|https://docs.microsoft.com/en-us/windows/wsl/install-win10]] e ` gcc`.

<!-- **Mac** users will want to install
[fl[XCode|https://developer.apple.com/xcode/]], and in particular the
command line tools. -->

Os usuários do **Mac** devem instalar o [fl[XCode|https://developer.apple.com/xcode/]], e em particular as ferramentas de linha de comando.

<!-- There are a lot of compilers out there, and virtually all of them will
work for this book. And a C++ compiler will compile a lot of (but not
all!) C code. Best use a proper C compiler if you can. -->

Existem muitos compiladores por aí, e praticamente todos eles funcionarão para este livro. E um compilador C++ compilará muito (mas não todos!) códigos C. Melhor usar um compilador específico para C, se puder.

<!-- ## Official Homepage -->

## Página oficial

<!-- This official location of this document is
[fl[https://beej.us/guide/bgc/|https://beej.us/guide/bgc/]]. Maybe
this'll change in the future, but it's more likely that all the other
guides are migrated off Chico State computers. -->

A localização oficial deste documento é [fl[https://beej.us/guide/bgc/|https://beej.us/guide/bgc/]]. Talvez isso mude no futuro, mas é mais provável que todos os outros guias sejam migrados dos computadores da Chico State.

<!-- ## Email Policy -->

## Política de e-mail

<!-- I'm generally available to help out with email questions so feel free to
write in, but I can't guarantee a response. I lead a pretty busy life
and there are times when I just can't answer a question you have. When
that's the case, I usually just delete the message. It's nothing
personal; I just won't ever have the time to give the detailed answer
you require. -->

Estou geralmente disponível para ajudar com perguntas por e-mail, então sinta-se à vontade para escrever, mas não posso garantir uma resposta. Eu levo uma vida muito ocupada e há momentos em que eu simplesmente não consigo responder a uma pergunta que você tem.
Quando esse é o caso, geralmente eu apenas apago a mensagem. Não é nada pessoal; Eu simplesmente não terei tempo para dar a resposta detalhada que você precisa.

<!-- As a rule, the more complex the question, the less likely I am to
respond. If you can narrow down your question before mailing it and be
sure to include any pertinent information (like platform, compiler,
error messages you're getting, and anything else you think might help me
troubleshoot), you're much more likely to get a response. -->

Como regra, quanto mais complexa a pergunta, menos provável é que eu responda. Se você puder restringir sua pergunta antes de enviá-la e incluir todas as informações pertinentes (como plataforma, compilador, mensagens de erro que está recebendo e qualquer outra coisa que possa me ajudar a solucionar problemas), é muito mais provável que você receba uma resposta.

<!-- If you don't get a response, hack on it some more, try to find the
answer, and if it's still elusive, then write me again with the
information you've found and hopefully it will be enough for me to help
out. -->

Se você não obtiver uma resposta, tente mais um pouco, tente encontrar a resposta e, se ainda for indescritível, escreva-me novamente com as informações que encontrou e espero que seja suficiente para eu ajudar.

<!-- Now that I've badgered you about how to write and not write me, I'd just
like to let you know that I _fully_ appreciate all the praise the guide
has received over the years. It's a real morale boost, and it gladdens
me to hear that it is being used for good! `:-)` Thank you! -->

Agora que eu o importunei sobre como escrever e não me escrever, gostaria apenas de informar que aprecio _plenamente_ todos os elogios que o guia recebeu ao longo dos anos. É um verdadeiro impulso moral, e me alegra saber que está sendo usado para o bem! `:-)` Obrigado!

<!-- ## Mirroring -->

## Espelhamento

<!-- You are more than welcome to mirror this site, whether publicly or
privately. If you publicly mirror the site and want me to link to it
from the main page, drop me a line at
[`beej@beej.us`](mailto:beej@beej.us). -->

Você é mais do que bem-vindo para espelhar este site, seja de forma pública ou privada. Se você espelhar publicamente o site e quiser que eu vincule a ele na página principal, mande-me um email para [`beej@beej.us`](mailto:beej@beej.us).

<!-- ## Note for Translators -->

## Nota para tradutores

<!-- If you want to translate the guide into another language, write me at
[`beej@beej.us`](beej@beej.us) and I'll link to your translation from
the main page. Feel free to add your name and contact info to the
translation. -->

Se você quiser traduzir o guia para outro idioma, escreva-me para [`beej@beej.us`](beej@beej.us) e eu linkarei sua tradução na página principal. Sinta-se à vontade para adicionar seu nome e informações de contato à tradução.

<!-- Please note the license restrictions in the Copyright and Distribution
section, below. -->

Observe as restrições de licença na seção Direitos autorais e distribuição, abaixo.

<!-- ## Copyright and Distribution -->

## Direitos autorais e distribuição

<!-- Beej's Guide to C is Copyright © 2021 Brian "Beej Jorgensen" Hall. -->

O Guia do Beej para C é Copyright © 2021 Brian "Beej Jorgensen" Hall.

<!-- With specific exceptions for source code and translations, below, this
work is licensed under the Creative Commons Attribution-Noncommercial-No
Derivative Works 3.0 License. To view a copy of this license, visit
[`https://creativecommons.org/licenses/by-nc-nd/3.0/`](https://creativecommons.org/licenses/by-nc-nd/3.0/)
or send a letter to Creative Commons, 171 Second Street, Suite 300, San
Francisco, California, 94105, USA. -->

Com exceções específicas para código-fonte e traduções, abaixo, esta obra está licenciada sob a Creative Commons Attribution-Noncommercial-No Derivative Works 3.0 License. Para ver uma cópia desta licença, visite [`https://creativecommons.org/licenses/by-nc-nd/3.0/`](https://creativecommons.org/licenses/by-nc-nd/3.0/) ou envie uma carta para Creative Commons, 171 Second Street, Suite 300, San Francisco, California, 94105, USA.

<!-- One specific exception to the "No Derivative Works" portion of the
license is as follows: this guide may be freely translated into any
language, provided the translation is accurate, and the guide is
reprinted in its entirety. The same license restrictions apply to the
translation as to the original guide. The translation may also include
the name and contact information for the translator. -->

Uma exceção específica à parte "No Derivative Works" da licença é a seguinte: este guia pode ser traduzido livremente para qualquer idioma, desde que a tradução seja precisa e o guia seja reimpresso em sua totalidade. As mesmas restrições de licença se aplicam à tradução e ao guia original. A tradução também pode incluir o nome e as informações de contato do tradutor.

<!-- The C source code presented in this document is hereby granted to the
public domain, and is completely free of any license restriction. -->

O código-fonte C apresentado neste documento é concedido ao domínio público e está completamente livre de qualquer restrição de licença.

<!-- Educators are freely encouraged to recommend or supply copies of this
guide to their students. -->

Os educadores são livremente encorajados a recomendar ou fornecer cópias deste guia a seus alunos.

<!-- Contact [`beej@beej.us`](beej@beej.us) for more information. -->

Entre em contato com [`beej@beej.us`](beej@beej.us) para obter mais informações.

<!-- ## Dedication -->

## Dedicatoria

<!-- The hardest things about writing these guides are: -->

As coisas mais difíceis de escrever esses guias são:

<!-- * Learning the material in enough detail to be able to explain it
* Figuring out the best way to explain it clearly, a seemingly-endless
  iterative process
* Putting myself out there as a so-called _authority_, when really
  I'm just a regular human trying to make sense of it all, just like
  everyone else
* Keeping at it when so many other things draw my attention -->

* Aprender o material com detalhes suficientes para poder explicá-lo
* Descobrir a melhor maneira de explicá-lo claramente, um processo iterativo aparentemente interminável
* Me colocar como uma suposta _autoridade_, quando na verdade sou apenas um humano normal tentando entender tudo, assim como todo mundo
* Continuando quando tantas outras coisas chamam minha atenção

<!-- A lot of people have helped me through this process, and I want to
acknowledge those who have made this book possible. -->

Muitas pessoas me ajudaram nesse processo, e quero agradecer àqueles que tornaram este livro possível.

<!-- * Everyone on the Internet who decided to help share their knowledge in
  one form or another. The free sharing of instructive information is
  what makes the Internet the great place that it is.
* The volunteers at [fl[cppreference.com|https://en.cppreference.com/]]
  who provide the bridge that leads from the spec to the real world.
* The helpful and knowledgeable folks on
  [fl[comp.lang.c|https://groups.google.com/g/comp.lang.c]] and 
  [fl[r/C_Programming|https://www.reddit.com/r/C_Programming/]] who got
  me through the tougher parts of the language.
* Everyone who submitted corrections and pull-requests on everything
  from misleading instructions to typos. -->

* Todos na Internet que decidiram ajudar a compartilhar seus conhecimentos de uma forma ou de outra. O compartilhamento gratuito de informações instrutivas é o que torna a Internet o grande lugar que é.
* Os voluntários do [fl[cppreference.com|https://en.cppreference.com/]] que fornecem a ponte que leva da especificação ao mundo real.
* As pessoas prestativas e inteligentes no [fl[comp.lang.c|https://groups.google.com/g/comp.lang.c]] e [fl[r/C_Programming|https://www.reddit.com/r/C_Programming/]] que me fizeram passar pelas partes mais difíceis da língua.
* Todos que enviaram correções e pull-requests em tudo, desde instruções enganosas até erros de digitação.

<!-- Thank you! ♥ -->

Obrigado! ♥