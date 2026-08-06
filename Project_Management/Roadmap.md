# Roadmap — Vertical Slice *O Templo Esquecido*

**Papel deste documento:** visão executiva do plano de produção. Detalhamento completo em `Milestones.md`, `Vertical_Slices.md`, `Design_Backlog/` e `Implementation_Backlog/`.

**Fonte de verdade (ordem de prioridade em caso de conflito):**
1. [`docs/Cronograma_Tendencias_de_Motores_de_Jogos.md`](../docs/Cronograma_Tendencias_de_Motores_de_Jogos.md) — sequência e escopo de cada semana.
2. [`PROJECT_ARCHITECTURE.md`](../PROJECT_ARCHITECTURE.md) — regras, arquitetura e o que pode/não pode ser implementado.
3. `docs/Tutoriais/*` — especificação concreta (nomes de arquivo, Nodes, métodos) para as Semanas 1–7 (Módulos 1–2; a partir do Módulo 3 não há tutoriais passo a passo, por regra pedagógica — ver `PEDAGOGICAL_RULES.md`).

Nenhuma informação deste plano contradiz essas três fontes. Onde as três são omissas sobre uma decisão necessária para implementar algo, este plano **não inventa a regra** — abre um Design Card (ver `Design_Backlog/Design_Cards.md`) e bloqueia o Implementation Card correspondente até a regra existir em `PROJECT_ARCHITECTURE.md`.

---

## Hierarquia do Planejamento

```
Milestones (5 — um por Módulo/Unidade do Cronograma)
   ↓
Vertical Slices (17 — uma por semana do Cronograma)
   ↓
Hero Cards (15 — um por sistema/família de sistemas)
   ↓
Design Cards (regras faltantes) ──→ atualizam PROJECT_ARCHITECTURE.md
   ↓
Implementation Cards (tarefas de código, Tipo A ou B, ≤ 8 pontos cada)
```

## Regra de Classificação (repetida de `Design_Backlog/README` para consulta rápida)

| Tipo | Situação | Ação |
|---|---|---|
| **A — Implementação Direta** | Especificação suficiente já existe (tutorial e/ou PROJECT_ARCHITECTURE.md). | Criar Implementation Card. |
| **B — Placeholder** | A arquitetura/estrutura existe, mas um valor numérico ou de conteúdo está em aberto (às vezes de propósito pedagógico — "com liberdade de solução"). | Criar Implementation Card, declarando explicitamente o placeholder e o que precisa ser confirmado depois. |
| **C — Bloqueado por Regra** | Não existe decisão de design suficiente para implementar (nenhuma menção, nem exemplo, nem liberdade explícita — apenas um vazio). | **Não** criar Implementation Card. Criar Design Card. A implementação correspondente fica `Blocked By` esse Design Card. |

---

## Milestones × Vertical Slices

| Milestone | Semanas | Vertical Slices | Produto Jogável ao Final |
|---|---|---|---|
| **MS-1** — Aprender a Ferramenta | 1–3 | VS-01, VS-02, VS-03 | Primeiro build executável: Player explora um graybox externo, com material, terreno e iluminação global. |
| **MS-2** — Construir Sistemas | 4–7 | VS-04, VS-05, VS-06, VS-07 | Gameplay funcional: portas, alavancas, baús e checkpoints conectados em um fluxo único, com progresso persistente entre sessões. |
| **MS-3** — Resolver Problemas | 8–11 | VS-08, VS-09, VS-10, VS-11 | Vertical Slice jogável completo: animação, HUD, inventário, interação ampliada, IA e combate simples integrados. |
| **MS-4** — Produzir como um Pequeno Estúdio | 12–14 | VS-12, VS-13, VS-14 | Vertical Slice final, polido, otimizado e exportado como build distribuível. |
| **MS-5** — Comparar Arquiteturas | 15–17 | VS-15, VS-16, VS-17 | Nenhum código novo. Produto = análise arquitetural e apresentação técnica final. |

🔴 = semana de encerramento de módulo (Checkpoint/Code Review/Playtest/Apresentação), conforme o Cronograma.

---

## Hero Cards (visão geral — detalhe em `Design_Backlog/Hero_Cards.md`)

| ID | Hero Card | Milestone | Semanas |
|---|---|---|---|
| HC-01 | Editor, Projeto e Scene Tree | MS-1 | 1 |
| HC-02 | Locomoção do Player e Input Map | MS-1 | 2 |
| HC-03 | Renderização, Terreno e Pipeline de Exportação | MS-1 | 3 |
| HC-04 | Framework de Autoload (GameManager/SaveManager) | MS-2 | 4 |
| HC-05 | Contrato Interactable e Signals | MS-2 | 5 |
| HC-06 | Camada de Dados (ItemData/Enum) | MS-2 | 6 |
| HC-07 | Persistência em Disco (SaveData/SaveComponent/Checkpoint) | MS-2 | 7 |
| HC-08 | HealthComponent e Sistema de Animação | MS-3 | 8 |
| HC-09 | HUD e UI (Control Nodes) | MS-3 | 9 |
| HC-10 | Inventário e Interação Ampliada | MS-3 | 10 |
| HC-11 | IA de Inimigos e Combate Simples | MS-3 | 11 |
| HC-12 | Materiais e Composição de Cena | MS-4 | 12 |
| HC-13 | Áudio, Profiling e Otimização | MS-4 | 13 |
| HC-14 | Exportação Final e Consolidação | MS-4 | 14 |
| HC-15 | Análise Arquitetural Comparada | MS-5 | 15–17 |

---

## Design Cards abertos (gaps Tipo C identificados nesta leitura — ver detalhe em `Design_Backlog/Design_Cards.md`)

| ID | Título | Bloqueia |
|---|---|---|
| DC-01 | Construção de `Chest`/`Pickup` nunca especificada | IC-VS06-03, IC-VS07-04 |
| DC-02 | Definição mecânica do "objetivo final único" | IC-VS14-03 (ou onde o objetivo for implementado) |
| DC-03 | Fluxo de morte/respawn do Player | IC-VS08-02 (parcial), IC-VS11-04 |
| DC-04 | Consequência da morte do Enemy | IC-VS11-04 |
| DC-05 | Evolução do schema de `SaveData` para os Módulos 3–4 (inventário, vida, estado de inimigos) | IC-VS10-04, IC-VS14-02 |

Nenhum destes cinco itens tem Implementation Card — apenas Design Card, até que `PROJECT_ARCHITECTURE.md` seja atualizado com a decisão.

---

## Como navegar este plano

1. Comece por `Milestones.md` para entender o produto esperado de cada módulo.
2. Abra `Vertical_Slices.md` para a semana específica — cada slice lista os Hero/Design/Implementation Cards relevantes.
3. Para implementar algo, vá direto ao Implementation Card em `Implementation_Backlog/` — ele contém o passo a passo, arquivos esperados, testes e critérios de aceite.
4. Se um Implementation Card estiver marcado `Blocked By: DC-XX`, resolva (ou peça ao professor/orientador para resolver) o Design Card primeiro, atualizando `PROJECT_ARCHITECTURE.md` — só depois volte ao Implementation Card.
5. `Codecks/` contém a mesma informação em JSON, pronta para importação em um board Codecks (ou equivalente), já que não há integração de API/MCP disponível neste ambiente.
