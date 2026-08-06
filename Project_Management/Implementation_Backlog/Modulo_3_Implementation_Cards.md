# Implementation Cards — Milestone MS-3 (Semanas 8–11)

**Nota de fonte:** a partir do Módulo 3 não existem Tutoriais passo a passo (regra pedagógica — Challenge Based Learning, ver `PEDAGOGICAL_RULES.md`). As cartas abaixo são derivadas de `PROJECT_ARCHITECTURE.md` §6/§7 e do Cronograma (Semanas 8–11), que descrevem o sistema e o conceito, mas deliberadamente não descrevem clique-a-clique. Por isso, a maioria das cartas aqui é **Tipo B** mesmo quando a arquitetura está clara — o valor de "quanto" (vida, dano, raio de detecção) fica em aberto por design da disciplina, não por omissão deste plano.

---

## IC-VS08-01 — Substituição da CapsuleMesh pelo Modelo Animado (Kenney Mini Characters)

**Objetivo:** trocar o placeholder visual do Player por um modelo com esqueleto e animações reais.

**Contexto:** pré-requisito de toda a semana — sem um modelo animado, não há AnimationTree possível (uma `CapsuleMesh` não tem animações).

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §3, §7; `Cronograma` (Semana 8).

**Tipo:** A

**Arquivos Esperados:** modificação em `Player.tscn` (substituição do Node `Malha`).

**Implementação:**
1. Remover a `CapsuleMesh` do Node `Malha` (manter o Node `CollisionShape3D` irmão intacto — não é afetado pela troca).
2. Instanciar o modelo do Kenney Mini Characters (`assets/characters/`) como filho de `Player`, no lugar da malha antiga.
3. Confirmar que o `AnimationPlayer` do modelo importado contém as animações idle/walk/run (aba Import).
4. Realinhar visualmente o novo modelo sobre a `CollisionShape3D` existente.

**Restrições:** não remover ou recriar a `CollisionShape3D` — só a malha visual é trocada.

**Testes:** F6; Player aparece com o novo modelo, alinhado à colisão, sem regressão de movimento (IC-VS02-02).

**Critérios de Aceite:**
- [ ] Modelo do Kenney Mini Characters substitui a `CapsuleMesh`, com `AnimationPlayer` funcional.

**Definition of Done:** nenhuma regressão em nenhum sistema do Módulo 1/2; animações confirmadas na aba Import.

**Dependências:** Blocked By: IC-VS07-04, IC-VS01-02. Blocks: IC-VS08-03.

**Story Points:** 2

---

## IC-VS08-02 — HealthComponent (Vida, Dano, Morte)

**Objetivo:** criar o Component reutilizável de vida/dano.

**Contexto:** primeiro Component do Módulo 3; será reutilizado pelo `Enemy` na Semana 11 sem duplicação.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §10; `Cronograma` (Semana 8).

**Tipo:** B — nenhum valor numérico de vida máxima ou de dano é especificado em nenhum documento-fonte (diferente da velocidade de movimento, aqui não há sequer um exemplo).

**Arquivos Esperados:** `res://scripts/components/health_component.gd` (ou Orchestration `orchestrations/health_component.torch`).

**Implementação:**
1. Criar `HealthComponent` (Node customizado), via Orchestrator ou GDScript (ambos igualmente válidos, ver `PROJECT_ARCHITECTURE.md` §6).
2. Propriedades: `vida_atual`, `vida_maxima` (**PLACEHOLDER**: definir um valor de exemplo, ex. 100, comentado como "aguardando definição em PROJECT_ARCHITECTURE.md").
3. Método público `apply_damage(quantidade: int) -> void`, reduzindo `vida_atual` e clampando em zero.
4. Sinal `died`, emitido quando `vida_atual` chega a zero.
5. Adicionar como Node filho de `Player`.

**Restrições:** `HealthComponent` não deve conhecer quem é seu dono (Player ou Enemy) — apenas expor vida, dano e o sinal `died`. Nenhuma reação a `died` é implementada nesta carta do lado do Player (ver DC-03 — bloqueado).

**Testes:** chamar `apply_damage` via debug; confirmar redução de vida e emissão de `died` ao chegar a zero.

**Critérios de Aceite:**
- [ ] `HealthComponent` funcional, testável isoladamente, com placeholder de vida documentado no código.

**Definition of Done:** Component genérico o suficiente para ser reaproveitado pelo Enemy (IC-VS11-01) sem alteração. **A reação ao `died` do Player permanece não implementada — Blocked By: DC-03.**

**Dependências:** Blocked By: IC-VS08-01. Blocks: IC-VS08-03, IC-VS09-01, IC-VS11-01 (reuso).

**Story Points:** 3

---

## IC-VS08-03 — AnimationTree: State Machine de Locomoção

**Objetivo:** transicionar entre idle/andar/correr conforme o movimento real do Player.

**Contexto:** segunda metade do Encontro 1 da Semana 8.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §12 (comparação com Animator Controller); `Cronograma` (Semana 8).

**Tipo:** A (estrutura totalmente especificada — AnimationTree/AnimationNodeStateMachine com 3 estados nomeados no próprio Cronograma).

**Arquivos Esperados:** modificação em `Player.tscn` (Node `AnimationTree`).

**Implementação:**
1. Adicionar Node `AnimationTree` como filho de `Player`, referenciando o `AnimationPlayer` do modelo (IC-VS08-01).
2. Configurar `AnimationNodeStateMachine` com 3 estados: idle, andar, correr.
3. Condicionar transições a uma variável real de movimento (ex.: magnitude de `velocity`), lida a partir da mesma Orchestration/script que já controla `move_and_slide` (IC-VS02-02).

**Restrições:** transições nunca incondicionais ("sempre transicionar"/"nunca transicionar") — cada uma depende de uma variável real de gameplay.

**Testes:** mover o Player nas 4 direções e observar transição idle → andar → correr coerente com a velocidade real.

**Critérios de Aceite:**
- [ ] State Machine com 3 estados, transições condicionadas corretamente.

**Definition of Done:** transições visíveis e coerentes durante o gameplay real (não apenas no preview do AnimationTree).

**Dependências:** Blocked By: IC-VS08-01, IC-VS08-02. Blocks: IC-VS08-04.

**Story Points:** 5

---

## IC-VS08-04 — BlendSpace/AnimationPlayer: Animação Contextual

**Objetivo:** conectar uma animação (contínua ou pontual) a um evento real de gameplay.

**Contexto:** Encontro 2 da Semana 8 — desafio de escolha própria entre dois mecanismos.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6; `Cronograma` (Semana 8, Encontro 2).

**Tipo:** B — "cada grupo propõe e implementa uma animação contextual própria... com liberdade de solução" (explícito no Cronograma).

**Arquivos Esperados:** modificação em `Player.tscn` (AnimationTree ampliado ou faixa adicional no AnimationPlayer).

**Implementação:**
1. Escolher entre BlendSpace1D/2D (para movimento direcional contínuo) ou uma faixa pontual do AnimationPlayer (para evento discreto).
2. Conectar a animação escolhida a um evento real já existente: `HealthComponent.apply_damage`/`died`, ou o Signal `interacted`/equivalente de um objeto do contrato `Interactable`.
3. Justificar a escolha (contínuo × discreto) em comentário no código.

**Restrições:** a animação deve se sobrepor à State Machine de locomoção (IC-VS08-03) sem substituí-la ou quebrá-la.

**Testes:** acionar o evento real escolhido (ex.: tomar dano via debug) e confirmar a animação correspondente, sem interromper a locomoção de base.

**Critérios de Aceite:**
- [ ] Animação contextual conectada a um evento real, com justificativa registrada.

**Definition of Done:** State Machine de locomoção (IC-VS08-03) permanece funcional após a integração.

**Dependências:** Blocked By: IC-VS08-03. Blocks: IC-VS09-01.

**Story Points:** 5

---

## IC-VS09-01 — Control Simples Vinculado ao HealthComponent

**Objetivo:** exibir a vida do Player em tempo real na tela.

**Contexto:** primeira etapa da Semana 9.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7; `Cronograma` (Semana 9, Encontro 1).

**Tipo:** A

**Arquivos Esperados:** `res://scenes/ui/` (Control temporário, absorvido pelo HUD em IC-VS09-02).

**Implementação:**
1. Criar um Control (Label) organizado por container e posicionado por anchor.
2. Ler o valor de `HealthComponent.vida_atual` do Player (binding via Orchestrator ou GDScript) e atualizar o Label a cada mudança (via Signal customizado no `HealthComponent`, ex. `vida_alterada`, ou `_process`).

**Restrições:** o Control deve apenas ler o valor exposto pelo `HealthComponent`, nunca duplicar ou recalcular o estado de vida.

**Testes:** reduzir a vida via debug e confirmar atualização imediata do Label.

**Critérios de Aceite:**
- [ ] Label exibe a vida atual em tempo real, sem duplicar o dado.

**Definition of Done:** nenhuma lógica de gameplay dentro do Control.

**Dependências:** Blocked By: IC-VS08-04. Blocks: IC-VS09-02.

**Story Points:** 2

---

## IC-VS09-02 — HUD Completo (CanvasLayer)

**Objetivo:** organizar múltiplos elementos de interface (vida + um segundo dado) sob uma única camada sempre visível.

**Contexto:** segunda etapa da Semana 9.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7 (HUD); `Cronograma` (Semana 9, Encontro 2).

**Tipo:** B — o Cronograma deixa explicitamente a critério de quem implementa "quais dados de gameplay já existentes... devem compor o HUD".

**Arquivos Esperados:** `res://scenes/ui/HUD.tscn`

**Implementação:**
1. Criar `HUD.tscn`: `CanvasLayer` raiz, contendo o Control de vida (IC-VS09-01) e ao menos um segundo dado (**PLACEHOLDER**: `SaveManager.itens_coletados`, até o `InventoryComponent` da VS-10 fornecer um dado mais completo).
2. Instanciar `HUD.tscn` em `level_exploration.tscn`.

**Restrições:** nenhum dado exibido pode ser exclusivo da UI — todo elemento do HUD espelha um sistema que já existe (`HealthComponent`, `SaveManager`).

**Testes:** F6; HUD permanece visível e atualizado durante o gameplay, incluindo sobre o terreno 3D.

**Critérios de Aceite:**
- [ ] HUD funcional sobre `CanvasLayer`, exibindo vida e um segundo dado real, em tempo real.

**Definition of Done:** Feedback formal (Semana 9) recebido.

**Dependências:** Blocked By: IC-VS09-01. Blocks: IC-VS09-03, IC-VS10-02 (InventoryUI reaproveita o mesmo padrão).

**Story Points:** 3

---

## IC-VS09-03 — PauseMenu

**Objetivo:** aplicar Control nodes a um segundo caso de interface, sobre o `GameManager`.

**Contexto:** extensão do desafio de HUD, mesma semana.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6, §7 (PauseMenu); `Cronograma` (Semana 9).

**Tipo:** B — opções de menu além de "retomar" não são especificadas em nenhum documento-fonte.

**Arquivos Esperados:** `res://scenes/ui/PauseMenu.tscn`

**Implementação:**
1. Criar `PauseMenu.tscn` (Control), com ao menos um botão "Retomar".
2. Conectar a uma Action de alto nível do Input Map (ex.: `pausar`) no script do Player, pausando a árvore (`get_tree().paused = true`) e exibindo o menu.
3. **PLACEHOLDER**: opções adicionais (ex.: "Sair") ficam a critério de quem implementa — nenhuma é obrigatória pelo Cronograma.

**Restrições:** o Player deve centralizar a leitura da Action de pausa (reforça a escolha arquitetural sem Pawn/Controller, `PROJECT_ARCHITECTURE.md` §12).

**Testes:** acionar a Action de pausa; confirmar que o jogo pausa e o menu aparece; retomar e confirmar despausa.

**Critérios de Aceite:**
- [ ] `PauseMenu` funcional, ao menos com opção de retomar.

**Definition of Done:** nenhuma regressão em HUD (IC-VS09-02) ao pausar/despausar.

**Dependências:** Blocked By: IC-VS09-02. Blocks: nenhuma direta (não bloqueia o restante do módulo).

**Story Points:** 2

---

## IC-VS10-01 — InventoryComponent

**Objetivo:** estruturar armazenamento de itens coletados.

**Contexto:** primeira etapa da Semana 10.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7 (InventoryComponent); `Cronograma` (Semana 10, Encontro 1).

**Tipo:** B — capacidade máxima e regras de duplicidade não são especificadas em nenhum documento-fonte; o Cronograma remete a esse detalhamento apenas no desafio do Encontro 2 (empilhar/combinar), como escolha livre.

**Arquivos Esperados:** `res://scripts/components/inventory_component.gd`

**Implementação:**
1. Criar `InventoryComponent` (Node customizado), com uma coleção (`Array[ItemData]`) e métodos `adicionar_item(item: ItemData)`, `remover_item(item: ItemData)`.
2. **PLACEHOLDER**: nenhum limite de capacidade nesta carta (comentar explicitamente que é ilimitado até decisão em contrário).
3. Adicionar como Node filho de `Player`.
4. Testar via chamada manual de `adicionar_item()` com uma instância `.tres` existente (Semana 6) — **a população via gameplay real (coletar de um `Chest`) depende de DC-01/IC-VS06-03 e não é parte desta carta.**

**Restrições:** o `InventoryComponent` não deve conhecer detalhes de UI — apenas expor os dados para a `InventoryUI` (IC-VS10-02) consultar.

**Testes:** chamada manual de `adicionar_item`/`remover_item` via debug; confirmar estado interno correto.

**Critérios de Aceite:**
- [ ] `InventoryComponent` funcional isoladamente (testável sem depender de `Chest`/`Pickup`).

**Definition of Done:** pronto para ser consumido pela `InventoryUI`; população real via gameplay marcada como pendente (DC-01).

**Dependências:** Blocked By: IC-VS09-03. Blocks: IC-VS10-02.

**Story Points:** 3

---

## IC-VS10-02 — InventoryUI

**Objetivo:** exibir os itens armazenados no `InventoryComponent`.

**Contexto:** mesma etapa da Semana 10, consumindo o Component da carta anterior.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7; `Cronograma` (Semana 10).

**Tipo:** A (padrão de binding já estabelecido em IC-VS09-01/02).

**Arquivos Esperados:** `res://scenes/ui/InventoryUI.tscn`

**Implementação:**
1. Criar `InventoryUI.tscn` (Control), lendo a coleção exposta por `InventoryComponent`.
2. Atualizar a exibição a cada alteração (Signal customizado no Component, ex. `inventario_alterado`).

**Restrições:** mesmo princípio de HC-09 — a UI só lê, nunca duplica o estado do inventário.

**Testes:** adicionar/remover item via debug (IC-VS10-01) e confirmar atualização imediata da UI.

**Critérios de Aceite:**
- [ ] `InventoryUI` reflete corretamente o estado do `InventoryComponent` em tempo real.

**Definition of Done:** integrável ao HUD (IC-VS09-02) sem conflito visual.

**Dependências:** Blocked By: IC-VS10-01. Blocks: IC-VS10-03.

**Story Points:** 2

---

## IC-VS10-03 — Ampliação da Interação (Novo Tipo)

**Objetivo:** suportar um novo tipo de interação conectado ao inventário.

**Contexto:** desafio da Semana 10, Encontro 2 — avaliado por Code Review.

**Documentos de Referência:** `Cronograma` (Semana 10, Encontro 2).

**Tipo:** B — "empilhar itens, combinar itens, ou interação com cooldown... com solução própria", explicitamente livre.

**Arquivos Esperados:** modificação no contrato `Interactable` e/ou em `InventoryComponent`, conforme a escolha.

**Implementação:**
1. Escolher um novo tipo de interação (empilhamento, combinação ou cooldown).
2. Implementar sem duplicar a detecção já existente no `InteractionComponent` (IC-VS05-02).
3. Conectar ao `InventoryComponent` (IC-VS10-01).

**Restrições:** não recriar o `InteractionComponent` — estender o contrato existente.

**Testes:** cenário específico do tipo escolhido (ex.: coletar dois itens iguais e confirmar empilhamento).

**Critérios de Aceite:**
- [ ] Novo tipo de interação funcional, integrado ao inventário.

**Definition of Done:** Code Review dos sistemas de inventário/interação (Semana 10) cumprido.

**Dependências:** Blocked By: IC-VS10-02. Blocks: IC-VS11-01.

**Story Points:** 3

---

## IC-VS10-04 — Persistência do Inventário no SaveData

**STATUS: BLOQUEADO — Tipo C. Nenhum passo de implementação é definido aqui.**

**Motivo:** `SaveData` (IC-VS07-01) só define `itens_coletados: Array[String]` — insuficiente para representar `ItemData` completos armazenados pelo `InventoryComponent`. Não há decisão registrada em `PROJECT_ARCHITECTURE.md` sobre o schema correto (caminhos de recurso? serialização direta?).

**Ver:** `Design_Backlog/Design_Cards.md` → **DC-05**.

**Dependências:** Blocked By: DC-05. Blocks: IC-VS14-02.

**Story Points:** não estimado.

---

## IC-VS11-01 — NavigationRegion3D + Enemy (Deslocamento Básico)

**Objetivo:** dar a um agente não-jogador a capacidade de se deslocar até um ponto sem input direto.

**Contexto:** primeira etapa da Semana 11, Encontro 1.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7 (Enemy), §3 (skin do Mini Characters); `Cronograma` (Semana 11, Encontro 1).

**Tipo:** A (estrutura totalmente especificada); a skin/aparência do Enemy é Tipo B (reaproveita o mesmo pacote do Player, skin alternativa — "se só houver uma skin, usar Material Override de cor diferente").

**Arquivos Esperados:**
```
res://scenes/characters/Enemy.tscn
(bake de NavigationRegion3D em level_exploration.tscn ou level_dungeon.tscn)
```

**Implementação:**
1. Adicionar `NavigationRegion3D` ao nível, com bake da malha de navegação sobre a geometria existente.
2. Criar `Enemy.tscn` (CharacterBody3D), reaproveitando o modelo do Kenney Mini Characters (IC-VS08-01) com skin distinta.
3. Adicionar `NavigationAgent3D`; mover o Enemy até um ponto-alvo de teste, sem lógica de decisão ainda.
4. Adicionar `HealthComponent` (IC-VS08-02) ao `Enemy`, sem duplicar a implementação — mesmo Component do Player.

**Restrições:** não confundir `NavigationAgent3D` com `move_and_slide` de input direto — o agente delega o cálculo de rota ao `NavigationServer`.

**Testes:** Enemy se desloca até o ponto-alvo sem colidir com obstáculos.

**Critérios de Aceite:**
- [ ] `NavigationRegion3D` calculado; `Enemy` se desloca corretamente via `NavigationAgent3D`; `HealthComponent` reaproveitado sem duplicação.

**Definition of Done:** malha de navegação cobre corretamente as áreas de circulação pretendidas.

**Dependências:** Blocked By: IC-VS10-03, IC-VS08-02. Blocks: IC-VS11-02.

**Story Points:** 5

---

## IC-VS11-02 — Behavior Tree + Blackboard (LimboAI)

**Objetivo:** dar ao Enemy a capacidade de decidir entre patrulhar e perseguir.

**Contexto:** segunda etapa da Semana 11, Encontro 2.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §13 (fora do escopo: IA avançada); `Cronograma` (Semana 11, Encontro 2); `Plano_de_Aula_Semana_11.md`.

**Tipo:** B — raio de detecção/perseguição e o padrão exato de patrulha não são especificados numericamente em nenhum documento; a estrutura (Behavior Tree + Blackboard) está totalmente definida.

**Arquivos Esperados:** tasks customizadas (`.gd`, extends `BTAction`/`BTCondition` — **exigência do addon LimboAI, GDScript obrigatório, o Orchestrator não gera esse tipo de classe**).

**Implementação:**
1. Instalar/confirmar o addon LimboAI.
2. Criar uma Behavior Tree simples (`BTPlayer` + árvore) com patrulha (deslocamento entre pontos via `NavigationAgent3D`, IC-VS11-01) e perseguição (mudança de alvo ao detectar o Player).
3. Usar um Blackboard para memória compartilhada (ex.: última posição conhecida do Player).
4. **PLACEHOLDER**: raio de detecção do Player (comentar como valor de exemplo, aguardando ajuste por playtesting).
5. Implementar um comportamento autônomo adicional, de livre escolha (patrulha estendida, alerta, fuga).

**Restrições:** as tasks customizadas (`BTAction`/`BTCondition`) devem ser GDScript — não é possível usar Orchestrator aqui, ao contrário de outros sistemas do projeto. Não reimplementar deslocamento manualmente dentro da árvore — delegar ao `NavigationAgent3D` já configurado.

**Testes:** Enemy patrulha entre pontos; ao detectar o Player dentro do raio placeholder, muda para perseguição.

**Critérios de Aceite:**
- [ ] Behavior Tree decide corretamente entre patrulha/perseguição; comportamento adicional funcional.

**Definition of Done:** Behavior Tree não excede o escopo de patrulha/perseguição básicas (IA avançada é Fora do Escopo, `PROJECT_ARCHITECTURE.md` §13).

**Dependências:** Blocked By: IC-VS11-01. Blocks: IC-VS11-03.

**Story Points:** 5

---

## IC-VS11-03 — Combate Simples (Area3D/RayCast3D → apply_damage)

**Objetivo:** o Player causa dano ao Enemy através de uma detecção de acerto simples.

**Contexto:** terceira etapa da Semana 11 — reaproveita `HealthComponent` sem duplicação.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §4 (Escopo — "uma forma de ataque do jogador, dano e vida"), §7; `Cronograma` (Semana 11, Encontro 2).

**Tipo:** B — o valor de dano por ataque, o alcance e o cooldown não têm nenhum valor (nem exemplo) especificado em `PROJECT_ARCHITECTURE.md`.

**Arquivos Esperados:** modificação em `Player.tscn` (Area3D ou RayCast3D de ataque).

**Implementação:**
1. Adicionar `Area3D` (ou `RayCast3D`) ao Player, representando o alcance de ataque.
2. Ao detectar o `Enemy` dentro da área/raio e a Action de ataque ser acionada, chamar `HealthComponent.apply_damage()` do Enemy (via Orchestrator ou GDScript).
3. **PLACEHOLDER**: valor de dano e cooldown de ataque (comentar como exemplo, aguardando ajuste por playtesting/definição em `PROJECT_ARCHITECTURE.md`).

**Restrições:** a chamada de dano deve usar o mesmo método público `apply_damage` já definido em IC-VS08-02 — nenhuma lógica de dano duplicada.

**Testes:** Player ataca o Enemy dentro do alcance; vida do Enemy reduz corretamente; ataque fora do alcance não produz efeito.

**Critérios de Aceite:**
- [ ] Combate funcional, sem duplicar lógica de `HealthComponent`.

**Definition of Done:** valores de placeholder (dano, cooldown) documentados no código.

**Dependências:** Blocked By: IC-VS11-02. Blocks: IC-VS11-04.

**Story Points:** 3

---

## IC-VS11-04 — Reação à Morte do Player e do Enemy 🔴

**STATUS: PARCIALMENTE BLOQUEADO — Tipo C.**

**O que PODE ser implementado (Tipo A, não bloqueado):** os sinais `died` de ambos os `HealthComponent` (Player e Enemy) já existem desde IC-VS08-02/IC-VS11-01 e podem ser emitidos corretamente quando a vida chega a zero — isso não depende de nenhuma decisão pendente.

**O que NÃO pode ser implementado nesta carta:** qualquer reação a esses sinais — respawn do Player, tela de game over, remoção/drop do Enemy — porque nenhuma dessas decisões existe em `PROJECT_ARCHITECTURE.md`. Implementá-las aqui seria inventar uma regra.

**Ver:** `Design_Backlog/Design_Cards.md` → **DC-03** (morte do Player) e **DC-04** (morte do Enemy).

**Dependências:** Blocked By: DC-03, DC-04. Blocks: fechamento formal da Definition of Done de VS-11 (o Milestone MS-3 pode ser considerado tecnicamente jogável sem isso, mas não "completo" quanto a consequência de derrota/vitória).

**Story Points:** não estimado (a parte não bloqueada — apenas confirmar emissão do sinal — já está coberta por IC-VS08-02/IC-VS11-03; nenhum ponto adicional é atribuído a uma implementação que não existe).
