---
date: '2026-10-13T12:34:59-03:00'
draft: true
title: 'Recompilação estática ou dinâmica de jogos, e o que isso significa para você'
---

Você deve ter visto isso recentemente: Bloodborne, God of War III, Forza Horizon e outros exclusivos de diversos consoles estão rodando nativamente em PCs com gráficos e taxa de quadros melhorada em comparação aos originais, dispensando uso de emuladores.

Recentemente houve uma grande evolução no mundo da recompilação de jogos. Historicamente, o maior obstáculo para rodar títulos de consoles no computador sempre foi a barreira da arquitetura de hardware. Processadores de videogames antigos operam com conjuntos de instruções totalmente diferentes daqueles lidos pelos processadores x86-64 ou ARM presentes nos PCs e smartphones atuais. Na prática, o Windows simplesmente não sabe interpretar o código de um disco de PS3 ou de um cartucho de Nintendo 64.

Para contornar essa incompatibilidade, a tecnologia segue duas vias de tradução de código. A primeira é a recompilação dinâmica (JIT - Just-in-Time), que atua como um intérprete simultâneo do código do jogo, e ao longo dos anos, foi a abordagem mais popular dos emuladores tradicionais. Já a segunda é a recompilação estática (AOT - Ahead-of-Time), processo que traduz o código original da máquina inteiramente antes de o jogo abrir, convertendo todo o código do jogo para a linguagem que o processador do computador entende, sem a necessidade de um intérprete.

