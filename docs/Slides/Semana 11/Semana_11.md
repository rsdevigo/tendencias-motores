---
marp: true
theme: academic-course
paginate: true
header: 'Semana 11 — Navigation, Behavior Trees (LimboAI), Blackboards e Combate Simples'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 11

## Navigation, Behavior Trees (LimboAI), Blackboards e Combate Simples

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Encerramento de Módulo 🔴** — Playtest coletivo e Showcase

</div>

<!--
A Semana 10 encerrou com um InventoryComponent funcional conectado a um Interaction System ampliado, capaz de coletar, usar e descartar itens, além de um novo tipo de interação proposto por cada grupo.
Até aqui, o Vertical Slice não possui nenhum agente que se mova ou decida de forma autônoma no mundo — todo movimento no projeto é do próprio jogador.
Metodologia: Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média. Esta semana encerra a Unidade III.
-->

---

## Objetivos da Semana

- Compreender Navigation (`NavigationRegion3D`/`NavigationAgent3D`) como base universal de deslocamento autônomo de agentes, independente de engine
- Compreender Behavior Tree e Blackboard como estrutura de decisão e memória compartilhada de um agente não-jogador, via addon LimboAI
- Implementar um combate simples que reutiliza o `HealthComponent` já existente, sem duplicar lógica entre `Player` e `Enemy`
- Propor e implementar, com solução própria, um comportamento autônomo para o `Enemy` do próprio projeto
- Consolidar e apresentar o Vertical Slice jogável do Módulo 3 em Playtest coletivo e Showcase

<!--
Encontro 1 resolve "como" o Enemy se move (Navigation). Encontro 2 resolve "o que" ele decide fazer com esse deslocamento (Behavior Tree/Blackboard) e fecha com combate simples, Playtest e Showcase.
Referência: Godot Docs — Navigation, Physics (Area3D, RayCast3D); LimboAI (github.com/limbonaut/limboai); Unity Manual — NavMesh.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Navigation: Ensinar um Agente a se Deslocar

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o nível já existente do Vertical Slice sem alterar nenhum sistema de gameplay funcional da Semana 10 — introduz a camada de navegação como pré-requisito do Enemy que será construído no Encontro 2.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 10 (Interaction System ampliado + inventário) (15 min)
- Introdução: por que um agente não-jogador precisa de um sistema dedicado de deslocamento (20 min)
- Demonstração: bake guiado de `NavigationRegion3D` e configuração de um `NavigationAgent3D` (30 min)
- Laboratório: cada grupo faz o bake da navegação no próprio nível e movimenta um agente de teste (55 min)
- Feedback e fechamento (15 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — a configuração de NavigationRegion3D/NavigationAgent3D é guiada, base direta da Behavior Tree e do combate simples do Encontro 2.
-->

---

<!-- _class: question -->

# O `Player` usa `move_and_slide` com input do teclado. Como o `Enemy` se move sem teclado nenhum?

Pense no que muda quando o "input" passa a ser uma decisão da própria engine.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que um agente não-jogador precisa calcular a própria rota, não apenas reagir a um evento de input.
Erro comum: assumir que basta mover o Enemy em linha reta até o Player.
-->

---

## O Problema: Deslocamento sem Input Direto

- Todo agente não-jogador que precisa se mover enfrenta o mesmo problema estrutural, em qualquer engine
- Calcular uma rota sobre uma superfície navegável e segui-la evitando obstáculos
- Essa lógica de baixo nível não pode ser reescrita a cada novo tipo de agente

<!--
Conceito universal: separar "como se mover" de "o que decidir" — mesmo princípio de responsabilidade única reforçado desde os Components da Semana 4 em diante.
Referência: PROJECT_ARCHITECTURE.md, seção de Componentes — NavigationRegion3D, Enemy.
-->

---

## `NavigationRegion3D` e `NavigationAgent3D`

- `NavigationRegion3D` — a área navegável, calculada previamente (bake) sobre a geometria do nível
- `NavigationAgent3D` — componente de deslocamento: dado um ponto-alvo, calcula e segue a rota dentro dessa região
- Deliberadamente introduzido antes de qualquer decisão de IA: primeiro o agente se move de A a B, depois — no Encontro 2 — aprende a decidir para onde ir

<!--
NavigationServer é quem resolve o cálculo de rota por trás do NavigationAgent3D — o agente delega, não reimplementa pathfinding.
Erro comum: confundir NavigationAgent3D com move_and_slide do Player, tentando aplicar lógica de input direto ao agente autônomo.
-->

---

<!-- _class: comparison -->

## Navegação no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `NavigationRegion3D` — malha navegável, bake no editor sobre a geometria do nível
- `NavigationAgent3D` — calcula e segue rota até um ponto-alvo

</div>
<div class="col negative">

### Unity

- NavMesh — malha navegável, gerada por bake (historicamente via NavMesh Baking / AI Navigation)
- `NavMeshAgent` — calcula e segue rota até um destino

</div>
</div>

<!--
Princípio universal idêntico: a malha navegável é pré-calculada sobre a geometria estática do nível, e o agente delega a esse sistema o cálculo de rota.
A diferença está no fluxo de configuração, não em qualquer diferença conceitual relevante.
-->

---

## Demonstração — Bake e Movimentação Guiados

O que será construído:

- Um `NavigationRegion3D` calculado sobre a geometria existente do nível
- Um `NavigationAgent3D`, em cena de teste, movendo-se até um ponto-alvo fixo

Por quê: dar a cada grupo a base direta para o `Enemy` do Encontro 2, sem qualquer lógica de decisão ainda.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Demonstrar primeiro o problema isolado (um cubo simples que precisa ir de um ponto a outro), antes de tocar no nível real do projeto.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a malha de navegação calculada sobre a geometria do nível e a rota seguida por um agente de teste.
> Enquadramento: vista superior do nível do Vertical Slice, malha de navegação sobreposta em destaque.
> Elementos presentes: `NavigationRegion3D` (malha translúcida sobre o chão navegável), um agente de teste (cubo simples) com uma linha pontilhada indicando a rota até um ponto-alvo.
> Destaque visual: contraste entre a área navegável (colorida) e obstáculos fora da malha (cinza).
> Legenda sugerida: "O NavigationAgent3D segue a rota calculada pelo NavigationServer sobre a malha do NavigationRegion3D."

<!--
Usar esta imagem durante a demonstração do bake, antes do laboratório.
-->

---

## Laboratório — Navegação Funcional

Cada grupo, no próprio nível:

1. Faz o bake de um `NavigationRegion3D` sobre a geometria existente
2. Configura um `NavigationAgent3D` em uma cena de agente de teste
3. Movimenta esse agente até um ponto-alvo fixo, sem colidir com obstáculos

<!--
Critério de sucesso: NavigationRegion3D corretamente calculado e agente de teste se deslocando autonomamente até o ponto-alvo.
Dificuldade esperada: malha mal calculada (buracos, áreas inacessíveis) por geometria ainda incompleta — reforçar checagem visual da malha antes de prosseguir.
Dificuldade esperada: agente "tremendo" ou preso perto do ponto-alvo — reforçar o ajuste do raio de tolerância do NavigationAgent3D.
-->

---

## Fechamento — Encontro 1

- `NavigationRegion3D` calculado sobre o nível de cada grupo
- Agente de teste deslocando-se autonomamente até um ponto-alvo, sem colidir com obstáculos
- Nenhuma alteração nos sistemas de gameplay já funcionais da Semana 10
- Próximo passo: Behavior Tree, Blackboard e combate simples, no Encontro 2

<!--
A malha de navegação configurada aqui é pré-requisito direto do Enemy construído no Encontro 2.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Behavior Tree, Blackboard e Combate Simples

<span class="chapter-number">02</span>

<!--
Retoma a navegação do Encontro 1, somando decisão (Behavior Tree/Blackboard via LimboAI) e um combate simples que reutiliza o HealthComponent da Semana 8. Encerra a Unidade III com Playtest coletivo e Showcase.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (navegação funcional do agente de teste) (15 min)
- Demonstração: Behavior Tree/Blackboard (LimboAI) — patrulha/perseguição — e combate simples (30 min)
- Apresentação do desafio: comportamento autônomo adicional do `Enemy` (15 min)
- Laboratório/Desafio: Behavior Tree, combate simples e comportamento escolhido (45 min)
- Playtest coletivo e Showcase — encerramento do Módulo 3 (30 min)

<!--
Reservar tempo real para o Playtest coletivo e o Showcase — são os instrumentos de encerramento da Unidade III, não devem ser comprimidos.
-->

---

## Montando o `Enemy` — Mesmo Rig, Outra Skin

- `Enemy` (CharacterBody3D) reutiliza o mesmo modelo do Kenney Mini Characters já usado pelo Player desde a Semana 8
- Skin diferente, mesmo `AnimationPlayer` e mesmas animações (idle, walking, running) — nenhum asset novo é importado
- Reforça o mesmo princípio de reutilização do `HealthComponent`: um pacote, dois personagens

<!--
Se o pacote Mini Characters do grupo só tiver uma skin, uma alternativa simples é aplicar um Material Override de cor diferente sobre o mesmo modelo — o objetivo é distinguir visualmente Player e Enemy, não a variedade de assets.
-->

---

<!-- _class: question -->

# O agente já sabe se mover até um ponto. Quem decide qual ponto?

Pense na diferença entre "como se mover" (Encontro 1) e "o que fazer" (agora).

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que falta uma camada de decisão sobre a navegação já funcional.
Erro comum: tentar resolver decisão e movimentação no mesmo script, sem separar responsabilidades.
-->

---

## O Problema: Decidir, Não Apenas Mover

- O Encontro 1 resolveu "como" o `Enemy` se move
- Falta resolver "o que" ele decide fazer com esse deslocamento — patrulhar, perseguir, atacar
- Essa decisão não deve criar um sistema de movimentação paralelo ao `NavigationAgent3D` já configurado

<!--
Reforçar: a árvore decide, o NavigationAgent3D executa o deslocamento — não o contrário.
-->

---

## Behavior Tree e Blackboard (LimboAI)

- **Behavior Tree** — estrutura de decisão hierárquica: sequências (passos em ordem), seletores (alternativas até uma funcionar), folhas (ações/condições)
- **Blackboard** — memória compartilhada entre os nós da árvore (ex.: última posição conhecida do `Player`)
- Nenhum dos dois é nativo do Godot — resolvidos pelo addon LimboAI

<!--
A ausência de solução nativa não significa ausência de padrão universal — apenas que a comunidade, não o núcleo da engine, mantém a implementação de referência.
Referência: LimboAI — github.com/limbonaut/limboai.
-->

---

<!-- _class: comparison -->

## Decisão Autônoma no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- LimboAI (addon, não nativo) — `BTPlayer`, Blackboard
- Nós de sequência, seletor e folha; memória compartilhada no Blackboard
- Tasks customizadas (`BTAction`/`BTCondition`) exigem GDScript — fora do alcance do Orchestrator

</div>
<div class="col negative">

### Unity

- Behavior Designer ou NodeCanvas (assets de terceiros, não nativos)
- Mesma lógica de nós; memória compartilhada por variáveis do asset ou `ScriptableObject` de estado

</div>
</div>

<!--
Princípio universal idêntico nas duas engines: nenhuma delas resolve Behavior Tree nativamente, ambas dependem de soluções de terceiros com filosofia semelhante.
-->

---

## Demonstração — Patrulha, Perseguição e Combate

O que será construído:

- Behavior Tree simples de patrulha (deslocamento entre pontos via `NavigationAgent3D`) e perseguição (mudança de alvo ao detectar o `Player`) — tasks em GDScript, exigência do LimboAI
- Combate simples: `Area3D`/`RayCast3D` do `Player` chamando `apply_damage` no `HealthComponent` do `Enemy`, via Orchestrator ou GDScript

Por quê: fixar o padrão guiado antes de abrir o desafio do comportamento autônomo adicional.

<!--
O HealthComponent é o mesmo Component fundamentado na Semana 8 — nenhuma lógica de vida/dano é duplicada, apenas aplicada a uma nova origem (Enemy) e a uma nova origem de dano (Area3D/RayCast3D do Player).
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a Behavior Tree do `Enemy` decidindo entre patrulha e perseguição, usando o Blackboard como memória compartilhada.
> Enquadramento: diagrama de árvore, seletor no topo com dois ramos (Patrulhar / Perseguir).
> Elementos presentes: nó seletor no topo; ramo "Patrulhar" com sequência de pontos; ramo "Perseguir" lendo a posição do `Player` a partir do Blackboard; folha final acionando o `NavigationAgent3D`.
> Destaque visual: o ramo ativo no momento (Perseguir) em cor sólida, o ramo inativo (Patrulhar) esmaecido.
> Legenda sugerida: "A Behavior Tree decide; o NavigationAgent3D, já configurado no Encontro 1, executa o deslocamento."

<!--
Usar esta imagem durante a demonstração da Behavior Tree, antes do desafio.
-->

---

## Arquitetura — Decisão, Deslocamento e Combate

- Behavior Tree/Blackboard (decisão) → `NavigationAgent3D` (deslocamento, Encontro 1) → `Enemy` se move
- `Area3D`/`RayCast3D` do `Player` → `apply_damage` → `HealthComponent` do `Enemy` (mesmo Component da Semana 8)
- Nenhum sistema anterior é reescrito: cada camada reutiliza a anterior

<!--
Diagrama sugerido: Player → (Area3D/RayCast3D) → apply_damage → HealthComponent(Enemy). Em paralelo: Behavior Tree/Blackboard → NavigationAgent3D → Enemy.
Erro comum: duplicar lógica de vida/dano no Enemy em vez de reutilizar o HealthComponent já existente desde a Semana 8.
-->

---

<!-- _class: exercise -->

# Desafio — Comportamento Autônomo do `Enemy`

Proponha e implemente um comportamento autônomo adicional para o `Enemy` do seu projeto — **patrulha**, **alerta**, **fuga** ou **interação com o jogador** — com liberdade de solução dentro da estrutura de Behavior Tree/Blackboard já fundamentada.

<div class="objectives">

**Entrega:** Vertical Slice jogável (encerramento do Módulo 3) — Playtest coletivo (Rubrica 5) e Showcase (Rubrica 6).

</div>

<!--
Cada grupo propõe e implementa solução própria. Reforçar: o objetivo pedagógico é patrulha/perseguição básicas, não um sistema de IA avançado — fora do escopo da disciplina.
-->

---

## Boas Práticas — Camadas Separadas

- A Behavior Tree decide; o `NavigationAgent3D` executa o deslocamento — nunca recalcular posição manualmente dentro da árvore
- O `HealthComponent` é o mesmo para `Player` e `Enemy` — nunca duplicar lógica de vida/dano
- Manter a Behavior Tree simples: patrulha/perseguição básicas resolvem o escopo do combate simples do projeto

<!--
Estes são exatamente os pontos observados no Playtest e no Showcase de encerramento do Módulo 3.
-->

---

## Playtest Coletivo e Showcase — Rubricas 5 e 6

- **Playtest** (Rubrica 5) — experiência efetiva de jogo, funcionamento, usabilidade e clareza para quem joga o Vertical Slice de cada grupo
- **Showcase** (Rubrica 6) — apresentação do projeto e capacidade de justificar decisões de arquitetura diante da turma
- Encerramento formal da Unidade III (Módulo 3 — Resolver Problemas)

<!--
Mesmo instrumento de Showcase aplicado na Semana 3 — reforçar a familiaridade da turma com o formato.
A Semana 17 usa a mesma Rubrica 6, mas como instrumento distinto (Apresentação Técnica Final, não Showcase) — não citar como "mesmo instrumento".
Grupos jogam os Vertical Slices uns dos outros durante o Playtest.
-->

---

## Fechamento — Encontro 2

- Behavior Tree/Blackboard (LimboAI) decidindo entre patrulha e perseguição, reutilizando o `NavigationAgent3D` do Encontro 1
- Combate simples funcional, reutilizando o `HealthComponent` da Semana 8 sem duplicação
- Comportamento autônomo adicional proposto e implementado com solução própria
- Vertical Slice avaliado em Playtest coletivo e apresentado em Showcase

<!--
Dificuldade esperada: reimplementar deslocamento dentro da própria Behavior Tree em vez de delegar ao NavigationAgent3D já configurado.
-->

---

## Resultado Esperado da Semana

- `Enemy` deslocando-se autonomamente por um `NavigationRegion3D`
- Comportamento decidido via Behavior Tree/Blackboard (LimboAI), incluindo um comportamento adicional proposto com solução própria
- Combate simples trocando dano entre `Player` e `Enemy`, reutilizando o `HealthComponent` sem duplicação de lógica
- Vertical Slice jogável completo — animação, HUD, inventário, interação, IA e combate — avaliado em Playtest e apresentado em Showcase

<!--
Este resultado corresponde à linha NavigationRegion3D/Enemy/Behavior Tree/Combate simples do roadmap (PROJECT_ARCHITECTURE.md) e encerra a Unidade III.
-->

---

## Checklist da Semana

- [ ] `NavigationRegion3D` calculado sobre o nível, sem áreas inacessíveis
- [ ] `Enemy` deslocando-se via `NavigationAgent3D`
- [ ] Behavior Tree/Blackboard (LimboAI) decidindo entre patrulha e perseguição
- [ ] Combate simples (`Area3D`/`RayCast3D` → `apply_damage`) reutilizando o `HealthComponent` sem duplicação
- [ ] Comportamento autônomo adicional implementado com solução própria
- [ ] Playtest coletivo e Showcase (Rubricas 5 e 6) concluídos

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 12.
-->

---

## Próximos Passos — Semana 12

O Vertical Slice jogável consolidado nesta semana é a base do Módulo 4 (Unidade IV — Produzir como um Pequeno Estúdio), que inicia na Semana 12 com o refinamento de Materials, Material Overrides e Foliage (`MultiMeshInstance3D`) — nenhum sistema novo de gameplay é introduzido; o foco passa a ser polimento técnico e produção em escala de estúdio, com autonomia alta e o professor atuando como diretor técnico.

Leitura recomendada: Godot Docs — Navigation, Physics (Area3D, RayCast3D); LimboAI (github.com/limbonaut/limboai); Unity Manual (consulta comparativa) — NavMesh.

<!--
Referências completas: ver Plano de Aula Semana 11. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
