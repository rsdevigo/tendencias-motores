# Semana 8 — HealthComponent, AnimationTree, BlendSpace e AnimationPlayer

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11) | **Metodologia:** Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.

## Introdução da Semana

A Semana 7 encerrou a Unidade II com um Vertical Slice em que `GameManager`, `SaveManager`, contrato `Interactable`, Signals, `ItemData`/Enum e `SaveData`/`Checkpoint` operam juntos em um fluxo jogável único, com progresso persistido entre sessões. A Semana 8 abre a Unidade III mudando a pergunta da disciplina: não mais "como construir cada sistema", mas "como resolver problemas com autonomia crescente" sobre o que já existe. A metodologia muda de Studio Based Learning para Challenge Based Learning — o professor apresenta o problema, os grupos propõem a solução. A semana resolve dois problemas complementares: onde vive o estado de vida/dano de um personagem (`HealthComponent`, seguindo o mesmo padrão de Component já estabelecido por `InteractionComponent`/`SaveComponent`) e como uma engine resolve a transição e a combinação de animações (AnimationTree, AnimationNodeStateMachine, BlendSpace1D/2D, faixas do AnimationPlayer).

## Objetivos Gerais

- Compreender o gerenciamento de estado de vida/dano como problema universal de qualquer engine, resolvido por composição (Component), não por herança.
- Construir `HealthComponent` (vida atual/máxima, `apply_damage`, sinal `died`), reutilizando o padrão de Component das Semanas 5–7.
- Fundamentar AnimationTree/AnimationNodeStateMachine como sistema de transição de estados de animação, e BlendSpace1D/2D + faixas do AnimationPlayer como sistema de combinação/sobreposição de animações.
- Propor e implementar, com autonomia crescente, uma animação contextual própria conectada a um evento real de gameplay.

## Resultados Esperados

Ao final da semana, cada grupo possui um `HealthComponent` funcional aplicado ao Player, uma State Machine básica de locomoção (idle, andar, correr) via AnimationTree, e uma animação contextual própria — escolhida entre BlendSpace ou animação pontual do AnimationPlayer — conectada a um evento real do projeto (dano, interação ou ataque).

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar por que vida/dano é modelado como Component reutilizável, não como lógica exclusiva do Player.
- Construir `HealthComponent` com vida atual/máxima, método `apply_damage` e sinal `died`.
- Fundamentar AnimationTree e AnimationNodeStateMachine como sistema de transição de estados de animação.
- Construir uma State Machine básica de locomoção (idle, andar, correr) para o Player.

## Conteúdos

- O problema de onde armazenar e expor o estado de vida/dano de um personagem sem duplicar lógica entre Player e Enemy.
- `HealthComponent`: vida atual/máxima, `apply_damage(quantidade)`, sinal `died`, seguindo o mesmo padrão de Component (Node customizado) já usado por `InteractionComponent` e `SaveComponent`.
- AnimationTree como camada que decide qual animação toca e como a transição entre elas ocorre, separada da lógica de gameplay.
- AnimationNodeStateMachine: estados, transições e condições de transição.
- Construção de uma State Machine básica: idle, andar, correr.

## Conceitos Fundamentais

Vida e dano são um exemplo canônico de estado que precisa ser compartilhado por múltiplos tipos de personagem (Player e, na Semana 11, Enemy) sem duplicação. A disciplina já ensinou, desde a Semana 5, que a resposta do Godot para isso é composição via Component — um Node filho com responsabilidade isolada, referenciado por quem precisa dele. O `HealthComponent` aplica esse mesmo princípio: qualquer Scene que o possua como filho ganha vida, dano e um sinal de morte, sem herdar de uma classe base comum a Player e Enemy. Em paralelo, toda engine com um personagem animado enfrenta o mesmo problema estrutural: animações isoladas (idle, andar, correr) precisam ser organizadas em um sistema que decide qual delas toca a cada instante e como uma transiciona suavemente para outra. O AnimationTree resolve isso com uma máquina de estados explícita (AnimationNodeStateMachine), na qual cada estado é uma animação e cada transição tem uma condição — o mesmo problema que a Unity resolve com o Animator Controller.

## Recursos do Godot

`HealthComponent` (Node customizado, implementado via Orchestrator ou GDScript), AnimationTree, AnimationNodeStateMachine.

## Comparação com Unity

A Unity resolve o mesmo problema de transição de animações com o Animator Controller, um asset visual próprio (`.controller`) com estados e transições configurados fora da hierarquia de GameObjects, geralmente vinculado a um Animator Component sobre o personagem. O Godot integra o AnimationTree como um Node dentro da própria Scene, seguindo o mesmo modelo de composição usado em todo o resto da disciplina, em vez de um asset externo referenciado por um Component. Para o `HealthComponent`, a Unity não tem um equivalente formal nativo — o padrão comum também é um MonoBehaviour próprio anexado ao GameObject, replicando a mesma ideia de composição via Component que o Godot já formaliza como convenção do projeto desde a Semana 5. O conceito universal — estado de vida isolado em um Component reutilizável, e animação organizada em uma máquina de estados separada da lógica de gameplay — é o mesmo nas duas engines.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 7, com `GameManager`, `SaveManager`, contrato `Interactable`, Signals, `ItemData`/Enum e `SaveData`/`Checkpoint` já integrados.
- Script/Orchestration de referência de `HealthComponent` (vida atual/máxima, `apply_damage`, sinal `died`) já preparado para demonstração, sem distribuir antes da aula — o professor decide se demonstra via Orchestrator ou GDScript, mantendo a mesma opção já oferecida desde a Semana 5.
- Animações de idle, andar e correr já disponíveis no asset do Player (ou placeholder equivalente) para a construção da State Machine.
- Slides com o comparativo AnimationTree/AnimationNodeStateMachine (Godot) × Animator Controller (Unity).
- Projeto de teste com o AnimationPlayer do Player já configurado com ao menos as três animações de locomoção.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 7 (integração final do Módulo 2, Code Review e Playtest) |
| 20 min | Introdução: mudança de metodologia para Challenge Based Learning; o problema do estado de vida/dano compartilhado |
| 30 min | Demonstração: construção do `HealthComponent` (vida, `apply_damage`, sinal `died`) aplicado ao Player |
| 30 min | Demonstração: fundamentação de AnimationTree/AnimationNodeStateMachine e construção guiada da State Machine (idle, andar, correr) |
| 25 min | Laboratório: cada grupo aplica `HealthComponent` ao próprio Player e ajusta a State Machine ao seu conjunto de animações |
| 15 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do projeto herdado da Semana 7 sem alterar nenhum sistema do Módulo 2, adicionando duas camadas novas e independentes entre si: estado de vida (`HealthComponent`) e transição de animação (AnimationTree). O professor demonstra primeiro a construção do `HealthComponent` como Node filho do Player, via Orchestrator ou GDScript, seguindo exatamente o padrão de Component já estabelecido — vida atual/máxima como propriedades, `apply_damage` como método público, `died` como sinal emitido quando a vida chega a zero. Em seguida, demonstra a fundamentação do AnimationTree: como um AnimationNodeStateMachine organiza estados de animação e transições entre eles, aplicando isso à construção guiada de uma State Machine básica de locomoção para o Player. Cada grupo replica ambas as construções sobre seu próprio projeto, adaptando a State Machine ao conjunto de animações já disponível.

## Desafio

Não há desafio de solução livre neste encontro: a construção de `HealthComponent` e da State Machine básica é guiada, servindo de base direta ao desafio de animação contextual do Encontro 2.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, um `HealthComponent` funcional aplicado ao Player (vida, `apply_damage`, sinal `died`) e uma State Machine básica via AnimationTree alternando corretamente entre idle, andar e correr conforme o movimento do personagem.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro (Rubrica 1 — Desenvolvimento Semanal, aplicada de forma contínua). O `HealthComponent` e a State Machine construídos aqui são pré-requisito direto do Desafio Técnico avaliado no Encontro 2 (Rubrica 2).

## Dificuldades Esperadas

- Implementar vida/dano diretamente no script/Orchestration do Player em vez de isolar em um `HealthComponent` — reforçar o princípio de composição via Component, central desde a Semana 5.
- Confundir o papel do AnimationPlayer (guarda as animações) com o do AnimationTree (decide qual delas toca e quando) — reforçar que são camadas complementares, não concorrentes.
- Configurar transições da State Machine sem condição clara (ex.: sempre transicionar, nunca transicionar) — reforçar que cada transição depende de uma variável real de gameplay (velocidade, input).

---

# Encontro 2

## Objetivos de Aprendizagem

- Fundamentar BlendSpace1D/2D como sistema de interpolação multidimensional de animações.
- Diferenciar o uso de BlendSpace de faixas do AnimationPlayer para animações pontuais sobrepostas.
- Propor e implementar, com autonomia própria, uma animação contextual conectada a um evento real de gameplay.

## Conteúdos

- BlendSpace1D/2D: interpolação entre múltiplas animações a partir de um ou dois eixos contínuos (ex.: velocidade e direção).
- Faixas (tracks) do AnimationPlayer como mecanismo de animações pontuais sobrepostas à locomoção (ex.: reação a dano, gesto de interação).
- Critério de escolha entre BlendSpace e animação pontual conforme a natureza do problema (contínuo e direcional versus discreto e pontual).
- Desafio: animação contextual própria de cada grupo, conectada a um evento real já existente no projeto (dano via `HealthComponent`, interação via contrato `Interactable`, ou ataque).

## Conceitos Fundamentais

O Encontro 1 resolveu a transição entre estados discretos de animação (idle → andar → correr). O Encontro 2 resolve um problema diferente: como misturar continuamente múltiplas animações a partir de uma variável contínua, como a intensidade e a direção do movimento. O BlendSpace1D interpola ao longo de um único eixo (ex.: parado até correndo); o BlendSpace2D interpola em duas dimensões simultaneamente (ex.: direção e velocidade), o que permite uma locomoção direcional suave sem a explosão combinatória de criar uma animação para cada combinação possível. Em paralelo, nem toda animação é contínua — reagir a um dano, executar um ataque ou responder a uma interação são eventos pontuais e discretos, resolvidos por faixas do AnimationPlayer sobrepostas à locomoção de base, não por uma State Machine ou BlendSpace. Reconhecer qual dos dois mecanismos resolve qual problema é, em si, o conceito central do encontro — e é exatamente a decisão que o desafio exige de cada grupo.

## Recursos do Godot

BlendSpace1D/2D, faixas do AnimationPlayer, `HealthComponent` (retomado do Encontro 1), contrato `Interactable` (retomado da Semana 5).

## Comparação com Unity

A Unity resolve o equivalente ao BlendSpace com Blend Trees dentro do próprio Animator Controller, configuradas por parâmetros (floats) que controlam os eixos de mistura — 1D Blend Tree para um eixo, 2D Blend Tree (Simple Directional ou Freeform) para dois. O BlendSpace1D/2D do Godot exige a configuração explícita de cada ponto no espaço de eixos dentro do AnimationTree, enquanto a Blend Tree da Unity organiza essa configuração como um asset próprio referenciado pelo Animator Controller — a lógica de interpolação multidimensional, porém, é a mesma nas duas engines. Para animações pontuais sobrepostas, a Unity usa Animation Layers com Avatar Masks (camadas que afetam apenas parte do esqueleto) ou eventos de animação diretos; o Godot resolve o caso mais simples — uma animação pontual completa sobreposta à base — com faixas do próprio AnimationPlayer, sem exigir a configuração de camadas e máscaras salvo quando o caso realmente pedir sobreposição parcial do esqueleto.

## Preparação do Professor

- Projeto de cada grupo com `HealthComponent` e State Machine básica do Encontro 1 já funcionais.
- Animações adicionais de locomoção direcional (ou placeholder) disponíveis para a demonstração de BlendSpace.
- Ao menos uma animação pontual (reação a dano, gesto de ataque ou interação) disponível no asset do Player para a demonstração de faixas do AnimationPlayer.
- Roteiro do desafio preparado: cada grupo escolhe entre BlendSpace ou animação pontual conforme o problema que decidir resolver (reação a dano, interação, ataque).
- Slides com o comparativo BlendSpace1D/2D (Godot) × Blend Tree (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (`HealthComponent`, State Machine básica) |
| 25 min | Demonstração: fundamentação e configuração de um BlendSpace1D/2D direcional |
| 20 min | Demonstração: configuração de uma animação pontual via faixa do AnimationPlayer |
| 15 min | Apresentação do desafio: escolha entre BlendSpace ou animação pontual conforme o problema proposto pelo grupo |
| 45 min | Laboratório/Desafio: cada grupo propõe e implementa sua animação contextual própria |
| 15 min | Feedback e fechamento da semana |

## Desenvolvimento

O encontro abre com a fundamentação e configuração guiada de um BlendSpace direcional simples sobre o Player, seguida da configuração de uma animação pontual via faixa do AnimationPlayer — ambas as demonstrações usando exemplos pequenos, sem se estender além do necessário para o desafio. A partir daí, o professor apresenta o problema central do encontro: cada grupo deve propor e implementar uma animação contextual própria, conectada a um evento real já existente no projeto — reação a dano (via sinal do `HealthComponent`), resposta a uma interação (via contrato `Interactable`) ou um gesto de ataque —, decidindo autonomamente se o caso pede um BlendSpace ou uma animação pontual sobreposta. O professor circula entre os grupos como facilitador do problema, não como fornecedor da solução, característico da Challenge Based Learning que abre a Unidade III.

## Desafio

Cada grupo propõe e implementa uma animação contextual própria (reação a dano, interação ou ataque), escolhendo entre BlendSpace ou animação pontual do AnimationPlayer conforme a natureza do problema escolhido, e conectando essa animação a um evento real já existente no projeto (`HealthComponent` ou contrato `Interactable`). **Entrega: animação contextual funcional, conectada a um evento real de gameplay.**

## Critérios de Sucesso

Cada grupo possui, ao final da semana, uma animação contextual funcional e conectada a um evento real do projeto, com a escolha entre BlendSpace e animação pontual justificada pela natureza do problema resolvido — sem quebrar a State Machine de locomoção construída no Encontro 1.

## Evidências para Avaliação

**Desafio Técnico** (Rubrica 2 do Sistema de Avaliação) — capacidade de propor solução própria dentro de um espaço de escolha real (BlendSpace ou animação pontual), justificando a decisão pela natureza do problema; conexão correta da animação a um evento real de gameplay (`HealthComponent` ou contrato `Interactable`), sem lógica duplicada ou retrabalho da State Machine do Encontro 1.

## Dificuldades Esperadas

- Escolher BlendSpace para um caso pontual e discreto (ex.: um único gesto de ataque) em vez de faixa do AnimationPlayer, ou o inverso — usar a pergunta "esse movimento varia continuamente ou é um evento único?" para calibrar a escolha.
- Conectar a animação contextual a uma condição artificial em vez de um evento real já existente no projeto (sinal `died`/dano do `HealthComponent`, contrato `Interactable`) — reforçar que todo exercício pertence ao Vertical Slice, nunca a um teste isolado.
- Quebrar a transição da State Machine de locomoção ao sobrepor a animação pontual — reforçar que a faixa do AnimationPlayer deve se sobrepor à base, não substituí-la.

---

# Resultado Esperado da Semana

Ao final da Semana 8, cada grupo possui um `HealthComponent` funcional aplicado ao Player (vida, `apply_damage`, sinal `died`), uma State Machine básica de locomoção via AnimationTree (idle, andar, correr) e uma animação contextual própria — BlendSpace direcional ou animação pontual do AnimationPlayer — conectada a um evento real de gameplay. A turma domina o papel de AnimationTree, AnimationNodeStateMachine, BlendSpace1D/2D e faixas do AnimationPlayer como camadas complementares de um mesmo sistema de animação, relaciona esse conjunto ao Animator Controller/Blend Tree da Unity, e vivenciou o primeiro desafio da Unidade III sob Challenge Based Learning.

# Preparação para a Próxima Semana

O `HealthComponent` construído nesta semana é consumido diretamente pelo HUD da Semana 9, que passa a exibir em tempo real dados de gameplay já existentes — vida, itens, progresso — via Control nodes e CanvasLayer. A State Machine e as animações contextuais não são retomadas diretamente na Semana 9, mas permanecem no projeto como parte do Vertical Slice, prontas para reaparecer na Semana 11, quando o `HealthComponent` é reutilizado pelo Enemy em um sistema de combate simples.

# Referências

- Godot Documentation — Animation: https://docs.godotengine.org/en/stable/tutorials/animation/index.html
- Godot Documentation — Nodes and Scene Instances: https://docs.godotengine.org/en/stable/getting_started/step_by_step/nodes_and_scenes.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — Animator Controller: https://docs.unity3d.com/Manual/class-AnimatorController.html
- Unity Manual (consulta comparativa) — Blend Trees: https://docs.unity3d.com/Manual/class-BlendTree.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
