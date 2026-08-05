---
marp: true
theme: academic-course
paginate: true
header: 'Semana 1 — Arquitetura do Godot, Nodes e Scene Tree'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 1

## Arquitetura do Godot, Nodes e Scene Tree

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade I — Aprender a Ferramenta** (Semanas 1–3)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
Abertura da disciplina. Reforçar que Godot 4.7 + Orchestrator é estudo de caso, não o objetivo final — o objetivo é aprender arquitetura de engines de forma transferível.
Perguntar à turma quem já usou Unity antes de prosseguir.
-->

---

## Objetivos da Semana

- Compreender o papel de uma game engine na produção de um jogo
- Reconhecer Node e Scene Tree como unidade universal de composição
- Criar a estrutura inicial do projeto do Vertical Slice
- Construir a primeira Scene funcional com Nodes filhos

<!--
Esses objetivos cobrem os dois encontros da semana. Encontro 1 cobre os dois primeiros; Encontro 2, os dois últimos.
Resultado esperado ao final: projeto Godot organizado + Scene com Nodes filhos, relacionado ao GameObject/Component da Unity.
-->

---

<!-- _class: chapter -->

## Encontro 1

# O Editor e a Estrutura do Projeto

<span class="chapter-number">01</span>

<!--
Encontro 1 é 100% guiado (Módulo 1, Scaffolded Learning). Autonomia muito baixa — o professor demonstra, o aluno replica.
-->

---

## Agenda do Encontro 1

- O que é uma game engine e por que ela existe (20 min)
- Demonstração: tour pelo Godot Editor (35 min)
- Laboratório: estrutura do projeto do Vertical Slice (50 min)
- Desafio: pasta adicional própria (20 min)
- Feedback e fechamento (10 min)

<!--
Encontro comporta compressão de até 20 min se a turma já tiver familiaridade com Unity (ver Cronograma, plano de contingência).
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
-->

---

<!-- _class: question -->

# O que a Unity resolveu "por trás" dos GameObjects nos projetos que vocês já fizeram?

Pense antes de qualquer tela do Godot aparecer.

<!--
Discussão em dupla ou com a turma toda, 2–3 minutos. Objetivo: fazer a turma nomear renderização, física, input, cena e assets sem depender de sintaxe de nenhuma engine específica.
Erro comum: respostas do tipo "fazer jogos mais fácil" sem citar problema concreto — insistir até surgir um problema nomeado.
-->

---

## O que é uma Game Engine

Um jogo resolve, por baixo da jogabilidade, um conjunto fixo de problemas técnicos:

- **Renderização** — desenhar imagens a cada frame
- **Física** — simular colisão e movimento
- **Input** — traduzir teclado/controle em ação
- **Organização de cena** — estruturar o mundo do jogo
- **Assets** — carregar e gerenciar arte, som e dados

<!--
Conceito universal, não específico de nenhuma engine. Esse é o primeiro dos quatro pontos que toda aula da disciplina deve responder (conceito universal / implementação Godot / implementação Unity-Unreal / transferência).
Referência: Godot Documentation — Getting Started / Introduction.
-->

---

## Por que uma Engine Existe

Uma game engine resolve essa camada **de forma reutilizável**, para que a equipe não precise reescrever tudo a cada novo jogo.

- É exatamente o papel que a Unity já cumpriu para vocês
- A diferença entre engines está em **como** cada uma organiza a solução — não em **se** ela existe
- Esse contraste (universal × implementação) se repete a cada novo conceito do semestre

<!--
Perguntar sempre "que problema universal isso resolve?" antes de "como se usa no Godot?" — hábito que deve se repetir a cada novo recurso apresentado no semestre.
-->

---

<!-- _class: comparison -->

## Godot × Unity — Primeiro Contato

<div class="columns">
<div class="col positive">

### Godot

- Project Manager (gerenciador de projetos)
- Viewport (edição espacial)
- FileSystem Dock (assets do projeto)
- Scene = árvore de Nodes em `.tscn`

</div>
<div class="col negative">

### Unity

- Unity Hub
- Scene View
- Project window
- Scene = contêiner de GameObjects

</div>
</div>

<!--
A diferença mais visível hoje é estrutural, não visual: no Godot uma Scene é uma árvore de Nodes salva em arquivo; na Unity, um contêiner de GameObjects. Será aprofundado no Encontro 2.
-->

---

## Demonstração — Tour pelo Godot Editor

O que será mostrado:

- Abertura do Project Manager e criação de um novo projeto
- Abas **2D**, **3D**, **Script** e **AssetLib**
- O **Viewport** — área de edição espacial da cena
- O **FileSystem Dock** — todos os arquivos do projeto (`res://`)

Resultado esperado: a turma localiza Viewport e FileSystem Dock sem confundi-los.

<!--
Não detalhar clique a clique aqui — isso é papel do Tutorial (Semana 1, Encontro 1, Parte 2). O slide só estrutura a demonstração ao vivo.
Erro comum a observar: confundir o Viewport com "o jogo rodando" — só existe jogo rodando ao pressionar Play, ainda não usado nesta aula.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o Godot Editor aberto, com Viewport 3D e FileSystem Dock visíveis simultaneamente.
> Enquadramento: captura de tela cheia do editor, com as duas áreas destacadas por retângulos coloridos.
> Elementos presentes: aba 3D ativa, Viewport central vazio, FileSystem Dock no canto inferior esquerdo listando `res://`.
> Destaque visual: contorno colorido separando Viewport (azul) de FileSystem Dock (verde).
> Legenda sugerida: "Viewport e FileSystem Dock — as duas áreas centrais do primeiro contato com o Godot."

<!--
Usar este slide durante a demonstração ao vivo, projetando o editor real em vez da imagem, se possível.
-->

---

## Laboratório — Estrutura do Vertical Slice

Cada estudante cria o projeto `TemploEsquecido` e organiza a estrutura de pastas:

```
res://
├── scenes/ (characters, interactables, ui, levels/exploration, levels/dungeon)
├── scripts/ (autoload, components)
├── orchestrations/
├── resources/ (items, save)
├── assets/ (dungeon, nature)
├── materials/  ├── audio/  └── animations/
```

<!--
A estrutura completa está no PROJECT_ARCHITECTURE.md e no Tutorial Semana 1 Encontro 1, Parte 3. Nenhuma pasta deve ficar de fora, mesmo vazia — serão preenchidas ao longo do semestre.
Erro comum: nomear pastas em PascalCase ou com espaços — a convenção do projeto é snake_case.
-->

---

## Boas Práticas — Organização de Projeto

- Nenhum asset solto na raiz de `res://`
- Toda pasta criada agora, mesmo vazia, evita retrabalho nas próximas 16 semanas
- Nunca mover ou renomear arquivos pelo sistema operacional — sempre pelo FileSystem Dock
- Nomenclatura consistente (snake_case para pastas e arquivos)

<!--
Reforçar que mover arquivos fora do FileSystem Dock quebra referências internas do projeto — isso é uma armadilha comum em quem vem de outras engines/editores de arquivos.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 1

Organize uma pasta adicional dentro da estrutura do projeto (ex.: `prototypes` ou `references`) e justifique a escolha ao colega ao lado.

<div class="objectives">

Não há solução única — o objetivo é praticar organização própria dentro de uma convenção compartilhada.

</div>

<!--
Circular pela sala durante o desafio, pedindo justificativas curtas em voz alta. Não há critério de avaliação formal aqui — é semana não-🔴.
-->

---

## Fechamento — Encontro 1

- Projeto Godot 4.7 criado e organizado
- Estrutura de pastas completa, pronta para receber conteúdo
- Próximo passo: a primeira Scene, com Nodes filhos, no Encontro 2

<!--
Sem instrumento formal de avaliação nesta semana. A estrutura criada aqui será observada informalmente e retomada no Checkpoint da Semana 3 (encerramento do Módulo 1).
Dificuldade esperada: ambiente não configurado (Godot ou Orchestrator ausentes) — ter contingência (pen drive/link) pronta.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Node, Scene Tree e Composição

<span class="chapter-number">02</span>

<!--
Encontro 2 depende diretamente do projeto criado no Encontro 1. Confirmar com a turma que todos abrem o projeto sem erros antes de prosseguir.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (10 min)
- Composição × herança, Node e Scene Tree (20 min)
- Demonstração: Scene com Nodes filhos via Orchestrator (35 min)
- Laboratório: réplica da Scene (45 min)
- Desafio: Node filho adicional (20 min)
- Feedback e fechamento (5 min)

<!--
Retomar rapidamente a estrutura de pastas do Encontro 1 antes de avançar — é pré-requisito direto.
-->

---

## Conceito — Composição × Herança

Toda engine moderna resolve o mesmo problema: como montar um objeto de jogo a partir de partes menores.

- **Herança** — uma classe herda comportamento de outra
- **Composição** — um objeto reúne partes independentes, cada uma responsável por um pedaço do comportamento

O Godot resolve esse problema através de **Node** e **Scene Tree**.

<!--
Node é o segundo conceito universal fundamental da disciplina (o primeiro foi "o que é uma engine"). Sempre explicar o conceito universal antes da implementação no Godot (PEDAGOGICAL_RULES.txt).
-->

---

## Node e Scene Tree

- **Scene** — uma árvore de Nodes, salva em um arquivo `.tscn`
- **Node** — unidade básica de composição; cada um já nasce especializado (Node3D, MeshInstance3D, Light3D...)
- Um Node filho adicionado a outro é, na prática, um componente de comportamento
- A Scene Tree **é** a própria hierarquia de composição

<!--
Reforçar: um Node3D com uma MeshInstance3D e uma Light3D como filhos não é "um objeto com propriedades de malha e luz" — é uma composição de três Nodes independentes.
Documentação: Godot Docs — Nodes and Scenes.
-->

---

<!-- _class: comparison -->

## Composição no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Node já nasce especializado
- Composição = organizar Nodes filhos
- A árvore inteira é a Scene

</div>
<div class="col negative">

### Unity

- GameObject nasce vazio
- Composição = anexar Components
- Components vivem "dentro" do GameObject

</div>
</div>

<!--
Resultado final parecido, modelo mental diferente: na Unity, comportamento se adiciona a um contêiner vazio; no Godot, comportamento se organiza em uma árvore de objetos já especializados.
Erro comum: tentar "adicionar Node a um Node vazio" como se fosse anexar Component — reforçar visualmente a Scene Tree no editor.
-->

---

<!-- _class: diagram -->

## Diagrama Sugerido — Hierarquia da Scene

> **Diagrama sugerido**
>
> Fluxo em árvore: `NivelTeste (Node3D)` no topo, com dois ramos filhos: `Chao (MeshInstance3D)` e `LuzPrincipal (DirectionalLight3D)`. Setas descendo do nó raiz para cada filho, sem setas entre os filhos (são independentes entre si).
> Objetivo: visualizar que a Scene Tree é uma árvore, não uma lista plana.
> Legenda sugerida: "A Scene Tree é composição: cada filho é responsável por sua própria função."

<!--
Pode ser desenhado ao vivo no quadro antes mesmo de abrir o Orchestrator, retomando o diagrama descrito no Tutorial Semana 1 Encontro 2, Parte 1.
-->

---

## Demonstração — Scene via Orchestrator

O que será construído:

- Scene `level_exploration.tscn` em `scenes/levels/exploration/`
- Nó raiz `NivelTeste` (Node3D)
- Filhos: `Chao` (MeshInstance3D) e `LuzPrincipal` (DirectionalLight3D)
- Orchestration `nivel_teste.os` com um evento **Ready** conectado a um log

Por quê: primeira peça de conteúdo visível do semestre, base direta do Player na Semana 2.

<!--
Não detalhar passo a passo aqui — o Tutorial (Semana 1, Encontro 2, Parte 2) cobre isso em detalhe. O slide apenas estrutura o que será demonstrado ao vivo.
Orchestrator é a camada principal de scripting da disciplina, equivalente ao Blueprint da Unreal — GDScript entra só como apoio quando o Orchestrator não cobre o recurso.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a árvore de cena (Scene Tree dock) com `NivelTeste`, `Chao` e `LuzPrincipal` já organizados, ao lado do Viewport 3D mostrando o chão iluminado.
> Enquadramento: captura de tela dividida — Scene Tree dock à esquerda, Viewport 3D à direita.
> Elementos presentes: hierarquia de três Nodes nomeados, malha visível e iluminada no Viewport.
> Destaque visual: realce na relação pai-filhos na árvore.
> Legenda sugerida: "Uma Scene simples: um Node3D pai com dois Nodes filhos especializados."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível (ex.: problema técnico de projeção).
-->

---

## Laboratório — Réplica da Scene

Cada estudante replica, no próprio projeto:

1. Scene `level_exploration.tscn` com nó raiz `NivelTeste`
2. Filhos `Chao` e `LuzPrincipal`, renomeados e configurados
3. Orchestration `nivel_teste.os` associada, com evento Ready testado
4. Teste da Scene isolada (F6), sem erros

<!--
Erro comum: MeshInstance3D sem Mesh atribuída no Inspector não renderiza nada — verificar antes de reportar "não apareceu nada".
Erro esperado e não bloqueante: aviso de "Main Scene" ausente ao testar isoladamente — ainda não configurado, sem problema neste momento.
-->

---

## Boas Práticas — Nomenclatura e Organização

- Nunca deixar Nodes com nome padrão do editor (`Node3D`, `MeshInstance3D2`)
- Sempre renomear para um nome que descreva a função
- Manter a Orchestration organizada desde o início, mesmo em grafos simples
- Seguir a convenção de nomenclatura do PROJECT_ARCHITECTURE.md

<!--
Hábito que paga dividendos a partir da Semana 2, quando a hierarquia cresce com o Player e a lógica de movimentação.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 2

Adicione um Node filho adicional à Scene, não demonstrado em aula, produzindo um comportamento visual diferente do exemplo do professor.

<div class="objectives">

Escolha livre, desde que compatível com o escopo do Vertical Slice (ver PROJECT_ARCHITECTURE.md).

</div>

<!--
Exemplos possíveis: um segundo MeshInstance3D com outra forma, ou uma OmniLight3D adicional. Circular observando se a hierarquia permanece legível — excesso de Nodes desorganizados é o erro mais comum aqui.
-->

---

## Resultado Esperado da Semana

- Projeto Godot 4.7 organizado, estrutura de pastas completa
- Scene funcional com ao menos três Nodes em hierarquia
- Um Node adicional criado de forma autônoma (desafio)
- Turma relaciona Node/Scene Tree ao par GameObject/Component da Unity

<!--
Sem instrumento formal de avaliação nesta semana (não é semana 🔴). Esta base será observada no Checkpoint de encerramento do Módulo 1, na Semana 3.
-->

---

## Checklist da Semana

- [ ] Projeto `TemploEsquecido` criado, abre sem erros
- [ ] Estrutura de pastas completa (scenes, scripts, orchestrations, resources, assets, materials, audio, animations)
- [ ] Scene `level_exploration.tscn` com `NivelTeste`, `Chao`, `LuzPrincipal`
- [ ] Orchestration `nivel_teste.os` funcional
- [ ] Node adicional do desafio, distinto do exemplo

<!--
Usar este checklist como roteiro de verificação rápida no início do próximo encontro (Semana 2).
-->

---

## Próximos Passos — Semana 2

A Scene e a estrutura desta semana são a base direta da Semana 2:

- Adição de um **CharacterBody3D** como Node filho
- Locomoção via **move_and_slide**
- Configuração do **Input Map**

Leitura recomendada: Godot Docs — Nodes and Scenes; Unity Manual (consulta comparativa).

<!--
Nada desta semana será refeito — apenas ampliado. Reforçar isso à turma para reduzir ansiedade sobre "ter feito certo".
Referências completas: ver Tutorial Semana 1 (Encontros 1 e 2) e Plano de Aula Semana 1.
-->
