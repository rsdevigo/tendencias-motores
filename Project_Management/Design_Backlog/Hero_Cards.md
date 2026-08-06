# Hero Cards

Cada Hero Card agrupa os Implementation Cards de um sistema (ou família de sistemas) e existe para dar contexto de por que aquele conjunto de tarefas existe — nunca é implementado diretamente; é o "guarda-chuva" sob o qual Design Cards e Implementation Cards vivem.

---

## HC-01 — Editor, Projeto e Scene Tree

**Objetivo:** estabelecer a estrutura física do projeto (pastas, assets, primeira Scene) sobre a qual todo o resto é construído.

**Escopo:** criação do projeto Godot 4.7; estrutura de pastas (`PROJECT_ARCHITECTURE.md` §8); importação dos 4 pacotes Kenney; primeira Scene com Nodes filhos (`NivelTeste`, `Chao`, `LuzPrincipal`); primeira Orchestration.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §3, §8, §9; `Tutorial_Semana_01_Encontro_1.md`; `Tutorial_Semana_01_Encontro_2.md`.

**Sistemas dependentes:** todos — é o pré-requisito universal do projeto.

---

## HC-02 — Locomoção do Player e Input Map

**Objetivo:** dar ao jogador controle físico sobre o Player, desacoplado do dispositivo de input.

**Escopo:** `Player` (CharacterBody3D), `CollisionShape3D`, `Malha` (placeholder), Input Map (4 Actions de movimento + 1 livre), Orchestration `player.torch` lendo Actions e aplicando `move_and_slide`.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 1), §7 (Scene Player); `Tutorial_Semana_02_Encontro_1.md`; `Tutorial_Semana_02_Encontro_2.md`.

**Sistemas dependentes:** HC-03 (build precisa de um Player controlável para ser testável); HC-05 (Interactable detecta a partir do Player); HC-08 (troca de mesh e HealthComponent vivem no Player); HC-11 (combate parte do Player).

---

## HC-03 — Renderização, Terreno e Pipeline de Exportação

**Objetivo:** dar aparência ao graybox e produzir o primeiro build distribuível.

**Escopo:** StandardMaterial3D + Terrain3D; WorldEnvironment/SDFGI; Export Templates, preset e build.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 1); `Tutorial_Semana_03_Encontro_1.md`; `Tutorial_Semana_03_Encontro_2.md`.

**Sistemas dependentes:** HC-12 (Materiais refatora o que HC-03 cria); HC-14 (Exportação final reaproveita o mesmo pipeline).

---

## HC-04 — Framework de Autoload (GameManager/SaveManager)

**Objetivo:** estabelecer onde vive o estado que sobrevive à troca de cena, antes de qualquer sistema de gameplay depender disso.

**Escopo:** `game_manager.gd`, `save_manager.gd`, registro em Project Settings > Autoload, validação de persistência entre cenas (em memória, não em disco).

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §7; `Tutorial_Semana_04_Encontro_1.md`; `Tutorial_Semana_04_Encontro_2.md`.

**Sistemas dependentes:** HC-05, HC-06, HC-07 (todos os sistemas de Módulo 2 em diante consultam ou alimentam GameManager/SaveManager); HC-09 (HUD lê GameManager).

---

## HC-05 — Contrato Interactable e Signals

**Objetivo:** permitir que qualquer objeto do mundo reaja ao Player sem que os dois se conheçam diretamente.

**Escopo:** `InteractionComponent` (Player), contrato `Interactable` (`has_method("interact")` ou interface Orchestrator), `Door.tscn`, Signal `interacted`, segundo objeto interativo do grupo/estudante (ex.: `Lever.tscn`).

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §7, §9; `Tutorial_Semana_05_Encontro_1.md`; `Tutorial_Semana_05_Encontro_2.md`.

**Sistemas dependentes:** HC-07 (`Checkpoint` reaproveita o contrato); HC-10 (interação ampliada); HC-11 (mesmo princípio de desacoplamento aplicado ao combate).

---

## HC-06 — Camada de Dados (ItemData/Enum)

**Objetivo:** desacoplar dado de design (o que é um item) de lógica de gameplay.

**Escopo:** `item_data.gd` (Resource + Enum `Categoria`), instâncias `.tres` de itens.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §9; `Tutorial_Semana_06_Encontro_1.md`; `Tutorial_Semana_06_Encontro_2.md`.

**Sistemas dependentes:** HC-07 (SaveData referencia itens coletados); HC-10 (InventoryComponent consome ItemData diretamente). **Bloqueado parcialmente por DC-01** quanto à aplicação prática (nenhuma Scene de coleta jamais construída no material-fonte).

---

## HC-07 — Persistência em Disco (SaveData/SaveComponent/Checkpoint)

**Objetivo:** transformar estado em memória em progresso real, sobrevivente ao fechamento do jogo.

**Escopo:** `save_data.gd` (Resource), `save_component.gd` (Node, `ResourceSaver`/`ResourceLoader`, `user://`), `Checkpoint.tscn` (reaproveita `Interactable`).

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 2), §7; `Tutorial_Semana_07_Encontro_1.md`; `Tutorial_Semana_07_Encontro_2.md`.

**Sistemas dependentes:** HC-10 (inventário deveria, eventualmente, persistir — ver DC-05); HC-14 (build final depende de um save íntegro).

---

## HC-08 — HealthComponent e Sistema de Animação

**Objetivo:** dar ao Player (e depois ao Enemy) vida/dano reutilizável, e substituir o placeholder visual por um modelo animado real.

**Escopo:** troca de `CapsuleMesh` pelo Kenney Mini Characters; `HealthComponent` (vida/dano/morte); AnimationTree/AnimationNodeStateMachine (idle/andar/correr); BlendSpace1D/2D + AnimationPlayer (animação contextual).

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §3, §6 (Módulo 3), §7; `Cronograma` (Semana 8); `Plano_de_Aula_Semana_08.md`. **Sem tutorial passo a passo** (Módulo 3 em diante).

**Sistemas dependentes:** HC-09 (HUD exibe vida); HC-11 (Enemy reutiliza `HealthComponent` e o mesmo modelo com skin distinta). **DC-03 e DC-04 dependem deste Hero Card para existir antes de serem resolvidos.**

---

## HC-09 — HUD e UI (Control Nodes)

**Objetivo:** comunicar o estado de jogo ao jogador em tempo real.

**Escopo:** Control simples vinculado a `HealthComponent`; HUD completo (CanvasLayer); `PauseMenu`.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 3), §7; `Cronograma` (Semana 9).

**Sistemas dependentes:** HC-10 (`InventoryUI` segue o mesmo padrão de binding).

---

## HC-10 — Inventário e Interação Ampliada

**Objetivo:** estruturar armazenamento/exibição de itens coletados e ampliar o Interaction System para múltiplos tipos.

**Escopo:** `InventoryComponent`, `InventoryUI`, ampliação do contrato `Interactable`.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 3), §7; `Cronograma` (Semana 10).

**Sistemas dependentes:** HC-14 (build final expõe inventário completo). **Bloqueado por DC-01** (não há de onde vir um item coletado em gameplay real) **e parcialmente por DC-05** (persistência do inventário).

---

## HC-11 — IA de Inimigos e Combate Simples

**Objetivo:** dar autonomia de deslocamento e decisão a um agente não-jogador, e o primeiro combate do jogo.

**Escopo:** `NavigationRegion3D`/`NavigationAgent3D`; `Enemy` (CharacterBody3D, skin do Kenney Mini Characters); Behavior Tree/Blackboard via LimboAI (tasks em GDScript — exigência do addon, Orchestrator não gera esse tipo de classe); combate simples (`Area3D`/`RayCast3D` → `apply_damage`).

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 3), §7; `Cronograma` (Semana 11); `Plano_de_Aula_Semana_11.md`.

**Sistemas dependentes:** HC-14 (objetivo final provavelmente envolve o combate — ver DC-02). **Bloqueado por DC-03 e DC-04** quanto ao estado final de morte de Player e Enemy.

---

## HC-12 — Materiais e Composição de Cena

**Objetivo:** padronizar/otimizar a produção visual sem alterar mecânica.

**Escopo:** auditoria de materiais, Material Override/Unique Material, `MultiMeshInstance3D` (Foliage).

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 12); `Plano_de_Aula_Semana_12.md`.

**Sistemas dependentes:** nenhum sistema de gameplay — puramente visual/performance.

---

## HC-13 — Áudio, Profiling e Otimização

**Objetivo:** integrar áudio a eventos reais e eliminar gargalos técnicos antes da entrega final.

**Escopo:** `AudioStreamPlayer` conectado a interação/passos/ambiente; Profiler/Debugger; otimização justificada por dado real.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 13).

**Sistemas dependentes:** HC-14 (build final deve estar otimizado).

---

## HC-14 — Exportação Final e Consolidação

**Objetivo:** empacotar o Vertical Slice completo como build distribuível e validado.

**Escopo:** revisão do pipeline de exportação (reaproveita HC-03); Code Review de encerramento; Playtest cruzado.

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 14).

**Sistemas dependentes:** nenhum novo — depende de **todos** os anteriores estarem consolidados, e de **DC-02 e DC-05 resolvidos**.

---

## HC-15 — Análise Arquitetural Comparada

**Objetivo:** consolidar a comparação Godot × Unity × motor adicional e apresentar tecnicamente o projeto.

**Escopo:** engenharia reversa de Godot Demo Projects; quadro comparativo (expande `PROJECT_ARCHITECTURE.md` §12); apresentação técnica final. **Nenhum código novo em nenhum card deste Hero Card.**

**Documentos relacionados:** `PROJECT_ARCHITECTURE.md` §12; `Cronograma` (Semanas 15–17).

**Sistemas dependentes:** nenhum — é o encerramento do projeto, consome todos os anteriores como objeto de análise.
