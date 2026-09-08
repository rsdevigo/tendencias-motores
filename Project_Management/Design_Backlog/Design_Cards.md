# Design Cards

Estes são os gaps **Tipo C** encontrados na leitura completa de `PROJECT_ARCHITECTURE.md`, do Cronograma e de todos os Tutoriais (Semanas 1–7). Cada um bloqueia pelo menos um Implementation Card. Nenhum deles pode ser resolvido "por bom senso" durante a implementação — a decisão precisa ser registrada em `PROJECT_ARCHITECTURE.md` primeiro (ver campo "Critério de Conclusão" de cada card).

Importante: isto **não** inclui lacunas numéricas simples (velocidade de movimento, dano por ataque, vida máxima, capacidade de inventário) — essas são Tipo B, já endereçadas como placeholder dentro dos próprios Implementation Cards, muitas vezes por escolha pedagógica deliberada ("com liberdade de solução"). Um Design Card só existe aqui quando **não há estrutura suficiente para sequer propor um placeholder coerente**.

---

## DC-01 — Construção de `Chest`/`Pickup` nunca especificada

**Objetivo:** definir como um item (`ItemData`) chega efetivamente a um objeto coletável em cena, e o que "coletar" significa mecanicamente.

**Problema de Design:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2) lista a linha `Chest, Pickup | Aplicar ItemData a coleta de itens | Resource customizado | ItemData, Interação`, e §7 lista `Door, Lever, Chest, Pickup` como "Cenas concretas que implementam o contrato Interactable". Porém, nenhum Tutorial (Semanas 5, 6 ou 7 — os três candidatos naturais) contém um passo sequer de criação de `Chest.tscn` ou `Pickup.tscn`. O Tutorial da Semana 7 (Encontro 2, Parte 1, passo 4) chega a instruir "confirme que ao menos um baú (`Chest`) no caminho concede um item", tratando a Scene como se já existisse — mas ela nunca foi construída em nenhum tutorial anterior. Sem esta Scene, `ItemData` (Semana 6) fica sem nenhum consumidor real em jogo, e o `InventoryComponent` (Semana 10) não tem de onde receber itens via gameplay.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §6 (linha "Chest, Pickup") e §7 (linha "Door, Lever, Chest, Pickup").

**Decisões necessárias:**
1. `Chest` é um contêiner com estado (aberto/fechado, um único item) ou uma fonte repetível? `Pickup` é um item já visível no chão (coleta instantânea ao interagir) ou idêntico ao Chest com outra malha?
2. O Signal emitido é o mesmo `interacted` genérico (como Door/Lever) ou um Signal próprio (ex.: `item_granted(item: ItemData)`)?
3. Para onde vai o item coletado **entre a Semana 6/7 (quando `Chest` precisaria existir) e a Semana 10 (quando `InventoryComponent` é criado)**? O `SaveData.itens_coletados: Array[String]` (Semana 7) é o destino provisório correto, ou isso também precisa de decisão?
4. Um `Chest` pode ser reaberto/reutilizado, ou fica marcado como "vazio" permanentemente (e isso precisa persistir no save)?

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §6, §7, §9 (nomenclatura); `Tutorial_Semana_06_Encontro_1.md` (cria `ItemData` sem consumidor); `Tutorial_Semana_07_Encontro_1.md` e `_Encontro_2.md` (assumem `Chest` já existente).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §6 e §7 atualizados com uma linha própria para `Chest`/`Pickup` no mesmo nível de detalhe já dado a `Door`/`Lever` (ver §7, linha Door/Lever/Checkpoint) — Node raiz, Signal, e o destino do item coletado até a Semana 10 existir.

**Impacto na implementação:** bloqueia IC-VS06-03 (aplicação prática do `ItemData`) e IC-VS07-04 (integração de "baú" ao fluxo do Módulo 2). Sem resolução, VS-07 e VS-10 devem ser entregues com essa pendência registrada explicitamente (ver Definition of Done de ambas em `Vertical_Slices.md`).

**STATUS: RESOLVIDO (2026-09-02).** Registrado em `PROJECT_ARCHITECTURE.md` §6 (Módulo 2) e §7 (Scenes principais + parágrafo de fluxo do item coletado).

**Decisões tomadas:**
1. **`Pickup`** (`Node3D`, Semana 7, Encontro 1): item visível no mundo, de uso único. Implementa `interact()` (mesmo contrato de Door/Lever/Chest — um único modelo de interação no Módulo 2). Expõe `@export var item: ItemData`. Ao ser interagido, emite `item_collected(item)` e faz `queue_free()`.
2. **`Chest`** (`Node3D`, Semana 7, Encontro 1): contêiner de uso único com estado `aberto: bool`. Implementa `interact()`. Expõe **um único** `@export var item: ItemData`. Na primeira interação passa a `aberto`, emite `item_collected(item)` uma vez e permanece aberto/vazio; interações seguintes não têm efeito. `Array[ItemData]` fica como extensão opcional, fora do escopo do Módulo 2.
3. **Signal:** o contrato `interact()` permanece genérico e sem retorno. `Door`/`Lever` reagem ao Signal genérico `interacted` e **não** concedem itens; `Pickup`/`Chest` declaram Signal próprio `item_collected(item: ItemData)` (nome alinhado a §9).
4. **Destino do item (Semanas 6–10):** `Chest`/`Pickup` não conhecem inventário nem save. Um handler único (nó do nível ou `GameManager`) recebe `item_collected` e, até a Semana 9, adiciona `item.nome` (`String`) à lista `itens_coletados` do `SaveManager`, gravada no `SaveData` pelo `SaveComponent` ao alcançar um `Checkpoint` (Semana 7). A partir da Semana 10, o mesmo handler repassa o `ItemData` ao `InventoryComponent`.
5. **Persistência do estado do baú:** não no Módulo 2. `Chest`/`Pickup` são de uso único em runtime; ao recarregar um save, o handler ignora item cujo `nome` já esteja em `itens_coletados` (idempotência), evitando duplicata. Persistência real do estado de objetos do mundo fica como item cruzado no **DC-05**.

**Local de construção:** `Pickup.tscn` e `Chest.tscn` passam a ser construídos no **Tutorial da Semana 7, Encontro 1** (nova Parte 3, antes do `Checkpoint`) — é o primeiro ponto do Cronograma em que `ItemData` (Semana 6) já existe e o resultado da coleta alimenta a persistência do `Checkpoint` na mesma aula.

---

## DC-02 — Definição mecânica do "objetivo final único"

**Objetivo:** definir o que precisa acontecer, em termos de jogo, para o Vertical Slice ser considerado "concluído" pelo jogador.

**Problema de Design:** `PROJECT_ARCHITECTURE.md` §4 (Escopo) lista, como item dentro do escopo: "Um objetivo final único que encerra o Vertical Slice." Esta é a única menção ao objetivo final em todo o documento — não há especificação de **qual** objetivo (chegar a um local? derrotar o Enemy? coletar um item específico? uma combinação?), nem de como ele é detectado (uma nova Area3D de "vitória"? uma condição verificada pelo `GameManager`?), nem do que acontece ao ser alcançado (tela de encerramento? apenas um log?). Diferente de um valor numérico com exemplo (como a velocidade de movimento), aqui não há nenhum ponto de partida — é um vazio de design, não um placeholder.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §2 (Conceito do Jogo) e §4 (Escopo).

**Decisões necessárias:**
1. Qual é o gatilho do objetivo final (localização, item, derrota do Enemy, ou combinação)?
2. Onde essa lógica vive — um novo Component, uma responsabilidade adicional do `GameManager`, ou uma Scene dedicada (`Objective.tscn`, análoga a `Checkpoint.tscn`)?
3. O que o jogador vê ao concluir (tela, HUD, apenas volta ao menu)? Pode espelhar a Scene `GameOver` do DC-03 (uma Scene `Victory` análoga, mesmo padrão Control + CanvasLayer).
4. O objetivo final depende do combate (DC-04) estar resolvido, ou é independente dele?

*Contexto do DC-03:* a condição de **derrota** já está definida (esgotar as tentativas → `GameOver`). O DC-02 é a condição de **vitória** simétrica — o `GameManager` já é o dono das "condições de vitória/derrota" no §7.

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §2, §4, §6 (nenhuma linha do roadmap trata disso explicitamente), §11 (a evolução do Vertical Slice não menciona onde o objetivo final é implementado).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §4 detalha o gatilho e a reação do objetivo final, e §6/§7 ganham uma linha/Scene correspondente, com uma semana de referência no roadmap (recomenda-se Módulo 3 ou 4, já que nenhuma semana do Cronograma o menciona explicitamente).

**Critério de Conclusão:** decisão registrada e refletida em `PROJECT_ARCHITECTURE.md` antes de IC-VS14-03 ser aberto.

**Impacto na implementação:** bloqueia IC-VS14-03. Sem resolução, o Milestone MS-4 não pode ser considerado formalmente concluído (não há "fim" jogável), embora o build ainda possa ser exportado e testado tecnicamente.

---

## DC-03 — Fluxo de morte/respawn do Player

**Objetivo:** definir o que acontece quando `HealthComponent.died` é emitido pelo Player.

**Problema de Design:** `PROJECT_ARCHITECTURE.md` §7 define `HealthComponent` com um sinal `died`, e §6 (Semana 8) descreve "sinal `died` emitido quando a vida chega a zero" — mas nenhum documento diz **quem escuta esse sinal quando o dono é o Player**, nem o que acontece a seguir. Volta ao último `Checkpoint`? Tela de game over? Reinício do nível? Isso é estruturalmente diferente de uma lacuna numérica: sem essa decisão, `died` é um sinal que existe mas não tem nenhum ouvinte definido no lado do Player, deixando o combate (Semana 11) sem consequência real de derrota.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §7 (linha HealthComponent) e §6 (Módulo 3, linha Combate simples).

**Decisões necessárias:**
1. Ao `died` do Player: respawn no último `Checkpoint.id_checkpoint` (via `SaveComponent.carregar()`), reinício total do nível, ou tela de game over com opção de retry?
2. A vida é restaurada ao máximo no respawn, ou mantém dano parcial?
3. Existe algum limite de "tentativas" (o `GameManager` já tem, desde a Semana 4, um exemplo de "contador de tentativas" no desafio do Encontro 1 — isso deveria se conectar aqui)?

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §7 (HealthComponent, Checkpoint, SaveComponent); `Cronograma` (Semana 8, Semana 11); `Tutorial_Semana_04_Encontro_1.md` (desafio de contador de tentativas, possível gancho).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §7 (linha HealthComponent) descreve o fluxo de morte do Player e sua integração com `Checkpoint`/`SaveComponent`.

**Impacto na implementação:** bloqueia parte de IC-VS08-02 (o sinal `died` pode ser implementado, mas nenhuma reação a ele pode ser codificada) e IC-VS11-04 (o combate fica sem consequência de derrota).

**STATUS: RESOLVIDO (2026-09-02).** Registrado em `PROJECT_ARCHITECTURE.md` §6 (Módulo 3: novas linhas "Fluxo de morte/respawn" e "GameOver"), §7 (linhas HealthComponent, GameManager, SaveManager, GameOver, SaveData + parágrafo "Fluxo de morte/respawn do Player"), §8 e §12.

**Decisões tomadas:**
1. **Reação ao `died` do Player:** respawn no último `Checkpoint` (ou `PlayerStart` se nenhum foi alcançado), reutilizando `GameManager.spawn_player()` (DC-06) — nenhum código novo de posicionamento. **Somada a um limite fixo de tentativas:** ao atingir `LIMITE_TENTATIVAS` mortes, o `GameManager` exibe a Scene `GameOver` (Control) em vez de respawnar.
2. **Vida no respawn:** restaurada ao máximo (`HealthComponent.reiniciar()`). Consequência: **a vida do Player não é persistida no `SaveData`** — resolve a decisão 2 do DC-05.
3. **Contador de tentativas:** `SaveManager.mortes: int`, incrementado a cada morte, persistido no `SaveData` (junto com `itens_coletados`/`ultimo_checkpoint`) e exposto ao HUD (Semana 9). `LIMITE_TENTATIVAS` é uma constante do `GameManager`, placeholder ajustável por grupo (ex.: 3).
4. **Wiring:** o Player conecta `HealthComponent.died` a um handler próprio que chama `GameManager.player_morreu()` — reação no `GameManager` (regra de partida), wiring no Player. Mesmo padrão do handler de coleta.
5. **`GameOver` (Control + CanvasLayer):** pausa a árvore; botão "Reiniciar" apaga `user://save_data.tres`, zera o `SaveManager` e recarrega o nível (Player volta ao `PlayerStart`). Base na Semana 8, refinada com o HUD na Semana 9.
6. **Construção:** Semana 8 (sem tutorial — Módulo 3+). Cartas IC-VS08-02 (parte do Player) e nova IC-VS08-05 (fluxo de morte + GameOver).

**Notas cruzadas:** define a condição de **derrota** do Vertical Slice; a **vitória** (objetivo final) fica no **DC-02**. O `mortes: int` no `SaveData` é o único acréscimo de schema aqui — a evolução maior (inventário real) segue no **DC-05**.

---

## DC-04 — Consequência da morte do Enemy

**Objetivo:** definir o que acontece quando `HealthComponent.died` é emitido pelo Enemy.

**Problema de Design:** simétrico ao DC-03, mas do lado do Enemy. `PROJECT_ARCHITECTURE.md` §7 diz que `Enemy` "reutiliza [HealthComponent] sem duplicação de lógica" — mas não diz o que acontece quando a vida do Enemy chega a zero: ele é removido da cena (`queue_free()`)? Fica em um estado "morto" na Behavior Tree (LimboAI) sem ser removido? Dropa algum item (o que reabriria a dependência de DC-01)? Isso é relevante inclusive para DC-02, caso o objetivo final envolva derrotar o Enemy.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §7 (linha Enemy) e §6 (Módulo 3, linha Enemy + Behavior Tree).

**Decisões necessárias:**
1. `Enemy` é removido da Scene (`queue_free()`) ou entra em um estado terminal (ex.: task `Dead` na Behavior Tree, mantendo o Node por eventuais animações de morte)?
2. A derrota do Enemy dropa item, contribui para o objetivo final (DC-02), ou é apenas remoção de obstáculo?
3. Existe apenas um `Enemy` no Vertical Slice (per "número reduzido de inimigos", §4), ou a morte de um precisa lidar com múltiplas instâncias?

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §4 (Escopo — "número reduzido de inimigos"), §7 (Enemy); `Cronograma` (Semana 11).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §7 (linha Enemy) descreve o comportamento ao morrer, e §4/§2 são atualizados se a morte do Enemy participar do objetivo final (dependência cruzada com DC-02).

**Impacto na implementação:** bloqueia IC-VS11-04 (o combate implementa `apply_damage`, mas não a reação a `died` do lado do Enemy).

---

## DC-05 — Evolução do schema de `SaveData` para os Módulos 3–4

**Objetivo:** definir como o `SaveData` (criado na Semana 7 com apenas `itens_coletados: Array[String]` e `ultimo_checkpoint: String`) passa a cobrir o estado introduzido nos Módulos 3 e 4 — inventário real (`ItemData`, não apenas nomes em `String`), vida do Player, e estado de inimigos/objetivo, se aplicável.

**Problema de Design:** `PROJECT_ARCHITECTURE.md` nunca revisita a definição de `SaveData` depois da Semana 7. O Tutorial da Semana 7 declara explicitamente `itens_coletados: Array[String]` — uma lista de nomes, não de referências a `ItemData` — o que já não é suficiente para representar o `InventoryComponent` da Semana 10 (que armazena `ItemData`, Resources completos, não Strings). Vida do `HealthComponent` (Semana 8) também não tem menção a persistência. Sem uma decisão aqui, o "build final consolidado" da Semana 14 não tem uma definição de o que exatamente é salvo.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §7 (linha SaveData) — atualmente descrita apenas como "objeto de Resource responsável por serializar o progresso do jogador (checkpoints, itens coletados)", sem detalhar o schema real após o Módulo 3.

**Decisões necessárias:**
1. `itens_coletados` passa a guardar caminhos de `.tres` (`Array[String]` com `res://resources/items/item_x.tres`) recarregáveis via `ResourceLoader`, ou uma estrutura própria (`Array[ItemData]` diretamente serializado)?
2. ~~A vida atual do Player é persistida no `SaveData`?~~ **Decidido pelo DC-03:** não. O respawn sempre restaura `vida_maxima`, então a vida do Player não entra no `SaveData`. O `SaveData` ganha apenas `mortes: int` (contador de tentativas).
3. O estado do `Enemy` (vivo/morto, posição) precisa persistir entre sessões, ou o Enemy sempre reinicia no estado padrão ao carregar um save (decisão cruzada com DC-04)?

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §7 (SaveData, InventoryComponent, HealthComponent); `Tutorial_Semana_07_Encontro_1.md` (schema original).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §7 (linha SaveData) descreve o schema final, cobrindo inventário, vida e (se DC-04 exigir) estado de inimigos.

**Impacto na implementação:** bloqueia IC-VS10-04 (persistência do inventário) e IC-VS14-02 (validação do save no build final).

---

## DC-06 — Ponto de spawn do Player e escolha de spawn (equivalente a `PlayerStart`/`ChoosePlayerStart` da UE5)

**Objetivo:** definir onde vive a informação de "onde o Player nasce" — tanto o ponto inicial do nível (sem save) quanto o ponto de respawn após alcançar um `Checkpoint` — e qual Scene/Autoload decide entre os dois ao carregar o nível.

**Problema de Design:** `PROJECT_ARCHITECTURE.md` §7 define a Scene `Checkpoint` ("dispara a gravação de progresso via `SaveComponent` ao ser alcançada/interagida") e o `SaveData` com `ultimo_checkpoint: String`, mas **não existe nenhuma menção a um ponto de início do nível** — o equivalente ao actor `PlayerStart` da Unreal. Nada diz de onde o Player parte quando o nível é carregado pela primeira vez, sem save. Também não há definição de **quem** decide o ponto de spawn na carga do nível (o equivalente a `GameMode.ChoosePlayerStart`): o `GameManager` "define as regras da partida (condições de início...)", mas nenhum documento afirma que a política de posicionamento inicial do Player é responsabilidade dele. Sem essa decisão, o fluxo de respawn do DC-03 não tem um alvo de posição definido, e o Player ou nasce numa posição fixa hard-coded na cena, ou na origem `(0,0,0)`.

Este card não redefine o que acontece na morte (isso é DC-03) — apenas onde a informação de posição de spawn é armazenada e lida.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §7 (Scenes principais — nova linha para o ponto de spawn; linha `GameManager`; linha `SaveManager`; linha `SaveData`) e §8 (estrutura de `level_exploration.tscn`).

**Decisões necessárias:**
1. O ponto inicial do nível é um Node marcador (`Marker3D`, ex.: `PlayerStart`) posicionado dentro de `level_exploration.tscn`, análogo ao actor `PlayerStart` da UE5? Ou uma propriedade de posição no `GameManager`/no nível?
2. Onde fica o **checkpoint ativo atual** (o ponto de respawn corrente): apenas no `SaveManager` em memória, apenas no `SaveData` em disco, ou nos dois (memória espelhando o que foi persistido)? Como o `ultimo_checkpoint: String` (um id) é resolvido para uma posição em cena — o `GameManager` procura o Node `Checkpoint` com aquele id?
3. Quem executa a política de spawn ao carregar o nível (equivalente a `ChoosePlayerStart`): o `GameManager` pergunta ao `SaveManager` se há `ultimo_checkpoint` e escolhe entre a posição do `Checkpoint` correspondente e o `Marker3D` inicial? Isso vira uma responsabilidade explícita listada na linha `GameManager` do §7?
4. As coordenadas ficam **sempre** nos Nodes da cena (marcador inicial + Scenes `Checkpoint`), nunca no `GameManager`/`SaveManager` (que guardam só *qual* ponto, não onde ele está)? Registrar isso explicitamente como regra, alinhado ao princípio de "local arquitetural único" (Rubrica 4).
5. Em qual semana isso é construído? O `Marker3D` inicial cabe na Semana 3–4 (junto ao Player/nível); a lógica de escolha de spawn depende de `Checkpoint` (Semana 7) e cruza com o respawn do DC-03 (Módulo 3).

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §7 (Checkpoint, GameManager, SaveManager, SaveData, SaveComponent), §8 (níveis); `Tutorial_Semana_04_Encontro_2.md` (SaveManager e `ultimo_checkpoint` conceitual); `Tutorial_Semana_07_Encontro_1.md`/`_2.md` (Checkpoint e schema do SaveData); dependência cruzada com DC-03 (fluxo de respawn) e DC-05 (schema do SaveData).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §7 ganha uma linha para o ponto de spawn inicial do Player (`Marker3D` no nível), a linha `GameManager` passa a citar explicitamente a responsabilidade de escolher o ponto de spawn ao carregar o nível (o "ChoosePlayerStart" daqui), e §8 registra o marcador na estrutura de `level_exploration.tscn`. A regra "coordenadas nos Nodes da cena, id do ponto ativo no SaveManager/SaveData" fica registrada.

**Impacto na implementação:** desbloqueia a parte de posicionamento do respawn de DC-03 (IC-VS08-02 / IC-VS11-04) e a construção do `Checkpoint` (IC-VS07 — Semana 7), que hoje grava `ultimo_checkpoint` sem um consumidor definido para essa informação.

**STATUS: RESOLVIDO (2026-09-02).** Registrado em `PROJECT_ARCHITECTURE.md` §6, §7 (Scenes principais + parágrafo "Fluxo de spawn do Player") e §8.

**Decisões tomadas:**
1. **Ponto inicial:** `Marker3D` chamado `PlayerStart`, filho do nó raiz de `level_exploration.tscn`, no grupo `player_start`. Guarda apenas a coordenada. Nenhuma posição de spawn vive no `GameManager`/`SaveManager`.
2. **Checkpoint ativo:** `SaveManager.ultimo_checkpoint: String` (id) em memória, espelhando `SaveData.ultimo_checkpoint` em disco. Cada `Checkpoint` está no grupo `checkpoints` e tem `@export var id_checkpoint: String` único. O `GameManager` resolve o id → Node varrendo o grupo `checkpoints`.
3. **Política de spawn:** `GameManager.spawn_player()` — método **público e reutilizável**. Se `SaveManager.ultimo_checkpoint != ""` e existe um `Checkpoint` com esse id → posiciona o Player nele; senão → no `PlayerStart`. É a responsabilidade explícita nova na linha `GameManager` do §7 (o "ChoosePlayerStart" daqui). O DC-03 apenas chamará `spawn_player()` de novo no fluxo de morte — sem reimplementar posicionamento.
4. **Regra registrada:** coordenadas sempre em Nodes da cena (`PlayerStart` + instâncias de `Checkpoint`); `GameManager`/`SaveManager` guardam só *qual* ponto e a política. (Rubrica 4 — local arquitetural único.)
5. **Construção:** Semana 4, Encontro 1 (nova Parte 3): `PlayerStart` + `spawn_player()` sem checkpoint, como primeira responsabilidade concreta do `GameManager`. Semana 7, Encontro 1 (nova Parte 5): `Checkpoint` grava `SaveManager.ultimo_checkpoint`; o nível carrega o `SaveData` no `_ready()` (via `SaveComponent.carregar()`) e `spawn_player()` ganha a escolha por checkpoint — fechando o ciclo do save.

**Nota cruzada:** o carregamento do `SaveData` ao iniciar cobre aqui apenas `itens_coletados`/`ultimo_checkpoint` (schema da Semana 7). A evolução do schema (inventário real, vida) segue no **DC-05**. O gatilho do respawn na morte segue no **DC-03**.
