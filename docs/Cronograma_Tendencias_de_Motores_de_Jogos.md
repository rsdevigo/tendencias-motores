# Cronograma Detalhado — Disciplina de Tendências de Motores de Jogos
**Curso Superior de Tecnologia em Jogos Digitais**
Vertical Slice Incremental | 17 Semanas | 102 h/a — 76h (2 encontros de 2h15/semana) | Unreal Engine 5.6

> 🔴 **Encerramento de módulo** — entrega de artefato jogável, checkpoint, playtest, code review ou apresentação que fecha uma Unidade/Módulo inteiro: semanas **3, 7, 11, 14, 16 e 17**
> 🔴 **Semana 17** — apresentação técnica final e encerramento; **não** há novo conteúdo introduzido
> 🔵 Semana regular (fundamentação e desenvolvimento do Vertical Slice) nas demais
> **Nota sobre 🔴 × 🔵 e instrumentos formais:** o emoji 🔴 marca especificamente o encerramento de uma Unidade/Módulo — não qualquer instrumento avaliativo formal isolado. Um Code Review formal intermediário, que não fecha módulo (como o da Semana 12, encerramento apenas do Encontro 1 de Materials/Foliage dentro da Unidade IV ainda em curso), permanece corretamente marcado 🔵: introduz conteúdo novo e não corresponde a um marco de fechamento de Unidade.

> **Nota de avaliação:** a disciplina não utiliza prova tradicional. Cada módulo encerra com instrumentos coerentes com sua metodologia — checkpoint, code review, playtest e/ou apresentação — conforme o Plano de Ensino (seção "Avaliação da Aprendizagem"). O peso entre critérios cresce em favor da justificativa técnica e da comparação arquitetural nos módulos finais.

> **Nota de fonte:** a documentação indicada em cada semana segue a Documentação Oficial da Epic Games e a Unreal Engine Learning Library (ver REFERENCES.md), consultadas de forma crítica — sem reprodução de trechos extensos — e sempre comparadas à documentação oficial da Unity (Unity Manual/Unity Learn) e, quando pertinente, de Godot, O3DE, Stride ou CryEngine.

> **Nota de ordem:** a disciplina não segue o sumário de um único livro-texto, mas a evolução do próprio Vertical Slice. Por isso, um mesmo sistema pode ser introduzido de forma mínima em um módulo e retomado com profundidade maior em outro — por exemplo, **Interaction** aparece na Semana 5 (interação simples via Interface/Event Dispatcher) e é ampliado na Semana 10 (múltiplos tipos de interação conectados ao Inventário). O professor deve sinalizar cada retomada à turma.

---

## Ancoragem no Calendário Acadêmico

As 17 semanas deste Cronograma são **letivas e sequenciais**, sem semana de reserva. Antes do início do semestre, o professor deve preencher a tabela abaixo confrontando-a com o calendário acadêmico do IFMS vigente, identificando de antemão os encontros que colidem com feriados, recessos, semanas de atividades institucionais ou eventos do campus.

| Semana | Data do Encontro 1 | Data do Encontro 2 | Observações (feriado, evento, reposição) |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 🔴 | | | *1º build executável* |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 🔴 | | | *code review + playtest* |
| 8 | | | |
| 9 | | | |
| 10 | | | |
| 11 🔴 | | | *playtest + showcase* |
| 12 | | | |
| 13 | | | |
| 14 🔴 | | | *entrega parcial + code review* |
| 15 | | | |
| 16 🔴 | | | *checkpoint de preparação final* |
| 17 🔴 | | | *apresentação final* |

### Plano de contingência

Como o Vertical Slice evolui em cadeia — cada módulo depende diretamente do sistema construído no módulo anterior — a perda de um encontro se propaga até a Semana 17 se não for absorvida no próprio módulo. Sem semana de folga disponível, a absorção depende de saber de antemão **o que é compressível**:

**Encontros com folga relativa (compressíveis em até 20 minutos, sem perda estrutural):**

- **Semana 1, Encontro 1** — o tour pelo editor comporta síntese caso a turma já tenha familiaridade prévia com engines de terceiros (Unity).
- **Semana 6, Encontro 1** — a introdução a Data Assets/Data Tables pode ser condensada, já que é retomada na aplicação da Semana 6, Encontro 2.
- **Semana 12, Encontro 1** — a refatoração de materiais em Material Instances pode ser reduzida se o projeto já usa poucos materiais base.
- **Semana 15, Encontro 1** — a análise do Lyra pode ser conduzida por leitura dirigida prévia, liberando tempo em aula para discussão.

**Encontros que não devem ser comprimidos:**

- **Semanas 3, 7, 11, 14, 16 e 17, Encontro 2** — concentram os instrumentos avaliativos de encerramento de módulo (checkpoint, code review, playtest ou apresentação). Comprimir aqui é comprimir avaliação.
- **Semana 7, Encontro 2** — o Code Review + Playtest de encerramento do Módulo 2 depende da integração de todos os desafios do módulo; não há espaço de compressão.
- **Semana 14, Encontro 1** — o Packaging do build final é pré-requisito do Playtest cruzado da Semana 14, Encontro 2; sem ele, o encontro seguinte trava.
- **Semana 17** — a apresentação final é o instrumento de maior peso do semestre.

**Se um encontro for perdido:** a primeira opção é redistribuir o conteúdo dentro do próprio módulo, comprimindo o encontro de fundamentação seguinte. A segunda é converter parte da fundamentação em consulta dirigida à documentação oficial da Epic, com verificação no início do encontro seguinte. Adiar a entrega de um módulo deve ser a última opção, porque desloca todas as entregas seguintes e compromete o feedback contínuo característico das metodologias ativas adotadas.

---

## Unidade I — Aprender a Ferramenta (Semanas 1–3)

*Pergunta da Unidade: como uma engine estrutura um mundo jogável?*
*Metodologia dominante: Scaffolded Learning — professor demonstra, aluno replica. Autonomia muito baixa.*

---

### Semana 1 🔵
**Tema:** Arquitetura da Unreal Engine, Actors e Components

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que é uma game engine e como ela organiza um mundo jogável? |
| **Documentação de Referência** | Unreal Engine Documentation — Visão geral do Editor; Gameplay Framework in Unreal Engine (introdução) |
| **Encontro 1** | Fundamentação: o que é uma engine e por que ela existe, antes de qualquer botão. Tour guiado pelo Unreal Editor — Viewport, Content Browser, estrutura de projeto. Criação e organização inicial do projeto do Vertical Slice. |
| **Encontro 2** | Fundamentação de Actor e Component como unidade universal de composição (composição versus herança), comparando brevemente com GameObject/Component da Unity. Criação guiada de um Actor com Components via Blueprint. **Desafio:** adicionar um Component adicional ao Actor, produzindo um comportamento visual diferente do demonstrado. |
| **Recursos da Unreal explorados** | Unreal Editor, Viewport, Content Browser, Actors, Components, Blueprint |
| **Entrega** | — |

---

### Semana 2 🔵
**Tema:** Character, Character Movement e Enhanced Input

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine desacopla a intenção do jogador (input) da ação no mundo? |
| **Documentação de Referência** | Enhanced Input in Unreal Engine |
| **Encontro 1** | Fundamentação de Character x Pawn e do Character Movement Component como sistema universal de locomoção. Configuração guiada de um Character controlável no nível de teste. |
| **Encontro 2** | Fundamentação de Enhanced Input — Input Actions, Input Mapping Contexts, Triggers e Modifiers — comparando com o Input System da Unity. Configuração de Enhanced Input para movimentação e câmera. **Desafio:** adicionar uma nova Input Action (correr, agachar ou pular) não demonstrada em aula, com liberdade de implementação. |
| **Recursos da Unreal explorados** | Character, Character Movement Component, Enhanced Input |
| **Entrega** | — |

---

### Semana 3 🔴
**Tema:** Materiais, Landscape, Lumen, Nanite e Packaging

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine renderiza e empacota um mundo jogável? |
| **Documentação de Referência** | Unreal Engine Materials; Nanite Virtualized Geometry; Lumen Global Illumination and Reflections; Packaging Your Project |
| **Encontro 1** | Fundamentação do Material Graph (conceito de shader nodal) e do Landscape como ferramenta de terreno. Criação guiada de um material simples e modelagem de um terreno básico para o mapa do projeto. |
| **Encontro 2** | Fundamentação dos conceitos universais de renderização moderna — geometria virtualizada (Nanite) e iluminação global dinâmica (Lumen) — e do pipeline de Packaging. Ativação e ajuste de Lumen/Nanite no nível. Geração do primeiro build empacotado do Vertical Slice. |
| **Recursos da Unreal explorados** | Materiais, Landscape, Nanite, Lumen, Packaging |
| **Entrega** | **Checkpoint de encerramento do Módulo 1** — primeiro build executável do Vertical Slice; Showcase em aula |
| **Observação** | Encerramento da Unidade I. |

---

## Unidade II — Construir Sistemas (Semanas 4–7)

*Pergunta da Unidade: como um jogo se estrutura por trás da jogabilidade visível?*
*Metodologia dominante: Studio Based Learning — professor demonstra, aluno adapta. Autonomia baixa.*

---

### Semana 4 🔵
**Tema:** GameMode, GameState, PlayerController e GameInstance

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine separa regras de partida, estado compartilhado e persistência entre níveis? |
| **Documentação de Referência** | Gameplay Framework in Unreal Engine |
| **Encontro 1** | Fundamentação de GameMode (regras da partida) e GameState (estado compartilhado), comparando com a ausência de um equivalente direto na Unity (padrão de Managers/Singletons). Criação guiada de GameMode/GameState customizados. |
| **Encontro 2** | Fundamentação de PlayerController (ponte entre jogador e Pawn) e GameInstance (persistência entre níveis). Implementação de uma variável persistente no GameInstance. **Desafio:** cada grupo define e implementa um dado próprio que deve persistir entre níveis (pontuação, item coletado, estado de progresso), com liberdade de escolha. |
| **Recursos da Unreal explorados** | GameMode, GameState, PlayerController, GameInstance |
| **Entrega** | — |

---

### Semana 5 🔵
**Tema:** Blueprint Interfaces e Event Dispatchers

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como comunicar sistemas sem criar dependência direta entre eles? |
| **Documentação de Referência** | Blueprints Visual Scripting in Unreal Engine |
| **Encontro 1** | Fundamentação de Blueprint Interfaces como mecanismo de comunicação desacoplada, comparando com Interfaces em C# na Unity. Criação guiada de uma interface de interação genérica implementada por um Actor. |
| **Encontro 2** | Fundamentação de Event Dispatchers como padrão observer, comparando com UnityEvent/C# Actions. Implementação de um Event Dispatcher acionado por interação. **Desafio:** cada grupo implementa um objeto interativo (porta ou equivalente escolhido pelo grupo) usando Interface + Event Dispatcher, permitindo diferentes soluções de acionamento (alavanca, chave, proximidade). |
| **Recursos da Unreal explorados** | Blueprint Interfaces, Event Dispatchers |
| **Entrega** | **Feedback formal** sobre as soluções de interação apresentadas pelos grupos |

---

### Semana 6 🔵
**Tema:** Data Assets, Data Tables, Structs e Enums

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como separar dados de design da lógica de gameplay? |
| **Documentação de Referência** | Gameplay Framework in Unreal Engine (Data Assets e Data Tables) |
| **Encontro 1** | Fundamentação de Data Assets e Data Tables como estruturas de dados desacopladas da lógica, comparando com ScriptableObjects na Unity. Criação guiada de uma Data Table para itens/entidades do projeto. |
| **Encontro 2** | Fundamentação de Structs e Enums como organizadores de dados tipados. **Desafio:** cada grupo modela seu próprio conjunto de itens coletáveis (baús, moedas, recursos) usando Data Table + Struct/Enum, com liberdade de categorias e atributos. |
| **Recursos da Unreal explorados** | Data Assets, Data Tables, Structs, Enums |
| **Entrega** | **Checkpoint de progresso** do Módulo 2 |

---

### Semana 7 🔴
**Tema:** SaveGame e consolidação do gameplay do Módulo 2

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine serializa e recupera o estado de progresso de um jogador? |
| **Documentação de Referência** | Unreal Engine Documentation — Saving and Loading Your Game |
| **Encontro 1** | Fundamentação de SaveGame Object como serialização de estado de jogo, comparando com PlayerPrefs/serialização em JSON na Unity. Implementação de save/load de um estado simples do projeto (ex.: itens coletados), seguida da construção de `BP_Checkpoint`, que reutiliza `BPI_Interactable` e o `SaveComponent` para gravar progresso. |
| **Encontro 2** | Revisão integrada de GameMode, Interfaces, Event Dispatchers, Data Tables e SaveGame. Integração final dos desafios do módulo (portas, baús, alavancas, NPCs, `BP_Checkpoint`) em um único fluxo jogável. **Desafio:** cada grupo apresenta sua integração completa, justificando as escolhas de arquitetura adotadas. |
| **Recursos da Unreal explorados** | SaveGame, `BP_Checkpoint`, GameMode, GameState, PlayerController, GameInstance, Blueprint Interfaces, Event Dispatchers, Data Assets, Data Tables, Structs, Enums |
| **Entrega** | **Gameplay funcional consolidado (Módulo 2)**; Code Review dos sistemas implementados; Playtest coletivo |
| **Observação** | Encerramento da Unidade II. |

---

## Unidade III — Resolver Problemas (Semanas 8–11)

*Pergunta da Unidade: como resolver, com autonomia crescente, os problemas de um Vertical Slice jogável?*
*Metodologia dominante: Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.*

---

### Semana 8 🔵
**Tema:** HealthComponent, Animation Blueprint, Blend Spaces e Montages

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Onde vive o estado de vida/dano de um personagem, e como uma engine resolve a transição e a combinação de animações? |
| **Documentação de Referência** | Animation Blueprints in Unreal Engine; Unreal Engine Documentation — Actors and Components |
| **Encontro 1** | Construção guiada de `HealthComponent` (vida atual/máxima, `ApplyDamage`, evento `OnDeath`), seguindo o mesmo padrão de `InteractionComponent`/`SaveComponent`. Fundamentação de Animation Blueprint e State Machines, comparando com o Animator Controller da Unity. Criação guiada de uma State Machine básica (idle, andar, correr). |
| **Encontro 2** | Fundamentação de Blend Spaces (interpolação multidimensional) e Montages (animações pontuais sobrepostas), comparando com Blend Trees na Unity. Configuração de um Blend Space direcional e uma Montage de ação. **Desafio:** cada grupo propõe e implementa uma animação contextual própria (reação a dano, interação, ataque), escolhendo entre Blend Space ou Montage conforme o problema. |
| **Recursos da Unreal explorados** | `HealthComponent`, Animation Blueprint, Blend Spaces, Montages |
| **Entrega** | — |

---

### Semana 9 🔵
**Tema:** UMG e HUD

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como comunicar em tempo real o estado do jogo ao jogador? |
| **Documentação de Referência** | UMG UI Designer |
| **Encontro 1** | Fundamentação de UMG como sistema universal de interface em tempo real — Widgets, Canvas Panel, binding de dados — comparando com UI Toolkit/uGUI na Unity. Criação guiada de um Widget simples vinculado a uma variável de gameplay existente. |
| **Encontro 2** | Fundamentação de HUD como camada de organização de múltiplos Widgets. Montagem guiada de um HUD com múltiplos elementos. **Desafio:** cada grupo define quais dados de gameplay já existentes (vida, itens, progresso) devem compor o HUD, propondo a própria solução visual e de binding. |
| **Recursos da Unreal explorados** | UMG, HUD |
| **Entrega** | **Feedback formal** sobre as soluções de HUD apresentadas |

---

### Semana 10 🔵
**Tema:** Inventário e ampliação do Interaction System

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como estruturar o armazenamento e a manipulação de itens em um jogo? |
| **Documentação de Referência** | Gameplay Framework in Unreal Engine (Data Assets aplicados a inventário) |
| **Encontro 1** | Fundamentação de padrões de Inventory System — armazenamento, adição/remoção, exibição. Estruturação inicial de um inventário reutilizando os itens modelados na Semana 6. |
| **Encontro 2** | Retomada e ampliação do Interaction System introduzido na Semana 5 — detecção, priorização e resposta a múltiplos tipos de interação. Conexão do sistema de interação ao inventário (coletar, usar, descartar). **Desafio:** cada grupo expande seu sistema de interação para suportar um novo tipo (empilhar itens, combinar itens, interação com cooldown), com solução própria. |
| **Recursos da Unreal explorados** | Inventory (Data Assets, UMG), Interaction |
| **Entrega** | **Code Review** dos sistemas de inventário e interação |

---

### Semana 11 🔴
**Tema:** Navigation, Behavior Trees, Blackboards e Combate Simples

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine dá autonomia de deslocamento e decisão a um agente não-jogador, e como detecta que um ataque acertou um alvo? |
| **Documentação de Referência** | Behavior Trees in Unreal Engine; Unreal Engine Documentation — Traces and Overlaps |
| **Encontro 1** | Fundamentação de Navigation e NavMesh como base universal de deslocamento de agentes, comparando com o NavMesh da Unity. Configuração de NavMesh no nível e movimentação de um agente até um ponto. |
| **Encontro 2** | Fundamentação de Behavior Tree (estrutura de decisão) e Blackboard (memória compartilhada), comparando com Behavior Designer/NodeCanvas na Unity. Implementação guiada de uma Behavior Tree simples (patrulha/perseguição) e de um combate simples (Trace/Overlap do `BP_Player` chamando `ApplyDamage` no `HealthComponent` de `BP_Enemy`). **Desafio:** cada grupo propõe um comportamento autônomo próprio para o NPC do seu projeto (patrulha, alerta, fuga, interação com o jogador), com liberdade de solução. |
| **Recursos da Unreal explorados** | Navigation, Behavior Trees, Blackboards, Line Trace/Overlap (combate simples) |
| **Entrega** | **Vertical Slice jogável (Módulo 3)** — animação, interface, inventário, interação e IA integrados; Playtest coletivo; Showcase |
| **Observação** | Encerramento da Unidade III. |

---

## Unidade IV — Produzir como um Pequeno Estúdio (Semanas 12–14)

*Pergunta da Unidade: como transformar um protótipo funcional em um produto entregável?*
*Metodologia dominante: Studio Based Learning — professor como diretor técnico. Autonomia alta.*

---

### Semana 12 🔵
**Tema:** Materials, Material Instances e Foliage

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como padronizar e otimizar a produção visual de um projeto em escala de estúdio? |
| **Documentação de Referência** | Unreal Engine Materials |
| **Encontro 1** | Fundamentação de Material Instance versus Material base como estratégia de parametrização e otimização, comparando com Material Property Blocks na Unity. Refatoração de materiais do projeto em Material Instances parametrizadas. |
| **Encontro 2** | Fundamentação da Foliage Tool como ferramenta de composição de cena — densidade, performance e composição visual. Composição de vegetação/elementos de cena no nível do Vertical Slice. |
| **Recursos da Unreal explorados** | Materials, Material Instances, Foliage |
| **Entrega** | **Code Review** de materiais e composição de cena |

---

### Semana 13 🔵
**Tema:** Áudio, Optimization e Profiling

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como integrar áudio como parte da experiência de jogo e identificar gargalos antes da entrega final? |
| **Documentação de Referência** | Unreal Engine Documentation — Audio Overview; Optimization Guide |
| **Encontro 1** | Fundamentação da integração de áudio a eventos de gameplay (não como elemento acessório). Integração de sons a ações já existentes no projeto (interação, passos, ambiente). |
| **Encontro 2** | Fundamentação de Optimization e Profiling como etapa obrigatória de produção, comparando com o Profiler da Unity. Profiling do próprio projeto e identificação de pontos críticos. **Desafio:** cada grupo otimiza um aspecto específico identificado no profiling do seu Vertical Slice (geometria, materiais, iluminação, lógica de Blueprint), justificando a escolha. |
| **Recursos da Unreal explorados** | Áudio, Optimization, Profiling |
| **Entrega** | **Feedback formal** sobre as otimizações realizadas |

---

### Semana 14 🔴
**Tema:** Packaging e consolidação do Vertical Slice final

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que diferencia um protótipo de um build distribuível? |
| **Documentação de Referência** | Packaging Your Project |
| **Encontro 1** | Fundamentação do pipeline de Packaging — configurações, plataformas-alvo, build de produção. Empacotamento guiado do Vertical Slice final. |
| **Encontro 2** | Revisão geral do projeto sob a perspectiva de um pequeno estúdio. Playtest cruzado entre grupos e ajustes finais no build. |
| **Recursos da Unreal explorados** | Materials, Material Instances, Foliage, Áudio, Optimization, Profiling, Packaging |
| **Entrega** | **Vertical Slice final (Módulo 4)** — otimizado e empacotado (entrega parcial); Playtest cruzado; Code Review de encerramento |
| **Observação** | Encerramento da Unidade IV. |

---

## Unidade V — Comparar Arquiteturas (Semanas 15–17)

*Pergunta da Unidade: como a arquitetura da Unreal se compara à de outras engines, e o que aprendemos sobre autonomia para aprender novos motores?*
*Metodologia dominante: Reverse Engineering — os estudantes analisam projetos profissionais e defendem tecnicamente o próprio projeto. Autonomia muito alta.*

---

### Semana 15 🔵
**Tema:** Engenharia reversa de projetos profissionais (Lyra, Stack O Bot, Content Examples)

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma equipe profissional estrutura a arquitetura de um jogo em produção real? |
| **Documentação de Referência** | Samples and Tutorials — Lyra Starter Game, Stack O Bot, Content Examples |
| **Encontro 1** | Estudo de caso — Lyra Starter Game: leitura arquitetural guiada do gameplay framework em produção real, com paralelo às decisões tomadas no Vertical Slice da turma. |
| **Encontro 2** | Estudo de caso — Stack O Bot e Content Examples. Comparação entre as soluções dos projetos de referência e as soluções adotadas pelo próprio grupo ao longo do semestre. **Desafio:** cada grupo identifica ao menos uma decisão arquitetural do seu projeto que poderia ser refeita à luz dos projetos de referência analisados. |
| **Recursos da Unreal explorados** | Lyra Starter Game, Stack O Bot, Content Examples |
| **Entrega** | **Feedback formal** sobre as análises arquiteturais |

---

### Semana 16 🔴
**Tema:** Comparação arquitetural Unreal x Unity x Godot x O3DE x Stride x CryEngine

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que é transferível entre engines, e o que é específico da Unreal? |
| **Documentação de Referência** | Unity Manual/Unity Learn; Godot Documentation; documentação pública de O3DE, Stride e CryEngine (consulta comparativa) |
| **Encontro 1** | Consolidação da comparação sistemática Unreal x Unity ao longo de toda a disciplina — gameplay framework, animação, IA, UI e pipeline de produção. Elaboração de quadro comparativo Unreal x Unity com base nos sistemas construídos no semestre. |
| **Encontro 2** | Ampliação da comparação para Godot, O3DE, Stride e CryEngine, quando pertinente a cada sistema estudado. Preparação da apresentação técnica final, incluindo Vertical Slice, decisões arquiteturais e comparação entre motores. **Desafio:** cada grupo escolhe, entre Godot, O3DE, Stride ou CryEngine, o motor mais relevante para comparação com seu próprio projeto, justificando a escolha. |
| **Recursos da Unreal explorados** | Revisão geral do Vertical Slice completo |
| **Entrega** | **Checkpoint de preparação** da apresentação técnica final |

---

### Semana 17 🔴
**Tema:** Apresentação técnica final do Vertical Slice

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que aprendemos sobre arquitetura de motores de jogos e autonomia para aprender novos motores? |
| **Documentação de Referência** | Síntese integrada de toda a documentação consultada no semestre |
| **Encontro 1** | Apresentações técnicas finais (primeiro grupo). Apresentação do Vertical Slice, justificativa de decisões arquiteturais e comparação com Unity e outros motores. |
| **Encontro 2** | Apresentações técnicas finais (grupos restantes) e encerramento. Discussão final sobre autonomia para aprendizagem de novos motores. |
| **Recursos da Unreal explorados** | Vertical Slice completo |
| **Entrega** | **Apresentação técnica final** |
| **Observação** | Encerramento da Unidade V e da disciplina. |

---

## Quadro de Avaliação Contínua

| Semana | Checkpoint | Apresentação | Code Review | Playtest | Feedback formal | Entrega parcial |
|---|---|---|---|---|---|---|
| 3 | X | X (Showcase) | | | | |
| 5 | | | | | X | |
| 6 | X | | | | | |
| 7 | | | X | X | | |
| 9 | | | | | X | |
| 10 | | | X | | | |
| 11 | | X (Showcase) | | X | | |
| 12 | | | X | | | |
| 13 | | | | | X | |
| 14 | | | X | X | | X |
| 15 | | | | | X | |
| 16 | X | | | | | |
| 17 | | X (Final) | | | | |

**Resultado final ao término da Semana 17:** Vertical Slice funcional completo; domínio dos principais sistemas da Unreal Engine explorados na disciplina; compreensão da arquitetura da Unreal Engine; capacidade de comparação técnica entre Unreal, Unity e outros motores; autonomia para aprendizagem de novos motores de jogos.

---

*Disciplina: Tendências de Motores de Jogos — Curso Superior de Tecnologia em Jogos Digitais*
*Instituição: Instituto Federal de Mato Grosso do Sul (IFMS) — Campus Dourados*
