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

---

## DC-02 — Definição mecânica do "objetivo final único"

**Objetivo:** definir o que precisa acontecer, em termos de jogo, para o Vertical Slice ser considerado "concluído" pelo jogador.

**Problema de Design:** `PROJECT_ARCHITECTURE.md` §4 (Escopo) lista, como item dentro do escopo: "Um objetivo final único que encerra o Vertical Slice." Esta é a única menção ao objetivo final em todo o documento — não há especificação de **qual** objetivo (chegar a um local? derrotar o Enemy? coletar um item específico? uma combinação?), nem de como ele é detectado (uma nova Area3D de "vitória"? uma condição verificada pelo `GameManager`?), nem do que acontece ao ser alcançado (tela de encerramento? apenas um log?). Diferente de um valor numérico com exemplo (como a velocidade de movimento), aqui não há nenhum ponto de partida — é um vazio de design, não um placeholder.

**Documento do Rulebook afetado:** `PROJECT_ARCHITECTURE.md` §2 (Conceito do Jogo) e §4 (Escopo).

**Decisões necessárias:**
1. Qual é o gatilho do objetivo final (localização, item, derrota do Enemy, ou combinação)?
2. Onde essa lógica vive — um novo Component, uma responsabilidade adicional do `GameManager`, ou uma Scene dedicada (`Objective.tscn`, análoga a `Checkpoint.tscn`)?
3. O que o jogador vê ao concluir (tela, HUD, apenas volta ao menu)? Isso implica uma nova Scene de UI não listada em §7?
4. O objetivo final depende do combate (DC-04) estar resolvido, ou é independente dele?

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
2. A vida atual do Player é persistida no `SaveData`, ou todo `Checkpoint` restaura vida máxima (o que tornaria essa persistência desnecessária — decisão cruzada com DC-03)?
3. O estado do `Enemy` (vivo/morto, posição) precisa persistir entre sessões, ou o Enemy sempre reinicia no estado padrão ao carregar um save (decisão cruzada com DC-04)?

**Referências do GDD:** `PROJECT_ARCHITECTURE.md` §7 (SaveData, InventoryComponent, HealthComponent); `Tutorial_Semana_07_Encontro_1.md` (schema original).

**Critério de Conclusão:** `PROJECT_ARCHITECTURE.md` §7 (linha SaveData) descreve o schema final, cobrindo inventário, vida e (se DC-04 exigir) estado de inimigos.

**Impacto na implementação:** bloqueia IC-VS10-04 (persistência do inventário) e IC-VS14-02 (validação do save no build final).
