---
marp: true
theme: academic-course
paginate: true
header: 'Semana 8 — HealthComponent, AnimationTree, BlendSpace e AnimationPlayer'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 8

## HealthComponent, AnimationTree, BlendSpace e AnimationPlayer

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
A Semana 7 encerrou a Unidade II com GameManager, SaveManager, contrato Interactable, Signals, ItemData/Enum e SaveData/Checkpoint operando juntos em um fluxo jogável único, com progresso persistido entre sessões.
A Semana 8 abre a Unidade III mudando a pergunta da disciplina: não mais "como construir cada sistema", mas "como resolver problemas com autonomia crescente" sobre o que já existe.
Metodologia: Challenge Based Learning — professor apresenta o problema, os grupos propõem a solução. Autonomia média.
-->

---

## Objetivos da Semana

- Compreender vida/dano como problema universal resolvido por composição (Component), não por herança
- Construir `HealthComponent` (vida atual/máxima, `apply_damage`, sinal `died`), reutilizando o padrão de Component das Semanas 5–7
- Fundamentar AnimationTree/AnimationNodeStateMachine (transição) e BlendSpace1D/2D + faixas do AnimationPlayer (combinação/sobreposição)
- Propor e implementar, com autonomia crescente, uma animação contextual conectada a um evento real de gameplay

<!--
Encontro 1 cobre HealthComponent e a State Machine básica de locomoção (idle, andar, correr).
Encontro 2 cobre BlendSpace1D/2D, faixas do AnimationPlayer e o desafio de animação contextual.
Referência: Godot Docs — Animation; Unity Manual — Animator Controller, Blend Trees.
-->

---

<!-- _class: chapter -->

## Encontro 1

# HealthComponent e State Machine de Locomoção

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o projeto da Semana 7 sem alterar GameManager, SaveManager, contrato Interactable ou ItemData/Enum — adiciona duas camadas novas e independentes entre si: estado de vida (HealthComponent) e transição de animação (AnimationTree).
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 7 (integração final do Módulo 2, Code Review e Playtest) (15 min)
- Introdução: mudança de metodologia para Challenge Based Learning; o problema do estado de vida/dano compartilhado (20 min)
- Demonstração: construção do `HealthComponent` aplicado ao Player (30 min)
- Demonstração: AnimationTree/AnimationNodeStateMachine e construção guiada da State Machine (30 min)
- Laboratório: cada grupo aplica `HealthComponent` e ajusta a State Machine ao próprio conjunto de animações (25 min)
- Feedback e fechamento (15 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — HealthComponent e State Machine básica são construção guiada, base direta do desafio de animação contextual do Encontro 2.
-->

---

<!-- _class: question -->

# Onde deve viver o estado de vida de um personagem, se Player e Enemy (Semana 11) precisam do mesmo comportamento?

Pense no que `InteractionComponent` e `SaveComponent` já resolveram desde a Semana 5.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que duplicar vida/dano no script do Player e, depois, no do Enemy, recria o mesmo problema que Component já resolveu antes.
Erro comum: propor uma classe base comum entre Player e Enemy em vez de composição via Component.
-->

---

## O Problema: Estado de Vida Compartilhado, Sem Duplicação

- Vida e dano são um exemplo canônico de estado que precisa ser compartilhado por múltiplos tipos de personagem (Player e, na Semana 11, Enemy)
- A disciplina já ensina, desde a Semana 5, que a resposta do Godot é composição via Component — um Node filho com responsabilidade isolada
- O `HealthComponent` aplica o mesmo princípio: qualquer Scene que o possua como filho ganha vida, dano e um sinal de morte

<!--
Conceito universal, não específico do Godot: toda engine com múltiplos tipos de personagem enfrenta o mesmo problema de onde colocar o estado compartilhado.
Referência: PROJECT_ARCHITECTURE.md, seção de Componentes — HealthComponent.
-->

---

## `HealthComponent`: Vida, Dano e Morte como Component

- Node customizado, seguindo o mesmo padrão de `InteractionComponent` (Semana 5) e `SaveComponent` (Semana 7)
- Propriedades: vida atual e vida máxima
- Método público `apply_damage(quantidade)`; sinal `died` emitido quando a vida chega a zero

<!--
Reforçar: HealthComponent não conhece quem é seu dono (Player ou Enemy) — apenas expõe vida, dano e o sinal died.
Erro comum: implementar vida/dano diretamente no script do Player em vez de isolar em um HealthComponent.
-->

---

<!-- _class: comparison -->

## Estado de Vida/Dano no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `HealthComponent`: Node customizado, seguindo a convenção de Component já usada no projeto desde a Semana 5

</div>
<div class="col negative">

### Unity

- Sem equivalente formal nativo
- Padrão comum: MonoBehaviour próprio anexado ao GameObject, mesma ideia de composição via Component

</div>
</div>

<!--
O conceito universal — estado de vida isolado em um Component reutilizável — é o mesmo nas duas engines; nenhuma delas resolve isso via herança de uma classe base de personagem.
-->

---

## Demonstração — Construção do `HealthComponent`

O que será construído:

- `HealthComponent` (Node) com vida atual/máxima, `apply_damage` e sinal `died`
- Aplicação do `HealthComponent` como filho do Player

Por quê: evita lógica de vida/dano duplicada entre Player e Enemy — qualquer Scene que precisar de vida conversa apenas com seu próprio `HealthComponent`.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial da semana, quando disponível.
Reforçar: HealthComponent emite died; quem decide o que acontece na morte (game over, respawn) é responsabilidade de quem escuta o sinal, não do Component.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o HealthComponent como Node filho reutilizável.
> Enquadramento: duas árvores de cena lado a lado.
> Elementos presentes: à esquerda, "Player" com filho "HealthComponent"; à direita, "Enemy" (Semana 11) com o mesmo filho "HealthComponent", destacado com a mesma cor nas duas árvores.
> Destaque visual: o HealthComponent idêntico nas duas árvores, reforçando reutilização sem duplicação.
> Legenda sugerida: "HealthComponent: o mesmo Component, reutilizado por Player e Enemy, sem herança compartilhada."

<!--
Usar esta imagem logo após a demonstração do HealthComponent, antes de avançar para AnimationTree.
-->

---

## Fundamentando AnimationTree: Quem Decide Qual Animação Toca

- Toda engine com um personagem animado enfrenta o mesmo problema: animações isoladas (idle, andar, correr) precisam ser organizadas em um sistema que decide qual toca e como transiciona
- AnimationPlayer guarda as animações; AnimationTree decide qual delas toca e quando, separado da lógica de gameplay
- AnimationNodeStateMachine organiza essa decisão como estados e transições, cada uma com uma condição

<!--
Erro comum: confundir o papel do AnimationPlayer (guarda as animações) com o do AnimationTree (decide qual delas toca e quando).
Referência: Godot Docs — Animation, AnimationTree.
-->

---

## AnimationNodeStateMachine: Estados e Transições

- Cada estado da State Machine é uma animação (idle, andar, correr)
- Cada transição depende de uma condição real (ex.: velocidade, input), nunca de uma transição automática sem critério
- Construção guiada de uma State Machine básica de locomoção para o Player

<!--
Erro comum: configurar transições sem condição clara (sempre transicionar, nunca transicionar) — reforçar que cada transição depende de uma variável real de gameplay.
-->

---

<!-- _class: comparison -->

## Transição de Animações no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- AnimationTree (Node na própria Scene) + AnimationNodeStateMachine
- Integrado à árvore de cena, seguindo o modelo de composição da disciplina

</div>
<div class="col negative">

### Unity

- Animator Controller (asset `.controller`), vinculado a um Animator Component
- Estados e transições configurados fora da hierarquia de GameObjects

</div>
</div>

<!--
O conceito universal — animação organizada em uma máquina de estados separada da lógica de gameplay — é o mesmo nas duas engines; a diferença está em asset externo (Unity) versus Node integrado à Scene (Godot).
-->

---

## Arquitetura — HealthComponent e AnimationTree como Camadas Independentes

- `HealthComponent` e AnimationTree resolvem problemas diferentes e não se conhecem diretamente
- Nenhum dos dois altera GameManager, SaveManager, contrato Interactable ou ItemData/Enum das semanas anteriores
- A conexão entre os dois (animação reagindo a dano) só aparece no desafio do Encontro 2

<!--
Diagrama sugerido: Player → HealthComponent (vida/dano/died) e Player → AnimationTree (AnimationNodeStateMachine: idle/andar/correr), como duas ramificações paralelas do mesmo Node Player.
Reforçar: por ora, as duas camadas são independentes — a integração é o objetivo do Encontro 2.
-->

---

## Laboratório — `HealthComponent` e State Machine de Locomoção

Cada grupo replica, no próprio projeto:

1. `HealthComponent` (Node) com vida atual/máxima, `apply_damage` e sinal `died`
2. Aplicação do `HealthComponent` como filho do Player
3. AnimationTree com AnimationNodeStateMachine para idle, andar e correr
4. Transições condicionadas a uma variável real de movimento (velocidade ou input)

<!--
Erro comum: transições da State Machine sem condição real, resultando em animações travadas ou trocando aleatoriamente.
-->

---

## Boas Práticas — Component e State Machine

- `HealthComponent` enxuto: apenas vida, dano e o sinal `died`, sem lógica de game over ou respawn
- Nomear estados da State Machine de forma clara e consistente com as animações do AnimationPlayer
- Um único `HealthComponent` ativo por personagem, assim como um único `SaveComponent` por projeto
- Testar cada transição isoladamente antes de avançar para a próxima

<!--
Esses hábitos evitam retrabalho na integração do desafio do Encontro 2 e sustentam a Rubrica 4 (Code Review).
-->

---

## Fechamento — Encontro 1

- `HealthComponent` funcional aplicado ao Player (vida, `apply_damage`, sinal `died`)
- State Machine básica de locomoção via AnimationTree, alternando corretamente entre idle, andar e correr
- GameManager, SaveManager, contrato Interactable, Signals e ItemData/Enum sem nenhuma alteração
- Próximo passo: BlendSpace, faixas do AnimationPlayer e o desafio de animação contextual, no Encontro 2

<!--
Dificuldade esperada: confundir o papel do AnimationPlayer com o do AnimationTree — reforçar que são camadas complementares, não concorrentes.
-->

---

<!-- _class: chapter -->

## Encontro 2

# BlendSpace, Faixas do AnimationPlayer e Desafio de Animação Contextual

<span class="chapter-number">02</span>

<!--
Primeiro desafio da Unidade III sob Challenge Based Learning: o professor apresenta o problema (animação contextual conectada a um evento real), os grupos decidem a solução.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (`HealthComponent`, State Machine básica) (15 min)
- Demonstração: fundamentação e configuração de um BlendSpace1D/2D direcional (25 min)
- Demonstração: configuração de uma animação pontual via faixa do AnimationPlayer (20 min)
- Apresentação do desafio: escolha entre BlendSpace ou animação pontual conforme o problema proposto pelo grupo (15 min)
- Laboratório/Desafio: cada grupo propõe e implementa sua animação contextual própria (45 min)
- Feedback e fechamento da semana (15 min)

<!--
Reservar tempo real para o professor circular entre os grupos como facilitador do problema, não como fornecedor da solução.
-->

---

<!-- _class: question -->

# Uma reação a dano e uma corrida direcional são o mesmo tipo de problema de animação?

Pense na diferença entre algo que varia continuamente e algo que acontece uma única vez.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que a State Machine do Encontro 1 resolve transição entre estados discretos, mas não resolve mistura contínua nem eventos pontuais sobrepostos.
-->

---

## O Problema: Misturar Continuamente Versus Sobrepor Pontualmente

- A State Machine resolve transição entre estados discretos (idle → andar → correr)
- Nem toda animação é discreta: locomoção direcional varia continuamente (velocidade e direção)
- Nem toda animação é contínua: reagir a dano, atacar ou responder a uma interação são eventos pontuais, sobrepostos à locomoção de base

<!--
Reconhecer qual mecanismo resolve qual problema é o conceito central do encontro — e é exatamente a decisão que o desafio exige de cada grupo.
-->

---

## BlendSpace1D/2D: Interpolação Multidimensional

- BlendSpace1D interpola ao longo de um único eixo contínuo (ex.: parado até correndo)
- BlendSpace2D interpola em duas dimensões simultaneamente (ex.: direção e velocidade)
- Evita a explosão combinatória de criar uma animação para cada combinação possível de direção e intensidade

<!--
Referência: Godot Docs — Animation, BlendSpace1D/2D dentro do AnimationTree.
-->

---

## Faixas do AnimationPlayer: Animações Pontuais Sobrepostas

- Mecanismo para animações discretas sobrepostas à locomoção de base (reação a dano, gesto de interação, ataque)
- Não substitui a State Machine nem o BlendSpace — soma-se a eles sem quebrar a locomoção
- Critério de escolha: o movimento varia continuamente (BlendSpace) ou é um evento único (faixa do AnimationPlayer)?

<!--
Erro comum: escolher BlendSpace para um caso pontual e discreto (um único gesto de ataque) em vez de faixa do AnimationPlayer, ou o inverso.
Erro comum: quebrar a transição da State Machine ao sobrepor a animação pontual — a faixa deve se sobrepor à base, não substituí-la.
-->

---

<!-- _class: comparison -->

## Mistura e Sobreposição de Animações no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- BlendSpace1D/2D: pontos configurados explicitamente dentro do AnimationTree
- Faixas do AnimationPlayer para sobreposição pontual simples

</div>
<div class="col negative">

### Unity

- Blend Tree (1D ou 2D, Simple Directional/Freeform) dentro do Animator Controller, por parâmetros (floats)
- Animation Layers com Avatar Masks para sobreposição parcial do esqueleto

</div>
</div>

<!--
A lógica de interpolação multidimensional é a mesma nas duas engines; a Unity organiza a configuração como asset próprio (Blend Tree) referenciado pelo Animator Controller, enquanto o Godot configura os pontos diretamente no AnimationTree.
Não transformar isso em aula de Unity — o objetivo é a lógica universal, não a sintaxe da Unity.
-->

---

## Demonstração — BlendSpace Direcional e Faixa Pontual

O que será construído:

- Um BlendSpace1D/2D direcional simples sobre o Player
- Uma animação pontual via faixa do AnimationPlayer (reação a dano, gesto de ataque ou interação)

Por quê: dar a cada grupo os dois mecanismos disponíveis antes de decidir qual deles resolve o desafio proposto.

<!--
Não estender as demonstrações além do necessário para o desafio — o tempo do encontro é do laboratório/desafio.
-->

---

> **Imagem sugerida**
>
> Objetivo: contrastar BlendSpace (contínuo) e faixa do AnimationPlayer (pontual).
> Enquadramento: diagrama de duas colunas.
> Elementos presentes: à esquerda, "BlendSpace2D" com eixos de velocidade e direção e um ponto se movendo entre animações; à direita, "Faixa do AnimationPlayer" com uma linha do tempo e um evento pontual sobreposto à animação base.
> Destaque visual: o ponto contínuo no BlendSpace versus o marcador único na faixa pontual.
> Legenda sugerida: "BlendSpace mistura continuamente; faixas do AnimationPlayer sobrepõem eventos pontuais à locomoção de base."

<!--
Usar esta imagem antes da apresentação do desafio, para fixar o critério de escolha.
-->

---

## Arquitetura — Onde a Animação Contextual se Conecta ao Vertical Slice

- A animação contextual deve se conectar a um evento real já existente: sinal `died`/dano do `HealthComponent`, ou contrato `Interactable`
- Nenhuma condição artificial ou tecla de teste isolada — sempre um evento real de gameplay
- A State Machine de locomoção do Encontro 1 permanece intacta; a animação contextual se sobrepõe a ela, não a substitui

<!--
Diagrama sugerido: HealthComponent.died/apply_damage → animação de reação (faixa do AnimationPlayer) — ou — InteractionComponent/Interactable → animação de interação, ambos sobrepostos à State Machine de locomoção.
Erro comum: conectar a animação contextual a uma condição artificial em vez de um evento real já existente no projeto.
-->

---

<!-- _class: exercise -->

# Desafio — Animação Contextual Própria

Proponha e implemente uma animação contextual conectada a um evento real do projeto (dano via `HealthComponent`, interação via contrato `Interactable`, ou ataque), escolhendo entre BlendSpace ou animação pontual conforme a natureza do problema.

<div class="objectives">

**Entrega:** animação contextual funcional, conectada a um evento real de gameplay, sem quebrar a State Machine de locomoção do Encontro 1.

</div>

<!--
O professor circula entre os grupos como facilitador do problema, não como fornecedor da solução — característico da Challenge Based Learning que abre a Unidade III.
Este é o Desafio Técnico avaliado pela Rubrica 2 do Sistema de Avaliação.
-->

---

## Boas Práticas — Animação Contextual

- Perguntar sempre "esse movimento varia continuamente ou é um evento único?" antes de escolher o mecanismo
- Justificar a escolha entre BlendSpace e animação pontual pela natureza do problema, não por preferência arbitrária
- Testar a animação contextual sem quebrar a State Machine de locomoção já construída
- Conectar sempre a um evento real do Vertical Slice, nunca a um teste isolado

<!--
Essas justificativas são exatamente o que a Rubrica 2 (Desafio Técnico) avalia neste encontro.
-->

---

## Fechamento — Encontro 2

- Animação contextual própria, conectada a um evento real (`HealthComponent` ou contrato `Interactable`)
- Escolha entre BlendSpace e animação pontual justificada pela natureza do problema
- State Machine de locomoção do Encontro 1 preservada, sem retrabalho
- Primeiro desafio da Unidade III sob Challenge Based Learning concluído

<!--
Dificuldade esperada: escolher o mecanismo errado (BlendSpace para um evento pontual, ou faixa para um movimento contínuo) — usar a pergunta de calibração para corrigir durante o laboratório.
-->

---

## Resultado Esperado da Semana

- `HealthComponent` funcional aplicado ao Player (vida, `apply_damage`, sinal `died`)
- State Machine básica de locomoção via AnimationTree (idle, andar, correr)
- Animação contextual própria — BlendSpace direcional ou animação pontual — conectada a um evento real de gameplay
- Turma domina AnimationTree, AnimationNodeStateMachine, BlendSpace1D/2D e faixas do AnimationPlayer como camadas complementares, relacionando-as ao Animator Controller/Blend Tree da Unity

<!--
Este resultado corresponde às linhas HealthComponent, AnimationTree e BlendSpace1D/2D + AnimationPlayer do roadmap (PROJECT_ARCHITECTURE.md).
-->

---

## Checklist da Semana

- [ ] `HealthComponent` (Node) com vida atual/máxima, `apply_damage` e sinal `died`
- [ ] State Machine via AnimationTree alternando corretamente entre idle, andar e correr
- [ ] BlendSpace1D/2D ou faixa do AnimationPlayer configurados na demonstração
- [ ] Animação contextual própria conectada a um evento real (`HealthComponent` ou `Interactable`)
- [ ] State Machine de locomoção preservada, sem retrabalho

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 9.
-->

---

## Próximos Passos — Semana 9

O `HealthComponent` construído nesta semana é consumido diretamente pelo HUD da Semana 9, que passa a exibir em tempo real dados de gameplay já existentes — vida, itens, progresso — via Control nodes e CanvasLayer. A State Machine e as animações contextuais não são retomadas diretamente na Semana 9, mas permanecem no projeto como parte do Vertical Slice, prontas para reaparecer na Semana 11, quando o `HealthComponent` é reutilizado pelo Enemy em um sistema de combate simples.

Leitura recomendada: Godot Docs — Animation; Unity Manual (consulta comparativa) — Animator Controller, Blend Trees.

<!--
Referências completas: ver Plano de Aula Semana 8. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
