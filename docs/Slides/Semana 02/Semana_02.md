---
marp: true
theme: academic-course
paginate: true
header: 'Semana 2 — CharacterBody3D, movimentação e Input Map'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 2

## CharacterBody3D, movimentação e Input Map

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade I — Aprender a Ferramenta** (Semanas 1–3)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
Retomar a Scene da Semana 1 (NivelTeste > Chao, LuzPrincipal) já aberta antes de começar. Confirmar que todos os projetos abrem sem erro.
Metodologia da semana: Scaffolded Learning, autonomia muito baixa — professor demonstra, aluno replica.
-->

---

## Objetivos da Semana

- Compreender por que uma engine desacopla a intenção do jogador da ação no mundo
- Configurar um CharacterBody3D controlável usando `move_and_slide`
- Configurar um Input Map e conectar Actions à movimentação do Player

<!--
Encontro 1 cobre física de locomoção (Player parado, mas sólido). Encontro 2 cobre Input Map e conecta tudo, produzindo o Player efetivamente controlável.
Resultado esperado ao final: Player com Input Map próprio e uma Action adicional não demonstrada em aula.
-->

---

<!-- _class: chapter -->

## Encontro 1

# CharacterBody3D e move_and_slide

<span class="chapter-number">01</span>

<!--
Encontro 100% guiado. O Player criado aqui ainda não se move — isso é intencional, reforçar para não gerar ansiedade na turma.
-->

---

## Agenda do Encontro 1

- Revisão da Scene da Semana 1 (15 min)
- Introdução: por que engines desacoplam intenção de ação (20 min)
- Demonstração: CharacterBody3D + CollisionShape3D via Orchestrator (35 min)
- Laboratório: cada estudante monta seu Player (45 min)
- Desafio: ajustar forma de colisão (20 min)
- Feedback e fechamento (10 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
-->

---

<!-- _class: question -->

# Como um personagem sabe que não deve atravessar uma parede?

Pense em qualquer jogo que vocês já jogaram, de qualquer engine.

<!--
Discussão rápida, 2–3 minutos. Objetivo: fazer a turma nomear "colisão" e "deslizamento em superfícies" sem depender de sintaxe de nenhuma engine específica.
Erro comum: respostas vagas ("a física resolve") — insistir até surgir o problema concreto de deslizar em obstáculos e rampas.
-->

---

## O Problema Universal da Locomoção

Todo personagem controlável — jogador ou inimigo — precisa resolver o mesmo problema físico:

- Mover-se no mundo sem atravessar paredes
- Deslizar suavemente ao encostar em obstáculos
- Responder corretamente a rampas e desníveis

Reimplementar isso do zero a cada projeto seria caro e repetitivo.

<!--
Conceito universal, não específico do Godot. Reforçar o hábito da disciplina: sempre perguntar "que problema universal isso resolve?" antes de "como se usa no Godot?".
Referência: Godot Documentation — Physics — CharacterBody3D.
-->

---

## CharacterBody3D e move_and_slide

- **CharacterBody3D** — Node especializado em corpos controlados por código
- Diferente do RigidBody3D, que é simulado livremente pela física
- `move_and_slide()` — resolve deslocamento e colisão em uma única chamada, a cada frame de física
- Ao final deste encontro, o Player existe e é sólido — mas ainda não se move sozinho

<!--
Reforçar: move_and_slide só produz movimento quando recebe uma velocity. Essa velocity vem do Input Map, só configurado no Encontro 2.
Documentação: Godot Docs — Physics — CharacterBody3D.
-->

---

<!-- _class: comparison -->

## Locomoção no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- CharacterBody3D já pronto
- `move_and_slide()` resolve tudo em uma chamada
- Solução de locomoção embutida no próprio Node

</div>
<div class="col negative">

### Unity

- CharacterController **ou** Rigidbody + script próprio
- Sem um único componente "pronto" equivalente
- Mais decisões de arquitetura recaem sobre o time

</div>
</div>

<!--
O Godot entrega a solução de locomoção pronta dentro do Node; na Unity, a equipe compõe a solução a partir de peças mais genéricas.
Não ensinar Unity em profundidade aqui — apenas contrastar arquitetura.
-->

---

## Demonstração — Montagem do Player

O que será construído:

- Node `Player` (CharacterBody3D), filho de `NivelTeste`
- `CollisionShape3D` — forma física de colisão
- `Malha` (MeshInstance3D) — representação visual
- Orchestration `player.os` chamando `move_and_slide` no PhysicsProcess

Por quê: primeiro personagem controlável do semestre, base direta do Input Map no Encontro 2.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 2, Encontro 1). O slide só estrutura a demonstração ao vivo.
Reforçar a separação entre CollisionShape3D (física) e MeshInstance3D (visual) como Nodes distintos.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a árvore de cena com `Player` (CharacterBody3D) já contendo `CollisionShape3D` e `Malha`, ao lado do Viewport 3D com a cápsula posicionada sobre o `Chao`.
> Enquadramento: captura de tela dividida — Scene dock à esquerda, Viewport 3D à direita.
> Elementos presentes: hierarquia `Player` > `CollisionShape3D`, `Malha`, cápsula alinhada ao chão no Viewport.
> Destaque visual: contorno colorido separando forma de colisão (vermelho, semi-transparente) da malha visual (azul).
> Legenda sugerida: "Player montado: colisão e malha visual como Nodes separados, alinhados sobre o chão."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — Montagem do Player

Cada estudante replica, no próprio projeto:

1. `Player` (CharacterBody3D) como filho de `NivelTeste`
2. `CollisionShape3D` com uma Shape atribuída (ex.: `CapsuleShape3D`)
3. `Malha` (MeshInstance3D) com uma Mesh atribuída, alinhada à colisão
4. Orchestration `player.os` chamando `move_and_slide` no PhysicsProcess

<!--
Erro comum: CollisionShape3D sem Shape atribuída — o Godot alerta com ícone de aviso no painel Scene.
Erro comum: Player afundando ou flutuando sobre o Chao — reajustar posição ou tamanho da forma de colisão.
-->

---

## Boas Práticas — Colisão e Composição

- Separar sempre `CollisionShape3D` (física) de `MeshInstance3D` (visual), mesmo quando parecem redundantes
- Nomear o Node raiz como `Player`, nunca deixar o nome padrão `CharacterBody3D`
- Confirmar visualmente o alinhamento entre colisão e malha antes de avançar
- Associar a Orchestration ao Node correto (`Player`, não `NivelTeste`)

<!--
Erros de alinhamento aqui geram bugs de movimento difíceis de depurar no Encontro 2, quando o Player passa a se mover de fato.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 1

Ajuste a forma ou o tamanho da `CollisionShape3D` do próprio Player — por exemplo, cápsula versus caixa, ou uma escala diferente da demonstrada.

<div class="objectives">

Justifique brevemente a escolha em relação ao personagem que pretende usar no Vertical Slice. Não há solução única.

</div>

<!--
Circular pela sala pedindo justificativas curtas em voz alta. Sem instrumento formal de avaliação nesta semana.
-->

---

## Fechamento — Encontro 1

- Player (CharacterBody3D) montado, sólido, alinhado ao `Chao`
- `move_and_slide` já chamado a cada frame de física, ainda sem velocity
- Próximo passo: conectar o Input Map à movimentação, no Encontro 2

<!--
Dificuldade esperada: Malha e forma de colisão desalinhadas — reforçar comparação visual no Viewport antes de encerrar.
Sem instrumento formal de avaliação nesta semana. Observado informalmente no Checkpoint da Semana 3.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Input Map e InputEvent

<span class="chapter-number">02</span>

<!--
Encontro 2 depende diretamente do Player montado no Encontro 1. Confirmar que todos abrem a Scene sem erros antes de prosseguir.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (Player parado) (15 min)
- Introdução: por que desacoplar dispositivo físico de ação lógica (25 min)
- Demonstração: Input Map + conexão com move_and_slide (35 min)
- Laboratório: cada estudante configura o próprio Input Map (45 min)
- Desafio: Action adicional (correr, agachar ou pular) (20 min)
- Feedback e fechamento (15 min)

<!--
Retomar rapidamente o estado do Player do Encontro 1 antes de avançar — é pré-requisito direto.
-->

---

<!-- _class: question -->

# Se o código do jogo checasse diretamente a tecla W, o que aconteceria ao tentar suportar um gamepad?

Pense antes de abrir o Project Settings.

<!--
Discussão em dupla ou com a turma toda, 2–3 minutos. Objetivo: levar a turma a concluir que remapeamento e múltiplos dispositivos exigem uma camada de abstração entre tecla e ação.
-->

---

## Input Map — Camada de Desacoplamento

Se o código lesse diretamente "tecla W pressionada", qualquer remapeamento exigiria reescrever a lógica do jogo inteira.

- O jogador aperta uma tecla física
- A engine traduz isso em uma **Action** nomeada (ex.: "mover para frente")
- O código de gameplay consome a Action — nunca a tecla em si

<!--
Segundo conceito universal do encontro, após "locomoção física" no Encontro 1. Sempre explicar o conceito universal antes da implementação no Godot.
Documentação: Godot Docs — Inputs.
-->

---

## Input Map e InputEvent no Godot

- **Input Map** — configurado uma vez em Project Settings, associa teclas a Actions
- **InputEvent** — evento gerado a cada interação do jogador, traduzido automaticamente para a Action
- A Orchestration só pergunta: "a Action `move_forward` está pressionada agora?"
- Actions desta semana: `move_forward`, `move_back`, `move_left`, `move_right`

<!--
Reforçar convenção de nomes por intenção do jogador, nunca pela tecla física (ex.: move_forward, não tecla_w).
-->

---

<!-- _class: comparison -->

## Input Map no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Input Map único e global do projeto
- Actions configuradas em um só lugar
- Mais simples para o caso de um único jogador

</div>
<div class="col negative">

### Unity

- Input System com Action Maps
- Componente Player Input conecta Actions ao código
- Mais granularidade para múltiplos esquemas/dispositivos

</div>
</div>

<!--
O Godot concentra tudo em um Input Map global, mais simples de configurar; a Unity oferece mais granularidade nativa (ex.: dois jogadores locais com Action Maps distintos), ao custo de mais camadas de configuração.
-->

---

<!-- _class: diagram -->

## Diagrama Sugerido — Fluxo do Input

> **Diagrama sugerido**
>
> Fluxo linear: `Tecla física (W)` → `InputEvent` → `Action (move_forward)` → `Orchestration lê a Action` → `velocity atribuída` → `move_and_slide()`.
> Objetivo: visualizar as camadas entre o dispositivo físico e o movimento efetivo do Player.
> Legenda sugerida: "Da tecla física ao movimento: cada seta é uma camada de desacoplamento."

<!--
Pode ser desenhado ao vivo no quadro antes de abrir o Project Settings, retomando o diagrama do Tutorial Semana 2 Encontro 2, Parte 1.
-->

---

## Demonstração — Input Map e Conexão

O que será construído:

- Quatro Actions no Input Map: `move_forward`, `move_back`, `move_left`, `move_right`
- Leitura das Actions dentro da Orchestration `player.os`
- Combinação em um vetor de direção, aplicado à `velocity` do Player
- `move_and_slide` chamado após a `velocity` ser atribuída

Por quê: transforma o Player sólido do Encontro 1 em um Player efetivamente controlável.

<!--
Não detalhar passo a passo aqui — o Tutorial (Semana 2, Encontro 2) cobre isso em detalhe.
Reforçar: a ordem importa — velocity precisa ser atribuída antes de move_and_slide.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a aba Input Map do Project Settings, com as quatro Actions de movimentação já configuradas.
> Enquadramento: captura de tela da janela Project Settings, aba Input Map.
> Elementos presentes: lista de Actions (`move_forward`, `move_back`, `move_left`, `move_right`), teclas associadas a cada uma.
> Destaque visual: o botão "Add" usado para criar uma nova Action.
> Legenda sugerida: "Input Map do projeto com as Actions de movimentação configuradas."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — Input Map e Movimentação

Cada estudante configura, no próprio projeto:

1. Quatro Actions no Input Map (`move_forward`, `move_back`, `move_left`, `move_right`)
2. Leitura das Actions na Orchestration `player.os`
3. Vetor de direção combinado e aplicado à `velocity`
4. Teste com F6, movendo o Player nas quatro direções

<!--
Erro comum: direção invertida — checar orientação do Node Player antes de depurar a lógica de input.
Erro comum: Player não se move — confirmar que velocity é atribuída antes de move_and_slide, não depois.
-->

---

## Boas Práticas — Nomenclatura de Input

- Nomear Actions por intenção do jogador (`move_forward`), nunca pela tecla física
- Centralizar toda leitura de input do Player dentro da própria Orchestration
- Testar cada Action isoladamente antes de combinar as quatro em um vetor
- Evitar espalhar chamadas de Input Map por múltiplos Nodes

<!--
Testar Action por Action facilita identificar qual está mal configurada em caso de erro.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 2

Adicione uma nova Action ao Input Map, não demonstrada em aula — correr, agachar ou pular.

<div class="objectives">

Liberdade de implementação: correr como multiplicador de velocidade, pular como impulso vertical simples. Não há solução única.

</div>

<!--
Circular pela sala observando as escolhas. Sem instrumento formal de avaliação — retomado no Checkpoint da Semana 3.
-->

---

## Resultado Esperado da Semana

- Player (CharacterBody3D) montado, com `CollisionShape3D` e `Malha` alinhados
- Input Map com quatro Actions de movimentação, mais uma Action do desafio
- Orchestration `player.os` lendo o Input Map e movendo o Player via `move_and_slide`
- Turma relaciona CharacterBody3D/Input Map aos equivalentes na Unity

<!--
Sem instrumento formal de avaliação nesta semana. Observado no Checkpoint de encerramento do Módulo 1, na Semana 3.
-->

---

## Checklist da Semana

- [ ] `Player` (CharacterBody3D) com `CollisionShape3D` e `Malha` alinhados
- [ ] Orchestration `player.os` associada ao `Player`
- [ ] Input Map com `move_forward`, `move_back`, `move_left`, `move_right`
- [ ] `velocity` atribuída antes de `move_and_slide`
- [ ] Player se move nas quatro direções, sem erros
- [ ] Action adicional do desafio (correr, agachar ou pular)

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 3.
-->

---

## Próximos Passos — Semana 3

O Player controlável desta semana é a base direta da Semana 3:

- Materiais e terreno (**Terrain3D**)
- Iluminação global (**SDFGI/VoxelGI**)
- Exportação do primeiro build executável, encerrando o Módulo 1

Leitura recomendada: Godot Docs — Physics (CharacterBody3D) e Inputs; Unity Manual (consulta comparativa) — Input System.

<!--
Nada desta semana será refeito — apenas ampliado. Reforçar isso à turma para reduzir ansiedade sobre "ter feito certo".
Referências completas: ver Tutorial Semana 2 (Encontros 1 e 2) e Plano de Aula Semana 2.
-->
