# Milestones

Cada Milestone corresponde a um Módulo/Unidade do [Cronograma](../docs/Cronograma_Tendencias_de_Motores_de_Jogos.md) e a uma linha da seção 11 ("Evolução do Vertical Slice") do [PROJECT_ARCHITECTURE.md](../PROJECT_ARCHITECTURE.md). A ordem é fixa — nenhum Milestone pode começar antes do anterior estar com sua Definition of Done satisfeita, pois cada um constrói sobre o produto jogável do anterior (princípio de Reutilização, seção 1 do PROJECT_ARCHITECTURE.md).

---

## MS-1 — Aprender a Ferramenta

**Semanas:** 1–3 · **Vertical Slices:** VS-01, VS-02, VS-03 · **Hero Cards:** HC-01, HC-02, HC-03

**Objetivo:** dar ao solo dev o domínio mínimo do Godot Editor, do modelo de composição (Node/Scene Tree) e do pipeline básico (material, terreno, iluminação, exportação) necessário para qualquer sistema futuro.

**Escopo:**
- Projeto Godot 4.7 criado e estruturado conforme `PROJECT_ARCHITECTURE.md` (seção 8).
- Os 4 pacotes de assets Kenney importados (Prototype, Dungeon, Nature, Mini Characters).
- Player (`CharacterBody3D`) controlável via Input Map.
- Nível de teste com terreno (Terrain3D), material e iluminação global (SDFGI/VoxelGI).
- Primeiro build exportado e executável fora do editor.

**Produto jogável ao final:** um executável em que o Player anda livremente por um graybox externo iluminado, sem nenhum sistema de gameplay ainda.

**Definition of Done do Milestone:**
- [ ] Todos os Critérios de Aceite de VS-01, VS-02 e VS-03 cumpridos.
- [ ] Checkpoint de encerramento (🔴 Semana 3) satisfeito: build exportado roda fora do editor.
- [ ] Nenhum Design Card pendente bloqueando um Implementation Card deste módulo.

---

## MS-2 — Construir Sistemas

**Semanas:** 4–7 · **Vertical Slices:** VS-04, VS-05, VS-06, VS-07 · **Hero Cards:** HC-04, HC-05, HC-06, HC-07

**Objetivo:** construir a espinha dorsal de gameplay — estado global, comunicação desacoplada entre sistemas, dados de design separados de lógica, e persistência real em disco.

**Escopo:**
- `GameManager` e `SaveManager` (Autoload).
- Contrato `Interactable` (duck typing/`has_method`) + Signals, aplicado a `Door` e a um segundo interativo (`Lever` ou equivalente).
- `ItemData` (Resource) + Enum de categoria, com conjunto próprio de itens.
- `SaveData` (Resource) + `SaveComponent` (FileAccess/ResourceSaver), persistindo em `user://`.
- `Checkpoint` (reaproveita o contrato `Interactable`).
- Integração de todos os sistemas do módulo em um único fluxo jogável.

**Produto jogável ao final:** o jogador percorre um caminho com porta, alavanca, baú(s) e checkpoint, com progresso salvo em disco e recuperado entre sessões.

**Definition of Done do Milestone:**
- [ ] Todos os Critérios de Aceite de VS-04 a VS-07 cumpridos.
- [ ] Code Review (Rubrica 4) e Playtest coletivo de encerramento (🔴 Semana 7) satisfeitos.
- [ ] DC-01 (construção de `Chest`/`Pickup`) resolvido **ou** contornado com o placeholder documentado no próprio Design Card antes de a VS-06/VS-07 serem dadas como concluídas.

---

## MS-3 — Resolver Problemas

**Semanas:** 8–11 · **Vertical Slices:** VS-08, VS-09, VS-10, VS-11 · **Hero Cards:** HC-08, HC-09, HC-10, HC-11

**Objetivo:** transformar o gameplay funcional em um Vertical Slice jogável completo — vida/dano, animação, interface em tempo real, inventário, IA de inimigo e combate simples.

**Escopo:**
- Troca da `CapsuleMesh` de placeholder pelo modelo animado do Kenney Mini Characters.
- `HealthComponent` (vida/dano/morte) + AnimationTree (State Machine) + BlendSpace/AnimationPlayer.
- HUD (Control nodes + CanvasLayer) e PauseMenu.
- `InventoryComponent` + `InventoryUI`, ampliação do sistema de interação.
- `NavigationRegion3D`/`NavigationAgent3D`, `Enemy` com Behavior Tree/Blackboard (LimboAI) e combate simples (`Area3D`/`RayCast3D` → `apply_damage`).

**Produto jogável ao final:** Vertical Slice completo — Player animado, vida, HUD, inventário funcional, um inimigo autônomo que persegue e troca dano com o Player.

**Definition of Done do Milestone:**
- [ ] Todos os Critérios de Aceite de VS-08 a VS-11 cumpridos.
- [ ] Playtest coletivo + Showcase de encerramento (🔴 Semana 11) satisfeitos.
- [ ] DC-03 (morte/respawn do Player) e DC-04 (consequência da morte do Enemy) resolvidos antes de a VS-11 ser dada como concluída — sem eles, o combate simples não tem estado final definido.

---

## MS-4 — Produzir como um Pequeno Estúdio

**Semanas:** 12–14 · **Vertical Slices:** VS-12, VS-13, VS-14 · **Hero Cards:** HC-12, HC-13, HC-14

**Objetivo:** polir tecnicamente o Vertical Slice já completo — nenhuma mecânica nova, apenas produção em escala de estúdio.

**Escopo:**
- Material Overrides/Unique Materials, auditoria e refatoração dos materiais existentes.
- `MultiMeshInstance3D` (Foliage) na zona externa.
- Áudio integrado a eventos (`AudioStreamPlayer`).
- Profiling e otimização com o Debugger/Profiler nativo.
- Export Templates, preset de exportação, build final.

**Produto jogável ao final:** o mesmo Vertical Slice de MS-3, agora visualmente consistente, sonorizado, otimizado e exportado como build distribuível.

**Definition of Done do Milestone:**
- [ ] Todos os Critérios de Aceite de VS-12 a VS-14 cumpridos.
- [ ] Code Review de materiais (Semana 12), Feedback formal de otimização (Semana 13) e entrega final + Playtest cruzado (🔴 Semana 14) satisfeitos.
- [ ] DC-02 (objetivo final) e DC-05 (evolução do `SaveData`) resolvidos — o build final não pode ser considerado "completo" sem um objetivo que o encerre e sem um save que cubra todo o estado acumulado.

---

## MS-5 — Comparar Arquiteturas

**Semanas:** 15–17 · **Vertical Slices:** VS-15, VS-16, VS-17 · **Hero Cards:** HC-15

**Objetivo:** nenhuma implementação nova. Análise arquitetural comparada (Godot Demo Projects, Unity, e um motor adicional) e apresentação técnica final.

**Escopo:** leitura dirigida, quadro comparativo, checkpoint de preparação, apresentação final. Nenhum Implementation Card existe neste Milestone — apenas cards de análise/documentação (ver `Implementation_Backlog/Modulo_5_Analysis_Cards.md`).

**Produto ao final:** nenhum artefato de código novo. O "produto" é a capacidade demonstrada de comparar a arquitetura do próprio projeto com referências externas.

**Definition of Done do Milestone:**
- [ ] Quadro comparativo Godot × Unity × motor adicional produzido (Semana 16).
- [ ] Apresentação técnica final realizada (Semana 17).
- [ ] Nenhuma tentativa de "corrigir" ou alterar código do Vertical Slice durante este módulo (regra explícita do Cronograma, Semana 15).
