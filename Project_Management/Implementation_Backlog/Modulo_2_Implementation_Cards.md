# Implementation Cards — Milestone MS-2 (Semanas 4–7)

Fonte primária: `docs/Tutoriais/Tutorial_Semana_04_*.md` a `Tutorial_Semana_07_*.md`. Todas as cartas são **Tipo A**, salvo indicação contrária.

> **Atualização (2026-09-02):** os **DC-01** e **DC-06** foram resolvidos e registrados em `PROJECT_ARCHITECTURE.md` §6/§7/§8.
> - DC-01: `Pickup`/`Chest` construídos no **Tutorial da Semana 7, Encontro 1, Parte 3** (nova), `Checkpoint` movido para a Parte 4. Cartas IC-VS06-03 e IC-VS07-04 deixam de ser stubs.
> - DC-06: `PlayerStart` (Marker3D) + `GameManager.spawn_player()` na **Semana 4, Encontro 1, Parte 3** (nova carta IC-VS04-04); escolha por `Checkpoint` + carregamento do save ao iniciar na **Semana 7, Encontro 1, Parte 5** (nova carta IC-VS07-05).

---

## IC-VS04-01 — GameManager (Orchestration + Registro como Autoload)

**Objetivo:** criar o primeiro ponto de estado global do projeto.

**Contexto:** abre o Módulo 2; nenhuma alteração visual ou de gameplay ocorre nesta carta — é puramente arquitetural. GDScript aparece nos documentos apenas como implementação de referência da lógica do grafo.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7, §9; `Tutorial_Semana_04_Encontro_1.md`.

**Tipo:** A

**Arquivos Esperados:** `res://orchestrations/autoload/game_manager.torch` (ou `.gd` equivalente, se o grupo optar por GDScript)

**Implementação:**
1. Criar `orchestrations/autoload/game_manager.torch`, classe base `Node`.
2. Registrar uma nota de responsabilidade no grafo (regras de partida + estado compartilhado).
3. Registrar em Project Settings > Autoload (Path: o `.torch` diretamente; Node Name: `GameManager`, PascalCase).
4. Validar acesso a partir do Player com um teste temporário (nó Print / `print(GameManager)`); remover após confirmar.

**Restrições:** não instanciar `GameManager` como Node dentro de uma Scene — apenas via registro em Autoload. Não deixar teste (`print`/nó Print) no grafo final.

**Testes:** F6 em `level_exploration.tscn`; Output confirma acesso sem erro (`Invalid get index`/`Identifier not declared` ausentes).

**Critérios de Aceite:**
- [ ] `game_manager.torch` (classe base `Node`) registrado e habilitado diretamente como Autoload.
- [ ] Acesso validado a partir de um script/grafo fora do próprio Autoload.

**Definition of Done:** checklist do Tutorial (Semana 4, Encontro 1) 100% (exceto desafio, ver IC-VS04-D).

**Dependências:** Blocked By: IC-VS03-04. Blocks: IC-VS04-02.

**Story Points:** 2

---

## IC-VS04-02 — SaveManager (Orchestration + Registro como Autoload)

**Objetivo:** criar o segundo Autoload, dedicado a dados que sobrevivem à troca de cena.

**Contexto:** `SaveManager` é independente do `GameManager` — guarda dados de progresso, não regras de partida.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7; `Tutorial_Semana_04_Encontro_2.md` (Parte 2).

**Tipo:** A

**Arquivos Esperados:** `res://orchestrations/autoload/save_manager.torch` (ou `.gd` equivalente)

**Implementação:**
1. Criar `orchestrations/autoload/save_manager.torch`, classe base `Node`.
2. Registrar como segundo Autoload independente, direto pelo `.torch` (Node Name: `SaveManager`).
3. Registrar uma nota com a distinção de responsabilidade frente ao `GameManager`.

**Restrições:** `SaveManager` e `GameManager` não devem depender de detalhes internos um do outro.

**Testes:** Project Settings > Autoload lista os dois; `print(SaveManager)` de teste confirma acesso global.

**Critérios de Aceite:**
- [ ] `save_manager.torch` registrado e habilitado, independente do `GameManager`.

**Definition of Done:** ver IC-VS04-03 para o teste de persistência completo.

**Dependências:** Blocked By: IC-VS04-01. Blocks: IC-VS04-03.

**Story Points:** 1

---

## IC-VS04-03 — Persistência Entre Cenas (Demonstração Guiada)

**Objetivo:** validar, com uma troca de cena real, que uma variável do `SaveManager` sobrevive à troca de Scene.

**Contexto:** demonstração guiada apenas — a variável usada aqui (`itens_coletados`) é o exemplo do tutorial. O desafio avaliado (uma variável própria, DIFERENTE desta) é uma carta separada: **IC-VS04-D — Desafio Técnico Semana 4**.

**Documentos de Referência:** `Tutorial_Semana_04_Encontro_2.md` (Parte 3).

**Tipo:** A (a parte guiada em si não tem ambiguidade — a variável de exemplo é dada pelo tutorial).

**Arquivos Esperados:** modificação em `save_manager.torch`; nova Scene temporária `res://scenes/levels/exploration/level_teste_persistencia.tscn` (descartável, não faz parte do nível final).

**Implementação:**
1. Em `save_manager.torch`, declarar a variável de exemplo `itens_coletados: int` (painel de variáveis) e uma função pública para alterá-la.
2. Criar `level_teste_persistencia.tscn` (Node3D + Label3D) apenas para o teste.
3. No Player, acionar temporariamente a função via uma tecla livre; validar incremento.
4. Trocar a Main Scene para `level_teste_persistencia.tscn`, confirmar que o valor persiste; reverter a Main Scene para `level_exploration.tscn`.
5. Remover código de teste temporário (prints, tecla de debug) ao final.

**Restrições:** nenhuma variável de teste deve permanecer hardcoded fora do Autoload; a Main Scene do projeto deve terminar revertida para `level_exploration.tscn`.

**Testes:** troca de cena real (não apenas leitura de código); Output confirma valor mantido.

**Critérios de Aceite:**
- [ ] Variável do `SaveManager` confirmadamente persistente entre duas Scenes reais.
- [ ] Main Scene revertida; nenhum código de teste residual.

**Definition of Done:** mecânica de persistência comprovada — serve de modelo direto para o desafio (IC-VS04-D).

**Dependências:** Blocked By: IC-VS04-02. Blocks: IC-VS04-D.

**Story Points:** 2

---

## IC-VS04-04 — PlayerStart e GameManager.spawn_player()

**Objetivo:** dar ao `GameManager` sua primeira responsabilidade concreta — posicionar o Player ao carregar o nível, lendo um Node marcador da cena.

**Contexto:** DC-06 resolvido. Semana 4, Encontro 1, Parte 3 (nova). Equivalente ao par `PlayerStart` + `GameMode.ChoosePlayerStart` da Unreal.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7 (linhas PlayerStart/GameManager + parágrafo "Fluxo de spawn do Player"), §8; `Tutorial_Semana_04_Encontro_1.md` (Parte 3).

**Tipo:** A

**Arquivos Esperados:** `res://scenes/levels/exploration/level_exploration.tscn` (novo Marker3D + chamada no `_ready()`); modificação em `game_manager.torch`.

**Implementação:**
1. Em `level_exploration.tscn`: adicionar um `Marker3D` filho do nó raiz, renomear para `PlayerStart`, posicionar no ponto inicial, adicionar ao grupo `player_start`.
2. Adicionar o Node do Player ao grupo `player`.
3. Em `game_manager.torch`: função pública `spawn_player()` que lê `get_first_node_in_group("player")` e `..._first_node_in_group("player_start")` e faz `player.global_position = inicio.global_position` (com guardas de `null`). Implementação de referência em GDScript no Tutorial (Parte 3).
4. No grafo/script raiz de `level_exploration.tscn`, chamar `GameManager.spawn_player()` no `_ready()` (nó Get Autoload → Call Function).

**Restrições:** nenhuma coordenada de spawn (`Vector3`/`Transform3D`) dentro de `game_manager.torch` — a posição é dado da cena. `spawn_player()` deve ser função pública (será reutilizada pelo respawn do Módulo 3).

**Testes:** rodar o nível → Player no `PlayerStart`; mover o marcador no editor → Player segue; comentar a chamada no `_ready()` → Player volta a nascer onde a instância está salva.

**Critérios de Aceite:**
- [ ] `Marker3D` `PlayerStart` em `level_exploration.tscn`, grupo `player_start`; Player no grupo `player`.
- [ ] `GameManager.spawn_player()` reposiciona o Player lendo os grupos, sem coordenada no grafo, chamado no `_ready()` do nível.

**Definition of Done:** checklist do Tutorial (Semana 4, Encontro 1), itens de PlayerStart/spawn.

**Dependências:** Blocked By: IC-VS04-01. Blocks: IC-VS07-05.

**Story Points:** 2

---

## IC-VS04-D — Desafio Técnico Semana 4: Variável Própria em GameManager/SaveManager

**Objetivo:** praticar autonomia sobre Autoload com liberdade de escolha total — este é o entregável avaliado pela **Rubrica 2 (Desafios Técnicos)** do Sistema de Avaliação para a Semana 4 (ver `docs/Sistema_de_Avaliacao_Tendencias_de_Motores_de_Jogos.md`).

**Contexto:** o Cronograma define dois desafios na Semana 4, um por encontro. A demonstração guiada (IC-VS04-01/02/03) não os substitui — o Encontro 2 pede explicitamente uma variável "diferente do usado na demonstração".

**Documentos de Referência:** `Tutorial_Semana_04_Encontro_1.md` (Desafio); `Tutorial_Semana_04_Encontro_2.md` (Desafio); Sistema_de_Avaliacao_Tendencias_de_Motores_de_Jogos.md (Rubrica 2).

**Tipo:** B — liberdade de escolha total, sem solução única, conforme o próprio Cronograma.

**Implementação:**
1. Encontro 1: adicionar ao `GameManager` UMA variável de estado de partida própria, não demonstrada em aula (ex.: contador de tentativas, flag de evento). Anotar no grafo por que ela pertence ao `GameManager`.
2. Encontro 2: implementar no `SaveManager` um dado próprio que deve persistir entre cenas — DIFERENTE de `itens_coletados` (a variável de exemplo de IC-VS04-03). Validar com uma troca de cena real, repetindo o procedimento de IC-VS04-03.

**Restrições:** a variável do Encontro 2 não pode ser a mesma já usada na demonstração de IC-VS04-03.

**Testes:** `print()` temporário confirmando leitura de ambas as variáveis; troca de cena real para a do `SaveManager`.

**Critérios de Aceite:**
- [ ] Variável própria no `GameManager`, com justificativa anotada no grafo.
- [ ] Variável própria (distinta da demo) no `SaveManager`, validada com troca de cena real.

**Definition of Done:** avaliado pela Rubrica 2 — Solução proposta, Uso correto do Godot, Criatividade, Organização, Funcionamento.

**Dependências:** Blocked By: IC-VS04-03. Blocks: IC-VS05-01.

**Story Points:** 2

---

## IC-VS05-01 — Contrato Interactable + Door (Reação Direta)

**Objetivo:** implementar o primeiro objeto que responde a uma chamada sem que o chamador conheça seu tipo concreto.

**Contexto:** primeira metade da Semana 5, Encontro 1 — a reação da Door ainda é direta (sem Signal, que só entra no Encontro 2).

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7 (Interactable, Door), §9; `Tutorial_Semana_05_Encontro_1.md`.

**Tipo:** A

**Arquivos Esperados:**
```
res://scenes/interactables/Door.tscn
res://scripts (ou orchestrations) — door.gd ou door.torch
```

**Implementação:**
1. Criar `Door.tscn` em `scenes/interactables/`: Node raiz (ex.: `Area3D` ou `StaticBody3D`, conforme a detecção escolhida), `CollisionShape3D`, `MeshInstance3D` (Kenney Mini Dungeon).
2. Criar script/Orchestration com `class_name Door`, implementando `interact() -> void`.
3. Corpo inicial de `interact()`: efeito direto simples (ex.: `print()` ou alteração visual imediata) — será substituído por Signal em IC-VS05-03.

**Restrições:** o nome do método deve ser exatamente `interact()` (contrato consumido por `has_method("interact")`).

**Testes:** chamada manual de `interact()` via debug confirma efeito.

**Critérios de Aceite:**
- [ ] `Door.tscn` implementa `interact()`, nomeado conforme o contrato.

**Definition of Done:** ver IC-VS05-02 para a detecção via Player.

**Dependências:** Blocked By: IC-VS04-03. Blocks: IC-VS05-02.

**Story Points:** 2

---

## IC-VS05-02 — InteractionComponent no Player

**Objetivo:** detectar objetos interativos próximos e chamar `interact()` sem conhecer o tipo concreto.

**Contexto:** completa o par contrato + detecção do Encontro 1 da Semana 5.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7 (InteractionComponent); `Tutorial_Semana_05_Encontro_1.md`.

**Tipo:** A

**Arquivos Esperados:** `res://scripts/components/interaction_component.gd` (ou Orchestration equivalente), adicionado como Node filho de `Player`.

**Implementação:**
1. Criar `InteractionComponent` (Node customizado, `Area3D` para detecção de proximidade) como filho de `Player`.
2. Ao detectar um objeto na área, checar `has_method("interact")` antes de chamar.
3. Conectar a uma Action do Input Map (ex.: `interagir`, tecla E) para acionar a chamada quando o objeto detectado suportar o contrato.

**Restrições:** o `InteractionComponent` nunca deve conhecer o tipo concreto do objeto (`Door`, `Lever` etc.) — apenas `has_method("interact")`.

**Testes:** aproximar o Player da `Door` e acionar a Action de interação; confirmar chamada de `interact()`.

**Critérios de Aceite:**
- [ ] `InteractionComponent` detecta e chama `interact()` via duck typing, sem acoplamento ao tipo concreto.

**Definition of Done:** checklist do Tutorial (Semana 5, Encontro 1) 100%.

**Dependências:** Blocked By: IC-VS05-01. Blocks: IC-VS05-03.

**Story Points:** 3

---

## IC-VS05-03 — Signal `interacted` na Door

**Objetivo:** substituir a reação direta de `interact()` por um Signal, desacoplando emissor de receptor.

**Contexto:** Encontro 2 da Semana 5, Parte 2.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §9 (nomenclatura de Signals); `Tutorial_Semana_05_Encontro_2.md` (Parte 2).

**Tipo:** A

**Arquivos Esperados:** modificação em `door.gd`/`door.torch`.

**Implementação:**
1. Declarar `signal interacted` no topo do script (abaixo de `class_name Door`).
2. `interact()` passa a apenas emitir: `interacted.emit()`.
3. Criar função de reação separada (ex.: `_abrir_fechar()`), alternando estado (`aberta: bool`) e efeito visual (rotação ou material).
4. Na subaba Node > Signals, conectar `interacted` a `_abrir_fechar()`.

**Restrições:** `interact()` nunca deve chamar `_abrir_fechar()` diretamente, apenas emitir o Signal.

**Testes:** aproximar e interagir repetidamente; confirmar abertura/fechamento alternado; subaba Signals mostra conexão ativa.

**Critérios de Aceite:**
- [ ] `interacted` declarado, emitido em `interact()`, conectado a uma função de reação separada.

**Definition of Done:** checklist do Tutorial (Semana 5, Encontro 2), itens da Door.

**Dependências:** Blocked By: IC-VS05-02. Blocks: IC-VS05-04, IC-VS07-03 (Checkpoint reaproveita o mesmo padrão).

**Story Points:** 2

---

## IC-VS05-04 — Segundo Objeto Interativo (Desafio: ex. Lever)

**Objetivo:** provar o desacoplamento construindo um segundo objeto interativo sem alterar o `InteractionComponent`.

**Contexto:** desafio de encerramento da Semana 5, avaliado por Feedback formal (Rubrica 2).

**Documentos de Referência:** `Tutorial_Semana_05_Encontro_2.md` (Parte 3).

**Tipo:** B — "mecanismo de acionamento livre (alavanca, chave, proximidade)", explicitamente aberto pelo tutorial.

**Arquivos Esperados:** `res://scenes/interactables/Lever.tscn` (ou nome equivalente escolhido).

**Implementação:**
1. Criar nova Scene em `scenes/interactables/`, seguindo a mesma estrutura da Door.
2. Declarar Signal próprio (ex.: `signal lever_pulled`), implementar `interact()` emitindo-o.
3. Implementar função de reação própria, conectada ao Signal.
4. Instanciar próxima à Door existente; testar ambos com o mesmo `InteractionComponent`, sem alterá-lo.

**Restrições:** não duplicar lógica do `InteractionComponent` dentro do novo objeto; não reaproveitar o nome do Signal `interacted` (usar um nome específico ao evento).

**Testes:** alternar interação entre Door e o novo objeto no mesmo teste, sem reiniciar o projeto.

**Critérios de Aceite:**
- [ ] Segundo objeto interativo funcional, com contrato e Signal próprios, sem alteração no `InteractionComponent`.

**Definition of Done:** Feedback formal (Semana 5) recebido; checklist do Tutorial 100%.

**Dependências:** Blocked By: IC-VS05-03. Blocks: IC-VS06-01.

**Story Points:** 3

---

## IC-VS06-01 — Classe ItemData (Resource)

**Objetivo:** criar a estrutura de dados desacoplada para itens do jogo.

**Contexto:** Encontro 1 da Semana 6.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §9; `Tutorial_Semana_06_Encontro_1.md`.

**Tipo:** A

**Arquivos Esperados:**
```
res://scripts/resources/item_data.gd
res://resources/items/item_moeda.tres
res://resources/items/item_chave.tres
```

**Implementação:**
1. Criar `scripts/resources/item_data.gd`: `extends Resource`, `class_name ItemData`.
2. Campos `@export`: `nome: String`, `icone: Texture2D`, `valor: int`, `descricao: String` (com valores padrão).
3. Gerar duas instâncias `.tres` em `resources/items/` (New Resource > ItemData), preenchendo campos distintos.
4. Adicionar um campo extra de desafio (ex.: `peso` ou `raridade`), não demonstrado.

**Restrições:** nenhuma lógica de gameplay dentro de `item_data.gd`; a classe estende `Resource`, nunca `Node`.

**Testes:** selecionar cada `.tres` e confirmar campos preenchidos e distintos no Inspector.

**Critérios de Aceite:**
- [ ] `ItemData` criado com os 4 campos base + 1 campo de desafio.
- [ ] 2+ instâncias `.tres` com valores próprios.

**Definition of Done:** checklist do Tutorial (Semana 6, Encontro 1) 100%.

**Dependências:** Blocked By: IC-VS05-04. Blocks: IC-VS06-02.

**Story Points:** 2

---

## IC-VS06-02 — Enum de Categoria + Conjunto Próprio de Itens

**Objetivo:** restringir a categoria de um item a um conjunto fechado, e modelar um conjunto temático próprio de 3+ itens.

**Contexto:** Encontro 2 da Semana 6 — Checkpoint de progresso do Módulo 2.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §9; `Tutorial_Semana_06_Encontro_2.md`.

**Tipo:** B — o conjunto de categorias e o tema dos itens são explicitamente de livre escolha ("ajuste ao tema do próprio Vertical Slice").

**Arquivos Esperados:** modificação em `item_data.gd`; 3+ instâncias `.tres` adicionais/ajustadas em `resources/items/`.

**Implementação:**
1. Declarar `enum Categoria { MOEDA, RECURSO, CHAVE }` (ou conjunto ajustado ao tema, 3–5 valores) em `item_data.gd`.
2. Adicionar campo `@export var categoria: Categoria`.
3. Preencher `categoria` em todas as instâncias existentes.
4. Criar/ajustar ao menos 3 instâncias `.tres` cobrindo o conjunto de categorias escolhido.

**Restrições:** manter o Enum pequeno (3–5 valores); nunca usar `String` livre para um campo fechado.

**Testes:** Inspector confirma menu suspenso (não campo de texto livre) para `categoria` em cada instância.

**Critérios de Aceite:**
- [ ] Enum `Categoria` aplicado; 3+ instâncias com `categoria` preenchida via menu suspenso.

**Definition of Done:** Checkpoint de progresso do Módulo 2 (Cronograma, Semana 6) apresentado; checklist do Tutorial 100%.

**Dependências:** Blocked By: IC-VS06-01. Blocks: IC-VS06-D.

**Story Points:** 2

---

## IC-VS06-D — Desafio Técnico Semana 6: Campo Extra + Conjunto Próprio de Itens

**Objetivo:** consolidar, como entregável avaliado pela **Rubrica 2 (Desafios Técnicos)**, os dois desafios da Semana 6 (Sistema de Avaliação — Semanas com Desafio Técnico: 1, 2, 4, 5, 6, 8, 9, 10, 11, 13).

**Contexto:** o campo extra (IC-VS06-01, passo 4) e o conjunto próprio de itens (IC-VS06-02, conteúdo integral) já cobrem tecnicamente este desafio — esta carta existe para que ele seja rastreável como unidade avaliada, em vez de ficar implícito dentro de outras cartas.

**Documentos de Referência:** `Tutorial_Semana_06_Encontro_1.md` (Desafio); `Tutorial_Semana_06_Encontro_2.md` (Desafio); Sistema_de_Avaliacao_Tendencias_de_Motores_de_Jogos.md (Rubrica 2).

**Tipo:** B — "liberdade de categorias e atributos", explícito no Cronograma.

**Implementação:** ver IC-VS06-01 (passo 4) e IC-VS06-02 (conteúdo integral). Nenhum passo adicional além do já descrito nessas duas cartas.

**Critérios de Aceite:** idênticos à soma de IC-VS06-01 (campo extra) + IC-VS06-02 (3+ itens temáticos).

**Definition of Done:** avaliado pela Rubrica 2 — Solução proposta, Uso correto do Godot, Criatividade, Organização, Funcionamento.

**Dependências:** Blocked By: IC-VS06-02. Blocks: IC-VS07-01.

**Story Points:** 2

---

## IC-VS06-03 — Pickup, Chest e Handler de Coleta (ItemData → SaveManager)

**Objetivo:** construir os primeiros objetos interativos que entregam um `ItemData` ao jogo e ligar o resultado da coleta ao `SaveManager` por um handler único.

**Contexto:** DC-01 resolvido (ver `Design_Backlog/Design_Cards.md` → DC-01). Apesar do número `VS06`, a construção acontece no **Tutorial da Semana 7, Encontro 1, Parte 3** — primeiro ponto do Cronograma em que `ItemData` (Semana 6) já existe e a coleta alimenta a persistência do `Checkpoint` na mesma aula.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7 (linhas Pickup/Chest + parágrafo do fluxo do item coletado), §9; `Tutorial_Semana_07_Encontro_1.md` (Parte 3).

**Tipo:** A (para as Scenes e o handler; a única variação por grupo é qual `ItemData` cada instância concede — Tipo B apenas nesse recorte).

**Arquivos Esperados:**
```
res://scenes/interactables/Pickup.tscn   + pickup.gd (ou pickup.torch)
res://scenes/interactables/Chest.tscn    + chest.gd  (ou chest.torch)
modificação em res://orchestrations/autoload/save_manager.torch
handler no grafo/script raiz de level_exploration.tscn (ou em game_manager.torch)
```

**Implementação:**
1. Em `save_manager.torch`: `var itens_coletados: Array[String] = []` (substituindo a variável `int` de demonstração da Semana 4, se ainda com esse nome) e a função pública `registrar_item(nome: String)` idempotente (`if nome in itens_coletados: return`). Implementação de referência em GDScript no Tutorial (Semana 7, Encontro 1).
2. `Pickup.tscn`: `Area3D` + `CollisionShape3D` + malha (Mini Dungeon), mesma estrutura de `Door`. `pickup.gd`: `class_name Pickup`, `signal item_collected(item: ItemData)`, `@export var item: ItemData`. `interact()` → `item_collected.emit(item)` + `queue_free()` (guarda `if item == null: return`).
3. `Chest.tscn`: mesma estrutura, malha de baú. `chest.gd`: `class_name Chest`, mesmo Signal e `@export`, mais `var aberto := false`. `interact()` → `if aberto or item == null: return`; `aberto = true`; `item_collected.emit(item)`.
4. Handler único `_ao_coletar_item(item: ItemData)` → `SaveManager.registrar_item(item.nome)`; conectar o Signal `item_collected` de cada instância a ele.
5. Posicionar ao menos um `Pickup` e um `Chest` no nível, cada um com um `.tres` do conjunto do grupo.

**Restrições:** nenhuma lógica de "efeito do item" dentro de `pickup.gd`/`chest.gd`; a Scene coletável nunca chama `SaveManager` diretamente — só emite o Signal. Um único handler no projeto. `Door`/`Lever` permanecem com `interacted` (sem carga), inalterados.

**Testes:** interagir com `Pickup` (some; nome entra em `itens_coletados`); interagir com `Chest` duas vezes (registra uma vez só); coletar item de mesmo nome de duas fontes (sem duplicata na lista).

**Critérios de Aceite:**
- [ ] `Pickup` e `Chest` implementam `interact()` e emitem `item_collected(item: ItemData)`.
- [ ] `Chest` concede o item apenas na primeira interação (`aberto`).
- [ ] Handler único registra `item.nome` via `SaveManager.registrar_item(...)`, sem duplicatas; nenhuma Scene coletável conhece o `SaveManager`.

**Definition of Done:** checklist do Tutorial (Semana 7, Encontro 1), itens de Pickup/Chest/handler.

**Dependências:** Blocked By: IC-VS06-02, IC-VS05-03. Blocks: IC-VS07-03, IC-VS07-04, IC-VS10-01.

**Story Points:** 3

---

## IC-VS07-01 — SaveData (Resource)

**Objetivo:** criar a estrutura de dados de progresso a ser persistida em disco.

**Contexto:** primeira etapa da Semana 7, Encontro 1.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7; `Tutorial_Semana_07_Encontro_1.md` (Parte 1).

**Tipo:** A

**Arquivos Esperados:** `res://scripts/resources/save_data.gd`

**Implementação:**
1. Criar `save_data.gd`: `extends Resource`, `class_name SaveData`.
2. Campos `@export`: `itens_coletados: Array[String] = []`, `ultimo_checkpoint: String = ""`.
3. **Não** criar instância `.tres` manual em `res://` — `SaveData` é instanciado em tempo de execução (ver IC-VS07-02).

**Restrições:** `SaveData` estende `Resource`, nunca `Node`; nenhuma instância manual em `res://`.

**Testes:** `class_name SaveData` compila sem erro.

**Critérios de Aceite:**
- [ ] `save_data.gd` criado com os 2 campos base.

**Definition of Done:** checklist do Tutorial (Semana 7, Encontro 1), Parte 1.

**Dependências:** Blocked By: IC-VS06-02. Blocks: IC-VS07-02.

**Story Points:** 1

---

## IC-VS07-02 — SaveComponent (Gravação/Leitura em `user://`)

**Objetivo:** centralizar a leitura/escrita de `SaveData` em disco.

**Contexto:** segunda etapa da Semana 7, Encontro 1.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §10 (Component); `Tutorial_Semana_07_Encontro_1.md` (Parte 2).

**Tipo:** A

**Arquivos Esperados:** `res://scripts/components/save_component.gd`

**Implementação:**
1. Criar `save_component.gd`: `extends Node`, `class_name SaveComponent`.
2. Constante `CAMINHO_SAVE := "user://save_data.tres"`.
3. Função `salvar(itens_coletados: Array[String], checkpoint: String) -> void`, montando um `SaveData` e gravando via `ResourceSaver.save()`.
4. Função `carregar() -> SaveData`, checando `FileAccess.file_exists()` antes de `ResourceLoader.load()`, retornando `null` se ausente.
5. Adicionar como Node filho de `Player` (ou raiz do nível, conforme organização adotada).
6. Testar `salvar()`/`carregar()` via atalho de debug temporário; confirmar arquivo em `user://` (Projeto > Abrir Pasta de Dados do Usuário); remover código de teste ao final.

**Restrições:** gravação exclusivamente em `user://`, nunca em `res://`; único `SaveComponent` ativo por vez; nenhuma outra Scene deve chamar `ResourceSaver`/`FileAccess` diretamente.

**Testes:** gravar, fechar e reabrir o jogo, carregar — dados devem ser idênticos. Apagar o arquivo manualmente e confirmar que `carregar()` retorna `null` sem erro.

**Critérios de Aceite:**
- [ ] `SaveComponent` grava/lê corretamente em `user://save_data.tres`, sobrevivendo ao fechamento do jogo.

**Definition of Done:** checklist do Tutorial (Semana 7, Encontro 1), Parte 2.

**Dependências:** Blocked By: IC-VS07-01. Blocks: IC-VS07-03.

**Story Points:** 3

---

## IC-VS07-03 — Checkpoint (Reaproveitando Interactable)

**Objetivo:** construir a Scene que aciona a gravação de progresso ao ser alcançada.

**Contexto:** quarta etapa da Semana 7, Encontro 1 — fecha o conjunto de sistemas novos do Módulo 2.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §8; `Tutorial_Semana_07_Encontro_1.md` (Parte 4).

**Tipo:** A

**Arquivos Esperados:** `res://scenes/interactables/Checkpoint.tscn`

**Implementação:**
1. Criar `Checkpoint.tscn` em `scenes/interactables/`: `Area3D` + `CollisionShape3D` + malha/marcador visual (asset do Mini Dungeon).
2. Implementar `interact()` (mesmo contrato de `Door`/`Lever`, via `has_method`).
3. Atribuir um `@export var id_checkpoint: String` único por instância; adicionar cada instância ao grupo `checkpoints`.
4. Dentro de `interact()`: gravar `SaveManager.ultimo_checkpoint = id_checkpoint` (ponto de respawn corrente) e chamar `SaveComponent.salvar(SaveManager.itens_coletados, id_checkpoint)` — a lista vem do handler de coleta de IC-VS06-03.
5. Posicionar ao menos uma instância no nível.

**Restrições:** não reimplementar detecção de proximidade dentro do `Checkpoint` — reutilizar o `InteractionComponent` já existente no Player. Nunca chamar `ResourceSaver`/`FileAccess` diretamente — sempre via `SaveComponent`. O `Checkpoint` grava o id em `SaveManager`, mas não resolve id → posição (isso é do `GameManager`, IC-VS07-05).

**Testes:** interagir com o Checkpoint; confirmar atualização do arquivo em `user://`; coletar um item, interagir, fechar/reabrir o jogo, confirmar persistência via `carregar()`.

**Critérios de Aceite:**
- [ ] `Checkpoint` implementa `Interactable`, aciona `SaveComponent.salvar()`, grava `SaveManager.ultimo_checkpoint`, com `id_checkpoint` único e no grupo `checkpoints`.

**Definition of Done:** checklist do Tutorial (Semana 7, Encontro 1), itens do Checkpoint.

**Dependências:** Blocked By: IC-VS07-02, IC-VS05-03, IC-VS06-03. Blocks: IC-VS07-05, IC-VS07-04.

**Story Points:** 3

---

## IC-VS07-05 — Carregar Save ao Iniciar + spawn_player() por Checkpoint

**Objetivo:** fechar o ciclo do save — ler o `SaveData` no carregamento do nível e fazer `GameManager.spawn_player()` escolher entre o `PlayerStart` e o último `Checkpoint` alcançado.

**Contexto:** DC-06 resolvido. Semana 7, Encontro 1, Parte 5 (nova). Dá consumidor a `SaveData.ultimo_checkpoint`, que hoje é gravado sem ninguém ler.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7 (parágrafo "Fluxo de spawn do Player"); `Tutorial_Semana_07_Encontro_1.md` (Parte 5).

**Tipo:** A

**Arquivos Esperados:** modificação em `game_manager.gd` e no script raiz de `level_exploration.tscn`.

**Implementação:**
1. Ampliar `GameManager.spawn_player()` (de IC-VS04-04): se `SaveManager.ultimo_checkpoint != ""`, varrer o grupo `checkpoints` procurando `cp.id_checkpoint == SaveManager.ultimo_checkpoint` e usar esse Node como destino; senão, cair no `PlayerStart`.
2. No `_ready()` do nível, antes de `spawn_player()`: `var dados := <SaveComponent>.carregar()`; se `dados`, copiar `dados.itens_coletados` e `dados.ultimo_checkpoint` para o `SaveManager`.
3. Ordem no `_ready()`: carregar → copiar para `SaveManager` → `GameManager.spawn_player()`.

**Restrições:** o `id_checkpoint` é resolvido para posição **no `GameManager`**, nunca no `SaveManager` (que guarda só o id). Nenhuma coordenada nos Autoloads. O carregamento cobre apenas `itens_coletados`/`ultimo_checkpoint` (schema da Semana 7) — evolução em DC-05. Nenhum tratamento de morte do Player aqui — DC-03.

**Testes:** sem save → Player no `PlayerStart`; após alcançar um `Checkpoint`, fechar/reabrir → Player nasce nesse checkpoint e `itens_coletados` volta preenchido.

**Critérios de Aceite:**
- [ ] `spawn_player()` escolhe entre `Checkpoint` ativo (por id) e `PlayerStart`.
- [ ] `_ready()` do nível carrega o `SaveData` e popula o `SaveManager` antes do spawn.
- [ ] Nenhuma coordenada em `game_manager.gd`/`save_manager.gd`.

**Definition of Done:** checklist do Tutorial (Semana 7, Encontro 1), itens do ciclo de spawn.

**Dependências:** Blocked By: IC-VS07-03, IC-VS04-04. Blocks: IC-VS07-04.

**Story Points:** 2

---

## IC-VS07-04 — Integração Final do Módulo 2 (Fluxo Único + Code Review + Playtest) 🔴

**Objetivo:** conectar porta, alavanca, `Pickup`, `Chest` e checkpoint em um único fluxo percorrível, e passar por Code Review/Playtest de encerramento da Unidade II.

**Contexto:** Encontro 2 da Semana 7 — não introduz sistema novo, apenas integra o que já existe. DC-01 resolvido: `Pickup`/`Chest` entram no fluxo normalmente.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6 ("Produto do Módulo 2"); `Tutorial_Semana_07_Encontro_2.md`.

**Tipo:** A.

**Arquivos Esperados:** reposicionamento de instâncias existentes em `level_exploration.tscn` (nenhum arquivo novo).

**Implementação:**
1. Posicionar/reposicionar `Door`, `Lever` (ou equivalente), `Pickup`, `Chest` e `Checkpoint` formando um caminho único, início a fim.
2. Confirmar que a alavanca controla a porta via o Signal já conectado (Semana 5).
3. Confirmar que `Pickup`/`Chest` no caminho concedem um item via `item_collected`, registrado em `SaveManager.itens_coletados` sem duplicatas.
4. Posicionar o `Checkpoint` em um ponto lógico do caminho (ex.: após a primeira sala resolvida), de forma que alcançá-lo grave os itens coletados até ali.
5. Posicionar o `PlayerStart` no início do caminho; confirmar que, sem save, o Player nasce nele.
6. Percorrer o caminho completo; fechar e reabrir o jogo; confirmar que o progresso é recuperado e que o Player nasce no último `Checkpoint` alcançado.
7. Preparar e apresentar a justificativa de arquitetura de cada sistema do módulo (Code Review, Rubrica 4).
8. Realizar Playtest coletivo (ou, em contexto solo, testar com uma pessoa externa ao desenvolvimento).

**Restrições:** preferir conectar sistemas existentes a criar novos objetos nesta carta — o objetivo é integração, não expansão de escopo.

**Testes:** percurso completo do fluxo, com fechamento/reabertura do jogo no meio do teste (verificando spawn no checkpoint).

**Critérios de Aceite:**
- [ ] Porta, alavanca, `Pickup`, `Chest` e checkpoint conectados em um único fluxo, sem retrabalho estrutural.
- [ ] Item coletado refletido em `SaveManager.itens_coletados` e persistido pelo `Checkpoint`.
- [ ] Progresso persistido confirmado após reiniciar o jogo; Player nasce no último `Checkpoint` (ou no `PlayerStart` sem save).
- [ ] Code Review e Playtest coletivo realizados.

**Definition of Done:** encerramento da Unidade II conforme o Cronograma (Semana 7 🔴).

**Dependências:** Blocked By: IC-VS07-03, IC-VS07-05. Blocks: todo o Milestone MS-3 (VS-08 em diante).

**Story Points:** 3
