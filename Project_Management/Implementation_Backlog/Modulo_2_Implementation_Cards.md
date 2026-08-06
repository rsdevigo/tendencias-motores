# Implementation Cards — Milestone MS-2 (Semanas 4–7)

Fonte primária: `docs/Tutoriais/Tutorial_Semana_04_*.md` a `Tutorial_Semana_07_*.md`. Todas as cartas são **Tipo A**, salvo indicação contrária. Duas entradas desta lista (IC-VS06-03, IC-VS07-04) são **stubs bloqueados — Tipo C** e não contêm passo a passo, conforme a Regra Absoluta do plano (nunca inventar a implementação de uma decisão inexistente).

---

## IC-VS04-01 — GameManager (Script + Registro como Autoload)

**Objetivo:** criar o primeiro ponto de estado global do projeto.

**Contexto:** abre o Módulo 2; nenhuma alteração visual ou de gameplay ocorre nesta carta — é puramente arquitetural.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7, §9; `Tutorial_Semana_04_Encontro_1.md`.

**Tipo:** A

**Arquivos Esperados:** `res://scripts/autoload/game_manager.gd`

**Implementação:**
1. Criar `scripts/autoload/game_manager.gd`, herdando `Node`.
2. Declarar `class_name GameManager` e um comentário de responsabilidade (regras de partida + estado compartilhado).
3. Registrar em Project Settings > Autoload (Path: o script; Node Name: `GameManager`, PascalCase).
4. Validar acesso a partir do script do Player com `print(GameManager)` temporário; remover após confirmar.

**Restrições:** não instanciar `GameManager` como Node dentro de uma Scene — apenas via registro em Autoload. Não deixar `print()` de teste no código final.

**Testes:** F6 em `level_exploration.tscn`; Output confirma acesso sem erro (`Invalid get index`/`Identifier not declared` ausentes).

**Critérios de Aceite:**
- [ ] `game_manager.gd` com `class_name GameManager`, registrado e habilitado como Autoload.
- [ ] Acesso validado a partir de um script fora do próprio Autoload.

**Definition of Done:** checklist do Tutorial (Semana 4, Encontro 1) 100% (exceto desafio, ver IC-VS04-03).

**Dependências:** Blocked By: IC-VS03-04. Blocks: IC-VS04-02.

**Story Points:** 2

---

## IC-VS04-02 — SaveManager (Script + Registro como Autoload)

**Objetivo:** criar o segundo Autoload, dedicado a dados que sobrevivem à troca de cena.

**Contexto:** `SaveManager` é independente do `GameManager` — guarda dados de progresso, não regras de partida.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7; `Tutorial_Semana_04_Encontro_2.md` (Parte 2).

**Tipo:** A

**Arquivos Esperados:** `res://scripts/autoload/save_manager.gd`

**Implementação:**
1. Criar `scripts/autoload/save_manager.gd`, herdando `Node`, com `class_name SaveManager`.
2. Registrar como segundo Autoload independente (Node Name: `SaveManager`).
3. Comentar a distinção de responsabilidade frente ao `GameManager`.

**Restrições:** `SaveManager` e `GameManager` não devem herdar um do outro nem depender de detalhes internos um do outro.

**Testes:** Project Settings > Autoload lista os dois; `print(SaveManager)` de teste confirma acesso global.

**Critérios de Aceite:**
- [ ] `SaveManager` registrado e habilitado, independente do `GameManager`.

**Definition of Done:** ver IC-VS04-03 para o teste de persistência completo.

**Dependências:** Blocked By: IC-VS04-01. Blocks: IC-VS04-03.

**Story Points:** 1

---

## IC-VS04-03 — Persistência Entre Cenas + Desafios do Módulo

**Objetivo:** validar, com uma troca de cena real, que uma variável do `SaveManager` sobrevive; e implementar as variáveis de desafio de ambos os encontros.

**Contexto:** fecha a Semana 4 — sem este teste, o Autoload não está comprovadamente funcional.

**Documentos de Referência:** `Tutorial_Semana_04_Encontro_1.md` (Desafio); `Tutorial_Semana_04_Encontro_2.md` (Parte 3 + Desafio).

**Tipo:** B — as variáveis de exemplo (`itens_coletados: int`, `progresso_atual`, `porta_principal_aberta`) são sugestões explícitas do tutorial ("por exemplo"); a variável final fica a critério de quem implementa.

**Arquivos Esperados:** modificação em `save_manager.gd`, `game_manager.gd`; nova Scene temporária `res://scenes/levels/exploration/level_teste_persistencia.tscn` (descartável, não faz parte do nível final).

**Implementação:**
1. Em `save_manager.gd`, declarar uma variável persistente (`# PLACEHOLDER: exemplo do tutorial — itens_coletados: int`) e uma função para alterá-la.
2. Criar `level_teste_persistencia.tscn` (Node3D + Label3D) apenas para o teste.
3. No Player, acionar temporariamente a função via uma tecla livre; validar incremento.
4. Trocar a Main Scene para `level_teste_persistencia.tscn`, confirmar que o valor persiste; reverter a Main Scene para `level_exploration.tscn`.
5. Adicionar ao `GameManager` uma variável de estado de partida própria (desafio do Encontro 1), comentando por que pertence ao `GameManager` e não a uma Scene.
6. Remover código de teste temporário (prints, tecla de debug) ao final.

**Restrições:** nenhuma variável de teste deve permanecer hardcoded fora do Autoload; a Main Scene do projeto deve terminar revertida para `level_exploration.tscn`.

**Testes:** troca de cena real (não apenas leitura de código); Output confirma valor mantido.

**Critérios de Aceite:**
- [ ] Variável do `SaveManager` confirmadamente persistente entre duas Scenes reais.
- [ ] Variável de estado própria no `GameManager`, comentada.
- [ ] Main Scene revertida; nenhum código de teste residual.

**Definition of Done:** checklist dos dois tutoriais da Semana 4 100%.

**Dependências:** Blocked By: IC-VS04-02. Blocks: IC-VS05-01.

**Story Points:** 3

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
1. Criar `Door.tscn` em `scenes/interactables/`: Node raiz (ex.: `Area3D` ou `StaticBody3D`, conforme a detecção escolhida), `CollisionShape3D`, `MeshInstance3D` (Kenney Dungeon Kit).
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

**Dependências:** Blocked By: IC-VS06-01. Blocks: IC-VS07-01.

**Story Points:** 2

---

## IC-VS06-03 — Aplicação do ItemData a um Objeto Coletável em Cena

**STATUS: BLOQUEADO — Tipo C. Nenhum passo de implementação é definido aqui.**

**Motivo:** não existe, em nenhum documento-fonte (`PROJECT_ARCHITECTURE.md`, Cronograma, ou qualquer Tutorial das Semanas 5–7), uma especificação de como uma Scene `Chest`/`Pickup` é construída, qual Signal ela emite, ou para onde o item coletado vai antes do `InventoryComponent` existir (Semana 10). Inventar essa implementação aqui violaria a Regra Absoluta do plano.

**Ver:** `Design_Backlog/Design_Cards.md` → **DC-01**.

**Dependências:** Blocked By: DC-01. Blocks: IC-VS07-04, IC-VS10-01.

**Story Points:** não estimado (carta não existe até DC-01 ser resolvido).

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

**Contexto:** terceira etapa da Semana 7, Encontro 1 — fecha o conjunto de sistemas novos do Módulo 2.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §8; `Tutorial_Semana_07_Encontro_1.md` (Parte 3).

**Tipo:** A

**Arquivos Esperados:** `res://scenes/interactables/Checkpoint.tscn`

**Implementação:**
1. Criar `Checkpoint.tscn` em `scenes/interactables/`: `Area3D` + `CollisionShape3D` + malha/marcador visual (Prototype ou Dungeon Kit).
2. Implementar `interact()` (mesmo contrato de `Door`/`Lever`, via `has_method`).
3. Dentro de `interact()`, obter referência ao `SaveComponent` e chamar `salvar()`, passando itens coletados atuais e um `id_checkpoint` (campo `@export` próprio, único por instância).
4. Posicionar ao menos uma instância no nível.

**Restrições:** não reimplementar detecção de proximidade dentro do `Checkpoint` — reutilizar o `InteractionComponent` já existente no Player. Nunca chamar `ResourceSaver`/`FileAccess` diretamente — sempre via `SaveComponent`.

**Testes:** interagir com o Checkpoint; confirmar atualização do arquivo em `user://`; coletar um item, interagir, fechar/reabrir o jogo, confirmar persistência via `carregar()`.

**Critérios de Aceite:**
- [ ] `Checkpoint` implementa `Interactable`, aciona `SaveComponent.salvar()`, com `id_checkpoint` único.

**Definition of Done:** checklist do Tutorial (Semana 7, Encontro 1) 100%.

**Dependências:** Blocked By: IC-VS07-02, IC-VS05-03. Blocks: IC-VS07-04.

**Story Points:** 3

---

## IC-VS07-04 — Integração Final do Módulo 2 (Fluxo Único + Code Review + Playtest) 🔴

**Objetivo:** conectar porta, alavanca, (baú — ver ressalva) e checkpoint em um único fluxo percorrível, e passar por Code Review/Playtest de encerramento da Unidade II.

**Contexto:** Encontro 2 da Semana 7 — não introduz sistema novo, apenas integra o que já existe.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6 ("Produto do Módulo 2"); `Tutorial_Semana_07_Encontro_2.md`.

**Tipo:** A para a integração de Door/Lever/Checkpoint; **a integração de um "baú" está BLOQUEADA — Tipo C, ver DC-01** (não incluir Chest no fluxo até DC-01 ser resolvido; registrar a ausência como pendência explícita).

**Arquivos Esperados:** reposicionamento de instâncias existentes em `level_exploration.tscn` (nenhum arquivo novo).

**Implementação:**
1. Posicionar/reposicionar `Door`, `Lever` (ou equivalente) e `Checkpoint` formando um caminho único, início a fim.
2. Confirmar que a alavanca controla a porta via o Signal já conectado (Semana 5).
3. Posicionar o `Checkpoint` em um ponto lógico do caminho (ex.: após a primeira sala resolvida).
4. Percorrer o caminho completo; fechar e reabrir o jogo; confirmar progresso recuperado.
5. Preparar e apresentar a justificativa de arquitetura de cada sistema do módulo (Code Review, Rubrica 4).
6. Realizar Playtest coletivo (ou, em contexto solo, testar com uma pessoa externa ao desenvolvimento).

**Restrições:** preferir conectar sistemas existentes a criar novos objetos nesta carta — o objetivo é integração, não expansão de escopo. Não incluir um "baú" funcional enquanto DC-01 estiver aberto — se incluído antes da resolução, deve ser documentado como protótipo temporário, não como sistema definitivo.

**Testes:** percurso completo do fluxo, com fechamento/reabertura do jogo no meio do teste.

**Critérios de Aceite:**
- [ ] Porta, alavanca e checkpoint conectados em um único fluxo, sem retrabalho estrutural.
- [ ] Progresso persistido confirmado após reiniciar o jogo.
- [ ] Code Review e Playtest coletivo realizados.
- [ ] Pendência de "baú" (DC-01) registrada explicitamente se ainda não resolvida.

**Definition of Done:** encerramento da Unidade II conforme o Cronograma (Semana 7 🔴).

**Dependências:** Blocked By: IC-VS07-03. Blocks: todo o Milestone MS-3 (VS-08 em diante).

**Story Points:** 3
