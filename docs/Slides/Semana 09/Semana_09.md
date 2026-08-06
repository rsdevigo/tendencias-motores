---
marp: true
theme: academic-course
paginate: true
header: 'Semana 9 — Control nodes e HUD'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 9

## Control nodes e HUD

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
A Semana 8 encerrou com HealthComponent funcional no Player, uma State Machine básica de locomoção via AnimationTree e uma animação contextual própria de cada grupo, conectada a um evento real do projeto.
Até aqui, todo o estado de jogo relevante — vida (HealthComponent), itens coletados (SaveComponent/ItemData) e progresso (GameManager/SaveData, checkpoints) — existe e funciona, mas é invisível ao jogador.
Metodologia: Challenge Based Learning — professor apresenta o problema, os grupos propõem a solução. Autonomia média.
-->

---

## Objetivos da Semana

- Compreender Control nodes como sistema universal de interface em tempo real, na mesma Scene Tree de qualquer outro Node do projeto
- Construir um Control simples vinculado a uma variável de gameplay já existente, entendendo o binding de dados entre lógica de jogo e interface
- Fundamentar CanvasLayer como camada de organização do HUD sobre a cena de jogo, e montar um HUD com múltiplos elementos
- Propor e implementar, com autonomia própria, quais dados de gameplay já existentes (vida, itens, progresso) compõem o HUD do grupo

<!--
Encontro 1 cobre Control nodes, containers, anchors e a construção guiada de um Control simples vinculado ao HealthComponent.
Encontro 2 cobre CanvasLayer e o desafio de montagem do HUD completo, com escolha própria de dados e solução visual.
Referência: Godot Docs — User Interface (UI); Unity Manual — UI Toolkit, Canvas.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Control Nodes: Interface em Tempo Real

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o projeto da Semana 8 sem alterar HealthComponent, State Machine ou animação contextual — introduz uma nova camada de leitura sobre o que já existe, sem criar nenhum sistema de gameplay novo.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 8 (animação contextual conectada a evento real) (15 min)
- Introdução: o problema de comunicar estado de jogo em tempo real; Control nodes na Scene Tree (20 min)
- Demonstração: containers e anchors como resolução de layout e ancoragem (20 min)
- Demonstração: construção guiada de um Control simples vinculado à vida do `HealthComponent` (35 min)
- Laboratório: cada grupo replica o Control simples sobre o próprio `HealthComponent` (30 min)
- Feedback e fechamento (15 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — o Control simples é construção guiada, base direta do HUD completo e do desafio do Encontro 2.
-->

---

<!-- _class: question -->

# Todo o estado do jogo já existe — vida, itens, progresso. Por que o jogador ainda não vê nada disso na tela?

Pense no que falta entre o `HealthComponent` e o que aparece na tela.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que nenhum sistema novo de gameplay é necessário — falta apenas uma camada de exposição desses dados já existentes.
Erro comum: propor recriar variáveis de vida/itens dentro da interface, em vez de apenas lê-las.
-->

---

## O Problema: Estado Invisível ao Jogador

- Vida (`HealthComponent`), itens (`SaveComponent`/`ItemData`) e progresso (`GameManager`/`SaveData`) já existem e funcionam desde os Módulos 2 e 3
- Nada na tela comunica esse estado em tempo real ao jogador
- A resposta do Godot é o Control node: um Node como qualquer outro na Scene Tree, especializado em desenho e interação 2D de interface

<!--
Conceito universal: toda engine moderna enfrenta o mesmo problema estrutural de expor estado interno de gameplay ao jogador em tempo real.
Referência: PROJECT_ARCHITECTURE.md, seção de Componentes — HealthComponent, SaveComponent, GameManager.
-->

---

## Control Node: UI na Mesma Scene Tree do Jogo

- Control é um Node comum, na mesma árvore de tudo o mais — não um sistema externo separado da cena de jogo
- HUD, menus e telas de gameplay compartilham a mesma árvore, a mesma composição e os mesmos Signals já ensinados desde a Semana 5
- Três problemas recorrentes de qualquer UI: organização automática (containers), ancoragem relativa ao viewport (anchors) e binding de dados

<!--
Reforçar a quebra de intuição: "UI é um sistema à parte" não se aplica ao Godot — Control é só mais um Node.
Erro comum: tratar a UI como algo desconectado da Scene Tree do jogo.
-->

---

## Containers e Anchors: Organização e Ancoragem

- Containers (`HBoxContainer`/`VBoxContainer`) organizam múltiplos elementos automaticamente, sem posicionamento manual
- Anchors ancoram um elemento a uma posição relativa ao viewport, independente de resolução — não é posição fixa em pixels
- Os dois resolvem problemas diferentes: um organiza o conjunto, o outro ancora a posição

<!--
Erro comum: confundir anchors com posicionamento absoluto em pixels.
Erro comum: ignorar containers e posicionar elementos manualmente, perdendo a organização automática de layout.
-->

---

<!-- _class: comparison -->

## Sistema de UI no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Control: Node comum, na mesma Scene Tree de tudo o mais
- Ancoragem e organização de layout nativas e unificadas (anchors e containers built-in)

</div>
<div class="col negative">

### Unity

- Dois caminhos paralelos: uGUI (GameObject + `RectTransform` + `Canvas`) e UI Toolkit (documentos UXML/USS)
- Divisão entre dois sistemas de UI que a Unity ainda mantém

</div>
</div>

<!--
O Control do Godot ocupa posição conceitual próxima ao uGUI, mas sem a divisão entre dois sistemas paralelos que a Unity mantém.
O binding de dados é idêntico nas duas engines: em nenhuma delas a UI deve conhecer a lógica interna do sistema que representa.
-->

---

## Binding de Dados: Ler, Nunca Duplicar

- Um Control não deve conter lógica de gameplay — apenas ler ou ser notificado sobre um dado que já existe em outro sistema
- `HealthComponent`, `SaveComponent`, `GameManager` continuam sendo os donos do estado; o Control apenas espelha esse estado
- Mesma separação de responsabilidades já cobrada desde o Code Review da Semana 7

<!--
Erro comum: implementar a leitura de vida como uma variável duplicada dentro do próprio Control, em vez de referenciar o HealthComponent existente.
Este é o ponto pedagógico mais importante do encontro.
-->

---

## Demonstração — Control Simples Vinculado à Vida

O que será construído:

- Um Control simples (Label) organizado por container e posicionado por anchor
- Binding do Label à vida atual do `HealthComponent` do Player, via Orchestrator ou GDScript

Por quê: dar a cada grupo a base direta para o HUD completo do Encontro 2, sem duplicar o estado de vida já existente.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Reforçar: o Control lê o valor exposto pelo HealthComponent, sem recalcular ou duplicar o estado de vida.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o Control node na mesma Scene Tree do jogo, lendo (não duplicando) o estado do HealthComponent.
> Enquadramento: uma única árvore de cena do Player.
> Elementos presentes: "Player" com filhos "HealthComponent" e "HUD" (Control), com uma seta pontilhada de "HealthComponent" para o Label dentro do "HUD" indicando leitura, não posse do dado.
> Destaque visual: a seta pontilhada de leitura, contrastando com uma alternativa errada (variável de vida duplicada dentro do Control) marcada com um X.
> Legenda sugerida: "O Control lê a vida do HealthComponent — nunca duplica o estado."

<!--
Usar esta imagem logo após a demonstração do Control simples, antes do laboratório.
-->

---

## Arquitetura — Control como Nova Camada de Leitura

- O Control simples não altera `HealthComponent`, State Machine ou animação contextual da Semana 8
- Nenhum sistema de gameplay novo é criado nesta semana — apenas uma camada de exposição sobre o que já existe
- A conexão é sempre unidirecional: o sistema de gameplay expõe, o Control lê

<!--
Diagrama sugerido: HealthComponent (vida atual) → Control/Label (exibição), seta única em uma direção, sem retorno do Control para o HealthComponent.
Reforçar: nenhuma lógica de gameplay deve viver dentro do Control.
-->

---

## Laboratório — Control Simples Vinculado à Vida

Cada grupo replica, no próprio projeto:

1. Um Control simples (Label) organizado por container
2. Ancoragem do Control a uma posição relativa ao viewport
3. Binding do Label à vida atual do próprio `HealthComponent`, sem duplicar o estado

<!--
Critério de sucesso: Control funcional exibindo vida em tempo real, layout organizado por container, posicionado por anchor, sem lógica de gameplay duplicada.
-->

---

## Fechamento — Encontro 1

- Control simples funcional, exibindo em tempo real a vida atual do Player a partir do `HealthComponent`
- Layout organizado por container e posicionado por anchor
- HealthComponent, State Machine e animação contextual da Semana 8 sem nenhuma alteração
- Próximo passo: CanvasLayer e o desafio do HUD completo, no Encontro 2

<!--
Dificuldade esperada: confundir anchors com posição fixa em pixels — reforçar a relação com o viewport durante o laboratório.
-->

---

<!-- _class: chapter -->

## Encontro 2

# CanvasLayer e o Desafio do HUD Completo

<span class="chapter-number">02</span>

<!--
Segundo desafio da Unidade III sob Challenge Based Learning: o professor apresenta o problema de composição (quais dados compõem o HUD), os grupos propõem a solução visual e de binding.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (Control simples vinculado à vida) (15 min)
- Demonstração: fundamentação de CanvasLayer e montagem guiada de um HUD com múltiplos elementos (25 min)
- Apresentação do desafio: cada grupo define quais dados compõem seu HUD e propõe a própria solução visual/de binding (15 min)
- Laboratório/Desafio: cada grupo monta seu HUD sobre CanvasLayer, conectando os dados escolhidos (50 min)
- Feedback formal: cada grupo apresenta e justifica as escolhas do próprio HUD (30 min)

<!--
Reservar tempo real para o professor circular entre os grupos como facilitador da decisão, não como fornecedor da solução.
-->

---

<!-- _class: question -->

# Um único Label de vida resolve o HUD completo do jogo?

Pense no que acontece quando vida, itens e progresso precisam aparecer juntos, sempre visíveis, independente da câmera 3D.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que o Encontro 1 resolveu um único elemento; falta o problema de composição de múltiplos elementos em uma camada sempre visível.
-->

---

## O Problema: Compor Múltiplos Elementos Sempre Visíveis

- O Encontro 1 resolveu a interface em tempo real no nível de um único elemento
- Falta compor múltiplos elementos (vida, itens, progresso) em um HUD coeso
- O HUD precisa permanecer sempre visível, independente da câmera 3D ou da profundidade da cena

<!--
Reforçar: o problema deixou de ser técnico (como ler um dado) e passou a ser de composição e decisão (quais dados, como organizá-los).
-->

---

## CanvasLayer: Camada 2D Independente do Mundo 3D

- CanvasLayer desenha seu conteúdo em uma camada 2D separada da renderização 3D do mundo
- Garante que o HUD nunca seja ocultado por geometria do cenário
- Organiza múltiplos Control nodes (vida, itens, progresso) sob um único CanvasLayer

<!--
Erro comum: posicionar elementos do HUD diretamente na cena 3D em vez de sob um CanvasLayer, fazendo com que a interface seja ocultada por geometria do cenário.
-->

---

<!-- _class: comparison -->

## Camada de HUD no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- CanvasLayer: um único Node na mesma Scene Tree de tudo o mais

</div>
<div class="col negative">

### Unity

- uGUI: Canvas em modo Screen Space - Overlay
- UI Toolkit: `UIDocument` associado a um `PanelSettings` de overlay

</div>
</div>

<!--
O princípio universal é idêntico nas duas engines — a UI do HUD precisa de uma camada de renderização desacoplada da profundidade do mundo 3D.
O Godot resolve isso com um único Node na mesma Scene Tree; a Unity exige configuração adicional fora da hierarquia comum de GameObjects.
-->

---

## Demonstração — HUD com Múltiplos Elementos

O que será construído:

- CanvasLayer com múltiplos Control nodes (vida, itens, progresso) organizados em um único HUD
- Reutilização exata dos dados já existentes no projeto, sem criar nenhum sistema de estado novo

Por quê: fixar a montagem guiada antes de abrir o espaço de decisão do desafio do encontro.

<!--
Não estender a demonstração além do necessário — o tempo do encontro é do laboratório/desafio.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o HUD completo organizado sobre um único CanvasLayer.
> Enquadramento: árvore de cena com destaque de camada.
> Elementos presentes: "CanvasLayer" como pai de três Controls — "Label Vida", "Label Itens", "Label Progresso" — sobrepostos a uma miniatura da cena 3D do jogo abaixo.
> Destaque visual: a camada do CanvasLayer flutuando visivelmente acima da geometria 3D.
> Legenda sugerida: "CanvasLayer: uma camada 2D sempre visível, independente da profundidade do mundo 3D."

<!--
Usar esta imagem antes da apresentação do desafio, para fixar o papel do CanvasLayer como camada de composição.
-->

---

## Arquitetura — Do Dado Existente ao HUD

- Cada elemento do HUD é sempre um espelho de um dado que já existe em outro sistema: vida (`HealthComponent`), itens/progresso (`SaveComponent`/`SaveData`/`GameManager`)
- Nenhum novo sistema de estado deve ser criado exclusivamente para a interface
- O desafio é de decisão — quais dados, e que solução visual/de binding representa cada um

<!--
Diagrama sugerido: HealthComponent → Control (vida); SaveComponent/SaveData → Control (itens); GameManager → Control (progresso) — três leituras paralelas convergindo em um único CanvasLayer/HUD.
Erro comum: incluir no HUD um dado que não existe no projeto, criado apenas para a interface.
-->

---

<!-- _class: exercise -->

# Desafio — HUD Próprio sobre CanvasLayer

Defina quais dados de gameplay já existentes (vida, itens, progresso) devem compor o HUD do seu grupo, propondo a própria solução visual e de binding para cada um, organizados sobre um único CanvasLayer.

<div class="objectives">

**Entrega:** Feedback formal — HUD funcional exibindo em tempo real ao menos vida e um segundo dado de gameplay já existente, com a escolha justificada perante o grupo e o professor.

</div>

<!--
O professor circula entre os grupos como facilitador da decisão, questionando por que cada dado foi incluído (ou não) e como o binding evita duplicação do estado de gameplay.
Este é o Desafio Técnico avaliado pela Rubrica 2 do Sistema de Avaliação.
-->

---

## Boas Práticas — HUD e Binding de Dados

- HUD sempre como espelho de um dado que já existe — nunca uma variável nova criada só para a interface
- Justificar a escolha de cada dado exibido pela relevância para o jogador, não por preferência arbitrária
- Um único CanvasLayer organizando todos os Controls do HUD, evitando camadas redundantes
- Testar cada Control isoladamente antes de compor o HUD completo

<!--
Essas justificativas são exatamente o que a Rubrica 2 (Desafio Técnico) avalia neste encontro.
-->

---

## Fechamento — Encontro 2

- HUD funcional sobre CanvasLayer, exibindo em tempo real vida e ao menos um segundo dado de gameplay
- Escolha dos dados e solução visual justificada perante o grupo e o professor
- Nenhuma lógica de gameplay duplicada dentro dos Control nodes
- Segundo desafio da Unidade III sob Challenge Based Learning concluído

<!--
Dificuldade esperada: duplicar o estado de gameplay dentro do próprio Control em vez de ler o sistema já existente — reforçar que o HUD é sempre um espelho, nunca uma cópia.
-->

---

## Resultado Esperado da Semana

- HUD funcional montado sobre CanvasLayer, com Control nodes exibindo em tempo real vida (`HealthComponent`) e um segundo dado já existente (itens ou progresso)
- Solução visual e de binding própria de cada grupo, apresentada e justificada em feedback formal
- Turma domina Control nodes, containers, anchors e CanvasLayer como sistema universal de interface em tempo real
- Comparação consolidada com uGUI/UI Toolkit da Unity

<!--
Este resultado corresponde à linha Control nodes/CanvasLayer/HUD do roadmap (PROJECT_ARCHITECTURE.md).
-->

---

## Checklist da Semana

- [ ] Control simples (Label) vinculado à vida do `HealthComponent`, organizado por container e posicionado por anchor
- [ ] CanvasLayer organizando múltiplos Control nodes em um único HUD
- [ ] HUD exibindo em tempo real vida e ao menos um segundo dado (`SaveComponent`/`SaveData` ou `GameManager`)
- [ ] Nenhuma lógica de gameplay duplicada dentro dos Control nodes
- [ ] Escolha dos dados do HUD justificada em feedback formal

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 10.
-->

---

## Próximos Passos — Semana 10

O HUD construído nesta semana ganha um novo consumidor na Semana 10: o `InventoryComponent`, que reutiliza os itens já modelados como `ItemData` desde a Semana 6 e passa a expor sua própria `InventoryUI` sobre os mesmos princípios de Control node e binding de dados fundamentados aqui. A Semana 10 também retoma e amplia diretamente o contrato `Interactable` da Semana 5, conectando-o ao novo sistema de inventário.

Leitura recomendada: Godot Docs — User Interface (UI); Unity Manual (consulta comparativa) — UI Toolkit, Canvas.

<!--
Referências completas: ver Plano de Aula Semana 9. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
