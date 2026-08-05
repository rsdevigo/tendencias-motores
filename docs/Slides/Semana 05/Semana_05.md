---
marp: true
theme: academic-course
paginate: true
header: 'Semana 5 — Contrato Interactable e Signals'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 5

## Contrato Interactable e Signals

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
Retomar o projeto da Semana 4 já aberto, com GameManager e SaveManager registrados como Autoload. Nada desse trabalho é alterado — apenas ampliado.
Esta semana resolve um problema diferente: como um objeto do mundo (porta, alavanca) comunica ao Player que pode ser acionado, sem que os dois precisem se conhecer diretamente.
Metodologia: Studio Based Learning, autonomia baixa — professor demonstra, aluno adapta.
-->

---

## Objetivos da Semana

- Compreender o contrato `Interactable` como mecanismo de comunicação desacoplada entre Player e objetos do mundo
- Compreender Signals como padrão observer para reação a eventos de interação
- Implementar um objeto interativo concreto (porta ou equivalente) usando contrato Interactable + Signal

<!--
Encontro 1 cobre o contrato Interactable e a detecção via InteractionComponent. Encontro 2 cobre Signals e o desafio de cada grupo construir seu próprio objeto interativo.
Resultado esperado ao final: contrato Interactable implementado por ao menos uma Scene, com Signal conectado a uma reação concreta.
Referência: Godot Docs — Signals; GDScript (has_method).
-->

---

<!-- _class: chapter -->

## Encontro 1

# O Contrato Interactable

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o projeto da Semana 4 sem alterar GameManager ou SaveManager — nível, Player e Autoloads permanecem intactos.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 4 (`GameManager` e `SaveManager` como Autoload) (15 min)
- Introdução: o problema da comunicação acoplada entre sistemas (20 min)
- Demonstração: criação do contrato `Interactable` e implementação em uma Scene (`Door.tscn`) (35 min)
- Laboratório: cada estudante cria seu próprio contrato e implementa uma Scene interativa (45 min)
- Desafio: adaptar a reação da Scene interativa (15 min)
- Feedback e fechamento (5 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
-->

---

<!-- _class: question -->

# Se o Player precisar reconhecer uma porta, uma alavanca e um baú, o que muda no código do Player a cada novo tipo?

Pense em como esse código cresceria a cada objeto interativo novo.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a concluir que a resposta correta é "nada deveria mudar" — e que essa é a garantia que um contrato oferece.
Erro comum: aceitar get_node/if-else por tipo como solução razoável sem perceber o custo de escala.
-->

---

## O Problema da Comunicação Acoplada

- Toda engine com múltiplos sistemas independentes precisa resolver o mesmo problema: como um sistema chama outro sem depender do tipo concreto dele
- Se o Player conhecesse `Door`, `Lever`, `Chest` explicitamente, cada objeto novo exigiria alterar o Player
- Esse acoplamento não escala — e se tornaria insustentável já na Semana 10 (interação conectada ao Inventário)

<!--
Conceito universal, não específico do Godot. Reforçar o hábito da disciplina: perguntar "que problema universal isso resolve?" antes de "como se usa no Godot?".
Referência: Godot Docs — GDScript (métodos, has_method).
-->

---

## O Contrato Interactable

- Define apenas um comportamento esperado: responder a `interact()`
- Não exige hierarquia de herança comum entre os objetos que o implementam
- Godot expressa isso via **duck typing** (`has_method("interact")`) ou nó de interface do Orchestrator
- Qualquer Node pode implementar o contrato sem herdar de uma classe base

<!--
Reforçar: contrato não é classe base. Door não estende Interactable, apenas declara uma função interact().
-->

---

<!-- _class: comparison -->

## Contrato de Comportamento no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Duck typing: `has_method("interact")`
- Checagem em tempo de execução
- Mais flexível, sem exigir declaração formal

</div>
<div class="col negative">

### Unity

- Interface formal de C#: `IInteractable`
- Checagem em tempo de compilação
- Exige que o `MonoBehaviour` declare a interface

</div>
</div>

<!--
O conceito universal — contrato de comportamento sem herança compartilhada — é o mesmo nas duas engines; muda apenas o momento em que o contrato é verificado.
Não transformar isso em aula de C#.
-->

---

## Demonstração — Contrato e Scene Door

O que será construído:

- Contrato `Interactable` via `has_method("interact")`
- Scene `scenes/interactables/Door.tscn`, script `door.gd` com `class_name Door`
- Função `interact()` implementada, reagindo com uma confirmação simples

Por quê: primeira Scene interativa do Vertical Slice, base de todo objeto interativo até a Semana 17.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 5, Encontro 1).
Reforçar: remover qualquer chamada de teste de interact() antes de seguir para a Parte 3.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a estrutura de pastas do projeto com `scenes/interactables/` e `scripts/components/` em destaque.
> Enquadramento: captura de tela do FileSystem Dock do Godot, árvore de pastas expandida.
> Elementos presentes: pastas `scenes/interactables/`, `scripts/components/`, `scripts/autoload/` (já existente).
> Destaque visual: as duas pastas novas desta semana.
> Legenda sugerida: "Novas pastas do projeto para interativos e Components, Semana 5."

<!--
Usar esta imagem como referência ao apresentar a organização de pastas antes da demonstração ao vivo.
-->

---

## Arquitetura — Detectando o Interactable

- `InteractionComponent`: novo Component do Player, dedicado a detectar objetos próximos
- Usa `Area3D` para detecção de proximidade
- Ao receber a ação `interagir`, checa `has_method("interact")` antes de chamar
- Nunca escreve `if objeto is Door` — apenas confirma que o objeto responde ao contrato

<!--
Diagrama sugerido: Player → InteractionComponent (Area3D) → detecta objeto → checa has_method("interact") → chama interact() → Door reage.
Este é o ponto exato em que o desacoplamento discutido antes se torna código.
-->

---

## Laboratório — Contrato e Scene Interativa

Cada estudante replica, no próprio projeto:

1. Pasta `scenes/interactables/` criada, conforme PROJECT_ARCHITECTURE.md
2. Scene `Door.tscn`, com script `door.gd` implementando `interact()`
3. `InteractionComponent` no Player, detectando via `Area3D`
4. Ação `interagir` adicionada ao Input Map
5. Teste de `interact()` com pelo menos duas instâncias de `Door.tscn`

<!--
Erro comum: nomear a função de forma diferente de interact — quebra a checagem has_method("interact").
Erro comum: usar get_node direto em vez de checar o contrato, reintroduzindo o acoplamento que o contrato existe para evitar.
-->

---

## Boas Práticas — Interactable

- Manter a lógica de reação dentro da função `interact()`, nunca fora dela (por exemplo, no `_process()`)
- Nomear a Scene pela função que representa (`Door.tscn`), nunca pela implementação
- Manter o `InteractionComponent` limitado a detectar e chamar o contrato — nenhuma lógica específica de `Door`, `Lever` ou `Chest` deve viver ali
- Testar sempre com pelo menos duas instâncias diferentes antes de considerar a etapa concluída

<!--
Esse hábito evita que o InteractionComponent acumule, nas semanas seguintes, lógica que deveria pertencer a cada objeto interativo.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 1

Adapte a reação da própria Scene interativa a um comportamento não demonstrado em aula — por exemplo, alternar entre dois estados visuais, ou emitir uma mensagem de depuração própria.

<div class="objectives">

Mantenha o contrato `Interactable` como único ponto de entrada — a reação continua vivendo dentro de `interact()`.

</div>

<!--
Circular pela sala conferindo se a reação está sendo implementada dentro de interact() e não em outro lugar do script.
Sem instrumento formal de avaliação neste encontro — pré-requisito do desafio avaliado do Encontro 2.
-->

---

## Fechamento — Encontro 1

- Contrato `Interactable` definido e implementado por ao menos uma Scene do Vertical Slice
- `InteractionComponent` detectando e chamando `interact()` sem conhecer o tipo concreto do objeto
- Desafio de reação própria implementado
- Próximo passo: Signals conectando a interação a uma reação desacoplada, no Encontro 2

<!--
Dificuldade esperada: confundir contrato com herança — reforçar que Interactable não é uma classe base.
Este resultado corresponde ao item "Contrato Interactable (interface via duck typing)" do roadmap (PROJECT_ARCHITECTURE.md, seção 6).
-->

---

<!-- _class: chapter -->

## Encontro 2

# Signals e o Objeto Interativo do Grupo

<span class="chapter-number">02</span>

<!--
Encontro depende diretamente do contrato Interactable do Encontro 1. Confirmar que Door.tscn e InteractionComponent estão testados antes de prosseguir.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (contrato `Interactable` implementado em uma Scene) (10 min)
- Introdução: Signals como padrão observer (20 min)
- Demonstração: declaração de um Signal de interação e conexão a uma função de reação (35 min)
- Laboratório e Desafio: cada grupo implementa seu objeto interativo com contrato + Signal (50 min)
- Feedback formal sobre as soluções apresentadas (20 min)

<!--
Reservar tempo real para o desafio em grupo — é o momento em que o par contrato + Signal se torna concreto para a turma.
-->

---

<!-- _class: question -->

# Se três sistemas diferentes precisassem reagir à interação com a porta, a função interact() deveria chamar os três diretamente?

Pense em abrir a porta, tocar um som e atualizar o GameManager ao mesmo tempo.

<!--
Discussão rápida, 2–3 minutos. Objetivo: concluir que a resposta é não — interact() deve apenas emitir um Signal, e cada sistema interessado se conecta a ele de forma independente.
Erro comum: achar que Signal e função são a mesma coisa com nomes diferentes.
-->

---

## Signals como Padrão Observer

- O contrato `Interactable` resolve "como um objeto responde a uma chamada"
- Signals resolvem um problema complementar: "como um objeto avisa que algo aconteceu, sem saber quem está ouvindo"
- Padrão **observer**, presente em praticamente toda engine de jogos moderna
- No Godot, um Signal é declarado na Scene emissora e conectado a funções de reação, sem que o emissor conheça o receptor

<!--
Reforçar: emissor de um Signal não precisa saber quantas (ou se alguma) função está conectada a ele.
Referência: Godot Docs — Signals.
-->

---

<!-- _class: comparison -->

## Padrão Observer no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Signals: mecanismo de primeira classe do editor
- Declarado, listado e conectado visualmente em qualquer Node

</div>
<div class="col negative">

### Unity

- `UnityEvent` (Inspector) ou `event`/`Action` de C# (código)
- Resultado depende de qual convenção a equipe escolheu adotar

</div>
</div>

<!--
A diferença relevante não é a sintaxe, mas o Godot tratar Signals como mecanismo nativo único, disponível tanto pelo editor quanto por código.
-->

---

## Demonstração — Signal interacted na Door

O que será construído:

- Signal `interacted` declarado em `door.gd`
- `interact()` passa a emitir o Signal em vez de reagir diretamente
- Função de reação separada (`_abrir_fechar()`), conectada ao Signal pela subaba **Signals**

Por quê: separa "avisar que a interação ocorreu" de "reagir à interação" — a mesma separação que sustentará a conexão ao Inventário na Semana 10.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 5, Encontro 2).
Reforçar: interact() deve apenas emitir, nunca também chamar a reação diretamente.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o painel Node do Godot com o Signal `interacted` declarado na Scene `Door.tscn` e sua conexão a uma função de reação.
> Enquadramento: captura de tela da aba **Node > Signals** do editor Godot, com `Door.tscn` aberta.
> Elementos presentes: lista de Signals do nó, o Signal `interacted` customizado, o ícone de conexão ativa.
> Destaque visual: o Signal `interacted` e a seta indicando a função conectada.
> Legenda sugerida: "Signal interacted declarado na Door e conectado à função de reação."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Arquitetura — Interactable + Signal

- `interact()` (contrato): recebe a chamada do `InteractionComponent`
- `interacted` (Signal): avisa que a interação ocorreu, sem saber quem reage
- Função de reação separada: conectada ao Signal, nunca chamada dentro de `interact()`
- Qualquer novo objeto interativo repete essa mesma estrutura, sem alterar o `InteractionComponent`

<!--
Diagrama sugerido: InteractionComponent → interact() → emite Signal interacted → função de reação conectada (ex.: _abrir_fechar()).
Reforçar que essa estrutura é o que permite ao Vertical Slice crescer até a Semana 17 sem reescrever o Player.
-->

---

## Boas Práticas — Signals

- Manter a lógica de reação sempre em uma função separada da função do contrato, mesmo na mesma Scene
- Nomear Signals no padrão `substantivo_verbo_passado` (`interacted`, `item_collected`)
- Conectar sempre pela subaba **Signals** — um Signal declarado mas não conectado não produz efeito visível
- Mostrar a conexão via código como alternativa, útil para objetos criados dinamicamente

<!--
Erro comum: nomear o Signal fora da convenção do projeto (ex.: OnInteract em vez de interacted).
-->

---

## Laboratório e Desafio — Objeto Interativo do Grupo

Cada grupo implementa um objeto interativo (porta ou equivalente) usando contrato `Interactable` + Signal:

- Scene própria em `scenes/interactables/`, com collider, `MeshInstance3D` e script com `class_name`
- Signal próprio (ex.: `lever_pulled`), emitido dentro de `interact()`
- Função de reação separada, conectada ao Signal
- Liberdade de mecanismo de acionamento: alavanca, chave, proximidade

<!--
Erro comum: duplicar lógica do InteractionComponent dentro do novo objeto — ele já existe no Player e deve ser reutilizado sem alteração.
Testar alternando entre Door e o novo objeto, sem reiniciar o projeto.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 2

Cada grupo implementa um objeto interativo (porta ou equivalente escolhido pelo grupo) usando contrato `Interactable` + Signal, com liberdade de mecanismo de acionamento (alavanca, chave, proximidade).

<div class="objectives">

**Entrega:** Feedback formal sobre as soluções apresentadas, avaliado pela Rubrica 2 — Desafios Técnicos.

</div>

<!--
Rubrica 2 — Desafios Técnicos: Solução proposta, Uso correto do Godot, Criatividade, Organização, Funcionamento.
Reservar os últimos 20 minutos do encontro para o Feedback formal em grupo.
-->

---

## Checkpoint — Base do Módulo 2

Ao final da semana, cada estudante/grupo possui:

- Contrato `Interactable`, implementado pela Scene `Door.tscn`, com Signal `interacted` conectado a uma reação visível
- `InteractionComponent` do Player, funcionando sem conhecer o tipo concreto do objeto
- Um segundo objeto interativo próprio do grupo, com o mesmo contrato e um Signal próprio

<!--
Este resultado corresponde à conclusão dos itens "Contrato Interactable" e "Signals de interação" e ao início de "Door, Lever" do roadmap (PROJECT_ARCHITECTURE.md, seção 6).
Pré-requisito direto do Checkpoint da Semana 6 e do Code Review de encerramento do Módulo 2 (Semana 7).
-->

---

## Fechamento — Encontro 2

- Signal `interacted` declarado, emitido e conectado a uma reação visível
- Objeto interativo próprio do grupo funcionando com o `InteractionComponent`, sem nenhuma alteração nele
- Feedback formal sobre as soluções de interação apresentadas
- Módulo 2 avança com o par contrato + Signal sustentando todo objeto interativo futuro

<!--
Dificuldade esperada: confundir o papel do Signal (avisar) com o papel do contrato (responder) — reforçar que são complementares.
-->

---

## Resultado Esperado da Semana

- Contrato `Interactable` implementado por ao menos uma Scene do Vertical Slice
- Signal de interação conectado a uma reação concreta
- Cada grupo com seu próprio objeto interativo (porta, alavanca ou equivalente)
- Turma relaciona contrato e Signal ao equivalente da Unity (`IInteractable` e `UnityEvent`/`event`/`Action`)

<!--
Este par — Interactable + Signal — sustenta todo objeto interativo do Vertical Slice até a Semana 17, incluindo a ampliação da Semana 10.
-->

---

## Checklist da Semana

- [ ] Contrato `Interactable` (`has_method("interact")`) definido e implementado em `Door.tscn`
- [ ] `InteractionComponent` no Player, detectando via `Area3D` e chamando `interact()`
- [ ] Ação `interagir` adicionada ao Input Map
- [ ] Signal `interacted` declarado, emitido em `interact()` e conectado a uma reação separada
- [ ] Segundo objeto interativo do grupo, com contrato e Signal próprios
- [ ] Feedback formal recebido sobre a solução de interação do grupo

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 6.
-->

---

## Próximos Passos — Semana 6

O par contrato `Interactable` + Signal construído nesta semana é pré-requisito direto da Semana 6, que introduz `ItemData` (Resource customizado) e Enums para separar dados de design da lógica de gameplay.

Leitura recomendada: Godot Docs — Signals, GDScript (`has_method`); Unity Manual (consulta comparativa) — Events, Interfaces em C#.

<!--
Os itens coletáveis modelados na Semana 6 poderão ser associados a objetos interativos (baús) que já implementam o contrato desta semana.
O par Interactable/Signal também será retomado e ampliado na Semana 10, quando a interação passar a se conectar ao Inventário.
Referências completas: ver Tutorial Semana 5 (Encontros 1 e 2) e Plano de Aula Semana 5.
-->
