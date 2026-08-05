# Cronograma Detalhado — Disciplina de Tendências de Motores de Jogos
**Curso Superior de Tecnologia em Jogos Digitais**
Vertical Slice Incremental | 17 Semanas | 102 h/a — 76h (2 encontros de 2h15/semana) | Godot 4.7 + Orchestrator

> 🔴 **Encerramento de módulo** — entrega de artefato jogável, checkpoint, playtest, code review ou apresentação que fecha uma Unidade/Módulo inteiro: semanas **3, 7, 11, 14, 16 e 17**
> 🔴 **Semana 17** — apresentação técnica final e encerramento; **não** há novo conteúdo introduzido
> 🔵 Semana regular (fundamentação e desenvolvimento do Vertical Slice) nas demais
> **Nota sobre 🔴 × 🔵 e instrumentos formais:** o emoji 🔴 marca especificamente o encerramento de uma Unidade/Módulo — não qualquer instrumento avaliativo formal isolado. Um Code Review formal intermediário, que não fecha módulo (como o da Semana 12, encerramento apenas do Encontro 1 de Materials/Foliage dentro da Unidade IV ainda em curso), permanece corretamente marcado 🔵: introduz conteúdo novo e não corresponde a um marco de fechamento de Unidade.

> **Nota de avaliação:** a disciplina não utiliza prova tradicional. Cada módulo encerra com instrumentos coerentes com sua metodologia — checkpoint, code review, playtest e/ou apresentação — conforme o Plano de Ensino (seção "Avaliação da Aprendizagem"). O peso entre critérios cresce em favor da justificativa técnica e da comparação arquitetural nos módulos finais.

> **Nota de fonte:** a documentação indicada em cada semana segue a Documentação Oficial do Godot Engine e a documentação do Orchestrator (ver REFERENCES.md), consultadas de forma crítica — sem reprodução de trechos extensos — e sempre comparadas à documentação oficial da Unity (Unity Manual/Unity Learn) e, quando pertinente, de Unreal Engine, O3DE ou Stride.

> **Nota de ordem:** a disciplina não segue o sumário de um único livro-texto, mas a evolução do próprio Vertical Slice. Por isso, um mesmo sistema pode ser introduzido de forma mínima em um módulo e retomado com profundidade maior em outro — por exemplo, **Interaction** aparece na Semana 5 (interação simples via contrato Interactable/Signal) e é ampliado na Semana 10 (múltiplos tipos de interação conectados ao Inventário). O professor deve sinalizar cada retomada à turma.

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
- **Semana 6, Encontro 1** — a introdução ao Resource customizado (ItemData) pode ser condensada, já que é retomada na aplicação da Semana 6, Encontro 2.
- **Semana 12, Encontro 1** — a refatoração de materiais em Material Overrides pode ser reduzida se o projeto já usa poucos materiais base.
- **Semana 15, Encontro 1** — a análise do TPS Demo pode ser conduzida por leitura dirigida prévia, liberando tempo em aula para discussão.

**Encontros que não devem ser comprimidos:**

- **Semanas 3, 7, 11, 14, 16 e 17, Encontro 2** — concentram os instrumentos avaliativos de encerramento de módulo (checkpoint, code review, playtest ou apresentação). Comprimir aqui é comprimir avaliação.
- **Semana 7, Encontro 2** — o Code Review + Playtest de encerramento do Módulo 2 depende da integração de todos os desafios do módulo; não há espaço de compressão.
- **Semana 14, Encontro 1** — a exportação do build final é pré-requisito do Playtest cruzado da Semana 14, Encontro 2; sem ela, o encontro seguinte trava.
- **Semana 17** — a apresentação final é o instrumento de maior peso do semestre.

**Se um encontro for perdido:** a primeira opção é redistribuir o conteúdo dentro do próprio módulo, comprimindo o encontro de fundamentação seguinte. A segunda é converter parte da fundamentação em consulta dirigida à documentação oficial do Godot, com verificação no início do encontro seguinte. Adiar a entrega de um módulo deve ser a última opção, porque desloca todas as entregas seguintes e compromete o feedback contínuo característico das metodologias ativas adotadas.

---

## Unidade I — Aprender a Ferramenta (Semanas 1–3)

*Pergunta da Unidade: como uma engine estrutura um mundo jogável?*
*Metodologia dominante: Scaffolded Learning — professor demonstra, aluno replica. Autonomia muito baixa.*

---

### Semana 1 🔵
**Tema:** Arquitetura do Godot, Nodes e Scene Tree

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que é uma game engine e como ela organiza um mundo jogável? |
| **Documentação de Referência** | Godot Documentation — Getting Started / Introduction; Orchestrator — Visão geral (orchestrator.cratercrash.space) |
| **Encontro 1** | Fundamentação: o que é uma engine e por que ela existe, antes de qualquer botão. Tour guiado pelo Godot Editor — Viewport, FileSystem Dock, estrutura de projeto. Criação e organização inicial do projeto do Vertical Slice. |
| **Encontro 2** | Fundamentação de Node e Scene Tree como unidade universal de composição (composição versus herança), comparando brevemente com GameObject/Component da Unity. Criação guiada de uma Scene com Nodes filhos via Orchestrator. **Desafio:** adicionar um Node filho adicional à Scene, produzindo um comportamento visual diferente do demonstrado. |
| **Recursos do Godot explorados** | Godot Editor, Viewport, FileSystem Dock, Node, Scene Tree, Orchestrator |
| **Entrega** | — |

---

### Semana 2 🔵
**Tema:** CharacterBody3D, movimentação e Input Map

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine desacopla a intenção do jogador (input) da ação no mundo? |
| **Documentação de Referência** | Godot Documentation — Inputs |
| **Encontro 1** | Fundamentação de CharacterBody3D e de `move_and_slide` como sistema universal de locomoção. Configuração guiada de um CharacterBody3D controlável no nível de teste. |
| **Encontro 2** | Fundamentação de Input Map e InputEvent — Actions, eventos de input, deadzones — comparando com o Input System da Unity. Configuração de Input Map para movimentação. **Desafio:** adicionar uma nova Action (correr, agachar ou pular) não demonstrada em aula, com liberdade de implementação. |
| **Recursos do Godot explorados** | CharacterBody3D, move_and_slide, Input Map, InputEvent |
| **Entrega** | — |

---

### Semana 3 🔴
**Tema:** Materiais, Terrain3D, SDFGI/VoxelGI e Exportação

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine renderiza e empacota um mundo jogável? |
| **Documentação de Referência** | Godot Documentation — Standard Material 3D; Global Illumination (SDFGI/VoxelGI); Exporting Projects; Terrain3D (addon) |
| **Encontro 1** | Fundamentação do Material Graph (conceito de shader nodal) e do addon Terrain3D como ferramenta de terreno — sem equivalente nativo no Godot. Criação guiada de um material simples e modelagem de um terreno básico para o mapa do projeto. |
| **Encontro 2** | Fundamentação dos conceitos universais de renderização moderna — iluminação global dinâmica (SDFGI/VoxelGI) — e discussão sobre geometria virtualizada como conceito ausente no Godot (comparação direta com Nanite da Unreal). Fundamentação do pipeline de exportação. Ativação e ajuste de SDFGI/VoxelGI no nível. Geração do primeiro build exportado do Vertical Slice. |
| **Recursos do Godot explorados** | Materiais, Terrain3D, SDFGI/VoxelGI, Exportação de projeto |
| **Entrega** | **Checkpoint de encerramento do Módulo 1** — primeiro build executável do Vertical Slice; Showcase em aula |
| **Observação** | Encerramento da Unidade I. |

---

## Unidade II — Construir Sistemas (Semanas 4–7)

*Pergunta da Unidade: como um jogo se estrutura por trás da jogabilidade visível?*
*Metodologia dominante: Studio Based Learning — professor demonstra, aluno adapta. Autonomia baixa.*

---

### Semana 4 🔵
**Tema:** GameManager e SaveManager (Autoload/Singleton)

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine separa regras de partida, estado compartilhado e persistência entre cenas? |
| **Documentação de Referência** | Godot Documentation — Nodes and Scene Instances (Autoload/Singleton) |
| **Encontro 1** | Fundamentação de Autoload/Singleton como mecanismo nativo de estado global — o `GameManager` reúne o papel de regras da partida e estado compartilhado que a Unreal separa em GameMode/GameState — comparando com a ausência de um equivalente formal na Unity (padrão de Managers/Singletons). Criação guiada de um `GameManager` customizado. |
| **Encontro 2** | Fundamentação de input de alto nível centralizado no próprio Player (sem separação nativa Pawn/Controller) e do `SaveManager` (Autoload) como persistência entre cenas. Implementação de uma variável persistente no `SaveManager`. **Desafio:** cada grupo define e implementa um dado próprio que deve persistir entre cenas (pontuação, item coletado, estado de progresso), com liberdade de escolha. |
| **Recursos do Godot explorados** | Autoload/Singleton, GameManager, SaveManager |
| **Entrega** | — |

---

### Semana 5 🔵
**Tema:** Contrato Interactable e Signals

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como comunicar sistemas sem criar dependência direta entre eles? |
| **Documentação de Referência** | Godot Documentation — GDScript; Orchestrator — Interfaces e Nodes de Evento |
| **Encontro 1** | Fundamentação do contrato `Interactable` como mecanismo de comunicação desacoplada — via duck typing/`has_method` em GDScript ou nó de interface do Orchestrator —, comparando com Interfaces em C# na Unity. Criação guiada de um contrato de interação genérico implementado por uma Scene. |
| **Encontro 2** | Fundamentação de Signals como padrão observer, comparando com UnityEvent/C# Actions. Implementação de um Signal acionado por interação. **Desafio:** cada grupo implementa um objeto interativo (porta ou equivalente escolhido pelo grupo) usando contrato Interactable + Signal, permitindo diferentes soluções de acionamento (alavanca, chave, proximidade). |
| **Recursos do Godot explorados** | Contrato Interactable, Signals |
| **Entrega** | **Feedback formal** sobre as soluções de interação apresentadas pelos grupos |

---

### Semana 6 🔵
**Tema:** Resource customizado (ItemData) e Enums

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como separar dados de design da lógica de gameplay? |
| **Documentação de Referência** | Godot Documentation — Resources |
| **Encontro 1** | Fundamentação de Resource customizado como estrutura de dados desacoplada da lógica, comparando com ScriptableObjects na Unity (equivalente quase direto). Criação guiada de um Resource (`ItemData`) para itens/entidades do projeto. |
| **Encontro 2** | Fundamentação de Enums como organizadores de dados tipados dentro de um Resource. **Desafio:** cada grupo modela seu próprio conjunto de itens coletáveis (baús, moedas, recursos) usando `ItemData` + Enum, com liberdade de categorias e atributos. |
| **Recursos do Godot explorados** | Resource customizado, Enums |
| **Entrega** | **Checkpoint de progresso** do Módulo 2 |

---

### Semana 7 🔴
**Tema:** Save/Load e consolidação do gameplay do Módulo 2

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine serializa e recupera o estado de progresso de um jogador? |
| **Documentação de Referência** | Godot Documentation — Saving Games (FileAccess, ResourceSaver/ResourceLoader) |
| **Encontro 1** | Fundamentação de `SaveData` (Resource) + FileAccess como serialização de estado de jogo, comparando com PlayerPrefs/serialização em JSON na Unity. Implementação de save/load de um estado simples do projeto (ex.: itens coletados), seguida da construção de `Checkpoint`, que reutiliza o contrato `Interactable` e o `SaveComponent` para gravar progresso. |
| **Encontro 2** | Revisão integrada de GameManager, contrato Interactable, Signals, Resources e save/load. Integração final dos desafios do módulo (portas, baús, alavancas, `Checkpoint`) em um único fluxo jogável. **Desafio:** cada grupo apresenta sua integração completa, justificando as escolhas de arquitetura adotadas. |
| **Recursos do Godot explorados** | Save/Load (SaveData, FileAccess), `Checkpoint`, GameManager, SaveManager, contrato Interactable, Signals, Resource customizado, Enums |
| **Entrega** | **Gameplay funcional consolidado (Módulo 2)**; Code Review dos sistemas implementados; Playtest coletivo |
| **Observação** | Encerramento da Unidade II. |

---

## Unidade III — Resolver Problemas (Semanas 8–11)

*Pergunta da Unidade: como resolver, com autonomia crescente, os problemas de um Vertical Slice jogável?*
*Metodologia dominante: Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.*

---

### Semana 8 🔵
**Tema:** HealthComponent, AnimationTree, BlendSpace e AnimationPlayer

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Onde vive o estado de vida/dano de um personagem, e como uma engine resolve a transição e a combinação de animações? |
| **Documentação de Referência** | Godot Documentation — Animation; Godot Documentation — Nodes and Scene Instances |
| **Encontro 1** | Construção guiada de `HealthComponent` (vida atual/máxima, `apply_damage`, sinal `died`), seguindo o mesmo padrão de `InteractionComponent`/`SaveComponent`. Fundamentação de AnimationTree e AnimationNodeStateMachine, comparando com o Animator Controller da Unity. Criação guiada de uma State Machine básica (idle, andar, correr). |
| **Encontro 2** | Fundamentação de BlendSpace1D/2D (interpolação multidimensional) e faixas do AnimationPlayer (animações pontuais sobrepostas), comparando com Blend Trees na Unity. Configuração de um BlendSpace direcional e uma animação pontual de ação. **Desafio:** cada grupo propõe e implementa uma animação contextual própria (reação a dano, interação, ataque), escolhendo entre BlendSpace ou animação pontual conforme o problema. |
| **Recursos do Godot explorados** | `HealthComponent`, AnimationTree, BlendSpace1D/2D, AnimationPlayer |
| **Entrega** | — |

---

### Semana 9 🔵
**Tema:** Control nodes e HUD

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como comunicar em tempo real o estado do jogo ao jogador? |
| **Documentação de Referência** | Godot Documentation — User Interface (UI) |
| **Encontro 1** | Fundamentação de Control nodes como sistema universal de interface em tempo real — containers, anchors, binding de dados — comparando com UI Toolkit/uGUI na Unity. Criação guiada de um Control simples vinculado a uma variável de gameplay existente. |
| **Encontro 2** | Fundamentação de CanvasLayer + Control como camada de organização do HUD. Montagem guiada de um HUD com múltiplos elementos. **Desafio:** cada grupo define quais dados de gameplay já existentes (vida, itens, progresso) devem compor o HUD, propondo a própria solução visual e de binding. |
| **Recursos do Godot explorados** | Control nodes, CanvasLayer, HUD |
| **Entrega** | **Feedback formal** sobre as soluções de HUD apresentadas |

---

### Semana 10 🔵
**Tema:** Inventário e ampliação do Interaction System

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como estruturar o armazenamento e a manipulação de itens em um jogo? |
| **Documentação de Referência** | Godot Documentation — Resources (ItemData aplicado a inventário) |
| **Encontro 1** | Fundamentação de padrões de Inventory System — armazenamento, adição/remoção, exibição. Estruturação inicial de um `InventoryComponent` reutilizando os itens modelados na Semana 6. |
| **Encontro 2** | Retomada e ampliação do Interaction System introduzido na Semana 5 — detecção, priorização e resposta a múltiplos tipos de interação. Conexão do sistema de interação ao inventário (coletar, usar, descartar). **Desafio:** cada grupo expande seu sistema de interação para suportar um novo tipo (empilhar itens, combinar itens, interação com cooldown), com solução própria. |
| **Recursos do Godot explorados** | Inventory (Resource customizado, Control nodes), Interaction |
| **Entrega** | **Code Review** dos sistemas de inventário e interação |

---

### Semana 11 🔴
**Tema:** Navigation, Behavior Trees (LimboAI), Blackboards e Combate Simples

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma engine dá autonomia de deslocamento e decisão a um agente não-jogador, e como detecta que um ataque acertou um alvo? |
| **Documentação de Referência** | Godot Documentation — Navigation; LimboAI (github.com/limbonaut/limboai); Godot Documentation — Physics (Area3D, RayCast3D) |
| **Encontro 1** | Fundamentação de NavigationRegion3D/NavigationAgent3D como base universal de deslocamento de agentes, comparando com o NavMesh da Unity. Configuração de NavigationRegion3D no nível e movimentação de um agente até um ponto. |
| **Encontro 2** | Fundamentação de Behavior Tree (estrutura de decisão) e Blackboard (memória compartilhada) via addon LimboAI — nenhum dos dois é nativo do Godot —, comparando com Behavior Designer/NodeCanvas na Unity. Implementação guiada de uma Behavior Tree simples (patrulha/perseguição) e de um combate simples (Area3D/RayCast3D do `Player` chamando `apply_damage` no `HealthComponent` do `Enemy`). **Desafio:** cada grupo propõe um comportamento autônomo próprio para o NPC do seu projeto (patrulha, alerta, fuga, interação com o jogador), com liberdade de solução. |
| **Recursos do Godot explorados** | NavigationRegion3D, NavigationAgent3D, Behavior Trees, Blackboards (LimboAI), Area3D/RayCast3D (combate simples) |
| **Entrega** | **Vertical Slice jogável (Módulo 3)** — animação, interface, inventário, interação e IA integrados; Playtest coletivo; Showcase |
| **Observação** | Encerramento da Unidade III. |

---

## Unidade IV — Produzir como um Pequeno Estúdio (Semanas 12–14)

*Pergunta da Unidade: como transformar um protótipo funcional em um produto entregável?*
*Metodologia dominante: Studio Based Learning — professor como diretor técnico. Autonomia alta.*

---

### Semana 12 🔵
**Tema:** Materials, Material Overrides e Foliage

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como padronizar e otimizar a produção visual de um projeto em escala de estúdio? |
| **Documentação de Referência** | Godot Documentation — Standard Material 3D |
| **Encontro 1** | Fundamentação de Material Override/Unique Material versus material base como estratégia de parametrização e otimização, comparando com Material Property Blocks na Unity. Refatoração de materiais do projeto em Overrides parametrizados. |
| **Encontro 2** | Fundamentação de MultiMeshInstance3D como ferramenta de composição de cena — densidade, performance e composição visual (equivalente à Foliage Tool). Composição de vegetação/elementos de cena no nível do Vertical Slice. |
| **Recursos do Godot explorados** | Materials, Material Overrides, MultiMeshInstance3D |
| **Entrega** | **Code Review** de materiais e composição de cena |

---

### Semana 13 🔵
**Tema:** Áudio, Optimization e Profiling

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como integrar áudio como parte da experiência de jogo e identificar gargalos antes da entrega final? |
| **Documentação de Referência** | Godot Documentation — Audio; Godot Documentation — Optimization (Debugger/Profiler) |
| **Encontro 1** | Fundamentação da integração de áudio a eventos de gameplay (não como elemento acessório) via AudioStreamPlayer. Integração de sons a ações já existentes no projeto (interação, passos, ambiente). |
| **Encontro 2** | Fundamentação de Optimization e Profiling como etapa obrigatória de produção, usando o Profiler/Debugger nativo do Godot, comparando com o Profiler da Unity. Profiling do próprio projeto e identificação de pontos críticos. **Desafio:** cada grupo otimiza um aspecto específico identificado no profiling do seu Vertical Slice (geometria, materiais, iluminação, lógica de script/Orchestration), justificando a escolha. |
| **Recursos do Godot explorados** | AudioStreamPlayer, Optimization, Profiler/Debugger |
| **Entrega** | **Feedback formal** sobre as otimizações realizadas |

---

### Semana 14 🔴
**Tema:** Exportação e consolidação do Vertical Slice final

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que diferencia um protótipo de um build distribuível? |
| **Documentação de Referência** | Godot Documentation — Exporting Projects |
| **Encontro 1** | Fundamentação do pipeline de exportação — Export Templates, presets, plataformas-alvo, build de produção. Exportação guiada do Vertical Slice final. |
| **Encontro 2** | Revisão geral do projeto sob a perspectiva de um pequeno estúdio. Playtest cruzado entre grupos e ajustes finais no build. |
| **Recursos do Godot explorados** | Materials, Material Overrides, MultiMeshInstance3D, AudioStreamPlayer, Optimization, Profiling, Exportação de projeto |
| **Entrega** | **Vertical Slice final (Módulo 4)** — otimizado e exportado (entrega parcial); Playtest cruzado; Code Review de encerramento |
| **Observação** | Encerramento da Unidade IV. |

---

## Unidade V — Comparar Arquiteturas (Semanas 15–17)

*Pergunta da Unidade: como a arquitetura do Godot se compara à de outras engines, e o que aprendemos sobre autonomia para aprender novos motores?*
*Metodologia dominante: Reverse Engineering — os estudantes analisam projetos profissionais e defendem tecnicamente o próprio projeto. Autonomia muito alta.*

---

### Semana 15 🔵
**Tema:** Engenharia reversa de projetos profissionais (Godot Demo Projects, TPS Demo, Platformer 2D Demo)

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | Como uma equipe profissional/comunidade estrutura a arquitetura de um jogo em produção real? |
| **Documentação de Referência** | Godot Demo Projects (github.com/godotengine/godot-demo-projects) — TPS Demo, Platformer 2D Demo |
| **Encontro 1** | Estudo de caso — TPS Demo (Third Person Shooter): leitura arquitetural guiada do gameplay framework em um projeto oficial, com paralelo às decisões tomadas no Vertical Slice da turma. |
| **Encontro 2** | Estudo de caso — Platformer 2D Demo e outros Godot Demo Projects relevantes. Comparação entre as soluções dos projetos de referência e as soluções adotadas pelo próprio grupo ao longo do semestre. **Desafio:** cada grupo identifica ao menos uma decisão arquitetural do seu projeto que poderia ser refeita à luz dos projetos de referência analisados. |
| **Recursos do Godot explorados** | Godot Demo Projects, TPS Demo, Platformer 2D Demo |
| **Entrega** | **Feedback formal** sobre as análises arquiteturais |

---

### Semana 16 🔴
**Tema:** Comparação arquitetural Godot x Unity x Unreal x O3DE x Stride

| Campo | Conteúdo |
|---|---|
| **Pergunta Norteadora** | O que é transferível entre engines, e o que é específico do Godot? |
| **Documentação de Referência** | Unity Manual/Unity Learn; Unreal Engine Documentation; documentação pública de O3DE e Stride (consulta comparativa) |
| **Encontro 1** | Consolidação da comparação sistemática Godot x Unity ao longo de toda a disciplina — gameplay framework, animação, IA, UI e pipeline de produção. Elaboração de quadro comparativo Godot x Unity com base nos sistemas construídos no semestre. |
| **Encontro 2** | Ampliação da comparação para Unreal Engine, O3DE e Stride, quando pertinente a cada sistema estudado. Preparação da apresentação técnica final, incluindo Vertical Slice, decisões arquiteturais e comparação entre motores. **Desafio:** cada grupo escolhe, entre Unreal Engine, O3DE ou Stride, o motor mais relevante para comparação com seu próprio projeto, justificando a escolha. |
| **Recursos do Godot explorados** | Revisão geral do Vertical Slice completo |
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
| **Recursos do Godot explorados** | Vertical Slice completo |
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

**Resultado final ao término da Semana 17:** Vertical Slice funcional completo; domínio dos principais sistemas do Godot Engine explorados na disciplina; compreensão da arquitetura do Godot; capacidade de comparação técnica entre Godot, Unity e outros motores; autonomia para aprendizagem de novos motores de jogos.

---

*Disciplina: Tendências de Motores de Jogos — Curso Superior de Tecnologia em Jogos Digitais*
*Instituição: Instituto Federal de Mato Grosso do Sul (IFMS) — Campus Dourados*
