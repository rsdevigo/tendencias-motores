# Semana 1 — Arquitetura do Godot, Nodes e Scene Tree

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade I — Aprender a Ferramenta** (Semanas 1–3) | **Metodologia:** Scaffolded Learning — professor demonstra, aluno replica. Autonomia muito baixa.

## Introdução da Semana

Esta é a primeira semana da disciplina. Antes de qualquer botão do Godot, a turma precisa entender o que é uma game engine e por que ela existe: um software que resolve, de forma reutilizável, os problemas recorrentes de qualquer jogo (renderização, física, input, organização de mundo, gerenciamento de assets), para que a equipe de desenvolvimento foque no jogo em si. O Godot 4.7 + Orchestrator é o estudo de caso da disciplina, não o objetivo — cada conceito apresentado aqui deve ser reconhecível em qualquer outra engine, especialmente Unity, que a turma já conhece.

A partir desta semana começa o Vertical Slice único do semestre (projeto de trabalho *O Templo Esquecido*), que crescerá continuamente até a Semana 17. Nada construído hoje será descartado.

## Objetivos Gerais

- Compreender o papel de uma game engine na produção de um jogo.
- Reconhecer Node e Scene Tree como unidade universal de composição de uma engine moderna.
- Criar a estrutura inicial do projeto do Vertical Slice.

## Resultados Esperados

Ao final da semana, a turma terá um projeto Godot organizado, com uma primeira Scene composta por Nodes filhos, e terá relacionado esse modelo de composição ao GameObject/Component da Unity.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o papel de uma game engine no desenvolvimento de jogos.
- Identificar as áreas principais do Godot Editor (Viewport, FileSystem Dock).
- Criar e organizar a estrutura inicial do projeto do Vertical Slice.

## Conteúdos

- O que é uma game engine e por que ela existe.
- Tour guiado pelo Godot Editor.
- Criação do projeto do Vertical Slice e organização de pastas no FileSystem Dock.

## Conceitos Fundamentais

Toda engine resolve o mesmo conjunto de problemas — renderização, física, input, organização de cena, gerenciamento de assets — para que a equipe não precise reescrever essa camada a cada jogo. O FileSystem Dock do Godot cumpre o mesmo papel que o Content Browser em outras engines: organizar e localizar os assets do projeto. Esse é o primeiro dos quatro pontos que toda aula da disciplina deve responder: o que é, por que existe, como funciona no Godot, e como se compara a outros motores.

## Recursos do Godot

Godot Editor, Viewport, FileSystem Dock.

## Comparação com Unity

O Godot Editor e a Unity organizam o projeto de forma equivalente: um painel de assets (FileSystem Dock ↔ Project window), um Viewport de cena, e um sistema de cenas próprio (Scene ↔ Scene do Unity). A diferença mais visível nesta primeira aula é estrutural, não visual: no Godot, uma Scene é uma árvore de Nodes salva em arquivo (.tscn), enquanto na Unity uma Scene é um contêiner de GameObjects. Essa diferença será aprofundada no Encontro 2.

## Preparação do Professor

- Projeto Godot 4.7 vazio, pronto para projeção.
- Orchestrator instalado e habilitado como plugin no projeto de demonstração.
- Estrutura de pastas sugerida para o Vertical Slice (ex.: `scenes/`, `scripts/`, `assets/`, `resources/`) definida previamente para reprodução guiada.
- Slides da Semana 1 com a definição de game engine e o roteiro do tour pelo editor.
- Confirmar que a máquina de cada estudante (ou os laboratórios) já possui o Godot 4.7 e o addon Orchestrator instalados.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 20 min | Introdução: o que é uma game engine e por que ela existe (antes de qualquer botão) |
| 35 min | Demonstração: tour guiado pelo Godot Editor — Viewport, FileSystem Dock |
| 50 min | Laboratório: criação e organização da estrutura inicial do projeto do Vertical Slice |
| 20 min | Desafio: organizar uma pasta adicional própria coerente com o projeto |
| 10 min | Feedback e fechamento |

*Semana 1, Encontro 1 comporta compressão de até 20 minutos caso a turma já tenha familiaridade prévia com engines de terceiros (Unity), conforme previsto no Cronograma.*

## Desenvolvimento

O encontro abre com uma discussão curta sobre o que já foi vivido em Unity — o que a engine resolveu por trás dos GameObjects — antes de qualquer tela do Godot. Em seguida, o professor projeta o editor e percorre Viewport e FileSystem Dock, nomeando cada área e seu papel. A turma então cria o próprio projeto do Vertical Slice, replicando a estrutura de pastas demonstrada, preparando o terreno para a Scene inicial que será construída no Encontro 2.

## Desafio

Cada estudante organiza uma pasta adicional dentro da estrutura do projeto (por exemplo, uma pasta para protótipos ou para referências), justificando brevemente a escolha ao colega ao lado. Não há solução única — o objetivo é praticar organização própria dentro de uma convenção compartilhada.

## Critérios de Sucesso

O projeto do Vertical Slice existe, abre sem erros no Godot 4.7, e possui uma estrutura de pastas organizada e coerente com o que será construído nas próximas semanas.

## Evidências para Avaliação

Este encontro não gera instrumento formal de avaliação (não é semana 🔴). A estrutura do projeto criada aqui será a base observada no Checkpoint de encerramento do Módulo 1, na Semana 3.

## Dificuldades Esperadas

- Estudantes que tentam pular direto para "fazer alguma coisa acontecer na tela" antes de entender a estrutura do projeto — reforçar que organização inicial evita retrabalho nas próximas 16 semanas.
- Confusão entre Scene do Godot e Scene da Unity — retomar brevemente no Encontro 2, quando o conceito de Node for formalizado.
- Ambiente não configurado (Godot ou Orchestrator ausentes) — ter pen drives ou link de download prontos como contingência.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Node e Scene Tree como unidade universal de composição.
- Comparar composição (Godot) com composição via Component (Unity).
- Criar uma Scene com Nodes filhos usando o Orchestrator.

## Conteúdos

- Node e Scene Tree como unidade universal de composição (composição versus herança).
- Criação guiada de uma Scene com Nodes filhos via Orchestrator.

## Conceitos Fundamentais

Toda engine moderna resolve o problema de "como compor um objeto de jogo" de duas formas possíveis: herança (uma classe herda comportamento de outra) ou composição (um objeto reúne partes independentes). O Godot resolve isso via Node e Scene Tree: uma Scene é uma árvore de Nodes, e cada Node especializado adicionado como filho é, na prática, um componente de comportamento. Esse é o mesmo princípio de composição por trás do par GameObject/Component da Unity — a diferença está em como cada engine implementa a árvore.

## Recursos do Godot

Node, Scene Tree, Orchestrator.

## Comparação com Unity

Na Unity, um GameObject é um contêiner vazio que recebe Components para ganhar comportamento (Transform, Rigidbody, script, etc.). No Godot, cada Node já nasce especializado (Node2D, Node3D, CharacterBody3D, etc.), e a composição acontece organizando Nodes filhos dentro de uma Scene — a própria Scene Tree é a hierarquia de composição. O resultado prático é parecido, mas o modelo mental é diferente: na Unity, comportamento se adiciona a um objeto vazio; no Godot, comportamento se organiza em uma árvore de objetos já especializados.

## Preparação do Professor

- Projeto de demonstração com uma Scene 3D vazia pronta para receber Nodes.
- Lista de dois ou três Nodes simples para a demonstração guiada (ex.: um Node3D pai com uma MeshInstance3D e uma Light3D como filhos).
- Orchestrator configurado e testado previamente na máquina de demonstração.
- Slides com o comparativo Node/Scene Tree × GameObject/Component.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 1 (estrutura do projeto criada) |
| 20 min | Introdução: composição versus herança, Node e Scene Tree |
| 35 min | Demonstração: criação de uma Scene com Nodes filhos via Orchestrator |
| 45 min | Laboratório: cada estudante replica a Scene demonstrada dentro do próprio projeto |
| 20 min | Desafio: adicionar um Node filho adicional, produzindo comportamento visual diferente |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro retoma a estrutura criada no Encontro 1 e introduz Node e Scene Tree como resposta ao problema de composição. O professor demonstra, via Orchestrator, a criação de uma Scene simples com dois ou três Nodes filhos, explicando o papel de cada um antes de adicioná-lo. A turma replica a mesma Scene dentro do próprio projeto do Vertical Slice, consolidando a primeira peça de conteúdo visível do semestre.

## Desafio

Cada estudante adiciona um Node filho adicional à Scene construída, não demonstrado em aula, produzindo um comportamento visual diferente do exemplo do professor — livre escolha do Node, desde que compatível com o escopo do Vertical Slice (ver PROJECT_ARCHITECTURE.md).

## Critérios de Sucesso

Cada estudante possui, ao final da semana, uma Scene funcional com ao menos três Nodes organizados em hierarquia, incluindo um Node não demonstrado em aula, dentro do projeto do Vertical Slice já estruturado.

## Evidências para Avaliação

Sem instrumento formal nesta semana. A Scene construída aqui é o alicerce observado informalmente pelo professor e retomado como base para o Player na Semana 2.

## Dificuldades Esperadas

- Confundir Node com Component da Unity ao ponto de tentar "adicionar Node a um Node vazio" em vez de organizar a árvore — reforçar visualmente a Scene Tree no editor.
- Excesso de Nodes desorganizados no desafio livre — orientar a manter a hierarquia legível, já que ela será reutilizada nas próximas semanas.
- Orchestrator novo para a turma — reservar tempo extra de suporte individual durante o laboratório.

---

# Resultado Esperado da Semana

Ao final da Semana 1, cada estudante possui um projeto Godot 4.7 organizado, com uma Scene funcional composta por Nodes filhos (incluindo pelo menos um Node adicionado de forma autônoma). A turma domina a distinção entre composição (Godot/Unity) e consegue nomear o papel de FileSystem Dock, Node e Scene Tree, relacionando-os aos equivalentes na Unity (Project window, GameObject/Component).

# Preparação para a Próxima Semana

A Scene e a estrutura de projeto construídas nesta semana serão a base direta da Semana 2, quando um CharacterBody3D será adicionado como Node filho para receber movimentação (`move_and_slide`) e Input Map. Nenhum conteúdo desta semana deve ser refeito — apenas ampliado.

# Referências

- Godot Documentation — Getting Started / Introduction: https://docs.godotengine.org/en/stable/getting_started/introduction/index.html
- Godot Documentation — Nodes and Scenes: https://docs.godotengine.org/en/stable/tutorials/scripting/nodes_and_scene_instances.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa): https://docs.unity3d.com/Manual/
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
