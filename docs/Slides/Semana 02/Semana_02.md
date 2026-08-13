---
marp: true
theme: academic-course
paginate: true
header: 'Semana 2 — CharacterBody3D, movimentação, Input Map e Câmera'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 2

## CharacterBody3D, movimentação, Input Map e Câmera

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
- Configurar uma câmera em terceira pessoa (`SpringArm3D` + `Camera3D`) que acompanha o Player sem atravessar paredes
- Ajustar o movimento para ser relativo à direção da câmera, não a eixos fixos do mundo

<!--
Encontro 1 cobre física de locomoção (Player parado, mas sólido). Encontro 2 cobre Input Map, câmera em terceira pessoa e o ajuste do movimento para ser relativo à câmera, produzindo o Player efetivamente controlável e jogável.
Resultado esperado ao final: Player com Input Map próprio, câmera em terceira pessoa funcional, movimento relativo à câmera e uma Action adicional não demonstrada em aula.
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

- Revisão da Scene da Semana 1 (10 min)
- Introdução: por que engines desacoplam intenção de ação (15 min)
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
- Orchestration `player.torch` chamando `move_and_slide` no PhysicsProcess
- `Player` salvo como Scene própria (`scenes/characters/Player.tscn`), reaproveitável em outros níveis

Por quê: primeiro personagem controlável do semestre, base direta do Input Map no Encontro 2.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 2, Encontro 1). O slide só estrutura a demonstração ao vivo.
Reforçar a separação entre CollisionShape3D (física) e MeshInstance3D (visual) como Nodes distintos.
-->

---

## Referência em GDScript — Encontro 1

```gdscript
extends CharacterBody3D

func _physics_process(delta: float) -> void:
    move_and_slide()
```

Isso é tudo que a Orchestration `player.torch` precisa fazer neste encontro: um único nó de evento PhysicsProcess chamando `move_and_slide`, sem nenhuma leitura de input ainda.

<!--
Mostrar o código só como referência para pensar na organização do grafo — não para copiar. A ausência de velocity é intencional: reforça que o Player fica sólido, mas parado, até o Encontro 2.
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
4. Orchestration `player.torch` chamando `move_and_slide` no PhysicsProcess
5. `Player` salvo como Scene própria em `scenes/characters/Player.tscn`

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

# Input Map, InputEvent e Câmera em Terceira Pessoa

<span class="chapter-number">02</span>

<!--
Encontro 2 depende diretamente do Player montado no Encontro 1. Confirmar que todos abrem a Scene sem erros antes de prosseguir.
Este encontro passou a cobrir dois blocos de conteúdo (Input Map e Câmera); revisar o Plano de Aula da Semana 2 para realinhar a distribuição de tempo antes de aplicar em turma.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (Player parado) (10 min)
- Introdução: por que desacoplar dispositivo físico de ação lógica (15 min)
- Demonstração: Input Map + conexão com move_and_slide (25 min)
- Laboratório: cada estudante configura o próprio Input Map (30 min)
- Introdução + Demonstração: câmera em terceira pessoa (`SpringArm3D` + `Camera3D`) (15 min)
- Laboratório: cada estudante configura a própria câmera (25 min)
- Desafio: Action adicional (correr, agachar ou pular) (10 min)
- Feedback e fechamento (5 min)

<!--
Retomar rapidamente o estado do Player do Encontro 1 antes de avançar — é pré-requisito direto.
Tempo total ainda soma 2h15 (135 min), redistribuído para caber a câmera. Se a turma estiver com dificuldade no Input Map, é aceitável comprimir o bloco de câmera e retomar na Semana 3, já que o resultado esperado da Semana 2 prioriza o Player controlável.
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
- Leitura das Actions dentro da Orchestration `player.torch`
- Combinação em um vetor de direção, aplicado à `velocity` do Player
- `move_and_slide` chamado após a `velocity` ser atribuída

Por quê: transforma o Player sólido do Encontro 1 em um Player efetivamente controlável.

<!--
Não detalhar passo a passo aqui — o Tutorial (Semana 2, Encontro 2) cobre isso em detalhe.
Reforçar: a ordem importa — velocity precisa ser atribuída antes de move_and_slide.
-->

---

## Referência em GDScript — Encontro 2

```gdscript
extends CharacterBody3D

const SPEED := 5.0

func _physics_process(delta: float) -> void:
    var input_dir := Input.get_vector("move_left", "move_right", "move_forward", "move_back")

    velocity.x = input_dir.x * SPEED
    velocity.z = input_dir.y * SPEED

    move_and_slide()
```

Este código não deve ser digitado — é a referência para pensar em como organizar os nós no Orchestrator: leitura de cada Action, combinação em um vetor de direção, multiplicação pela velocidade e atribuição à `velocity` antes de `move_and_slide`.

<!--
Reforçar que o Orchestrator resolve exatamente a mesma lógica com nós visuais — o código só ajuda o estudante a planejar o grafo antes de montá-lo.
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
2. Leitura das Actions na Orchestration `player.torch`
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

<!-- _class: question -->

# Se a câmera simplesmente ficasse presa atrás do personagem, o que aconteceria ao encostar numa parede?

Pense antes de configurarmos a câmera no editor.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a nomear o problema de "câmera atravessando geometria" antes de apresentar o SpringArm3D como solução.
-->

---

## Câmera em Terceira Pessoa — Problema Universal

Toda câmera que segue um personagem por trás precisa resolver o mesmo problema:

- Acompanhar o Player suavemente, sem ficar "grudada"
- Girar ao redor do personagem conforme o jogador movimenta o mouse
- Nunca atravessar paredes ou objetos do cenário

Sem tratamento de colisão, a câmera atravessa geometria sempre que o Player encosta em um obstáculo.

<!--
Conceito universal, como no Encontro 1 com locomoção. Reforçar o hábito da disciplina: conceito antes de implementação.
Referência: Godot Documentation — Camera3D e SpringArm3D.
-->

---

## SpringArm3D + Camera3D no Godot

- **CameraPivot** (`Node3D`) — filho do Player, gira no eixo Y (yaw) conforme o mouse
- **SpringArm3D** — filho do CameraPivot, gira no eixo X (pitch) e resolve a colisão da câmera automaticamente
- **Camera3D** — filho do SpringArm3D, herda a posição já resolvida
- O SpringArm3D encurta a distância sozinho quando algo bloqueia a linha até a câmera

<!--
Reforçar a hierarquia: CameraPivot (yaw) > SpringArm3D (pitch + colisão) > Camera3D. Separar yaw e pitch em Nodes distintos facilita o clamp do pitch.
Documentação: Godot Docs — SpringArm3D, Camera3D.
-->

---

<!-- _class: comparison -->

## Câmera em Terceira Pessoa no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `SpringArm3D` é um Node nativo, sem addons
- Colisão de câmera resolvida automaticamente
- Configuração simples: spring length + collision mask

</div>
<div class="col negative">

### Unity

- Depende do pacote **Cinemachine** (não nativo)
- Virtual Camera + Collider fazem o papel do SpringArm3D
- Mais componentes, porém mais recursos avançados (blends, damping)

</div>
</div>

<!--
O Godot resolve o caso comum com um único Node nativo; a Unity exige um pacote separado, com mais camadas de configuração mas também mais recursos (transições entre câmeras, confiners, etc.).
Não aprofundar Cinemachine aqui — apenas contrastar arquitetura.
-->

---

## Demonstração — Câmera em Terceira Pessoa

O que será construído:

- `CameraPivot` (Node3D) como filho do `Player`
- `SpringArm3D` dentro do `CameraPivot`, com Spring Length e Collision Mask configurados
- `Camera3D` dentro do `SpringArm3D`, definida como câmera ativa
- Orchestration `player.torch` capturando o mouse e rotacionando `CameraPivot` (yaw) e `SpringArm3D` (pitch, com clamp)

Por quê: sem câmera própria, o jogador não consegue de fato jogar o Vertical Slice em terceira pessoa.

<!--
Não detalhar passo a passo aqui — o Tutorial (Semana 2, Encontro 2, Parte 2) cobre isso em detalhe.
Reforçar: pitch precisa de clamp, senão a câmera vira de cabeça para baixo.
-->

---

## Referência em GDScript — Câmera (Encontro 2)

```gdscript
extends CharacterBody3D

@onready var camera_pivot: Node3D = $CameraPivot
@onready var spring_arm: SpringArm3D = $CameraPivot/SpringArm3D

const MOUSE_SENSITIVITY := 0.003
const PITCH_MIN := deg_to_rad(-40.0)
const PITCH_MAX := deg_to_rad(60.0)

func _ready() -> void:
    Input.mouse_mode = Input.MOUSE_MODE_CAPTURED

func _unhandled_input(event: InputEvent) -> void:
    if event is InputEventMouseMotion:
        camera_pivot.rotate_y(-event.relative.x * MOUSE_SENSITIVITY)
        spring_arm.rotation.x = clamp(
            spring_arm.rotation.x - event.relative.y * MOUSE_SENSITIVITY,
            PITCH_MIN,
            PITCH_MAX
        )
```

Referência para pensar a organização no Orchestrator: um nó de Ready capturando o mouse, e um nó de Unhandled Input lendo o `InputEventMouseMotion` e rotacionando CameraPivot (yaw) e SpringArm3D (pitch, com clamp).

<!--
Mostrar o código só como referência — não para copiar. Reforçar que o clamp do pitch é o ponto mais fácil de esquecer ao montar no Orchestrator.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a árvore de cena com `Player` > `CameraPivot` > `SpringArm3D` > `Camera3D`, ao lado do Viewport 3D em modo Play, com a câmera posicionada atrás do Player.
> Enquadramento: captura de tela dividida — Scene dock à esquerda, Viewport 3D à direita.
> Elementos presentes: hierarquia completa da câmera, Inspector do SpringArm3D com Spring Length e Collision Mask visíveis.
> Destaque visual: seta indicando a direção do Spring Length, do CameraPivot até a Camera3D.
> Legenda sugerida: "Hierarquia da câmera em terceira pessoa: CameraPivot (yaw), SpringArm3D (pitch + colisão), Camera3D."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — Câmera em Terceira Pessoa

Cada estudante configura, no próprio projeto:

1. `CameraPivot` (Node3D) como filho do `Player`
2. `SpringArm3D` dentro do `CameraPivot`, com Spring Length e Collision Mask ajustados
3. `Camera3D` dentro do `SpringArm3D`, definida como câmera ativa
4. Captura do mouse e rotação de yaw/pitch na Orchestration `player.torch`
5. Teste com F6: girar a câmera com o mouse e encostar em uma parede do nível de teste

<!--
Erro comum: Collision Mask do SpringArm3D incluindo o próprio Player, fazendo a câmera colidir com a cápsula do personagem.
Erro comum: esquecer o clamp do pitch, deixando a câmera girar 360° verticalmente.
-->

---

## Boas Práticas — Câmera

- Separar yaw (CameraPivot) e pitch (SpringArm3D) em Nodes distintos, nunca na mesma rotação
- Sempre aplicar clamp ao pitch, evitando que a câmera vire de cabeça para baixo
- Ajustar a Collision Mask do SpringArm3D para detectar apenas o cenário, nunca o próprio Player
- Centralizar a lógica de câmera na mesma Orchestration do Player

<!--
Mistura de yaw e pitch no mesmo Node dificulta o clamp e é o erro mais comum nesta etapa.
-->

---

<!-- _class: question -->

# Se o Player sempre anda no mesmo eixo do mundo, o que acontece quando eu giro a câmera 180°?

Pense no que já foi montado até aqui.

<!--
Discussão rápida. Objetivo: a turma perceber sozinha que o movimento construído no Laboratório de Input Map ainda ignora a câmera — "frente" sempre anda para o mesmo lado do mundo, mesmo depois de girar a câmera.
-->

---

## Tank Controls × Movimento Relativo à Câmera

- Como construído até aqui, `input_dir` é aplicado direto aos eixos globais X/Z — **tank controls** (Resident Evil clássico)
- Jogos de aventura em terceira pessoa modernos (Zelda, Dark Souls, TPS Demo do Godot) usam **movimento relativo à câmera**
- Pressionar "frente" deve mover na direção para onde a câmera está olhando, não em um eixo fixo do mundo

<!--
Retomar o resultado do Laboratório de Input Map: funciona, mas "frente" não muda quando a câmera gira. Esse é o problema que esta seção resolve.
-->

---

## Corrigindo o Movimento — Basis do CameraPivot

- O vetor de direção 2D (`input_dir`) precisa ser rotacionado pela Basis do `CameraPivot`, não aplicado direto aos eixos do mundo
- `CameraPivot` só gira em Y (yaw) — sua Basis não tem pitch, então o movimento continua horizontal mesmo com a câmera inclinada
- Nunca usar a Basis do `SpringArm3D` para isso — ela contém o pitch, e inclinaria o movimento junto com a câmera

<!--
Esse é o motivo pedagógico de ter separado yaw (CameraPivot) e pitch (SpringArm3D) em Nodes diferentes na seção anterior: a separação paga dividendo aqui.
-->

---

## Referência em GDScript — Player Completo (Encontro 2)

```gdscript
extends CharacterBody3D

const SPEED := 5.0
const MOUSE_SENSITIVITY := 0.003
const PITCH_MIN := deg_to_rad(-40.0)
const PITCH_MAX := deg_to_rad(60.0)

@onready var camera_pivot: Node3D = $CameraPivot
@onready var spring_arm: SpringArm3D = $CameraPivot/SpringArm3D

func _ready() -> void:
    Input.mouse_mode = Input.MOUSE_MODE_CAPTURED

func _unhandled_input(event: InputEvent) -> void:
    if event is InputEventMouseMotion:
        camera_pivot.rotate_y(-event.relative.x * MOUSE_SENSITIVITY)
        spring_arm.rotation.x = clamp(
            spring_arm.rotation.x - event.relative.y * MOUSE_SENSITIVITY,
            PITCH_MIN, PITCH_MAX
        )

func _physics_process(delta: float) -> void:
    var input_dir := Input.get_vector("move_left", "move_right", "move_forward", "move_back")
    var direction := (camera_pivot.transform.basis * Vector3(input_dir.x, 0, input_dir.y)).normalized()

    velocity.x = direction.x * SPEED
    velocity.z = direction.z * SPEED
    move_and_slide()
```

Este é o script completo da semana — Input Map, câmera e movimento relativo à câmera juntos. Referência para planejar o grafo completo do Orchestrator, não para copiar.

<!--
Esta é a versão final do player.torch para a Semana 2. Reforçar: get_vector() substitui a leitura manual de quatro Actions por um único nó.
-->

---

## Laboratório — Integrando Câmera e Movimento

Cada estudante ajusta, no próprio projeto:

1. Localizar os nós de `input_dir` e atribuição de `velocity` construídos no Laboratório de Input Map
2. Substituir a Basis usada no cálculo pela Basis do `CameraPivot` (não a do Player, não a do SpringArm3D)
3. Testar: girar a câmera parado, depois andar, e confirmar que o Player segue a direção da câmera
4. Testar: inclinar a câmera para cima/baixo e confirmar que o movimento continua horizontal

<!--
Erro comum: usar a Basis do SpringArm3D em vez do CameraPivot — resultado é movimento inclinado ao olhar para cima/baixo.
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
- Câmera em terceira pessoa (`CameraPivot` + `SpringArm3D` + `Camera3D`) acompanhando o Player sem atravessar paredes
- Orchestration `player.torch` movendo o Player via `move_and_slide` **relativo à direção da câmera**, não a eixos fixos do mundo
- Turma relaciona CharacterBody3D/Input Map/SpringArm3D aos equivalentes na Unity (CharacterController, Input System, Cinemachine)

<!--
Sem instrumento formal de avaliação nesta semana. Observado no Checkpoint de encerramento do Módulo 1, na Semana 3.
-->

---

## Checklist da Semana

- [ ] `Player` (CharacterBody3D) com `CollisionShape3D` e `Malha` alinhados, salvo em `scenes/characters/Player.tscn`
- [ ] Orchestration `player.torch` associada ao `Player`
- [ ] Input Map com `move_forward`, `move_back`, `move_left`, `move_right`
- [ ] `velocity` atribuída antes de `move_and_slide`
- [ ] Player se move nas quatro direções, sem erros
- [ ] `CameraPivot` + `SpringArm3D` + `Camera3D` configurados como filhos do Player
- [ ] Câmera gira com o mouse (yaw no CameraPivot, pitch com clamp no SpringArm3D) e não atravessa paredes
- [ ] Movimento usa a Basis do `CameraPivot` (não eixos fixos do mundo) — "frente" segue a direção da câmera
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

Leitura recomendada: Godot Docs — Physics (CharacterBody3D), Inputs, SpringArm3D e Camera3D; Unity Manual (consulta comparativa) — Input System e Cinemachine.

<!--
Nada desta semana será refeito — apenas ampliado. Reforçar isso à turma para reduzir ansiedade sobre "ter feito certo".
Referências completas: ver Tutorial Semana 2 (Encontros 1 e 2) e Plano de Aula Semana 2.
-->
