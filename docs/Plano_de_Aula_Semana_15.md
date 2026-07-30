# Semana 15 🔵

## Introdução da Semana

A Semana 15 abre a Unidade V — Comparar Arquiteturas, encerrando o ciclo de produção da Unidade IV (Semanas 12–14) e inaugurando a metodologia de Reverse Engineering, com autonomia muito alta: o professor deixa de atuar como diretor técnico de produção e passa a conduzir discussões e análises comparativas. Nenhum sistema novo é implementado no Vertical Slice a partir desta semana — `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD`, `BP_Enemy` com Behavior Tree/Blackboard, Material Instances, Foliage, Áudio e o build empacotado na Semana 14 permanecem exatamente como estão. O trabalho da semana é olhar para trás: comparar as decisões arquiteturais tomadas pelos próprios grupos ao longo do semestre com as decisões de projetos profissionais de referência da Unreal Engine. O Encontro 1 conduz a leitura arquitetural guiada do Lyra Starter Game, o gameplay framework de referência da Epic, traçando paralelos diretos com o Vertical Slice da turma (GameMode/GameState/PlayerController, Components, interação via Interfaces). O Encontro 2 amplia a análise para Stack O Bot e Content Examples, dois exemplos com escopo mais próximo do Vertical Slice da disciplina, e propõe o desafio de cada grupo identificar uma decisão arquitetural própria que poderia ser refeita à luz do que foi observado, preparando diretamente a consolidação comparativa da Semana 16.

## Objetivos Gerais

- Analisar a arquitetura de gameplay framework de um projeto profissional em produção real (Lyra Starter Game).
- Identificar paralelos e divergências entre as decisões arquiteturais do Lyra e as decisões tomadas no Vertical Slice da turma.
- Analisar as soluções arquiteturais do Stack O Bot e do Content Examples e compará-las com as soluções do próprio projeto.
- Propor, com justificativa técnica, ao menos uma decisão arquitetural do próprio projeto que poderia ser refeita à luz dos projetos de referência analisados.

## Resultados Esperados

Ao final da semana, cada grupo terá produzido uma análise arquitetural comparando o próprio Vertical Slice com Lyra Starter Game, Stack O Bot e Content Examples, identificando pelo menos uma decisão de projeto que poderia ser reformulada com base nos exemplos profissionais estudados, com a justificativa técnica registrada. Essa entrega corresponde ao **Feedback formal** sobre as análises arquiteturais previsto no Cronograma, e alimenta diretamente o quadro comparativo Unreal x Unity da Semana 16.

---

# Encontro 1

## Objetivos de Aprendizagem

- Descrever a estrutura de gameplay framework do Lyra Starter Game (GameMode, GameState, PlayerState, Pawn Data, Experience).
- Comparar a estrutura do Lyra com o gameplay framework construído no próprio Vertical Slice desde o Módulo 2.
- Identificar por que um projeto profissional adiciona camadas de abstração que o Vertical Slice da disciplina não precisou implementar.

## Conteúdos

- Estrutura geral do Lyra Starter Game: organização de pastas, Game Feature Plugins, Experience Primary Data Assets.
- Gameplay framework do Lyra: `LyraGameMode`, `LyraGameState`, `LyraPlayerState`, `LyraPawnData` — e seu paralelo direto com `BP_GameMode`, `BP_GameState` e `BP_PlayerController` do Vertical Slice.
- Leitura arquitetural guiada: por que o Lyra separa dados de configuração (Pawn Data, Experience) da lógica de framework, e o que essa separação custaria de complexidade se aplicada ao escopo da disciplina.

## Conceitos Fundamentais

O conceito universal desta aula é que arquitetura de software é sempre uma resposta a escala e a requisitos, não um padrão fixo a ser copiado. O Vertical Slice da disciplina resolveu GameMode/GameState/PlayerController de forma direta porque seu escopo é fixo e conhecido desde a Semana 4; o Lyra resolve o mesmo papel com camadas adicionais — Game Feature Plugins, Experience Primary Data Assets, Pawn Data — porque precisa suportar múltiplos modos de jogo, plataformas e equipes trabalhando em paralelo sobre a mesma base de código. O paralelo entre `BP_GameMode` e `LyraGameMode`, entre `BP_GameState` e `LyraGameState`, mostra que o conceito ensinado desde o Módulo 2 (separar regras de partida de estado compartilhado) é o mesmo nos dois projetos; o que muda é o grau de indireção necessário para sustentar esse conceito em produção em larga escala. Essa é a generalização central da Unidade V: reconhecer o que é universal (o papel arquitetural) e o que é contextual (o grau de abstração exigido pela escala do projeto).

## Recursos da Unreal

Lyra Starter Game (projeto de exemplo oficial da Epic, via Fab/Epic Games Launcher ou Learning Sample), Content Browser do Lyra para navegação guiada, documentação oficial de Gameplay Framework.

## Comparação com Unity

O padrão que o Lyra resolve com GameMode/GameState/Experience corresponde, na Unity, à ausência de uma classe nativa equivalente — times de Unity normalmente constroem seu próprio Game Manager/Singleton para cumprir o mesmo papel, com o grau de abstração dependendo inteiramente de convenção interna do estúdio, não de uma estrutura imposta pela engine. O Lyra evidencia, portanto, um caso em que a Unreal formaliza nativamente uma decisão arquitetural que a Unity deixa em aberto.

## Preparação do Professor

- Baixar e abrir o projeto Lyra Starter Game previamente (via Epic Games Launcher/Fab) em uma máquina de demonstração.
- Selecionar previamente 3–4 pontos de navegação no Content Browser do Lyra que ilustrem a comparação com `BP_GameMode`, `BP_GameState`, `BP_PlayerController` e `BP_GameInstance` do Vertical Slice.
- Ter à mão o PROJECT_ARCHITECTURE.md (seção 7) projetado ao lado do Lyra para comparação direta durante a demonstração.
- Opcional para compressão de tempo: disponibilizar a leitura arquitetural do Lyra como leitura dirigida prévia (documentação oficial + vídeo curto), liberando o tempo de aula para discussão em vez de navegação básica — recomendado caso a Semana 14 tenha sofrido atraso.

## Cronograma do Encontro

20 min — Revisão do Vertical Slice: recapitular GameMode/GameState/PlayerController/GameInstance do próprio projeto (PROJECT_ARCHITECTURE.md, seção 7).

15 min — Introdução ao Lyra Starter Game: contexto, propósito e escala do projeto de referência.

40 min — Demonstração: leitura arquitetural guiada do gameplay framework do Lyra, com paralelo direto ao vocabulário já usado pela turma.

45 min — Laboratório em grupo: cada grupo mapeia, em um quadro comparativo simples, os elementos do Lyra que correspondem a cada Blueprint do próprio framework.

15 min — Feedback: cada grupo apresenta brevemente um paralelo identificado.

## Desenvolvimento

A aula abre revisando o gameplay framework já construído pela turma desde a Semana 4, com o professor projetando a seção 7 do PROJECT_ARCHITECTURE.md como ponto de partida comum. Em seguida, o professor apresenta o Lyra Starter Game como projeto de referência oficial da Epic, contextualizando seu propósito (template de produção para jogos multiplayer em escala). A demonstração percorre o Content Browser do Lyra de forma guiada, mostrando `LyraGameMode`, `LyraGameState`, `LyraPlayerState` e `LyraPawnData`, sempre voltando ao paralelo com os Blueprints equivalentes do Vertical Slice. No laboratório, cada grupo constrói um quadro comparativo simples (duas colunas: elemento do Lyra × elemento equivalente no próprio projeto), registrando também o que o Lyra resolve que o Vertical Slice não precisou resolver, e por quê. O encontro fecha com apresentações curtas dos paralelos mais relevantes identificados por cada grupo.

## Desafio

Não há desafio formal neste encontro — o Encontro 1 é dedicado à leitura arquitetural guiada, condição de base para o desafio proposto no Encontro 2.

## Critérios de Sucesso

Cada grupo produziu um quadro comparativo entre o gameplay framework do Lyra e o do próprio Vertical Slice, identificando corretamente ao menos três correspondências (GameMode, GameState, PlayerController/PlayerState) e articulando por que o Lyra adiciona camadas de abstração ausentes no projeto da disciplina.

## Evidências para Avaliação

O quadro comparativo produzido no laboratório alimenta a entrega de Feedback formal da semana, avaliada à luz da Rubrica 6 (justificativa técnica de decisões) e da Rubrica 7 (arquitetura e consistência do Vertical Slice, em sua dimensão de capacidade de explicar decisões).

## Dificuldades Esperadas

Grupos podem se perder na complexidade visual do Lyra, tentando entender cada Blueprint em profundidade em vez de focar no paralelo arquitetural solicitado — o professor deve redirecionar constantemente para a pergunta "qual papel isso cumpre, e quem cumpre esse papel no nosso projeto?", evitando que o encontro vire uma exploração livre do Lyra sem conexão com o Vertical Slice.

---

# Encontro 2

## Objetivos de Aprendizagem

- Descrever as soluções arquiteturais do Stack O Bot e do Content Examples para sistemas equivalentes aos do Vertical Slice.
- Comparar essas soluções com as decisões já tomadas pelo próprio grupo ao longo do semestre.
- Propor e justificar tecnicamente ao menos uma decisão arquitetural do próprio projeto que poderia ser refeita à luz dos exemplos analisados.

## Conteúdos

- Estudo de caso Stack O Bot: estrutura de personagem, interação e progressão em um projeto de escopo compacto, mais próximo em escala ao Vertical Slice do que o Lyra.
- Estudo de caso Content Examples: exemplos isolados de sistemas específicos (materiais, iluminação, física, UI), usados como referência pontual, não como projeto integrado.
- Desafio: identificação de uma decisão arquitetural própria candidata a revisão, com justificativa técnica.

## Conceitos Fundamentais

Se o Lyra ilustrou arquitetura em escala de produção, o Stack O Bot ilustra o extremo oposto: um projeto pequeno, de escopo fechado, com decisões arquiteturais mais diretamente comparáveis às do Vertical Slice — reforçando que a analogia entre os dois projetos é mais literal do que com o Lyra. O Content Examples cumpre um terceiro papel: não é um projeto integrado, mas uma coleção de exemplos pontuais, o que ensina que nem toda referência arquitetural precisa vir de um jogo completo — às vezes a referência certa é um exemplo isolado de um único sistema (um Material Instance, uma configuração de iluminação). O conceito universal fechado neste encontro é que comparação arquitetural madura não busca copiar soluções, mas justificar tecnicamente por que uma solução própria foi mantida ou deveria ser revista — exatamente o que o desafio da semana exige de cada grupo.

## Recursos da Unreal

Stack O Bot (projeto de exemplo oficial da Epic), Content Examples (projeto de exemplo oficial da Epic), ambos via Epic Games Launcher/Fab, PROJECT_ARCHITECTURE.md do próprio Vertical Slice.

## Comparação com Unity

Rapidamente: a Unity mantém um papel equivalente aos Content Examples através de seus próprios pacotes de exemplo (Unity Learn, Sample Projects), com a diferença de que a Unity frequentemente distribui exemplos como projetos completos separados por versão do Input System ou Render Pipeline em uso, enquanto os exemplos da Epic tendem a ser mantidos como um único projeto integrado por versão da engine.

## Preparação do Professor

- Baixar e abrir Stack O Bot e Content Examples previamente (via Epic Games Launcher/Fab).
- Selecionar previamente 2–3 sistemas do Stack O Bot com paralelo direto ao Vertical Slice (interação, coleta, progressão) e 2–3 exemplos do Content Examples relevantes ao Módulo 4 (materiais, iluminação).
- Ter à mão o PROJECT_ARCHITECTURE.md do grupo, para consulta durante o laboratório e o desafio.
- Preparar um modelo simples de registro do desafio (decisão candidata + justificativa) para orientar os grupos.

## Cronograma do Encontro

15 min — Revisão do quadro comparativo produzido no Encontro 1.

25 min — Demonstração: estudo de caso Stack O Bot, com paralelo direto ao Vertical Slice.

20 min — Demonstração: estudo de caso Content Examples, com foco nos sistemas do Módulo 4 (materiais, iluminação).

60 min — Laboratório/Desafio: cada grupo analisa o próprio Vertical Slice à luz dos três projetos de referência e identifica ao menos uma decisão arquitetural candidata a revisão, registrando a justificativa.

15 min — Feedback formal: cada grupo compartilha brevemente a decisão candidata identificada e recebe retorno do professor.

## Desenvolvimento

O encontro retoma o quadro comparativo do Encontro 1 e amplia a análise para o Stack O Bot, cujo escopo compacto (personagem, interação, coleta, progressão simples) permite comparação direta e detalhada com o Vertical Slice da turma. Em seguida, a demonstração passa ao Content Examples, usado de forma pontual para revisitar decisões do Módulo 4 — Material Instances e configuração de iluminação — sob a perspectiva de exemplos oficiais da Epic. No laboratório final, cada grupo usa os três projetos de referência (Lyra, Stack O Bot, Content Examples) para revisar criticamente o próprio PROJECT_ARCHITECTURE.md e identificar uma decisão que poderia ser refeita, registrando a decisão, o que os exemplos de referência sugerem como alternativa, e por que a decisão original foi ou não a mais adequada ao escopo da disciplina. O encontro fecha com apresentações curtas e feedback formal do professor sobre cada análise.

## Desafio

Cada grupo identifica, entre as decisões arquiteturais tomadas em seu próprio projeto ao longo do semestre, ao menos uma que poderia ser refeita à luz do Lyra, do Stack O Bot ou do Content Examples, e registra por escrito a decisão original, a alternativa observada nos projetos de referência e a justificativa técnica para manter ou propor a revisão. O desafio permite diferentes soluções: não há resposta única esperada, e grupos podem legitimamente concluir que a decisão original foi a mais adequada ao escopo da disciplina, desde que a justificativa seja tecnicamente consistente.

## Critérios de Sucesso

Cada grupo apresentou por escrito uma decisão arquitetural própria, uma referência concreta a um dos três projetos analisados e uma justificativa técnica coerente com os princípios do PROJECT_ARCHITECTURE.md (simplicidade, clareza, reutilização, viabilidade em um semestre).

## Evidências para Avaliação

O registro do desafio constitui a entrega de Feedback formal da semana, avaliado pela Rubrica 6 (justificativa técnica de decisões) e pela Rubrica 7 (capacidade de explicar decisões arquiteturais do Vertical Slice), preparando diretamente o quadro comparativo sistemático da Semana 16.

## Dificuldades Esperadas

Grupos podem propor revisões que extrapolam o escopo fixo do projeto (por exemplo, sugerir Game Feature Plugins ou sistemas de Experience do Lyra em escala incompatível com um semestre) — o professor deve intervir lembrando que o objetivo é justificar decisões dentro do escopo já definido pelo PROJECT_ARCHITECTURE.md, não redesenhar o projeto. Também é comum que grupos concluam apressadamente que "tudo deveria ter sido feito como no Lyra" sem considerar a diferença de escala — o professor deve cobrar explicitamente essa diferenciação na justificativa.

---

# Resultado Esperado da Semana

Ao final da Semana 15, cada grupo terá analisado a arquitetura de três projetos de referência oficiais da Epic (Lyra Starter Game, Stack O Bot, Content Examples), produzido um quadro comparativo entre o gameplay framework do Lyra e o próprio Vertical Slice, e registrado por escrito ao menos uma decisão arquitetural própria candidata a revisão, com justificativa técnica fundamentada nos exemplos analisados. Nenhum sistema novo foi adicionado ao projeto: `BP_Player`, `BP_Enemy`, o framework de GameMode/GameState/PlayerController/GameInstance, os sistemas de interação, inventário, HUD, IA, combate, materiais, foliage, áudio e o build empacotado da Semana 14 permanecem intactos. O estudante domina, ao final da semana, a leitura crítica de arquitetura de projetos profissionais da Unreal Engine e a capacidade de justificar tecnicamente as próprias decisões de projeto em contraste com referências externas.

# Preparação para a Próxima Semana

A Semana 16 consolida a comparação arquitetural sistemática entre Unreal e Unity ao longo de todos os sistemas construídos no semestre, ampliando em seguida para Godot, O3DE, Stride e CryEngine. O quadro comparativo produzido no Encontro 1 desta semana e a justificativa técnica registrada no desafio do Encontro 2 são insumos diretos para o quadro comparativo Unreal x Unity da Semana 16, Encontro 1 — nenhum dos dois deve ser descartado ou refeito do zero.

# Referências

- Epic Games — Lyra Starter Game (Epic Games Launcher/Fab, Samples and Tutorials).
- Epic Games — Stack O Bot (Epic Games Launcher/Fab, Samples and Tutorials).
- Epic Games — Content Examples (Epic Games Launcher/Fab, Samples and Tutorials).
- Epic Developer Community — documentação oficial de Gameplay Framework (GameMode, GameState, PlayerState).
- Unity Manual — visão geral de Game Manager patterns, para contextualizar a comparação da seção "Comparação com Unity".

Vídeos, quando necessários como apoio complementar (nunca como fonte principal): canal oficial Unreal Engine (visão geral do Lyra Starter Game).
