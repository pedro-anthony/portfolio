---
date: '2026-11-12T18:00:46-03:00'
draft: false
title: 'Decomps, recomps ou camadas de compatibilidade: o que tem por trás dessa onda de jogos exclusivos rodando no PC?'
description: 'Como emuladores, recomps, decomps e camadas de compatibilidade estão levando exclusivos de console para o PC, e o papel da IA nisso.'
tags: ['games', 'emulação', 'engenharia reversa', 'IA']
cover:
  image: 'cover.jpg'
  relative: true
  alt: 'Ilustração de um cartucho e um disco passando por um chip x86-64 até um monitor'
showToc: true
tocOpen: false
---

Bloodborne, God of War III, Shadow of the Colossus e Forza Horizon (o primeiro) estão rodando em PCs com gráficos e taxa de quadros melhorados em comparação aos originais, dispensando o uso de emuladores.

Historicamente, o maior obstáculo para rodar títulos de consoles no computador sempre foi a barreira do hardware. Os processadores de videogames antigos operam com um conjunto de instruções totalmente diferente daquele lido pelos processadores comuns nos PCs atuais. Na prática, o Windows simplesmente não sabe interpretar o código de um disco de PS3 ou de um cartucho de Nintendo 64.

Hoje existem basicamente quatro formas de contornar esse problema, e o que muda entre elas é quando e quanto do jogo precisa ser traduzido. O emulador traduz o código enquanto o jogo roda. A recompilação faz essa tradução toda de uma vez, antes de o jogo abrir. A decompilação reconstrói o código-fonte do jogo para que ele possa ser compilado de novo, agora para o PC. Já a camada de compatibilidade, usada nos ports de PS4, nem chega a traduzir o código do jogo, só aquilo que ele pede ao sistema do console.

{{< svg src="caminhos.svg" >}}

## Emulação tradicional

A tradução de código pode acontecer de duas formas. A primeira é a recompilação dinâmica, usada pelos emuladores, que atua como um intérprete simultâneo do código do jogo enquanto ele roda. Ao longo dos anos, essa foi a abordagem mais popular para jogar títulos de console no PC, em projetos como o Dolphin, o PCSX2 e o RPCS3. A desvantagem é que traduzir tudo em tempo real tem um custo alto, e o computador costuma precisar ser bem mais potente que o console original para dar conta.

## Recompilação estática

A segunda forma é a recompilação estática, processo que traduz o código do jogo inteiramente antes de ele abrir, convertendo tudo para a linguagem que o processador do computador entende, sem a necessidade de um intérprete.

É essa via que está por trás dos chamados "recomps". O mais conhecido deles é o [Zelda 64: Recompiled](https://github.com/Zelda64Recomp/Zelda64Recomp), lançado em 2024, que trouxe o Majora's Mask do Nintendo 64 para o PC com suporte a widescreen, taxas de quadros altas e mods. Em 2025 foi a vez do [Unleashed Recompiled](https://github.com/hedge-dev/UnleashedRecomp), que fez o mesmo com o Sonic Unleashed do Xbox 360.

## Decompilação

A decompilação segue um caminho diferente e bem mais trabalhoso. Em vez de traduzir o código do jogo automaticamente, os fãs reconstroem à mão, função por função, um código-fonte equivalente ao que os desenvolvedores escreveram originalmente. Depois de pronto, esse código pode ser adaptado para rodar no PC ou em praticamente qualquer outra plataforma. Projetos assim costumam levar anos e envolver dezenas de pessoas, e foi desse jeito que surgiram os ports de [Super Mario 64](https://github.com/n64decomp/sm64) e o [Ship of Harkinian](https://github.com/HarbourMasters/Shipwright), a versão de PC do Ocarina of Time original.

## Camadas de compatibilidade

Nenhuma dessas opções é o que tem sido usado nos ports mais recentes de jogos de PS4, como o [BBPort](https://github.com/deadinside28/bloodborne_pc) e o [SpartanPort](https://github.com/FelipePrado0/SpartanPort). Diferente do PS3 ou do Nintendo 64, o PlayStation 4 e o Xbox One já usam processadores AMD da mesma arquitetura dos processadores de qualquer PC moderno. Ou seja, o código desses jogos já está, essencialmente, na língua que o computador entende, e não há nada a ser recompilado.

O que separa um executável de PS4 de um .exe do Windows não é o processador, e sim todo o ecossistema em volta dele: o sistema operacional do console (o Orbis OS, derivado do FreeBSD), suas bibliotecas proprietárias e a API gráfica da própria Sony, que conversa diretamente com a placa de vídeo.

O trabalho desses projetos é construir uma camada de tradução e compatibilidade. As chamadas que o jogo faz ao sistema e às bibliotecas do console são interceptadas e redirecionadas para equivalentes no Windows ou no Linux, enquanto os comandos gráficos são convertidos para APIs como Vulkan ou DirectX 12. O código do jogo continua rodando direto no processador, sem intérprete e sem recompilação, o que se parece bem mais com o que o Wine faz para rodar programas de Windows no Linux do que com um emulador tradicional.

O PS5 segue a mesma lógica, já que também usa um processador AMD de arquitetura compatível com a dos PCs. O [AnyPS5](https://github.com/boykopovar/anyps5) é um projeto de código aberto que tenta fazer isso com os jogos da geração atual: ele converte o executável de um jogo de PS5 em um programa nativo de Windows ou Linux e liga esse programa a reimplementações próprias das bibliotecas do sistema do console. O projeto ainda está no começo, com pouquíssimos jogos rodando do início ao fim, mas já mostra que o caminho aberto pelos ports de PS4 deve se repetir.

| | Como funciona | Exemplos |
|---|---|---|
| Emulador | Traduz o código do jogo enquanto ele roda | [Dolphin](https://github.com/dolphin-emu/dolphin), [RPCS3](https://github.com/RPCS3/rpcs3), [PCSX2](https://github.com/PCSX2/pcsx2) |
| Recomp | Traduz todo o código antes de o jogo abrir | Zelda 64: Recompiled, Unleashed Recompiled |
| Decomp | Reconstrói o código-fonte do jogo | Super Mario 64, Ship of Harkinian |
| Camada de compatibilidade | Roda o código original e traduz só as chamadas ao sistema | BBPort, SpartanPort, AnyPS5 |

## O papel da IA

Boa parte da velocidade com que esses projetos vêm aparecendo tem a ver com o uso de LLMs. A decompilação, que antes dependia de anos de trabalho manual, passou a ser feita em grande parte por agentes de IA como o Claude Code e o Codex, que leem o código de máquina de uma função, escrevem uma versão em C equivalente e repetem o processo até cobrir o jogo inteiro.

O problema é que um modelo de linguagem consegue escrever código que parece correto sem que ele de fato seja. Por isso, os projetos mais sérios usam uma verificação automática: cada função escrita pela IA é compilada com o mesmo compilador usado no jogo original, e o resultado é comparado byte a byte com o executável. Se não bater, a função volta para ser refeita. Essa técnica é chamada de decompilação exata (*matching decompilation*), e é o que garante que o código reconstruído se comporta exatamente como o original. Em um [relato publicado em outubro de 2026](https://momo5502.com/posts/2026-10-09-game-decompilation/), um desenvolvedor descreve como usou vários agentes trabalhando ao mesmo tempo para decompilar um jogo de tiro em primeira pessoa:

> Em cerca de **três meses**, os agentes reconstruíram **99%** das funções do jogo, **83%** delas idênticas ao original byte a byte, com um gasto estimado de **600 a 700 bilhões de tokens**.

Parte disso também se deve a ferramentas que conectam esses agentes aos programas de engenharia reversa. O [REA (Reverse Engineer Anything)](https://github.com/morluto/rea) é uma das mais usadas: um projeto de código aberto que dá a agentes como o Claude Code acesso a ferramentas como o Ghidra, permitindo que eles analisem um executável, mapeiem suas funções e reconstruam o código sem que a pessoa precise dominar engenharia reversa. Sites como o [Reversed with AI](https://reversedwithai.com/ai-game-decompilation) já catalogam centenas de projetos feitos dessa forma, entre eles uma versão de PC do Shadow of the Colossus de PS2 feita com Claude e Codex. A IA também começa a aparecer nas camadas de compatibilidade: o AnyPS5, por exemplo, aceita contribuições escritas com ajuda de IA, desde que o autor declare isso no pedido.

Vale lembrar que muitos desses projetos ainda são incompletos e que boa parte dos números divulgados vem dos próprios autores, sem verificação independente.

## Legalidade

Nenhum desses projetos distribui o jogo em si. O que é disponibilizado é apenas a ferramenta, e cabe ao usuário fornecer a sua própria cópia do jogo original para que ela funcione, o que é o que permite que boa parte deles continue no ar. Mesmo assim, o assunto ainda é uma área cinzenta, e empresas como a Nintendo já derrubaram projetos e vídeos relacionados, como aconteceu com o port de Super Mario 64 para PC em 2020. O uso de IA traz uma camada extra de dúvida, já que ainda não está claro como a justiça vai tratar código reconstruído automaticamente a partir de um jogo protegido.

## Por que agora

Além da IA, essa onda tem outros motivos. O primeiro é o acesso às ferramentas. Até alguns anos atrás, engenharia reversa de nível profissional dependia de programas caros como o IDA Pro. Isso mudou em 2019, quando a NSA, a agência de segurança nacional dos Estados Unidos, liberou o Ghidra como código aberto. Gratuito e com um decompilador embutido, ele virou a base de boa parte desses projetos, e é justamente a ele que ferramentas como o REA conectam os agentes de IA.

O segundo é a preservação. Nos últimos anos, várias lojas digitais de consoles antigos fecharam: a eShop do Wii U e do 3DS em março de 2023 e a loja do Xbox 360 em julho de 2024. Com isso, dezenas de jogos que só existiam em formato digital deixaram de ser vendidos e ficaram presos a aparelhos que nem são mais fabricados, sem nenhuma versão oficial disponível, e os projetos de fãs ganharam peso como forma de mantê-los jogáveis.

As comunidades em volta desses projetos também cresceram e se organizaram, e a popularização de PCs portáteis como o Steam Deck ajudou a criar um público grande interessado em jogar tudo em um único aparelho.

Enquanto as versões oficiais desses jogos não chegam ao PC, ou chegam em condições piores que as feitas por fãs, a tendência é que a lista de exclusivos rodando no computador continue crescendo.
