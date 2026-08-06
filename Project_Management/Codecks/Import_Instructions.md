# Import Instructions

Nenhuma integração de API/MCP com Codecks estava disponível no ambiente em que este plano foi gerado. Esta pasta é o fallback em arquivo descrito no prompt original ("Caso não exista [API]: Gerar `Project_Management/...`"). Os arquivos aqui são estruturados para importação manual ou para alimentar um script de importação futuro, caso uma integração de API venha a existir.

## Estrutura dos arquivos

- `Manifest.json` — visão geral do projeto e contagem de cards por deck.
- `Heroes.json` — **não gerado como JSON separado**; o conteúdo completo dos 15 Hero Cards vive em `../Design_Backlog/Hero_Cards.md` (cada `##` é um Hero Card pronto para virar um card de deck "Heroes"). Isso evita duplicar texto longo em dois formatos.
- `Design_Cards.json` — os 5 Design Cards (gaps Tipo C), em formato estruturado, com `body_ref` apontando para o texto completo em `../Design_Backlog/Design_Cards.md`.
- `Implementation_Cards.json` — os 51 Implementation Cards (46 executáveis + 5 stubs bloqueados Tipo C), com `body_ref` apontando para o texto completo (todos os campos do template obrigatório — Objetivo, Contexto, Implementação, Restrições, Testes, Critérios de Aceite, Definition of Done) em `../Implementation_Backlog/Modulo_N_*.md`.
- `Dependencies.json` — grafo de dependências (`blocked_by`/`blocks`) em formato de arestas, para quem for montar a visualização de dependências no board.

## Por que o corpo completo não está duplicado em JSON

Cada Implementation Card tem, no `.md`, entre 200 e 500 palavras de conteúdo estruturado (passo a passo, restrições, testes). Duplicar isso integralmente em JSON criaria dois textos-fonte divergindo com o tempo. O JSON carrega os campos que um board precisa para **estrutura e automação** (id, título, tipo, pontos, dependências, deck/milestone) — o campo `body_ref` aponta para o texto completo, que deve ser colado no campo de descrição do card ao importar manualmente.

## Passo a passo de importação manual (Codecks ou equivalente)

1. Criar um Deck "Milestones" com 5 cards, um por bloco `## MS-N` de `../Milestones.md`.
2. Criar um Deck "Vertical Slices" com 17 cards, um por bloco `## VS-NN` de `../Vertical_Slices.md`. Vincular cada um ao Milestone correspondente (ver `Roadmap.md`, tabela "Milestones × Vertical Slices").
3. Criar um Deck "Hero Cards" com 15 cards, um por bloco `## HC-NN` de `../Design_Backlog/Hero_Cards.md`.
4. Criar um Deck "Design Cards" a partir de `Design_Cards.json` — para cada entrada, criar um card com o título, colar o corpo completo de `../Design_Backlog/Design_Cards.md` (seção correspondente ao `id`), e marcar a tag `blocked-by-design`.
5. Criar um Deck "Implementation Cards" a partir de `Implementation_Cards.json` — para cada entrada:
   - Título = `title`.
   - Corpo = colar a seção correspondente de `Implementation_Backlog/Modulo_N_*.md` (usar `body_ref`).
   - Tag de tipo: `tipo-a`, `tipo-b` ou `tipo-c-bloqueado`.
   - Story Points = campo `story_points` (cards `C_blocked_stub` não recebem pontos — não são estimáveis até o Design Card ser resolvido).
   - Vincular ao Hero Card (`hero_card`) e à Vertical Slice (`vertical_slice`).
6. Usar `Dependencies.json` para criar as relações "Blocked By"/"Blocks" entre cards no board (a maioria dos boards com suporte a dependências aceita importação de arestas `from`/`to`).
7. Cards com `type: "C_blocked_stub"` devem ser criados no board **sem** permitir que sejam movidos para "Em Progresso"/"Concluído" até o Design Card correspondente (`blocked_by`) ser fechado — configurar essa regra manualmente se o board não suportar bloqueio automático via dependência.

## Manutenção

Sempre que um Design Card (`DC-XX`) for resolvido (ou seja, `PROJECT_ARCHITECTURE.md` for atualizado com a decisão que faltava):
1. Atualizar o `status` do Design Card para `"resolved"` em `Design_Cards.json`.
2. Escrever o Implementation Card completo (que hoje é apenas um stub bloqueado) em seu arquivo `Implementation_Backlog/Modulo_N_*.md`, seguindo o mesmo template de todas as outras cartas.
3. Adicionar a entrada correspondente, agora com `type: "A"` ou `"B"` e `story_points` definidos, em `Implementation_Cards.json`.
4. Remover a aresta `design_card_edges` correspondente de `Dependencies.json` (o Design Card não bloqueia mais nada) e, se necessário, adicionar novas arestas `implementation_card_edges`.
