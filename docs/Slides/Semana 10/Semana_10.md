---
marp: true
theme: academic-course
paginate: true
header: 'Semana 10 — Inventário e ampliação do Interaction System'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 10

## Inventário e ampliação do Interaction System

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
A Semana 9 encerrou com um HUD funcional sobre CanvasLayer, exibindo vida (HealthComponent) e um segundo dado de gameplay, cada grupo com solução visual e de binding própria.
Até aqui, os itens do jogo existem apenas como ItemData (Resource + Enum, desde a Semana 6) e são coletados via Chest/Pickup, mas não há lugar nenhum onde sejam armazenados, listados ou manipulados — eles simplesmente desaparecem da cena.
Metodologia: Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.
-->

---

## Objetivos da Semana

- Compreender padrões de Inventory System — armazenamento, adição/remoção, exibição — como problema estrutural comum a qualquer engine
- Estruturar um `InventoryComponent` reutilizando diretamente o `ItemData` já modelado na Semana 6, sem duplicar dados de item
- Retomar e ampliar o contrato `Interactable` da Semana 5 para múltiplos tipos de interação
- Conectar o Interaction System ampliado ao inventário (coletar, usar, descartar), propondo com autonomia própria um novo tipo de interação
- Submeter os sistemas de inventário e interação a Code Review formal (Rubrica 4)

<!--
Encontro 1 cobre os três problemas de todo Inventory System e a estruturação guiada do InventoryComponent.
Encontro 2 retoma o contrato Interactable, conecta ao inventário e conduz o Code Review formal da Rubrica 4.
Referência: Godot Docs — Resources, Nodes and Scene Instances, Signals; Unity Manual — ScriptableObject.
-->

---

<!-- _class: chapter -->

## Encontro 1

# InventoryComponent: Armazenar o que já existe

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o projeto da Semana 9 sem alterar o HUD ou qualquer sistema de gameplay já funcional — introduz o InventoryComponent como novo Component do Player.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 9 (HUD funcional sobre CanvasLayer) (15 min)
- Introdução: os três problemas de todo Inventory System (20 min)
- Demonstração: estruturação guiada de um `InventoryComponent` reutilizando `ItemData` já existente (30 min)
- Laboratório: cada grupo estrutura seu próprio `InventoryComponent`, conectando-o à coleta já existente (55 min)
- Feedback e fechamento (15 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — a estruturação do InventoryComponent é guiada, base direta da InventoryUI e da ampliação de interação do Encontro 2.
-->

---

<!-- _class: question -->

# Os itens já existem como `ItemData`. Para onde vão quando o jogador os coleta?

Pense no que acontece hoje, no projeto, quando um `Chest` ou `Pickup` é coletado.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que os itens simplesmente desaparecem da cena — não há nenhum lugar que os armazene, liste ou manipule.
Erro comum: assumir que o ItemData por si só já resolve o problema de posse do jogador.
-->

---

## O Problema: Onde Vive a Posse do Item?

- `ItemData` (Resource + Enum, desde a Semana 6) define nome, ícone e tipo do item — mas não diz quem o possui
- Itens coletados via `Chest`/`Pickup` hoje simplesmente desaparecem da cena
- Falta um lugar que armazene, liste e permita manipular os itens que o jogador possui agora

<!--
Conceito universal: os dados de definição de um item precisam ser separados do estado de posse daquele item por um jogador específico.
Referência: PROJECT_ARCHITECTURE.md, seção de Componentes — ItemData, Chest, Pickup.
-->

---

## Três Problemas de Todo Inventory System

- **Armazenamento** — onde vive a lista de itens que o jogador possui
- **Adição/remoção** — como itens entram e saem dessa lista ao longo do jogo
- **Exibição** — como esse estado se torna visível ao jogador (resolvido no Encontro 2, sobre os princípios de Control node da Semana 9)

<!--
Esses três problemas são estruturais, independentes da engine escolhida.
Reforçar: a exibição é tratada como problema à parte, sem antecipar a InventoryUI ainda neste encontro.
-->

---

## InventoryComponent: Mesmo Padrão de Component

- Novo Component do Player, seguindo o mesmo padrão de composição de `InteractionComponent`, `HealthComponent` e `SaveComponent`
- Armazena referências a instâncias de `ItemData` já modeladas — nunca duplica ou recria seus dados
- Reforça o princípio de composição ensinado desde a Semana 4 (`GameManager`): cada responsabilidade isolada em um Component reutilizável

<!--
Opção pedagógica deliberada: tratar o inventário como Component do Player, não como cena ou sistema separado.
Erro comum: colocar a lógica de inventário diretamente no script do Player, em vez de isolá-la em um Component.
-->

---

<!-- _class: comparison -->

## Armazenamento de Itens no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `ItemData` (Resource) define o item
- `InventoryComponent` (Node filho do Player) armazena as instâncias possuídas

</div>
<div class="col negative">

### Unity

- `ScriptableObject` define o item — equivalente direto ao `ItemData`
- `MonoBehaviour` de inventário (ou `ScriptableObject` de runtime set) armazena as instâncias possuídas

</div>
</div>

<!--
Princípio universal idêntico nas duas engines: dados de definição do item nunca se confundem com o estado de posse.
A diferença está na convenção de arquitetura, não na engine em si — no Godot, composição via Component é o caminho já estabelecido pelo projeto.
-->

---

## Demonstração — InventoryComponent Guiado

O que será construído:

- Um `InventoryComponent` capaz de adicionar, remover e consultar `ItemData` já modelados
- Conexão à coleta já existente via `Chest`/`Pickup`

Por quê: dar a cada grupo a base direta para a `InventoryUI` do Encontro 2, sem duplicar dados de item.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Reforçar: o Component armazena apenas referências aos itens, sem duplicar dados de definição.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o `InventoryComponent` armazenando referências a `ItemData` sem duplicar seus dados.
> Enquadramento: árvore de cena do Player ao lado de uma coleção de recursos.
> Elementos presentes: "Player" com filhos "InteractionComponent", "HealthComponent" e "InventoryComponent"; setas do `InventoryComponent` apontando para instâncias de `ItemData` já existentes (não para cópias).
> Destaque visual: a seta de referência, contrastando com uma alternativa errada (dados de item recriados dentro do `InventoryComponent`) marcada com um X.
> Legenda sugerida: "O InventoryComponent referencia o ItemData — nunca recria seus dados."

<!--
Usar esta imagem logo após a demonstração, antes do laboratório.
-->

---

## Arquitetura — Do Chest/Pickup ao Inventário

- Coleta via `Chest`/`Pickup` passa a notificar o `InventoryComponent`, em vez de apenas remover o item da cena
- O item some do mundo e passa a existir como entrada no inventário — evento único, sem duplicação
- Nenhum sistema de coleta é reescrito: o `InventoryComponent` se conecta ao que já existe

<!--
Diagrama sugerido: Chest/Pickup → (coleta) → InventoryComponent (adiciona ItemData) → remove objeto da cena.
Erro comum: esquecer de remover o item da cena ao adicioná-lo ao inventário, resultando em coleta duplicada.
-->

---

## Laboratório — InventoryComponent Funcional

Cada grupo estrutura, no próprio projeto:

1. Um `InventoryComponent` com métodos de adicionar, remover e consultar `ItemData`
2. Conexão do `InventoryComponent` à coleta já existente via `Chest`/`Pickup`
3. Verificação de que o item é removido da cena ao ser adicionado ao inventário

<!--
Critério de sucesso: InventoryComponent funcional armazenando ItemData coletados, sem duplicar dados já modelados.
-->

---

## Fechamento — Encontro 1

- `InventoryComponent` funcional, armazenando os `ItemData` coletados via `Chest`/`Pickup`
- Adicionar, remover e consultar itens sem duplicar dados de definição
- Nenhuma alteração no HUD ou em outro sistema de gameplay da Semana 9
- Próximo passo: ampliação do contrato `Interactable` e Code Review, no Encontro 2

<!--
Dificuldade esperada: colocar a lógica de inventário no script do Player em vez de isolá-la em um Component — reforçar o padrão já usado por InteractionComponent/HealthComponent/SaveComponent.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Ampliando o Interaction System

<span class="chapter-number">02</span>

<!--
Retoma o contrato Interactable da Semana 5, ampliando-o para múltiplos tipos de interação conectados ao inventário. Encerra com Code Review formal (Rubrica 4).
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (`InventoryComponent` funcional) (15 min)
- Demonstração: ampliação guiada do contrato `Interactable`, conectado ao inventário (25 min)
- Apresentação do desafio: empilhar, combinar ou interação com cooldown (15 min)
- Laboratório/Desafio: conexão inventário-interação e o novo tipo de interação (50 min)
- Code Review formal (Rubrica 4) (30 min)

<!--
Reservar tempo real para o Code Review individual por grupo, abrindo scripts/Orchestrations ao vivo.
-->

---

<!-- _class: question -->

# O contrato `Interactable` já resolveu portas e alavancas. Ele precisa ser reescrito para coletar, usar e descartar itens?

Pense no que já existe desde a Semana 5, antes de propor algo novo.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que o contrato não precisa ser reescrito, apenas estendido para múltiplos tipos de interação.
Erro comum: propor um sistema de comunicação paralelo ao Interactable já existente.
-->

---

## O Problema: Conectar Inventário e Ação no Mundo

- O Encontro 1 resolveu o armazenamento de itens
- Falta conectar esse armazenamento à ação do jogador no mundo — coletar, usar, descartar
- O contrato `Interactable` (Semana 5) já resolve comunicação desacoplada; a ampliação apenas o aplica a múltiplos tipos simultâneos

<!--
Reforçar: nenhum sistema novo de comunicação é criado — apenas uma extensão do que já existe desde a Semana 5.
-->

---

## Retomando o Contrato Interactable

- Fundamentado na Semana 5 para casos simples (`Door`, `Lever`): detecção via `InteractionComponent`/Area3D, resposta via `has_method`/Signals
- Ampliação: múltiplos tipos de interação exigem **priorização** (qual interativo responde quando mais de um está ao alcance)
- Ampliação: resposta **diferenciada** conforme o tipo — coletar não é a mesma ação que usar ou descartar

<!--
Mostrar que um mesmo padrão arquitetural, bem desenhado, escala para novos casos de uso sem precisar ser reescrito.
Este princípio será cobrado diretamente no Code Review (critério "Reutilização").
-->

---

## Conectando ao InventoryComponent

- **Coletar** — adiciona o item ao `InventoryComponent`
- **Usar** — consome ou aplica o efeito de um item já no inventário
- **Descartar** — remove do inventário e reintroduz o item no mundo

<!--
Todas as três ações resolvidas pelo mesmo padrão de contrato e Signals já dominado desde a Semana 5.
-->

---

<!-- _class: comparison -->

## Ampliação de Interação no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Mesmo contrato `Interactable` (`has_method`/duck typing), estendido com tipo de interação
- Priorização entre múltiplos interativos resolvida no `InteractionComponent`

</div>
<div class="col negative">

### Unity

- Mesma interface C# (ex.: `IInteractable`) estendida, ou interfaces adicionais (`ICollectible`, `IUsable`, `IDiscardable`)
- Priorização tipicamente por distância ou `SphereCollider`/`OverlapSphere`, equivalente ao Area3D

</div>
</div>

<!--
Princípio universal idêntico: a ampliação de um sistema de interação nunca deveria exigir reescrever o contrato existente, apenas estendê-lo.
-->

---

## Demonstração — Interação Ampliada e Conectada

O que será construído:

- Contrato `Interactable` ampliado para múltiplos tipos, com priorização entre interativos ao alcance
- Conexão de coletar/usar/descartar ao `InventoryComponent` do Encontro 1

Por quê: fixar a ampliação guiada antes de abrir o desafio de um novo tipo de interação.

<!--
Não estender além do necessário — reservar tempo real para o Desafio e o Code Review.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a priorização entre múltiplos interativos detectados simultaneamente pelo `InteractionComponent`.
> Enquadramento: cena de jogo em planta baixa, Player ao centro.
> Elementos presentes: Player com raio de alcance do `InteractionComponent`, dois interativos dentro do alcance (um `Chest`, um `NPC`), com destaque no interativo priorizado.
> Destaque visual: o interativo priorizado em cor sólida, o não priorizado esmaecido.
> Legenda sugerida: "A decisão de qual interativo responde pertence ao InteractionComponent, não a cada Interactable."

<!--
Usar esta imagem durante a demonstração da ampliação, antes do desafio.
-->

---

## Arquitetura — Contrato Estendido, Não Reescrito

- `ItemData` (Semana 6) e o contrato `Interactable` (Semana 5) continuam sendo os mesmos, apenas reutilizados em um novo cenário
- A priorização entre interativos é responsabilidade do `InteractionComponent`, nunca de cada `Interactable` individualmente
- Nenhuma lógica de coleta/uso/descarte deve duplicar o que já existe no `InventoryComponent`

<!--
Diagrama sugerido: InteractionComponent → (prioriza) → Interactable ampliado → (coletar/usar/descartar) → InventoryComponent.
Erro comum: resolver a priorização com lógica ad-hoc dispersa pelo código, em vez de concentrá-la no InteractionComponent.
-->

---

<!-- _class: exercise -->

# Desafio — Novo Tipo de Interação

Expanda seu sistema de interação para suportar um novo tipo — **empilhar itens**, **combinar itens** ou **interação com cooldown** — mantendo a comunicação desacoplada via contrato `Interactable`.

<div class="objectives">

**Entrega:** Code Review (Rubrica 4) — organização, modularidade, reutilização de `ItemData` e do contrato `Interactable`, comunicação desacoplada entre sistemas.

</div>

<!--
Cada grupo propõe e implementa solução própria. O professor conduz o Code Review formal ao vivo, pedindo que o grupo explique sua lógica.
-->

---

## Boas Práticas — Extensão sem Duplicação

- Estender o contrato `Interactable` existente, nunca reescrevê-lo do zero para um novo caso
- Concentrar a priorização entre interativos no `InteractionComponent`, não em cada `Interactable`
- Reutilizar a lógica já existente no `InventoryComponent` ao implementar o novo tipo de interação, sem duplicá-la

<!--
Estes são exatamente os pontos observados pelos critérios "Modularidade" e "Reutilização" do Code Review.
-->

---

## Code Review — Rubrica 4

- Organização dos scripts/Orchestrations e nomenclatura
- Modularidade e reutilização de `ItemData` (Semana 6) e do contrato `Interactable` (Semana 5)
- Comunicação desacoplada entre sistemas
- Conduzido como diálogo técnico: o próprio grupo explica sua lógica ao professor

<!--
Abrir os scripts/Orchestrations ao vivo com cada grupo, verificando se sistemas anteriores continuam sendo usados, não silenciosamente substituídos.
-->

---

## Fechamento — Encontro 2

- `InventoryComponent` conectado ao Interaction System ampliado — coletar, usar, descartar
- Novo tipo de interação (empilhar, combinar ou cooldown) proposto e implementado com solução própria
- Sistemas submetidos a Code Review formal (Rubrica 4), sem duplicação de lógica entre `Chest`/`Pickup`/`InventoryComponent`

<!--
Dificuldade esperada: implementar o novo tipo de interação duplicando lógica já existente no InventoryComponent, em vez de reutilizá-la.
-->

---

## Resultado Esperado da Semana

- `InventoryComponent` funcional armazenando os `ItemData` coletados, com `InventoryUI` inicial exibindo esses dados
- Interaction System ampliado conectando coletar, usar e descartar itens ao inventário
- Novo tipo de interação (empilhar, combinar ou cooldown) proposto e implementado com solução própria
- Conjunto submetido a Code Review formal (Rubrica 4)

<!--
Este resultado corresponde à linha InventoryComponent/InventoryUI/Ampliação da Interação do roadmap (PROJECT_ARCHITECTURE.md).
-->

---

## Checklist da Semana

- [ ] `InventoryComponent` armazenando `ItemData` coletados via `Chest`/`Pickup`, sem duplicar dados de definição
- [ ] Contrato `Interactable` ampliado para múltiplos tipos, com priorização no `InteractionComponent`
- [ ] Coletar, usar e descartar conectados ao `InventoryComponent`
- [ ] Novo tipo de interação (empilhar, combinar ou cooldown) implementado com solução própria
- [ ] Code Review (Rubrica 4) concluído, sem duplicação de lógica entre sistemas

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 11.
-->

---

## Próximos Passos — Semana 11

O `HealthComponent` (Semana 8) e o Interaction System ampliado desta semana são pré-requisitos diretos da Semana 11, que encerra o Módulo 3 (Unidade III) introduzindo NavigationRegion3D/NavigationAgent3D, Behavior Tree e Blackboard via LimboAI para dar autonomia a um `Enemy`, além de um combate simples (Area3D/RayCast3D chamando `apply_damage` no `HealthComponent` do `Enemy`). A Semana 11 encerra a Unidade III, concentrando os instrumentos avaliativos que fecham o módulo.

Leitura recomendada: Godot Docs — Resources, Nodes and Scene Instances, Signals; Unity Manual (consulta comparativa) — ScriptableObject.

<!--
Referências completas: ver Plano de Aula Semana 10. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
