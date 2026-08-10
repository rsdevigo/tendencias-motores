# Implementation Cards — Milestone MS-1 (Semanas 1–3)

Fonte primária: `docs/Tutoriais/Tutorial_Semana_01_*.md` a `Tutorial_Semana_03_*.md` (Módulo 1 tem tutorial passo a passo completo — todas as cartas abaixo são **Tipo A**, salvo indicação contrária).

---

## IC-VS01-01 — Estrutura Inicial de Pastas do Projeto

**Objetivo:** criar a estrutura de pastas do projeto conforme a convenção oficial, antes de qualquer asset ou script.

**Contexto:** primeira tarefa do semestre — nenhum arquivo do projeto existe ainda além do `project.godot` gerado pelo Godot ao criar o projeto `TemploEsquecido`.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §8; `Tutorial_Semana_01_Encontro_1.md` (Parte 3).

**Tipo:** A

**Arquivos Esperados:** apenas pastas (nenhum arquivo de conteúdo ainda):
```
res://scenes/{characters,interactables,ui,levels/exploration,levels/dungeon}
res://scripts/{autoload,components}
res://orchestrations/
res://resources/{items,save}
res://assets/{prototype,dungeon,nature,characters}
res://materials/
res://audio/
res://animations/
```

**Implementação:**
1. No FileSystem Dock, criar cada pasta acima via botão direito > New Folder.
2. Confirmar contra a listagem de `PROJECT_ARCHITECTURE.md` §8 — nenhuma pasta faltando, mesmo vazia.

**Restrições:** não usar PascalCase ou espaços em nomes de pasta (convenção é snake_case); nenhum asset solto na raiz de `res://`.

**Testes:** inspeção visual do FileSystem Dock contra a árvore de `PROJECT_ARCHITECTURE.md` §8.

**Critérios de Aceite:**
- [ ] Todas as pastas listadas acima existem.
- [ ] Nenhum nome de pasta fora da convenção snake_case.

**Definition of Done:** estrutura idêntica à listagem do Tutorial (Semana 1, Encontro 1, checklist).

**Dependências:** Blocked By: nenhuma. Blocks: IC-VS01-02, IC-VS01-03.

**Story Points:** 1

---

## IC-VS01-02 — Download e Importação dos 3 Pacotes Kenney

**Objetivo:** ter todos os assets de arte do projeto disponíveis desde a primeira semana.

**Contexto:** os 3 pacotes (Mini Dungeon, Mini Forest, Mini Characters) só serão *usados* em semanas distintas (3/5, 8, 12), mas são importados de uma só vez para não interromper semanas futuras.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §3; `Tutorial_Semana_01_Encontro_1.md` (Parte 4).

**Tipo:** A

**Arquivos Esperados:**
```
res://assets/dungeon/*.glb (ou .gltf)
res://assets/forest/*.glb
res://assets/characters/*.glb (Kenney Mini Characters)
```

**Implementação:**
1. Baixar em kenney.nl: Mini Dungeon, Mini Forest, Mini Characters.
2. Extrair cada `.zip` fora do projeto.
3. Arrastar os arquivos de modelo de cada pacote para a subpasta correspondente em `assets/` via FileSystem Dock.
4. Aguardar importação; conferir ausência de ícone de erro em cada arquivo.
5. Para Mini Characters, confirmar na aba **Import** que as animações (idle, walk, run) aparecem listadas.

**Restrições:** nunca copiar o `.zip` inteiro para dentro de `assets/`; nunca mover arquivos já importados pelo explorador do SO (sempre pelo FileSystem Dock).

**Testes:** clicar em um arquivo importado de cada pasta e confirmar pré-visualização na aba Import, sem erro.

**Critérios de Aceite:**
- [ ] As 4 subpastas contêm arquivos, sem ícone de erro.
- [ ] Animações do Mini Characters visíveis na aba Import.

**Definition of Done:** checklist do Tutorial (Semana 1, Encontro 1) 100% quanto a assets.

**Dependências:** Blocked By: IC-VS01-01. Blocks: IC-VS02-01 (Malha), IC-VS03-01 (material), IC-VS08-01 (troca de modelo do Player).

**Story Points:** 2

---

## IC-VS01-03 — Primeira Scene: NivelTeste, Chao, LuzPrincipal

**Objetivo:** construir a primeira Scene do projeto, demonstrando composição via Nodes filhos.

**Contexto:** encerra o Encontro 2 da Semana 1; é a base sobre a qual o Player (VS-02) e o terreno (VS-03) serão construídos.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §9; `Tutorial_Semana_01_Encontro_2.md`.

**Tipo:** A

**Arquivos Esperados:**
```
res://scenes/levels/exploration/level_exploration.tscn
res://orchestrations/nivel_teste.torch
```

**Implementação:**
1. Criar Scene com Node raiz `Node3D`, renomeado para `NivelTeste`.
2. Adicionar `MeshInstance3D` + `StaticBody3D`/`CollisionShape3D` como filho, renomeado `Chao`, com uma malha plana (ex.: `PlaneMesh` ou `BoxMesh` achatado).
3. Adicionar `DirectionalLight3D` ou `OmniLight3D` como filho, renomeado `LuzPrincipal`.
4. Salvar em `scenes/levels/exploration/level_exploration.tscn`.
5. Criar Orchestration associada ao Node raiz, salva como `nivel_teste.torch`, com um evento **Ready** conectado a um log de teste.
6. Rodar com F6, confirmar log no Output.

**Restrições:** nenhum Node com nome padrão do editor (`Node3D`, `MeshInstance3D` genérico) — todos renomeados por função.

**Testes:** F6 sem erro; log do evento Ready visível no Output.

**Critérios de Aceite:**
- [ ] Hierarquia `NivelTeste` > `Chao`, `LuzPrincipal` existe e está nomeada corretamente.
- [ ] Orchestration `nivel_teste.torch` funcional (evento Ready testado).

**Definition of Done:** checklist do Tutorial (Semana 1, Encontro 2) 100%.

**Dependências:** Blocked By: IC-VS01-01. Blocks: IC-VS01-04, IC-VS02-01.

**Story Points:** 2

---

## IC-VS01-04 — Desafio: Node Adicional Autônomo

**Objetivo:** praticar composição de forma independente, sem demonstração prévia.

**Contexto:** desafio de encerramento do Encontro 2 da Semana 1 — primeira tarefa sem passo a passo guiado.

**Documentos de Referência:** `Tutorial_Semana_01_Encontro_2.md` (seção Desafio).

**Tipo:** B — liberdade de escolha explícita ("não há solução única"); qualquer Node filho coerente com o Vertical Slice satisfaz o critério.

**Arquivos Esperados:** modificação em `level_exploration.tscn` (Node adicional, sem novo arquivo).

**Implementação:**
1. Adicionar um Node filho a `NivelTeste`, distinto do demonstrado (ex.: um segundo `MeshInstance3D` com forma diferente, ou uma `OmniLight3D` extra).
2. Nomear por função, não pelo tipo padrão.

**Restrições:** o Node deve produzir um comportamento/efeito visual diferente do já demonstrado (não uma cópia).

**Testes:** inspeção visual no Viewport (F6).

**Critérios de Aceite:**
- [ ] Node adicional existe, nomeado por função, com efeito visual distinto do exemplo do professor/tutorial.

**Definition of Done:** hierarquia permanece legível (sem excesso de Nodes desorganizados).

**Dependências:** Blocked By: IC-VS01-03. Blocks: nenhuma.

**Story Points:** 1

---

## IC-VS02-01 — Player: CharacterBody3D, Colisão e Malha Placeholder

**Objetivo:** montar o Node do Player, fisicamente sólido, ainda sem movimento.

**Contexto:** primeira etapa da Semana 2; o Player ainda não responde a input algum ao final desta carta.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §7, §9; `Tutorial_Semana_02_Encontro_1.md`.

**Tipo:** A

**Arquivos Esperados:**
```
res://scenes/characters/Player.tscn
res://orchestrations/player.torch
```

**Implementação:**
1. Em `level_exploration.tscn`, adicionar `CharacterBody3D` filho de `NivelTeste`, renomeado `Player`.
2. Adicionar `CollisionShape3D` filho (ex.: `CapsuleShape3D`).
3. Adicionar `MeshInstance3D` filho, renomeado `Malha`, com `CapsuleMesh` (placeholder de graybox — ver IC-VS08-01 para a substituição futura).
4. Alinhar `Malha` e `CollisionShape3D` visualmente sobre `Chao`.
5. Criar Orchestration `player.torch`, com evento **PhysicsProcess** chamando `move_and_slide()` (sem atribuir velocidade ainda).
6. **Save Branch as Scene** → `scenes/characters/Player.tscn`.
7. F6: confirmar Player sólido, parado, sem erro.

**Restrições:** não atribuir velocidade a `velocity` nesta carta — isso pertence a IC-VS02-02. Não deixar o Player como Node solto (deve ser salvo como Scene própria).

**Testes:** F6 sem erro; Player não afunda nem flutua sobre `Chao`.

**Critérios de Aceite:**
- [ ] `Player.tscn` existe como Scene própria, instanciada em `level_exploration.tscn`.
- [ ] `CollisionShape3D` e `Malha` alinhados.
- [ ] `player.torch` chama `move_and_slide()` a cada PhysicsProcess, sem erro.

**Definition of Done:** checklist do Tutorial (Semana 2, Encontro 1) 100%.

**Dependências:** Blocked By: IC-VS01-03, IC-VS01-02 (Malha placeholder não depende de asset externo, mas a pasta `assets/characters/` já deve existir). Blocks: IC-VS02-02.

**Story Points:** 3

---

## IC-VS02-02 — Input Map e Movimentação

**Objetivo:** tornar o Player controlável nas 4 direções.

**Contexto:** segunda etapa da Semana 2; conecta o Input Map lido pela Orchestration à `velocity` do `CharacterBody3D`.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §6; `Tutorial_Semana_02_Encontro_2.md`.

**Tipo:** B — a velocidade de movimento não tem valor canônico definido em `PROJECT_ARCHITECTURE.md`; o próprio tutorial usa "por exemplo, 5.0" como placeholder explícito.

**Arquivos Esperados:** modificação em `player.torch`; 4 novas Actions em `project.godot` (Input Map).

**Implementação:**
1. Em Project Settings > Input Map, criar Actions `move_forward` (W), `move_back` (S), `move_left` (A), `move_right` (D).
2. Em `player.torch`, dentro do PhysicsProcess já existente, ler as 4 Actions (`Input.get_action_strength` ou nó equivalente do Orchestrator).
3. Combinar em um vetor de direção 2D; transformar em velocidade 3D multiplicando por uma constante placeholder (**declarar explicitamente**: `# PLACEHOLDER: velocidade de movimento aguardando definição em PROJECT_ARCHITECTURE.md — valor de exemplo do tutorial: 5.0`).
4. Atribuir o resultado a `velocity` **antes** da chamada já existente a `move_and_slide()`.

**Restrições:** a leitura de input e a movimentação devem ocorrer dentro do evento PhysicsProcess, nunca em Process comum. A ordem `velocity` → `move_and_slide()` é obrigatória.

**Testes:** F6; mover nas 4 direções; encostar em obstáculo e confirmar deslizamento sem travar/atravessar.

**Critérios de Aceite:**
- [ ] Input Map com as 4 Actions de movimento.
- [ ] Player se move corretamente nas 4 direções e desliza em colisões.
- [ ] Comentário de placeholder presente no código junto à constante de velocidade.

**Definition of Done:** checklist do Tutorial (Semana 2, Encontro 2) 100% (exceto o item do desafio, ver IC-VS02-03).

**Dependências:** Blocked By: IC-VS02-01. Blocks: IC-VS02-03, IC-VS03-01 (build precisa de Player móvel para ser testável), IC-VS05-02.

**Story Points:** 3

---

## IC-VS02-03 — Desafio: Action Adicional (Correr/Agachar/Pular)

**Objetivo:** praticar extensão do Input Map com liberdade de implementação.

**Contexto:** desafio de encerramento da Semana 2.

**Documentos de Referência:** `Tutorial_Semana_02_Encontro_2.md` (seção Desafio).

**Tipo:** B — "liberdade de implementação... não há solução única" (explícito no tutorial).

**Arquivos Esperados:** nova Action em Input Map; modificação em `player.torch`.

**Implementação:**
1. Escolher e criar uma Action não demonstrada (`run`, `crouch` ou `jump`).
2. Implementar o efeito (ex.: multiplicador de velocidade para correr; impulso em `velocity.y` para pular), reaproveitando o placeholder de velocidade de IC-VS02-02.

**Restrições:** não remover ou quebrar as 4 Actions de movimento já existentes.

**Testes:** F6; acionar a nova Action e confirmar o efeito esperado.

**Critérios de Aceite:**
- [ ] Nova Action funcional, sem regressão nas demais.

**Definition of Done:** checklist do Tutorial (Semana 2, Encontro 2) 100%.

**Dependências:** Blocked By: IC-VS02-02. Blocks: nenhuma.

**Story Points:** 2

---

## IC-VS03-01 — Material do Graybox (StandardMaterial3D + Kenney Mini Dungeon)

**Objetivo:** dar aparência de superfície ao `Chao`.

**Contexto:** primeira etapa da Semana 3; primeiro uso efetivo das texturas do Kenney Mini Dungeon (importado desde a Semana 1).

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §3; `Tutorial_Semana_03_Encontro_1.md` (Parte 1).

**Tipo:** A

**Arquivos Esperados:** `res://materials/chao_prototype.tres`

**Implementação:**
1. Selecionar `Chao`; no Inspector, criar **New StandardMaterial3D** em Material Override.
2. Salvar como recurso externo: `materials/chao_prototype.tres`.
3. Atribuir textura do Kenney Mini Dungeon ao campo Albedo.
4. Ajustar Roughness entre 0.6 e 0.8.
5. Confirmar visualmente textura sem distorção exagerada (ajustar UV1 Scale se necessário).

**Restrições:** material deve ser recurso externo (`.tres`), nunca embutido na Scene.

**Testes:** inspeção visual no Viewport.

**Critérios de Aceite:**
- [ ] `chao_prototype.tres` existe, aplicado ao `Chao`, com textura e Roughness ajustados.

**Definition of Done:** checklist do Tutorial (Semana 3, Encontro 1), itens de material.

**Dependências:** Blocked By: IC-VS01-02, IC-VS02-02. Blocks: IC-VS03-02.

**Story Points:** 2

---

## IC-VS03-02 — Terreno via Terrain3D

**Objetivo:** modelar um terreno básico (elevação + depressão) sobre a área de exploração.

**Contexto:** segunda etapa da Semana 3, mesmo Encontro 1.

**Documentos de Referência:** `Tutorial_Semana_03_Encontro_1.md` (Parte 1, passos de Terrain3D).

**Tipo:** A

**Arquivos Esperados:** `res://resources/terrain/` (Terrain3D Storage).

**Implementação:**
1. Confirmar addon Terrain3D instalado/habilitado em Project Settings > Plugins.
2. Adicionar Node `Terrain3D` a `level_exploration.tscn`; Storage salva em `resources/terrain/`.
3. Esculpir uma elevação suave e uma depressão rasa em áreas distintas.
4. Pintar ao menos uma textura do Kenney Mini Dungeon sobre a área esculpida.
5. Reposicionar o `Player` sobre uma área plana do novo terreno (evitar spawn dentro de elevação).

**Restrições:** não esculpir relevo sob o ponto de spawn do Player.

**Testes:** F6; confirmar Player não preso/flutuando sobre o novo terreno; movimentação (IC-VS02-02) continua funcional sobre a superfície esculpida.

**Critérios de Aceite:**
- [ ] Node `Terrain3D` com Storage salva externamente, elevação/depressão visíveis, textura pintada.
- [ ] Player posicionado corretamente sobre área plana.

**Definition of Done:** checklist do Tutorial (Semana 3, Encontro 1) 100%.

**Dependências:** Blocked By: IC-VS03-01. Blocks: IC-VS03-03.

**Story Points:** 3

---

## IC-VS03-03 — Iluminação Global (WorldEnvironment + SDFGI)

**Objetivo:** ativar iluminação indireta em tempo real sobre o nível.

**Contexto:** primeira etapa do Encontro 2 da Semana 3.

**Documentos de Referência:** `Tutorial_Semana_03_Encontro_2.md` (Parte 1).

**Tipo:** A

**Arquivos Esperados:** `res://resources/environment_exploration.tres`

**Implementação:**
1. Adicionar Node `WorldEnvironment` a `NivelTeste` (se ainda não existir).
2. Criar recurso `Environment`, salvo em `resources/environment_exploration.tres`.
3. Habilitar SDFGI; ajustar escala/célula compatível com a extensão do terreno.
4. Ajustar intensidade de `LuzPrincipal` em conjunto com o SDFGI, comparando visualmente ativado/desativado.

**Restrições:** `Environment` deve ser recurso externo, nunca embutido.

**Testes:** F6; comparar visualmente SDFGI ligado/desligado — diferença deve ser perceptível nas áreas de sombra.

**Critérios de Aceite:**
- [ ] `WorldEnvironment` com `Environment` externo, SDFGI habilitado e com efeito visível.

**Definition of Done:** checklist do Tutorial (Semana 3, Encontro 2), itens de iluminação.

**Dependências:** Blocked By: IC-VS03-02. Blocks: IC-VS03-04.

**Story Points:** 2

---

## IC-VS03-04 — Pipeline de Exportação e Primeiro Build 🔴

**Objetivo:** gerar o primeiro executável do Vertical Slice, fora do editor. **Checkpoint de encerramento do Milestone MS-1.**

**Contexto:** última etapa da Semana 3 — fecha a Unidade I.

**Documentos de Referência:** `Tutorial_Semana_03_Encontro_2.md` (Parte 3).

**Tipo:** A

**Arquivos Esperados:** `builds/semana_03/` (executável + arquivos de dados gerados pelo Godot).

**Implementação:**
1. Confirmar Export Templates instalados (Editor > Manage Export Templates).
2. Project > Export > Add... > selecionar plataforma-alvo do laboratório/máquina.
3. Nomear preset de forma identificável ("Build Semana 3"); conferir aba Resources.
4. Export Project → `builds/semana_03/`, nome de executável identificável.
5. Executar o binário gerado **fora do editor**; confirmar nível completo (terreno, material, iluminação) e Player controlável.

**Restrições:** não considerar a etapa concluída sem testar o executável fora do editor — "rodar no editor" não é build validado.

**Testes:** execução direta do binário; movimentação do Player testada fora do editor.

**Critérios de Aceite:**
- [ ] Executável gerado em `builds/semana_03/`.
- [ ] Roda fora do editor sem erro, com todos os sistemas do Módulo 1 funcionais.

**Definition of Done:** Checkpoint de encerramento do Módulo 1 (Cronograma, Semana 3) cumprido; Showcase em aula realizado (se aplicável ao contexto de entrega).

**Dependências:** Blocked By: IC-VS03-03. Blocks: todo o Milestone MS-2 (VS-04 em diante).

**Story Points:** 3
