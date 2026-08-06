# Semana 9 — Control nodes e HUD

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11) | **Metodologia:** Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.

## Introdução da Semana

A Semana 8 encerrou com `HealthComponent` funcional no Player, uma State Machine básica de locomoção via AnimationTree e uma animação contextual própria de cada grupo, conectada a um evento real do projeto. Até aqui, todo o estado de jogo relevante — vida (`HealthComponent`), itens coletados (`SaveComponent`/`ItemData`) e progresso (`GameManager`/`SaveData`, checkpoints) — existe e funciona, mas é invisível ao jogador: nada na tela comunica esse estado em tempo real. A Semana 9 resolve exatamente esse problema, introduzindo Control nodes como sistema universal de interface em tempo real e CanvasLayer como camada de organização do HUD. Nenhum sistema de gameplay novo é criado nesta semana — o trabalho é inteiramente de exposição de dados que já existem no Vertical Slice, reforçando o princípio de que toda funcionalidade nova se conecta ao que já foi construído.

## Objetivos Gerais

- Compreender Control nodes como sistema universal de interface em tempo real, e sua posição na mesma Scene Tree que qualquer outro Node do projeto.
- Construir um Control simples vinculado a uma variável de gameplay já existente, compreendendo o fluxo de binding de dados entre lógica de jogo e interface.
- Fundamentar CanvasLayer como camada de organização do HUD sobre a cena de jogo, e montar um HUD com múltiplos elementos.
- Propor e implementar, com autonomia própria, quais dados de gameplay já existentes (vida, itens, progresso) compõem o HUD do grupo, e como.

## Resultados Esperados

Ao final da semana, cada grupo possui um HUD funcional, montado sobre CanvasLayer, exibindo em tempo real ao menos os dados de vida (`HealthComponent`), itens/progresso (`SaveComponent`/`SaveData`) já existentes no projeto, com solução visual e de binding própria, defendida perante o grupo e o professor em feedback formal.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar por que Control nodes resolvem o problema de interface em tempo real como parte da mesma Scene Tree do jogo, não como sistema externo.
- Diferenciar containers, anchors e binding de dados como os três problemas centrais de qualquer sistema de UI em tempo real.
- Construir um Control simples vinculado a uma variável de gameplay já existente no projeto.

## Conteúdos

- O problema de comunicar estado de jogo ao jogador em tempo real, sem acoplar lógica de gameplay à lógica de interface.
- Control nodes: posição na Scene Tree, containers (organização automática de layout), anchors (ancoragem relativa ao viewport).
- Binding de dados: como um Control lê (ou é atualizado por) uma variável de gameplay já existente, sem duplicar o estado.
- Construção guiada de um Control simples (ex.: um Label) vinculado a um dado real já existente no projeto (ex.: vida atual do `HealthComponent`).

## Conceitos Fundamentais

Toda engine moderna enfrenta o mesmo problema estrutural: o jogador precisa perceber, em tempo real, informações que só existem como estado interno de gameplay — vida, itens, progresso. A resposta do Godot para esse problema é o Control node, um Node como qualquer outro na Scene Tree, especializado em desenho e interação 2D de interface. Isso contrasta com a intuição comum de que "UI é um sistema à parte": no Godot, HUD, menus e telas de gameplay compartilham a mesma árvore, os mesmos princípios de composição e os mesmos Signals já ensinados desde a Semana 5. Dentro de um Control, dois problemas recorrentes aparecem em qualquer sistema de UI: como organizar múltiplos elementos automaticamente (containers, como `HBoxContainer`/`VBoxContainer`) e como ancorar um elemento a uma posição relativa ao viewport, independente de resolução (anchors). O terceiro problema — talvez o mais importante pedagogicamente — é o binding de dados: um Control não deve conter lógica de gameplay, apenas ler ou ser notificado sobre um dado que já existe em outro sistema (`HealthComponent`, `SaveComponent`, `GameManager`), reforçando a mesma separação de responsabilidades já cobrada desde o Code Review da Semana 7.

## Recursos do Godot

Control, containers (`HBoxContainer`/`VBoxContainer`), anchors, `HealthComponent` (retomado da Semana 8). O binding de dados que conecta o Control ao `HealthComponent` é implementado via Orchestrator ou GDScript, à escolha do professor/grupo.

## Comparação com Unity

A Unity resolve o mesmo problema historicamente por dois caminhos: uGUI, baseado em GameObjects com Component `RectTransform` e `Canvas`, e UI Toolkit, baseado em documentos UXML/USS inspirados em web. O Control node do Godot ocupa uma posição conceitual mais próxima do uGUI — é um Node comum na mesma árvore de tudo o mais — mas resolve ancoragem e organização de layout de forma nativa e unificada (anchors e containers built-in), sem a divisão entre dois sistemas paralelos que a Unity ainda mantém. O problema de binding de dados é idêntico nas duas engines: em nenhuma delas a UI deve conhecer a lógica interna do sistema que representa — a interface lê ou é notificada por um dado exposto por outro sistema, nunca implementa a regra de negócio por conta própria.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 8, com `HealthComponent`, State Machine e animação contextual já funcionais.
- Cena de exemplo com um Control simples (Label vinculado à vida do `HealthComponent` via Orchestrator ou GDScript) preparada para demonstração, sem distribuir antes da aula.
- Slides com o comparativo Control node (Godot) × uGUI/UI Toolkit (Unity).
- Lista dos dados de gameplay já existentes no projeto disponíveis para binding (vida via `HealthComponent`, itens/progresso via `SaveComponent`/`SaveData`, estado de partida via `GameManager`).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 8 (animação contextual conectada a evento real) |
| 20 min | Introdução: o problema de comunicar estado de jogo em tempo real; Control nodes na Scene Tree |
| 20 min | Demonstração: containers e anchors como resolução de layout e ancoragem |
| 35 min | Demonstração: construção guiada de um Control simples vinculado à vida do `HealthComponent` |
| 30 min | Laboratório: cada grupo replica o Control simples sobre o próprio `HealthComponent`, ajustando containers/anchors ao seu layout |
| 15 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do projeto herdado da Semana 8 sem alterar nenhum sistema de gameplay existente, introduzindo apenas uma nova camada de leitura sobre o que já existe. O professor demonstra primeiro os dois problemas estruturais de qualquer Control — organização automática via containers e ancoragem via anchors — com exemplos pequenos e isolados, antes de conectar qualquer dado real. Em seguida, demonstra a construção guiada de um Control simples (um Label de vida) vinculado ao `HealthComponent` já existente no Player — o binding em si implementado via Orchestrator ou GDScript —, deixando explícito que o Control apenas lê o valor exposto pelo Component, sem duplicar ou recalcular o estado de vida. Cada grupo replica essa construção sobre seu próprio projeto, adaptando o layout do Control ao restante da sua interface.

## Desafio

Não há desafio de solução livre neste encontro: a construção do Control simples vinculado à vida é guiada, servindo de base direta à montagem do HUD completo e ao desafio do Encontro 2.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, um Control simples funcional exibindo em tempo real a vida atual do Player a partir do `HealthComponent`, com layout organizado por container e posicionado por anchor, sem qualquer lógica de gameplay duplicada dentro do Control.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro (Rubrica 1 — Desenvolvimento Semanal, aplicada de forma contínua). O Control simples construído aqui é pré-requisito direto do desafio de HUD avaliado no Encontro 2.

## Dificuldades Esperadas

- Implementar a leitura de vida como uma variável duplicada dentro do próprio Control, em vez de referenciar o `HealthComponent` existente — reforçar que o Control lê o dado, nunca o recria.
- Confundir anchors com posicionamento absoluto em pixels — reforçar que anchors definem a relação com o viewport, não uma posição fixa.
- Ignorar containers e posicionar elementos manualmente, perdendo a organização automática de layout — reforçar o papel do container antes de qualquer ajuste manual de posição.

---

# Encontro 2

## Objetivos de Aprendizagem

- Fundamentar CanvasLayer como camada de organização do HUD sobre a cena de jogo.
- Montar um HUD com múltiplos elementos organizados sobre um único CanvasLayer.
- Propor e implementar, com autonomia própria, quais dados de gameplay compõem o HUD do grupo e qual solução visual/de binding representa cada um.

## Conteúdos

- CanvasLayer como camada independente da profundidade 3D da cena, garantindo que o HUD permaneça sempre visível sobre o mundo do jogo.
- Organização de múltiplos Control nodes dentro de um único HUD (vida, itens, progresso) sob um mesmo CanvasLayer.
- Desafio: cada grupo define quais dados de gameplay já existentes (vida, itens, progresso) devem compor o HUD, propondo a própria solução visual e de binding para cada um.

## Conceitos Fundamentais

O Encontro 1 resolveu a interface em tempo real no nível de um único elemento. O Encontro 2 resolve o problema de composição: como organizar múltiplos elementos de interface (vida, itens, progresso) em um HUD coeso, que permaneça sempre visível independentemente da câmera 3D ou da profundidade da cena. O CanvasLayer resolve isso desenhando seu conteúdo em uma camada 2D separada da renderização 3D do mundo, garantindo que o HUD nunca seja ocultado por geometria do cenário. A partir daí, o problema deixa de ser técnico e passa a ser de decisão: quais dados de gameplay já existentes (vida via `HealthComponent`, itens/progresso via `SaveComponent`/`SaveData`, estado de partida via `GameManager`) merecem estar no HUD, e que solução visual e de binding representa cada um. Essa é a essência do desafio do encontro — não há solução única correta, mas toda solução deve reutilizar dados já existentes, nunca criar um novo sistema de estado exclusivo para a interface.

## Recursos do Godot

CanvasLayer, Control (retomado do Encontro 1), `HealthComponent`, `SaveComponent`/`SaveData`, `GameManager` (retomados dos Módulos 2 e 3). O binding de cada elemento do HUD é implementado via Orchestrator ou GDScript, conforme a escolha já praticada no Encontro 1.

## Comparação com Unity

A Unity resolve o equivalente ao CanvasLayer com o Canvas em modo Screen Space - Overlay (uGUI), que também desenha sua hierarquia de UI independentemente da câmera 3D da cena; a UI Toolkit resolve o mesmo problema com um `UIDocument` associado a um `PanelSettings` de overlay. O princípio universal é idêntico nas duas engines — a interface do HUD precisa de uma camada de renderização desacoplada da profundidade do mundo 3D — mas o Godot resolve isso com um único Node (CanvasLayer) na mesma Scene Tree de tudo o mais, enquanto a Unity historicamente exige a configuração adicional do Component Canvas (uGUI) ou de um documento próprio (UI Toolkit) fora da hierarquia comum de GameObjects.

## Preparação do Professor

- Projeto de cada grupo com o Control simples de vida do Encontro 1 já funcional.
- Cena de exemplo com CanvasLayer e HUD de múltiplos elementos (vida, itens, progresso) preparada para demonstração, sem distribuir antes da aula.
- Lista consolidada dos dados de gameplay já existentes disponíveis para o desafio: vida (`HealthComponent`), itens/progresso (`SaveComponent`/`SaveData`), estado de partida (`GameManager`).
- Roteiro do desafio preparado: cada grupo escolhe quais dados compõem seu HUD e propõe a própria solução visual e de binding.
- Slides com o comparativo CanvasLayer (Godot) × Canvas Screen Space - Overlay/UIDocument (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (Control simples vinculado à vida) |
| 25 min | Demonstração: fundamentação de CanvasLayer e montagem guiada de um HUD com múltiplos elementos |
| 15 min | Apresentação do desafio: cada grupo define quais dados compõem seu HUD e propõe a própria solução visual/de binding |
| 50 min | Laboratório/Desafio: cada grupo monta seu HUD sobre CanvasLayer, conectando os dados escolhidos |
| 30 min | Feedback formal: cada grupo apresenta e justifica as escolhas do próprio HUD |

## Desenvolvimento

O encontro abre com a fundamentação e montagem guiada de um HUD de exemplo sobre CanvasLayer, combinando múltiplos Control nodes (vida, itens, progresso) em um único layout organizado, usando exatamente os dados já existentes no projeto. A partir daí, o professor apresenta o problema central do encontro: cada grupo deve decidir quais dados de gameplay já existentes compõem o próprio HUD e propor a solução visual e de binding para cada um, sem introduzir nenhum sistema de estado novo. O professor circula entre os grupos como facilitador da decisão, questionando por que cada dado foi incluído (ou não) e como o binding evita duplicação do estado de gameplay — postura característica da Challenge Based Learning que já orienta a Unidade III desde a Semana 8.

## Desafio

Cada grupo define quais dados de gameplay já existentes (vida, itens, progresso) devem compor o HUD, propondo a própria solução visual e de binding para cada um, organizados sobre um único CanvasLayer. **Entrega: Feedback formal** sobre as soluções de HUD apresentadas.

## Critérios de Sucesso

Cada grupo possui, ao final da semana, um HUD funcional sobre CanvasLayer, exibindo em tempo real ao menos vida e um segundo dado de gameplay já existente (itens ou progresso), com a escolha dos dados e a solução visual justificada perante o grupo, sem qualquer lógica de gameplay duplicada dentro dos Control nodes.

## Evidências para Avaliação

**Desafio Técnico** (Rubrica 2 do Sistema de Avaliação) — capacidade de propor solução própria dentro de um espaço de escolha real (quais dados exibir e como), justificando a decisão pela relevância do dado para o jogador; binding correto aos sistemas já existentes (`HealthComponent`, `SaveComponent`/`SaveData`, `GameManager`), sem duplicação de estado ou lógica de gameplay dentro da interface. **Feedback formal** conduzido na apresentação de cada grupo ao final do encontro.

## Dificuldades Esperadas

- Duplicar o estado de gameplay dentro do próprio Control (ex.: uma variável de vida separada no HUD) em vez de ler o `HealthComponent` existente — reforçar que o HUD é sempre um espelho de um dado que já existe em outro sistema.
- Posicionar elementos do HUD diretamente na cena 3D em vez de sob um CanvasLayer, fazendo com que a interface seja ocultada por geometria do cenário — reforçar o papel do CanvasLayer como camada 2D independente.
- Incluir no HUD um dado que não existe no projeto (ex.: um contador criado apenas para a interface) — reforçar que todo exercício pertence ao Vertical Slice e reutiliza dados já modelados nos módulos anteriores.

---

# Resultado Esperado da Semana

Ao final da Semana 9, cada grupo possui um HUD funcional montado sobre CanvasLayer, com Control nodes exibindo em tempo real ao menos vida (`HealthComponent`) e um segundo dado de gameplay já existente (itens via `SaveComponent`/`SaveData` ou progresso via `GameManager`), com solução visual e de binding própria, apresentada e justificada em feedback formal. A turma domina Control nodes, containers, anchors e CanvasLayer como sistema universal de interface em tempo real, relaciona esse conjunto a uGUI/UI Toolkit da Unity, e consolidou a prática de expor dados de gameplay já existentes sem duplicação de estado.

# Preparação para a Próxima Semana

O HUD construído nesta semana ganha um novo consumidor na Semana 10: o `InventoryComponent`, que reutiliza os itens já modelados como `ItemData` desde a Semana 6 e passa a expor sua própria `InventoryUI` sobre os mesmos princípios de Control node e binding de dados fundamentados aqui. A Semana 10 também retoma e amplia diretamente o contrato `Interactable` da Semana 5, conectando-o ao novo sistema de inventário.

# Referências

- Godot Documentation — User Interface (UI): https://docs.godotengine.org/en/stable/tutorials/ui/index.html
- Godot Documentation — Nodes and Scene Instances: https://docs.godotengine.org/en/stable/getting_started/step_by_step/nodes_and_scenes.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — UI Toolkit: https://docs.unity3d.com/Manual/UIElements.html
- Unity Manual (consulta comparativa) — Canvas: https://docs.unity3d.com/Manual/UICanvas.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
