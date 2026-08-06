# Vertical Slices

Uma Vertical Slice por semana do [Cronograma](../docs/Cronograma_Tendencias_de_Motores_de_Jogos.md). A ordem é a ordem do Cronograma — não pode ser alterada. Cada slice descreve um incremento **jogável e testável** sobre o slice anterior; nenhuma slice remove ou substitui o que a anterior construiu (princípio de Reutilização, `PROJECT_ARCHITECTURE.md` §1).

Convenção de IDs de card usada abaixo: `IC-VSxx-yy` (Implementation Card), `DC-xx` (Design Card), `HC-xx` (Hero Card).

---

## VS-01 — Arquitetura do Godot, Nodes e Scene Tree

**Objetivo:** ter um projeto Godot 4.7 estruturado, com os 4 pacotes de assets importados, e uma primeira Scene com Nodes filhos.

**Experiência Jogável:** nada "jogável" no sentido de gameplay ainda — mas o projeto abre, roda (F6) e mostra uma cena 3D simples com uma luz e um chão, validável visualmente. É o piso mínimo sobre o qual tudo mais é construído.

**Sistemas Envolvidos:** Estrutura de projeto, FileSystem Dock, Node/Scene Tree, importação de assets.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §8 (estrutura de pastas), §3 (Direção de Arte); `docs/Tutoriais/Tutorial_Semana_01_Encontro_1.md`, `Tutorial_Semana_01_Encontro_2.md`.

**Dependências:** nenhuma (primeira slice).

**Cards necessários:** HC-01; IC-VS01-01, IC-VS01-02, IC-VS01-03, IC-VS01-04.

**Critérios de Aceite:**
- [ ] Projeto `TemploEsquecido` criado em Godot 4.7, abre sem erros.
- [ ] Estrutura de pastas completa conforme `PROJECT_ARCHITECTURE.md` §8 (incluindo `assets/prototype/`, `dungeon/`, `nature/`, `characters/`).
- [ ] Os 4 pacotes Kenney importados sem erro (ver Tutorial Semana 1, Encontro 1, Parte 4).
- [ ] Scene `level_exploration.tscn` existe, com `NivelTeste` > `Chao` (MeshInstance3D + StaticBody3D/CollisionShape3D) e `LuzPrincipal` (DirectionalLight3D ou OmniLight3D).
- [ ] Orchestration `nivel_teste.torch` com evento Ready funcional (log de teste).

**Definition of Done:** F6 roda a Scene sem erro no Output; a hierarquia de Nodes é visível e nomeada corretamente (sem `Node3D`/`MeshInstance` genéricos); checklist do Tutorial da Semana 1 (ambos os encontros) 100% marcado.

---

## VS-02 — CharacterBody3D, Movimentação e Input Map

**Objetivo:** um Player controlável nas 4 direções, com física de colisão.

**Experiência Jogável:** o jogador pressiona W/A/S/D e o Player se move pelo graybox, deslizando ao encostar em obstáculos — a primeira interação real com o jogo.

**Sistemas Envolvidos:** CharacterBody3D, `move_and_slide`, Input Map/InputEvent, Orchestrator.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 1), §7 (Scene Player); `Tutorial_Semana_02_Encontro_1.md`, `Tutorial_Semana_02_Encontro_2.md`.

**Dependências:** VS-01 (Scene e projeto existentes).

**Cards necessários:** HC-02; IC-VS02-01, IC-VS02-02, IC-VS02-03.

**Critérios de Aceite:**
- [ ] `Player` (CharacterBody3D) existe como Scene própria (`scenes/characters/Player.tscn`), com `CollisionShape3D` e `Malha` (`CapsuleMesh` placeholder) alinhados.
- [ ] Input Map com as Actions `move_forward`, `move_back`, `move_left`, `move_right`.
- [ ] Orchestration `player.torch` lê as 4 Actions, monta um vetor de direção e aplica a `velocity` antes de `move_and_slide`.
- [ ] Uma Action adicional (correr, agachar ou pular — livre escolha) implementada e funcional.

**Definition of Done:** Player se move nas 4 direções, desliza em obstáculos sem travar; Action adicional testada; checklist dos dois tutoriais da Semana 2 100% marcado.

---

## VS-03 — Materiais, Terrain3D, SDFGI/VoxelGI e Exportação 🔴

**Objetivo:** dar aparência ao graybox e produzir o primeiro executável fora do editor. **Encerra o Milestone MS-1.**

**Experiência Jogável:** o mesmo Player da VS-02, agora andando sobre um terreno esculpido, texturizado e iluminado de forma indireta — rodando como um `.exe`/binário autônomo, sem precisar do editor aberto.

**Sistemas Envolvidos:** StandardMaterial3D, Terrain3D (addon), WorldEnvironment/SDFGI, Export Templates/Project Export.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 1, linha "Renderização moderna e build"); `Tutorial_Semana_03_Encontro_1.md`, `Tutorial_Semana_03_Encontro_2.md`.

**Dependências:** VS-02.

**Cards necessários:** HC-03; IC-VS03-01, IC-VS03-02, IC-VS03-03, IC-VS03-04.

**Critérios de Aceite:**
- [ ] `StandardMaterial3D` aplicado ao `Chao`, salvo em `materials/chao_prototype.tres`, com textura do Kenney Prototype Kit.
- [ ] Terreno esculpido via Terrain3D, com Storage salva em `resources/terrain/`.
- [ ] `WorldEnvironment` com recurso `Environment` (`resources/environment_exploration.tres`) e SDFGI habilitado, com efeito visível.
- [ ] Export Templates instalados; preset de exportação criado; build gerado em `builds/semana_03/`.
- [ ] Build executado fora do editor: nível carrega, Player responde ao Input Map, sem erro.

**Definition of Done:** Checkpoint de encerramento do Módulo 1 cumprido — build joga corretamente fora do editor. Checklist dos dois tutoriais 100%.

---

## VS-04 — GameManager e SaveManager (Autoload)

**Objetivo:** primeiro estado global do jogo, sobrevivente a troca de cena.

**Experiência Jogável:** ainda não há mudança visível para quem joga — o teste é de arquitetura (um valor persiste ao trocar de Scene), validado via `print()`/depurador, não por uma tela nova.

**Sistemas Envolvidos:** Autoload/Singleton, GDScript (`class_name`), Project Settings.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §7 (GameManager/SaveManager); `Tutorial_Semana_04_Encontro_1.md`, `Tutorial_Semana_04_Encontro_2.md`.

**Dependências:** VS-03 (projeto e Player estáveis; nenhuma alteração de nível nesta slice).

**Cards necessários:** HC-04; IC-VS04-01, IC-VS04-02, IC-VS04-03.

**Critérios de Aceite:**
- [ ] `scripts/autoload/game_manager.gd` com `class_name GameManager`, registrado em Project Settings > Autoload.
- [ ] Acesso ao `GameManager` validado a partir do script do Player (`print(GameManager)` sem erro, depois removido).
- [ ] `scripts/autoload/save_manager.gd` com `class_name SaveManager`, registrado como segundo Autoload independente.
- [ ] Uma variável em `SaveManager` (ex.: `itens_coletados: int`) validada como persistente entre duas Scenes reais (`level_exploration.tscn` e uma Scene de teste descartável).
- [ ] Variável de estado própria no `GameManager` (desafio da Semana 4, Encontro 1) implementada e comentada.

**Definition of Done:** os dois Autoloads aparecem habilitados em Project Settings; persistência validada com troca de cena real; Main Scene revertida para `level_exploration.tscn` ao final do teste; checklist dos dois tutoriais 100%.

---

## VS-05 — Contrato Interactable e Signals

**Objetivo:** primeira comunicação desacoplada do projeto — o Player interage com o mundo sem conhecer o tipo concreto do objeto.

**Experiência Jogável:** o jogador se aproxima de uma porta, pressiona a tecla de interação, a porta abre/fecha visivelmente. O mesmo vale para um segundo objeto interativo (ex.: alavanca) com uma reação diferente.

**Sistemas Envolvidos:** Contrato `Interactable` (`has_method`/interface Orchestrator), `Area3D` (`InteractionComponent`), Signals.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §7 (Interactable, Door/Lever), §9 (nomenclatura de Signals); `Tutorial_Semana_05_Encontro_1.md`, `Tutorial_Semana_05_Encontro_2.md`.

**Dependências:** VS-04.

**Cards necessários:** HC-05; IC-VS05-01, IC-VS05-02, IC-VS05-03, IC-VS05-04.

**Critérios de Aceite:**
- [ ] `InteractionComponent` no Player, detectando objetos próximos via `Area3D` e chamando `interact()` via `has_method`.
- [ ] `Door.tscn` (`scenes/interactables/`) implementa `interact()`.
- [ ] Signal `interacted` declarado em `door.gd`, emitido dentro de `interact()`, conectado a `_abrir_fechar()` (função de reação separada).
- [ ] Segundo objeto interativo (ex.: `Lever.tscn`) implementado com o mesmo contrato e um Signal próprio (ex.: `lever_pulled`), sem qualquer alteração no `InteractionComponent`.

**Definition of Done:** Player interage com os dois objetos sem erro; Feedback formal (instrumento do Cronograma, Semana 5) recebido; checklist dos dois tutoriais 100%.

---

## VS-06 — ItemData (Resource) e Enums

**Objetivo:** separar dado de design (o que é um item) de lógica de gameplay.

**Experiência Jogável:** ainda não há coleta funcional em jogo (ver DC-01) — o "jogável" desta semana é o Inspector do Godot: selecionar uma instância `.tres` e ver seus campos preenchidos, incluindo um menu suspenso de categoria.

**Sistemas Envolvidos:** Resource customizado, Enum, `@export`.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2, linha ItemData), §9; `Tutorial_Semana_06_Encontro_1.md`, `Tutorial_Semana_06_Encontro_2.md`.

**Dependências:** VS-05.

**Cards necessários:** HC-06; IC-VS06-01, IC-VS06-02; **DC-01 aberto (ver abaixo) — bloqueia a aplicação prática do `ItemData` a um objeto coletável em cena.**

**Critérios de Aceite:**
- [ ] Classe `ItemData` (`scripts/resources/item_data.gd`), estendendo `Resource`, com campos `nome`, `icone`, `valor`, `descricao`.
- [ ] Enum `Categoria` declarado e aplicado como campo `@export`.
- [ ] Pelo menos 3 instâncias `.tres` em `resources/items/`, com todos os campos preenchidos, incluindo `categoria`.
- [ ] Checkpoint de progresso do Módulo 2 (instrumento do Cronograma, Semana 6) apresentado.

**Definition of Done:** instâncias `.tres` visíveis e corretas no Inspector; nenhuma lógica de gameplay dentro de `item_data.gd`; checklist dos dois tutoriais 100%. **Nota:** a aplicação do `ItemData` a uma Scene coletável (`Chest`/`Pickup`) não é feita nesta slice nem em nenhuma outra do material lido — ver DC-01.

---

## VS-07 — Save/Load, Checkpoint e Consolidação do Módulo 2 🔴

**Objetivo:** persistência real em disco, e integração de tudo que o Módulo 2 construiu em um único fluxo. **Encerra o Milestone MS-2.**

**Experiência Jogável:** o jogador percorre porta → alavanca → (baú — ver ressalva DC-01) → checkpoint; fecha o jogo, reabre, e o progresso salvo no checkpoint está lá.

**Sistemas Envolvidos:** `SaveData` (Resource), `SaveComponent` (FileAccess/ResourceSaver/ResourceLoader), `Checkpoint` (reaproveita `Interactable`).

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §7 (SaveComponent, Checkpoint, SaveData); `Tutorial_Semana_07_Encontro_1.md`, `Tutorial_Semana_07_Encontro_2.md`.

**Dependências:** VS-06.

**Cards necessários:** HC-07; IC-VS07-01, IC-VS07-02, IC-VS07-03; **DC-01 impacta o Critério de Aceite sobre "baú" abaixo.**

**Critérios de Aceite:**
- [ ] `SaveData` (Resource) com `itens_coletados: Array[String]` e `ultimo_checkpoint: String`.
- [ ] `SaveComponent` grava/lê em `user://save_data.tres` via `ResourceSaver`/`ResourceLoader`; testado com o jogo fechado e reaberto.
- [ ] `Checkpoint.tscn` implementa `Interactable`, aciona `SaveComponent.salvar()` ao ser interagido, com `id_checkpoint` próprio.
- [ ] Porta, alavanca e checkpoint (e baú, **apenas se DC-01 já estiver resolvido** — caso contrário, registrar a ausência como pendência explícita, não como item concluído) conectados em um único fluxo percorrível do início ao fim.
- [ ] Code Review (Rubrica 4) e Playtest coletivo realizados.

**Definition of Done:** progresso sobrevive a fechar/reabrir o jogo; Code Review e Playtest de encerramento da Unidade II cumpridos; checklist dos dois tutoriais 100%; DC-01 registrado como pendência conhecida se ainda não resolvido (não bloqueia o encerramento do módulo, mas deve ser resolvido antes da VS-10, que depende de itens coletáveis funcionais).

---

## VS-08 — HealthComponent, AnimationTree, BlendSpace e AnimationPlayer

**Objetivo:** vida/dano reutilizável e um Player animado (substituindo o placeholder de cápsula).

**Experiência Jogável:** o Player agora tem um modelo com animações de idle/andar/correr reagindo ao movimento, e pode "tomar dano" (ainda sem uma fonte de dano em jogo até a VS-11) reduzindo uma vida interna.

**Sistemas Envolvidos:** Kenney Mini Characters, `HealthComponent`, AnimationTree/AnimationNodeStateMachine, BlendSpace1D/2D, AnimationPlayer.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §3, §6 (Módulo 3), §7 (HealthComponent); `Plano_de_Aula_Semana_08.md`, `Cronograma` (Semana 8) — não há tutorial passo a passo (Módulo 3 em diante, ver `PEDAGOGICAL_RULES.md`).

**Dependências:** VS-07.

**Cards necessários:** HC-08; IC-VS08-01, IC-VS08-02, IC-VS08-03, IC-VS08-04; **DC-03 (morte do Player) impacta o comportamento do sinal `died`, mas não bloqueia a construção do Component em si.**

**Critérios de Aceite:**
- [ ] `Malha` (CapsuleMesh) do Player substituída pelo modelo do Kenney Mini Characters, com `AnimationPlayer` funcional (idle/walk/run confirmados na aba Import).
- [ ] `HealthComponent` (Node customizado, Orchestrator ou GDScript) com vida atual/máxima (placeholder numérico — Tipo B, ver IC-VS08-02), `apply_damage(quantidade)`, sinal `died`.
- [ ] State Machine básica via AnimationTree/AnimationNodeStateMachine (idle → andar → correr), condicionada a uma variável real de movimento.
- [ ] Uma animação contextual (BlendSpace direcional OU animação pontual do AnimationPlayer) conectada a um evento real (`HealthComponent.apply_damage` ou `Interactable`).

**Definition of Done:** State Machine transiciona corretamente durante o movimento real do Player; `HealthComponent` testável isoladamente (chamar `apply_damage` via debug reduz a vida e emite `died` ao chegar a zero); nenhuma regressão nos sistemas do Módulo 2.

---

## VS-09 — Control Nodes e HUD

**Objetivo:** comunicar o estado de jogo ao jogador em tempo real.

**Experiência Jogável:** o jogador vê, na tela, sua vida atual (e ao menos um segundo dado — itens ou progresso) sem precisar abrir o editor ou o depurador.

**Sistemas Envolvidos:** Control nodes (containers, anchors), CanvasLayer, binding de dados, PauseMenu.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 3), §7 (HUD, PauseMenu); `Cronograma` (Semana 9).

**Dependências:** VS-08 (HUD exibe `HealthComponent`).

**Cards necessários:** HC-09; IC-VS09-01, IC-VS09-02, IC-VS09-03.

**Critérios de Aceite:**
- [ ] Control simples (Label) vinculado à vida do `HealthComponent`, organizado por container/anchor.
- [ ] HUD (`CanvasLayer` + Control) exibindo em tempo real vida e ao menos um segundo dado já existente (`SaveManager.itens_coletados` como placeholder, até a VS-10 introduzir o inventário real).
- [ ] `PauseMenu` (Control) acionado por uma Action de alto nível do Player, ao menos com opção de retomar o jogo (Tipo B — o Cronograma não lista opções obrigatórias além de "reforçar o fluxo de UI sobre o GameManager"; retomar sozinho já satisfaz o escopo mínimo, opções extras como "Sair" ficam a critério de quem implementa).
- [ ] Nenhuma lógica de gameplay duplicada dentro de um Control (o Control só lê, nunca recalcula, o dado de origem).

**Definition of Done:** HUD reflete corretamente o estado real do `HealthComponent` durante o gameplay; Feedback formal (Semana 9) recebido.

---

## VS-10 — Inventário e Ampliação do Interaction System

**Objetivo:** estruturar armazenamento/exibição de itens e ampliar a interação para múltiplos tipos.

**Experiência Jogável:** o jogador coleta itens de fato (uma vez que DC-01 esteja resolvido) e os vê refletidos em uma UI de inventário; a interação passa a suportar mais de um tipo de resposta.

**Sistemas Envolvidos:** `InventoryComponent`, `InventoryUI`, ampliação do contrato `Interactable`.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 3), §7 (InventoryComponent); `Cronograma` (Semana 10).

**Dependências:** VS-09; **DC-01 deve estar resolvido antes desta slice ser dada como concluída** — sem `Chest`/`Pickup` funcionais, não há como popular o inventário a partir de gameplay real.

**Cards necessários:** HC-10; IC-VS10-01, IC-VS10-02, IC-VS10-03, IC-VS10-04 (a IC-VS10-04, que persiste o inventário no `SaveData`, está `Blocked By: DC-05`).

**Critérios de Aceite:**
- [ ] `InventoryComponent` armazena/adiciona/remove `ItemData` coletados, expondo dados para a `InventoryUI` sem conhecer detalhes de UI.
- [ ] `InventoryUI` (Control) exibe os itens armazenados, atualizada em tempo real.
- [ ] Interação ampliada para suportar um novo tipo (empilhar, combinar ou cooldown — livre escolha, ver IC-VS10-03), conectada ao inventário.
- [ ] Code Review dos sistemas de inventário/interação realizado.

**Definition of Done:** coletar um item em jogo atualiza `InventoryComponent` e a `InventoryUI` sem reiniciar a cena; Code Review (Semana 10) cumprido.

---

## VS-11 — Navigation, Behavior Trees (LimboAI), Blackboards e Combate Simples 🔴

**Objetivo:** dar autonomia de deslocamento e decisão a um agente não-jogador, e um primeiro combate. **Encerra o Milestone MS-3.**

**Experiência Jogável:** um `Enemy` se desloca sozinho pelo nível, decide entre patrulhar/perseguir, e troca dano com o Player — o primeiro risco real dentro do jogo.

**Sistemas Envolvidos:** `NavigationRegion3D`/`NavigationAgent3D`, LimboAI (Behavior Tree + Blackboard), `Area3D`/`RayCast3D`, `HealthComponent` (reutilizado).

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 3), §7 (Enemy); `Cronograma` (Semana 11); `Plano_de_Aula_Semana_11.md`.

**Dependências:** VS-10.

**Cards necessários:** HC-11; IC-VS11-01, IC-VS11-02, IC-VS11-03; IC-VS11-04 está `Blocked By: DC-03, DC-04`.

**Critérios de Aceite:**
- [ ] `NavigationRegion3D` calculado sobre o nível; `Enemy` (CharacterBody3D, reaproveitando skin do Kenney Mini Characters) se desloca via `NavigationAgent3D` até um ponto.
- [ ] Behavior Tree (LimboAI) simples de patrulha/perseguição, com Blackboard para memória compartilhada (ex.: última posição conhecida do Player). Tasks customizadas em GDScript (exigência do addon — Orchestrator não se aplica aqui, ver HC-11).
- [ ] Combate simples: `Area3D`/`RayCast3D` do Player chamando `apply_damage` no `HealthComponent` do `Enemy` (via Orchestrator ou GDScript).
- [ ] Comportamento autônomo adicional proposto pelo grupo/estudante (patrulha, alerta, fuga — livre escolha).
- [ ] Playtest coletivo e Showcase de encerramento realizados.

**Definition of Done:** Enemy persegue e recebe dano corretamente; Playtest+Showcase (Semana 11) cumpridos. **O que acontece quando o Player morre (DC-03) ou quando o Enemy morre (DC-04) permanece indefinido e não bloqueia o Showcase**, mas deve ser resolvido antes do Milestone MS-4 ser fechado (a experiência de "objetivo final", DC-02, depende de ambos os fluxos existirem).

---

## VS-12 — Materials, Material Overrides e Foliage

**Objetivo:** padronizar e otimizar a produção visual. Nenhuma mecânica nova.

**Experiência Jogável:** visualmente idêntico em termos de gameplay — o jogo joga exatamente igual à VS-11, mas os materiais são parametrizados e a zona externa ganha vegetação/densidade via instancing.

**Sistemas Envolvidos:** StandardMaterial3D, Material Override/Unique Material, `MultiMeshInstance3D`.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 12); `Plano_de_Aula_Semana_12.md`.

**Dependências:** VS-11.

**Cards necessários:** HC-12; IC-VS12-01, IC-VS12-02.

**Critérios de Aceite:**
- [ ] Auditoria dos materiais existentes (desde a Semana 3); ao menos um conjunto de objetos refatorado para material base + Override, sem duplicar material equivalente.
- [ ] `MultiMeshInstance3D` compondo vegetação/elementos de cena do Kenney Nature Kit na zona externa, sem regressão de performance perceptível.
- [ ] Nenhuma alteração de mecânica, geometria ou sistema de gameplay.
- [ ] Code Review de materiais e composição de cena realizado.

**Definition of Done:** Code Review (Semana 12) cumprido; nenhum teste de gameplay das VS anteriores quebrou.

---

## VS-13 — Áudio, Optimization e Profiling

**Objetivo:** integrar som a eventos reais de gameplay e eliminar ao menos um gargalo real de desempenho.

**Experiência Jogável:** interação, passos e ambiente agora emitem som; o jogo roda de forma mensuravelmente mais leve em pelo menos um aspecto identificado no profiling.

**Sistemas Envolvidos:** `AudioStreamPlayer`, Profiler/Debugger nativo do Godot.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 13).

**Dependências:** VS-12.

**Cards necessários:** HC-13; IC-VS13-01, IC-VS13-02.

**Critérios de Aceite:**
- [ ] Sons integrados a interação (`Interactable`), passos do Player e ambiente, via `AudioStreamPlayer` (placeholder de asset — Kenney Audio, Tipo B quanto ao SFX exato escolhido).
- [ ] Profiling do próprio projeto realizado; um gargalo real identificado e corrigido (geometria, materiais, iluminação ou lógica de script/Orchestration), com justificativa registrada.
- [ ] Feedback formal sobre a otimização realizada.

**Definition of Done:** Feedback formal (Semana 13) cumprido; a otimização aplicada é mensurável (antes/depois no Profiler), não apenas alegada.

---

## VS-14 — Exportação e Consolidação do Vertical Slice Final 🔴

**Objetivo:** empacotar o produto final como build distribuível e validá-lo de forma cruzada. **Encerra o Milestone MS-4.**

**Experiência Jogável:** o Vertical Slice completo, do início ao objetivo final, jogável por qualquer pessoa a partir de um executável — sem o editor aberto.

**Sistemas Envolvidos:** Export Templates/Project Export (revisão), Code Review de encerramento.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 14).

**Dependências:** VS-13; **DC-02 (objetivo final) e DC-05 (schema do `SaveData`) devem estar resolvidos antes desta slice ser dada como concluída** — não é possível "consolidar" um Vertical Slice sem um objetivo que o encerre nem um save que cubra o estado acumulado desde o Módulo 3.

**Cards necessários:** HC-14; IC-VS14-01, IC-VS14-02 (`Blocked By: DC-05`), IC-VS14-03 (`Blocked By: DC-02`).

**Critérios de Aceite:**
- [ ] Build exportado do Vertical Slice completo (Módulos 1–4), testado fora do editor.
- [ ] Playtest cruzado entre builds (ou, em projeto solo, um playtest externo — ver nota no Hero Card HC-14) realizado.
- [ ] Code Review de encerramento cobrindo todos os sistemas acumulados, sem lógica duplicada entre módulos.
- [ ] `SaveData` cobre todo o estado relevante acumulado (inventário, vida, checkpoints) — depende de DC-05.
- [ ] Objetivo final implementado e alcançável — depende de DC-02.

**Definition of Done:** Entrega parcial + Code Review de encerramento (Semana 14) cumpridos; build final não depende de nenhum Design Card em aberto.

---

## VS-15 — Engenharia Reversa de Projetos Profissionais

**Objetivo:** ler a arquitetura do TPS Demo e do Platformer 2D Demo (Godot Demo Projects oficiais) e traçar paralelos com o próprio projeto. **Nenhum código novo.**

**Experiência Jogável:** não aplicável — produto é analítico.

**Sistemas Envolvidos:** nenhum novo; leitura do próprio Vertical Slice como objeto de comparação.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §12 (Comparações com Unity, a ser expandida); `Cronograma` (Semana 15).

**Dependências:** VS-14 (o projeto precisa estar consolidado para servir de base de comparação).

**Cards necessários:** HC-15; IC-VS15-01 (card de análise, não de implementação).

**Critérios de Aceite:**
- [ ] Leitura arquitetural do TPS Demo e do Platformer 2D Demo concluída, com paralelos explícitos ao próprio projeto.
- [ ] Ao menos uma decisão arquitetural própria identificada como "refazível" à luz da análise, registrada por escrito.
- [ ] Feedback formal sobre as análises realizado.
- [ ] Nenhuma alteração de código no Vertical Slice durante esta semana (regra explícita do Cronograma).

**Definition of Done:** Feedback formal (Semana 15) cumprido; nenhum commit/alteração de gameplay nesta semana.

---

## VS-16 — Comparação Arquitetural Godot × Unity × Motor Adicional 🔴

**Objetivo:** consolidar a comparação sistemática feita ao longo do semestre e prepará-la para a apresentação final.

**Experiência Jogável:** não aplicável — produto é o quadro comparativo e o checkpoint de preparação.

**Sistemas Envolvidos:** nenhum novo.

**Documentos do GDD utilizados:** `PROJECT_ARCHITECTURE.md` §12 (base do quadro, a expandir — nunca substituir); `Cronograma` (Semana 16).

**Dependências:** VS-15.

**Cards necessários:** HC-15; IC-VS16-01, IC-VS16-02 (cards de análise/documentação).

**Critérios de Aceite:**
- [ ] Quadro comparativo Godot × Unity cobrindo gameplay framework, animação, IA, UI e pipeline de produção, com base nos sistemas realmente construídos (Milestones 1–4).
- [ ] Comparação ampliada para um motor adicional (Unreal Engine, O3DE ou Stride), escolhido e justificado.
- [ ] Checkpoint de preparação da apresentação técnica final entregue.

**Definition of Done:** Checkpoint (Semana 16) cumprido.

---

## VS-17 — Apresentação Técnica Final do Vertical Slice 🔴

**Objetivo:** apresentar e defender tecnicamente o Vertical Slice completo. **Encerra o projeto.**

**Experiência Jogável:** demonstração ao vivo (ou vídeo/build) do Vertical Slice completo, do Módulo 1 ao 4.

**Sistemas Envolvidos:** nenhum novo — síntese de tudo.

**Documentos do GDD utilizados:** todos os anteriores, de forma integrada.

**Dependências:** VS-16.

**Cards necessários:** HC-15; IC-VS17-01 (apresentação).

**Critérios de Aceite:**
- [ ] Vertical Slice demonstrado ao vivo (ou build/vídeo, conforme infraestrutura).
- [ ] Decisões arquiteturais centrais justificadas, articulando conceito universal → implementação Godot → comparação com outro motor.
- [ ] Perguntas técnicas respondidas com domínio real do projeto.

**Definition of Done:** Apresentação técnica final realizada. Fim do plano de produção.
