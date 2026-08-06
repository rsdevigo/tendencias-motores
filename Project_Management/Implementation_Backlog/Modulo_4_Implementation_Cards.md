# Implementation Cards — Milestone MS-4 (Semanas 12–14)

**Nota de fonte:** sem Tutoriais passo a passo (Módulo 4, autonomia alta — professor como diretor técnico). Cartas derivadas de `PROJECT_ARCHITECTURE.md` §6 e do Cronograma (Semanas 12–14). Nenhuma mecânica nova é introduzida neste Milestone — apenas produção/polimento, exceto onde barrado por Design Card (objetivo final e schema de save).

---

## IC-VS12-01 — Auditoria e Refatoração de Materiais (Material Override)

**Objetivo:** eliminar duplicação de materiais acumulada desde a Semana 3.

**Contexto:** primeira etapa da Semana 12 — não altera geometria, mecânica ou gameplay.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6 (Módulo 4); `Cronograma` (Semana 12, Encontro 1).

**Tipo:** A

**Arquivos Esperados:** modificação em materiais existentes (`materials/`); nenhum arquivo de gameplay tocado.

**Implementação:**
1. Auditar os materiais existentes no projeto (acumulados desde a Semana 3).
2. Identificar candidatos a Material Override/Unique Material — instâncias de um mesmo tipo de objeto com pequenas variações que hoje duplicam o material inteiro.
3. Refatorar ao menos um conjunto de objetos para material base + Override parametrizado por instância.

**Restrições:** nenhuma alteração de mecânica, geometria ou sistema de gameplay; não introduzir Override onde já não há duplicação real (evitar otimização de baixo impacto).

**Testes:** comparação visual antes/depois — nenhuma mudança de aparência não intencional.

**Critérios de Aceite:**
- [ ] Ao menos um conjunto de objetos refatorado para material base + Override, sem duplicação equivalente.

**Definition of Done:** nenhuma regressão visual ou de gameplay em relação à VS-11.

**Dependências:** Blocked By: IC-VS11-04 (o combate precisa estar minimamente fechado antes do polimento começar — mesmo com a parte bloqueada de DC-03/DC-04 pendente). Blocks: IC-VS12-02.

**Story Points:** 3

---

## IC-VS12-02 — Foliage via MultiMeshInstance3D

**Objetivo:** compor a densidade visual da zona externa com performance controlada.

**Contexto:** segunda etapa da Semana 12.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §3 (Kenney Nature Kit), §6; `Cronograma` (Semana 12, Encontro 2).

**Tipo:** A

**Arquivos Esperados:** modificação em `level_exploration.tscn` (Node `MultiMeshInstance3D`).

**Implementação:**
1. Adicionar `MultiMeshInstance3D` à zona externa, usando assets do Kenney Nature Kit (`assets/nature/`, importado desde a Semana 1).
2. Compor vegetação/elementos de cena com atenção à densidade e ao impacto de performance.

**Restrições:** elementos compostos via `MultiMeshInstance3D` não têm lógica própria (sem colisão/interação individual) — não confundir com Scenes de gameplay.

**Testes:** Profiler (preview rápido) confirma que a densidade escolhida não derruba o frame rate de forma perceptível.

**Critérios de Aceite:**
- [ ] Zona externa composta via `MultiMeshInstance3D`, mantendo desempenho estável.
- [ ] Code Review de materiais e composição de cena realizado.

**Definition of Done:** Code Review (Semana 12) cumprido.

**Dependências:** Blocked By: IC-VS12-01. Blocks: IC-VS13-01.

**Story Points:** 3

---

## IC-VS13-01 — Áudio Integrado a Eventos de Gameplay

**Objetivo:** integrar som a interação, passos e ambiente — nunca como trilha genérica desconectada.

**Contexto:** primeira etapa da Semana 13.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6; `Cronograma` (Semana 13, Encontro 1).

**Tipo:** B — nenhum SFX específico é definido em `PROJECT_ARCHITECTURE.md`; a escolha de arquivos de áudio (ex.: Kenney Audio/Interface Sounds, mesma filosofia CC0 já usada para arte) fica a critério de quem implementa.

**Arquivos Esperados:** `res://audio/*` (arquivos de som); modificação nas Scenes de interação (`Door`, `Lever`, `Checkpoint`), no Player (passos) e no nível (ambiente).

**Implementação:**
1. Selecionar uma biblioteca CC0 de efeitos sonoros (ex.: Kenney Audio).
2. Adicionar `AudioStreamPlayer`/`AudioStreamPlayer3D` a cada evento: interação (Signal `interacted`/equivalente), passos do Player (condicionado ao movimento real), ambiente (loop de fundo).
3. **PLACEHOLDER**: escolha exata de cada som e seus volumes — documentar como decisão de quem implementa, sujeita a ajuste posterior.

**Restrições:** áudio deve reagir a eventos reais já existentes, nunca ser adicionado como camada desconectada da lógica.

**Testes:** cada evento (interagir, andar, ambiente) produz o som correspondente durante o gameplay real.

**Critérios de Aceite:**
- [ ] Sons integrados aos 3 tipos de evento (interação, passos, ambiente).

**Definition of Done:** nenhum som toca fora do evento que o justifica.

**Dependências:** Blocked By: IC-VS12-02. Blocks: IC-VS13-02.

**Story Points:** 3

---

## IC-VS13-02 — Profiling e Otimização

**Objetivo:** identificar e corrigir ao menos um gargalo real de desempenho, com base em dado medido, não em suposição.

**Contexto:** segunda etapa da Semana 13.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6; `Cronograma` (Semana 13, Encontro 2).

**Tipo:** B — o aspecto a otimizar (geometria, materiais, iluminação ou lógica de script/Orchestration) é escolha livre, condicionada ao que o profiling real do projeto revelar.

**Arquivos Esperados:** variável, conforme o gargalo identificado (pode tocar materiais, geometria, scripts ou Orchestrations).

**Implementação:**
1. Rodar o Profiler/Debugger nativo do Godot sobre o Vertical Slice completo.
2. Identificar o gargalo de maior impacto real (não o mais fácil de corrigir).
3. Aplicar uma otimização justificada pelos dados observados (ex.: instancing, LOD, occlusion culling, redução de complexidade de script).
4. Registrar a justificativa técnica (antes/depois no Profiler).

**Restrições:** a escolha do que otimizar deve ser justificada por dado real do Profiler, não por suposição.

**Testes:** comparação de métricas do Profiler antes/depois da otimização.

**Critérios de Aceite:**
- [ ] Gargalo real identificado e corrigido, com métrica de antes/depois registrada.

**Definition of Done:** Feedback formal sobre a otimização (Semana 13) recebido.

**Dependências:** Blocked By: IC-VS13-01. Blocks: IC-VS14-01.

**Story Points:** 5

---

## IC-VS14-01 — Build Final e Playtest Cruzado 🔴

**Objetivo:** empacotar o Vertical Slice completo (Módulos 1–4) e validá-lo de forma cruzada.

**Contexto:** primeira parte da Semana 14 — reaproveita o pipeline de exportação de IC-VS03-04.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6; `Cronograma` (Semana 14).

**Tipo:** A

**Arquivos Esperados:** `builds/semana_14/` (ou pasta equivalente de build final).

**Implementação:**
1. Confirmar Export Templates e preset já configurados (reaproveitar IC-VS03-04).
2. Exportar o Vertical Slice completo, acumulado desde a Semana 1.
3. Realizar Playtest cruzado (testar com alguém fora do próprio desenvolvimento) sobre o build exportado, sem acesso ao projeto no editor.
4. Registrar problemas encontrados (bugs, desempenho, usabilidade), distinguindo ajuste pontual de retrabalho amplo.
5. Aplicar ajustes finais pontuais a partir do feedback, sem reabrir escopo.

**Restrições:** o Playtest deve ser conduzido sobre o build exportado, nunca sobre o projeto aberto no editor.

**Testes:** build roda fora do editor, do início ao fim, sem depender do ambiente de desenvolvimento.

**Critérios de Aceite:**
- [ ] Build final exportado e testado fora do editor.
- [ ] Playtest cruzado realizado, com observações registradas.
- [ ] Code Review de encerramento cobrindo todos os sistemas acumulados.

**Definition of Done:** entrega parcial + Code Review de encerramento (Semana 14 🔴) cumpridos.

**Dependências:** Blocked By: IC-VS13-02. Blocks: IC-VS14-02, IC-VS14-03.

**Story Points:** 5

---

## IC-VS14-02 — Validação do SaveData Completo no Build Final

**STATUS: BLOQUEADO — Tipo C. Nenhum passo de implementação é definido aqui.**

**Motivo:** não é possível validar que o "progresso completo" persiste corretamente em um `SaveData` cujo schema final ainda não foi definido para cobrir inventário (`ItemData` completos, não apenas Strings), vida do Player e, possivelmente, estado do Enemy.

**Ver:** `Design_Backlog/Design_Cards.md` → **DC-05**.

**Dependências:** Blocked By: DC-05, IC-VS10-04. Blocks: fechamento formal de MS-4.

**Story Points:** não estimado.

---

## IC-VS14-03 — Implementação do Objetivo Final

**STATUS: BLOQUEADO — Tipo C. Nenhum passo de implementação é definido aqui.**

**Motivo:** `PROJECT_ARCHITECTURE.md` §4 lista "um objetivo final único que encerra o Vertical Slice" como item de escopo, mas não define seu gatilho, sua lógica, nem sua reação. Não há especificação suficiente para propor sequer um placeholder coerente sem inventar mecânica não descrita em nenhum documento-fonte.

**Ver:** `Design_Backlog/Design_Cards.md` → **DC-02**.

**Dependências:** Blocked By: DC-02. Blocks: fechamento formal de MS-4 e de VS-14 como "Vertical Slice completo e jogável do início ao fim".

**Story Points:** não estimado.
