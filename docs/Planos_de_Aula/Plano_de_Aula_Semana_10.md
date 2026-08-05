# Semana 10 — Inventário e ampliação do Interaction System

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11) | **Metodologia:** Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.

## Introdução da Semana

A Semana 9 encerrou com um HUD funcional sobre CanvasLayer, exibindo em tempo real vida (`HealthComponent`) e um segundo dado de gameplay já existente, cada grupo com solução visual e de binding própria. Até aqui, os itens do jogo existem apenas como `ItemData` (Resource + Enum, desde a Semana 6) e são coletados via `Chest`/`Pickup`, mas não há nenhum lugar no projeto onde esses itens sejam armazenados, listados ou manipulados pelo jogador — eles simplesmente desaparecem da cena ao serem coletados. A Semana 10 resolve esse problema estruturando um `InventoryComponent` que reutiliza diretamente o `ItemData` já modelado, e expõe seus dados através de uma `InventoryUI` construída sobre os mesmos princípios de Control node e binding fundamentados na Semana 9. No Encontro 2, a semana retoma e amplia o contrato `Interactable` introduzido na Semana 5, conectando-o ao inventário recém-criado — nenhum sistema novo de comunicação é criado, apenas uma extensão do que já existe. A semana fecha com o Code Review da Rubrica 4 sobre os sistemas de inventário e interação.

## Objetivos Gerais

- Compreender padrões de Inventory System — armazenamento, adição/remoção, exibição — como problema estrutural comum a qualquer engine.
- Estruturar um `InventoryComponent` reutilizando diretamente o `ItemData` já modelado na Semana 6, sem duplicar dados de item.
- Retomar e ampliar o contrato `Interactable` da Semana 5 para detectar, priorizar e responder a múltiplos tipos de interação.
- Conectar o Interaction System ampliado ao inventário (coletar, usar, descartar), propondo e implementando com autonomia própria um novo tipo de interação.
- Submeter os sistemas de inventário e interação a Code Review formal (Rubrica 4), com foco em organização, modularidade e comunicação desacoplada entre sistemas.

## Resultados Esperados

Ao final da semana, cada grupo possui um `InventoryComponent` funcional armazenando os `ItemData` coletados pelo jogador, exposto por uma `InventoryUI` construída sobre Control nodes, e um Interaction System ampliado que conecta a coleta, o uso e o descarte de itens ao inventário — incluindo um novo tipo de interação proposto e implementado pelo próprio grupo (empilhar, combinar ou interação com cooldown) — com o conjunto avaliado em Code Review formal.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar os três problemas centrais de qualquer Inventory System: armazenamento, adição/remoção e exibição de itens.
- Estruturar um `InventoryComponent` que armazena instâncias de `ItemData` já modeladas na Semana 6, sem duplicar dados de item.
- Reconhecer o `InventoryComponent` como um Component reutilizável, seguindo o mesmo padrão de `InteractionComponent`/`HealthComponent`/`SaveComponent`.

## Conteúdos

- O problema de armazenamento de itens: onde vive a lista de itens que o jogador possui, e por que não deve viver dentro do próprio `Chest`/`Pickup` que os originou.
- Padrões de Inventory System: adição, remoção e consulta de itens armazenados, reutilizando o `ItemData` (Resource + Enum) já existente desde a Semana 6.
- Estruturação inicial de um `InventoryComponent` como Component do Player, seguindo o mesmo padrão de composição de `InteractionComponent`, `HealthComponent` e `SaveComponent`.
- Exposição inicial dos dados do `InventoryComponent` para consumo futuro por uma `InventoryUI` (sem construir a UI ainda neste encontro).

## Conceitos Fundamentais

Todo jogo com coleta de itens enfrenta o mesmo problema estrutural, independentemente da engine: os dados de definição de um item (nome, ícone, tipo — já resolvidos pelo `ItemData` desde a Semana 6) precisam ser separados do estado de posse daquele item por um jogador específico. Esse estado de posse — quais itens, em que quantidade, o jogador carrega agora — é responsabilidade de um novo Component, o `InventoryComponent`, que armazena referências a instâncias de `ItemData` sem duplicar ou recriar seus dados. A opção pedagógica de tratar o inventário como um Component do Player, e não como uma cena ou sistema separado, é deliberada: reforça o mesmo princípio de composição ensinado desde a Semana 4 (GameManager) e aplicado em `InteractionComponent`, `HealthComponent` e `SaveComponent` — cada responsabilidade isolada em um Component reutilizável, nunca concentrada no script do Player. A exibição do inventário é tratada como um problema à parte, resolvido no Encontro 2 e no início da próxima aplicação, reutilizando diretamente os Control nodes e o binding de dados fundamentados na Semana 9.

## Recursos do Godot

`ItemData` (Resource + Enum, retomado da Semana 6), `InventoryComponent` (Node customizado), padrão de Component já estabelecido por `InteractionComponent`/`HealthComponent`/`SaveComponent`.

## Comparação com Unity

A Unity resolve o mesmo problema estrutural tipicamente com um `ScriptableObject` para os dados de definição do item — equivalente direto ao `ItemData` do Godot — e um `MonoBehaviour` de inventário (ou um `ScriptableObject` de runtime set, em arquiteturas mais avançadas) responsável por armazenar as instâncias possuídas pelo jogador. O princípio universal é idêntico nas duas engines: dados de definição do item nunca se confundem com o estado de posse, e o inventário nunca duplica os dados que já existem no `ItemData`/`ScriptableObject`. A diferença está mais na convenção de arquitetura do que na engine em si — no Godot, a composição via Component (Node filho) é o caminho natural já estabelecido pelo projeto; na Unity, a mesma separação pode ser resolvida tanto por composição de `MonoBehaviour`s quanto por padrões orientados a eventos com `ScriptableObject`s.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 9, com HUD funcional exibindo vida e um segundo dado de gameplay.
- Lista dos `ItemData` já modelados desde a Semana 6, disponíveis para uso no `InventoryComponent`.
- Cena de exemplo com um `InventoryComponent` básico (adicionar/remover/consultar itens) preparada para demonstração, sem distribuir antes da aula.
- Slides com o comparativo `InventoryComponent` (Godot) × ScriptableObject de inventário (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 9 (HUD funcional sobre CanvasLayer) |
| 20 min | Introdução: os três problemas de todo Inventory System — armazenamento, adição/remoção, exibição |
| 30 min | Demonstração: estruturação guiada de um `InventoryComponent` reutilizando `ItemData` já existente |
| 55 min | Laboratório: cada grupo estrutura seu próprio `InventoryComponent`, conectando-o à coleta já existente (`Chest`/`Pickup`) |
| 15 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do projeto herdado da Semana 9, sem alterar o HUD ou qualquer sistema de gameplay já funcional, introduzindo o `InventoryComponent` como novo Component do Player. O professor demonstra primeiro os três problemas estruturais de qualquer Inventory System de forma isolada, antes de conectar qualquer dado real do projeto. Em seguida, demonstra a estruturação guiada de um `InventoryComponent` simples, capaz de adicionar, remover e consultar `ItemData` já modelados, deixando explícito que o Component armazena apenas referências aos itens, sem duplicar seus dados de definição. Cada grupo replica essa estruturação sobre o próprio projeto, conectando o novo `InventoryComponent` à coleta de itens já existente via `Chest`/`Pickup`, de modo que itens coletados passem a ser armazenados no inventário em vez de simplesmente desaparecerem da cena.

## Desafio

Não há desafio de solução livre neste encontro: a estruturação do `InventoryComponent` é guiada, servindo de base direta à exibição via `InventoryUI` e à ampliação da interação do Encontro 2.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, um `InventoryComponent` funcional que armazena os `ItemData` coletados via `Chest`/`Pickup` já existentes, permitindo adicionar, remover e consultar itens, sem duplicar dados já modelados no `ItemData`.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro (Rubrica 1 — Desenvolvimento Semanal, aplicada de forma contínua). O `InventoryComponent` construído aqui é pré-requisito direto do Code Review do Encontro 2.

## Dificuldades Esperadas

- Duplicar os dados do `ItemData` dentro do próprio `InventoryComponent` (ex.: recriar nome/ícone do item como variáveis novas) em vez de armazenar a referência ao `ItemData` existente — reforçar que o inventário armazena instâncias, não recria dados.
- Colocar a lógica de inventário diretamente no script do Player, em vez de isolá-la em um Component — reforçar o mesmo padrão de composição já usado por `InteractionComponent`/`HealthComponent`/`SaveComponent`.
- Esquecer de remover o item da cena (`Chest`/`Pickup`) ao adicioná-lo ao inventário, resultando em coleta duplicada — reforçar que a coleta é um evento único que atualiza o inventário e remove o objeto do mundo.

---

# Encontro 2

## Objetivos de Aprendizagem

- Retomar o contrato `Interactable` da Semana 5, reconhecendo sua extensão para múltiplos tipos de interação como o mesmo padrão de desacoplamento, aplicado a um novo caso de uso.
- Conectar o Interaction System ampliado ao `InventoryComponent`, suportando coletar, usar e descartar itens.
- Propor e implementar, com solução própria, um novo tipo de interação (empilhar, combinar ou interação com cooldown).
- Participar do Code Review formal (Rubrica 4) sobre os sistemas de inventário e interação.

## Conteúdos

- Retomada do contrato `Interactable` (Semana 5): detecção via `InteractionComponent`/Area3D, resposta via `has_method`/Signals.
- Ampliação do contrato para múltiplos tipos de interação: detecção, priorização (quando mais de um interativo está ao alcance) e resposta diferenciada conforme o tipo.
- Conexão do Interaction System ampliado ao `InventoryComponent`: coletar (adicionar ao inventário), usar (consumir/aplicar efeito de um item) e descartar (remover do inventário e reintroduzir no mundo).
- Desafio: cada grupo expande seu sistema de interação para suportar um novo tipo (empilhar itens, combinar itens, interação com cooldown), com solução própria.
- Code Review (Rubrica 4) dos sistemas de inventário e interação.

## Conceitos Fundamentais

O Encontro 1 resolveu o armazenamento de itens. O Encontro 2 resolve o problema de conectar esse armazenamento à ação do jogador no mundo, sem criar um sistema de comunicação paralelo ao já existente. O contrato `Interactable`, fundamentado na Semana 5 para casos simples (`Door`, `Lever`), já resolve o problema geral de comunicação desacoplada entre o `InteractionComponent` do Player e qualquer objeto do mundo — a ampliação desta semana não substitui esse contrato, apenas o aplica a um cenário com múltiplos tipos de interação simultâneos, exigindo priorização (qual interativo responde quando mais de um está ao alcance) e resposta diferenciada (coletar não é a mesma ação que usar ou descartar). Essa retomada é deliberadamente pedagógica: mostra que um mesmo padrão arquitetural, bem desenhado, escala para novos casos de uso sem precisar ser reescrito — princípio que será cobrado diretamente no Code Review da Rubrica 4, cujo critério de "Reutilização" avalia exatamente se sistemas de módulos anteriores continuam sendo usados, e não silenciosamente substituídos.

## Recursos do Godot

Contrato `Interactable`/Signals (retomados da Semana 5), `InteractionComponent` (retomado da Semana 5), `InventoryComponent` (do Encontro 1), `ItemData` (retomado da Semana 6).

## Comparação com Unity

A Unity resolveria a mesma ampliação mantendo a mesma interface C# já usada para os interativos simples da Semana 5 (por exemplo, `IInteractable`), estendendo seu contrato com um parâmetro de tipo de interação ou com interfaces adicionais específicas (`ICollectible`, `IUsable`, `IDiscardable`), e resolvendo a priorização entre múltiplos objetos detectados tipicamente por distância ou por um `SphereCollider`/`OverlapSphere` equivalente ao Area3D do Godot. O princípio universal é idêntico: a ampliação de um sistema de interação nunca deveria exigir reescrever o contrato existente, apenas estendê-lo — seja via `has_method`/duck typing no Godot, seja via interfaces C# adicionais na Unity.

## Preparação do Professor

- Projeto de cada grupo com `InventoryComponent` funcional do Encontro 1.
- Cena de exemplo com Interaction System ampliado (priorização entre múltiplos interativos, resposta diferenciada para coletar/usar/descartar) preparada para demonstração, sem distribuir antes da aula.
- Roteiro do desafio preparado: cada grupo escolhe entre empilhar itens, combinar itens ou interação com cooldown.
- Ficha de Code Review (Rubrica 4 do Sistema de Avaliação) impressa ou digital, uma por grupo.
- Slides com o comparativo Interaction System ampliado (Godot) × interfaces C# adicionais (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (`InventoryComponent` funcional) |
| 25 min | Demonstração: ampliação guiada do contrato `Interactable` para múltiplos tipos de interação, conectado ao inventário (coletar/usar/descartar) |
| 15 min | Apresentação do desafio: cada grupo escolhe empilhar, combinar ou interação com cooldown |
| 50 min | Laboratório/Desafio: cada grupo implementa a conexão inventário-interação e o novo tipo de interação escolhido |
| 30 min | Code Review formal (Rubrica 4): organização, modularidade, reutilização e comunicação entre sistemas |

## Desenvolvimento

O encontro abre com a demonstração guiada da ampliação do contrato `Interactable` para múltiplos tipos de interação, conectando a coleta já existente ao novo `InventoryComponent` e adicionando as ações de usar e descartar — todas resolvidas pelo mesmo padrão de contrato e Signals já dominado desde a Semana 5. A partir daí, o professor apresenta o desafio: cada grupo escolhe um novo tipo de interação (empilhar, combinar ou cooldown) e propõe a própria solução de implementação, mantendo a comunicação desacoplada já estabelecida. Na última fatia do encontro, o professor conduz o Code Review formal da Rubrica 4 com cada grupo, abrindo os scripts/Orchestrations ao vivo e pedindo que o próprio grupo explique sua lógica, verificando se `ItemData` (Semana 6) e o contrato `Interactable` (Semana 5) seguem sendo reutilizados corretamente, sem duplicação ou substituição silenciosa.

## Desafio

Cada grupo expande seu sistema de interação para suportar um novo tipo (empilhar itens, combinar itens ou interação com cooldown), com solução própria de implementação, mantendo a comunicação desacoplada via contrato `Interactable`. **Entrega: Code Review** (Rubrica 4) dos sistemas de inventário e interação.

## Critérios de Sucesso

Cada grupo possui, ao final da semana, um `InventoryComponent` conectado ao Interaction System ampliado, suportando coletar, usar e descartar itens, além de um novo tipo de interação proposto e implementado com solução própria, com o conjunto submetido a Code Review sem duplicação de lógica entre `Chest`/`Pickup`/`InventoryComponent`.

## Evidências para Avaliação

**Code Review** (Rubrica 4 do Sistema de Avaliação) — organização dos scripts/Orchestrations, nomenclatura, modularidade, reutilização de `ItemData` (Semana 6) e do contrato `Interactable` (Semana 5), comunicação desacoplada entre sistemas e boas práticas gerais do Godot 4.7. Conduzido como diálogo técnico, com o próprio grupo explicando sua lógica ao professor.

O desafio de propor e implementar o novo tipo de interação (empilhar, combinar ou cooldown) é adicionalmente avaliado pela **Rubrica 2 — Desafios Técnicos** (solução proposta, uso correto do Godot, criatividade, organização, funcionamento), já que a Semana 10 consta na lista de aplicação desta rubrica no Sistema de Avaliação, de forma complementar — não sobreposta — ao Code Review da Rubrica 4, que avalia o conjunto (inventário + interação) sob o critério de organização/reutilização.

## Dificuldades Esperadas

- Reescrever o contrato `Interactable` do zero para o novo caso de múltiplos tipos, em vez de estendê-lo — reforçar que a ampliação reaproveita o mesmo `has_method`/Signals já existente, apenas com um parâmetro ou método adicional.
- Resolver a priorização entre múltiplos interativos com lógica ad-hoc dispersa pelo código, em vez de concentrá-la no `InteractionComponent` — reforçar que a decisão de qual interativo responde pertence ao Component, não a cada `Interactable` individualmente.
- Implementar o novo tipo de interação (empilhar/combinar/cooldown) duplicando lógica já existente no `InventoryComponent`, em vez de reutilizá-la — este é exatamente o ponto observado pelo critério "Modularidade" e "Reutilização" do Code Review.

---

# Resultado Esperado da Semana

Ao final da Semana 10, cada grupo possui um `InventoryComponent` funcional armazenando os `ItemData` coletados, uma `InventoryUI` inicial exibindo esses dados, e um Interaction System ampliado que conecta coletar, usar e descartar itens ao inventário, incluindo um novo tipo de interação (empilhar, combinar ou cooldown) proposto e implementado com solução própria. O conjunto foi submetido a Code Review formal (Rubrica 4), verificando organização, modularidade, reutilização de `ItemData` e do contrato `Interactable`, e comunicação desacoplada entre sistemas. A turma domina padrões de Inventory System, relaciona-os a ScriptableObjects de inventário na Unity, e consolidou a prática de ampliar um contrato existente em vez de recriá-lo para cada novo caso de uso.

# Preparação para a Próxima Semana

O `HealthComponent` (Semana 8) e o Interaction System ampliado desta semana são pré-requisitos diretos da Semana 11, que encerra o Módulo 3 (Unidade III) introduzindo NavigationRegion3D/NavigationAgent3D, Behavior Tree e Blackboard via LimboAI para dar autonomia de deslocamento e decisão a um `Enemy`, além de um combate simples (Area3D/RayCast3D chamando `apply_damage` no `HealthComponent` do `Enemy`). A Semana 11 é marcada como encerramento de módulo (🔴), concentrando os instrumentos avaliativos que fecham a Unidade III.

# Referências

- Godot Documentation — Resources: https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html
- Godot Documentation — Nodes and Scene Instances: https://docs.godotengine.org/en/stable/getting_started/step_by_step/nodes_and_scenes.html
- Godot Documentation — Signals: https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — ScriptableObjects: https://docs.unity3d.com/Manual/class-ScriptableObject.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
