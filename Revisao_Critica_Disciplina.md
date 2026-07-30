# Revisão Crítica — Disciplina "Tendências de Motores de Jogos"

*Comitê de revisão: Ensino Superior, Design Curricular, Unreal Engine 5, Desenvolvimento de Jogos, Engenharia de Software, Metodologias Ativas, Studio Based Learning, Challenge Based Learning, Game Design, Arquitetura de Software.*

---

## Pontos Fortes

1. **Coerência arquitetural notável entre Cronograma, Planos de Aula e PROJECT_ARCHITECTURE.md nas Semanas 1–7.** Cada Plano de Aula (1 a 7) reproduz com precisão os sistemas, dependências e nomenclaturas definidos em PROJECT_ARCHITECTURE.md (seção 6), incluindo referências cruzadas corretas ("retomado da Semana X") e antecipação do que será usado na semana seguinte.

2. **A progressão de autonomia (Scaffolded → Studio Based → Challenge Based → Studio Based/diretor técnico → Reverse Engineering) está de fato implementada**, não apenas declarada. As seções "Desafio" dos Planos de Aula mudam de "não há desafio, demonstração guiada" (Semanas 1–4) para desafios de liberdade real (a partir da Semana 4/5) e desafios sem indicação de ferramenta correta (Semana 8 em diante), o que é coerente com PEDAGOGICAL_RULES.txt.

3. **As quatro perguntas exigidas pelo CLAUDE.md (conceito universal / Unreal / Unity / transferência) aparecem sistematicamente** em praticamente todos os Planos de Aula e Slides revisados, com seções dedicadas "Conceitos Fundamentais" e "Comparação com Unity" bem escritas, sem cópia de documentação oficial (paráfrase didática consistente).

4. **Regra "tutoriais apenas nos Módulos 1 e 2" corretamente aplicada.** Os 14 tutoriais cobrem exatamente Semanas 1–7 (Encontros 1 e 2), e o Tutorial da Semana 5 Encontro 2, por exemplo, abre com o conceito universal (padrão observer) antes do passo a passo, conforme exigido por PEDAGOGICAL_RULES.txt.

5. **Bibliografia oficial e ementa reproduzidas integralmente e sem paráfrase** no Plano de Ensino, batendo literalmente com REFERENCES.md e CLAUDE.md.

6. **Slides bem construídos como apoio, não como substituto da aula**: pouco texto em tela, notas do apresentador ricas, sem reprodução de documentação da Epic, com "Imagem sugerida" descrita textualmente em vez de texto denso.

7. **Rubricas do Sistema de Avaliação são detalhadas, com guia para o professor, erros comuns e modelo de preenchimento** — raro em documentos desse tipo, e evita ambiguidade na aplicação.

---

## Problemas Encontrados

### 1. HealthComponent é tratado como pré-existente em três semanas seguidas, mas nunca é ensinado (Crítica)

A partir da **Semana 9** (`Plano_de_Aula_Semana_09.md`), o `HealthComponent` é citado como algo "já existente desde o Módulo 2" — textualmente: *"o `HealthComponent` já gerencia vida corretamente desde o Módulo 2"* (Semana 9, Conceitos Fundamentais) e *"`HealthComponent` (retomado do Módulo 2)"* (Semana 9, Recursos da Unreal). O mesmo padrão se repete na **Semana 10** (*"seguindo o mesmo padrão de composição já usado por `HealthComponent`"*) e na **Semana 11** (*"reutilizando o `HealthComponent` já existente"*, *"HealthComponent (reutilizado do Módulo 2)"*).

Não há nenhuma ocorrência de `HealthComponent` em nenhum Plano de Aula das Semanas 1 a 8. Nenhuma aula constrói, explica ou introduz o `HealthComponent`. O mesmo vale para o slide da Semana 9, que também assume o Component como pré-existente ("A vida do seu personagem já existe no projeto").

PROJECT_ARCHITECTURE.md (seção 6, tabela do Módulo 3) lista `HealthComponent` como sistema novo do **Módulo 3** ("Suporte mínimo a dano e combate simples"), não do Módulo 2 — o que reforça que a atribuição repetida ao "Módulo 2" nos Planos de Aula das Semanas 9–11 é um erro de continuidade, não apenas uma imprecisão de rótulo: o sistema nunca aparece em lugar nenhum como conteúdo novo.

**Impacto:** um professor que siga o material literalmente chegará à Semana 9 e tentará "recapitular" um Component que a turma nunca construiu. Isso quebra a promessa central da disciplina (nenhum sistema descartado, tudo construído incrementalmente) e compromete diretamente a apresentação final.

### 2. Sistema de combate (dano jogador↔inimigo) nunca é explicitamente ensinado (Crítica, ligada ao problema 1)

PROJECT_ARCHITECTURE.md define "Combate simples (uma forma de ataque do jogador, dano e vida)" como parte do escopo do jogo (seção 4) e do Módulo 3 (seção 6). O "Produto do módulo" (Semana 11) e os resumos das Semanas 15–17 mencionam "combate" como sistema já integrado ao Vertical Slice. Entretanto, nenhum Encontro entre as Semanas 1 e 11 tem como objetivo de aprendizagem, conteúdo ou "Recursos da Unreal" a implementação de dano do jogador a um inimigo ou vice-versa. O único ponto de contato é uma opção *facultativa* no desafio da Semana 8 ("reação a dano" como uma entre três opções de animação contextual).

**Impacto:** o "combate simples" citado como entregue no Módulo 3 e reafirmado nas Semanas 15–17 (inclusive na Apresentação Técnica Final, Semana 17) não tem lastro pedagógico em nenhuma aula, comprometendo diretamente a Rubrica 7 ("Gameplay: todos os sistemas de gameplay construídos ao longo do semestre... estão integrados").

### 3. BP_Checkpoint nunca recebe uma aula dedicada (Alta)

PROJECT_ARCHITECTURE.md (seção 6, Módulo 2) e COURSE_CONTEXT.md ("Desafios: Portas / Baús / Alavancas / NPCs / Checkpoints") listam `BP_Checkpoint` como sistema obrigatório do Módulo 2. Nenhuma das Semanas 4 a 7 tem checkpoint como objetivo de aprendizagem, conteúdo ou desafio. A única menção em todo o material didático é condicional, na Semana 7: *"conecta portas, alavancas, baús, **checkpoints (se já modelados)**"* — uma admissão implícita de que o checkpoint pode simplesmente não existir no projeto do grupo.

**Impacto:** um sistema arquiteturalmente obrigatório (presente na estrutura de pastas do PROJECT_ARCHITECTURE.md, seção 8: `Interactables/BP_Checkpoint`) nunca tem uma aula que o construa.

### 4. "Desafios Técnicos" da Sistema de Avaliação não cobre todas as semanas que de fato têm desafio no Cronograma (Média)

A Rubrica 2 ("Aplicação") e a tabela "Distribuição das notas" listam os desafios técnicos como ocorrendo nas Semanas 1, 2, 4, 5, 6, 8, 9, 10, 11, 13 e 16. Porém, o Cronograma contém desafios explícitos, com o mesmo formato textual (`**Desafio:**`), também nas Semanas 7 e 15. Nenhum dos dois aparece na lista de "Desafios Técnicos" da Rubrica 2.

**Impacto:** ambiguidade real para o professor sobre como esses dois desafios devem ser avaliados; a omissão parece não intencional.

### 5. Estrutura "Unidade VI" no Cronograma não corresponde aos "cinco módulos" exigidos pelo CLAUDE.md (Média)

CLAUDE.md e COURSE_CONTEXT.md definem taxativamente cinco módulos. PROJECT_ARCHITECTURE.md e o Sistema de Avaliação tratam o Módulo 5 como cobrindo as Semanas 15–17 de forma unificada. Entretanto, o Cronograma cria explicitamente uma "Unidade VI — Apresentação Final e Encerramento (Semana 17)", separada da "Unidade V — Comparar Arquiteturas (Semanas 15–16)".

**Impacto:** um professor substituto que use apenas o Cronograma como referência pode concluir, incorretamente, que a disciplina tem 6 unidades/módulos.

### 6. Semana 12 é rotulada 🔵 (semana regular) mas concentra um Code Review formal de encerramento (Baixa)

A legenda do Cronograma define 🔴 como "Encerramento de módulo — entrega de artefato jogável, checkpoint, playtest, code review ou apresentação". A Semana 12 tem um Code Review formal (Rubrica 4) mas está marcada 🔵, gerando ambiguidade de leitura sobre o critério de marcação.

---

## Sugestão de Correção

**Problema 1 (HealthComponent fantasma):** inserir, no `Plano_de_Aula_Semana_07.md` (Encontro 2) ou no início da `Plano_de_Aula_Semana_08.md`, a construção explícita de um `HealthComponent` mínimo (vida atual/máxima, função `ApplyDamage`, evento de morte), seguindo o padrão pedagógico já usado para `InteractionComponent` (Semana 5) e `SaveComponent` (Semana 7). Corrigir todas as referências "(retomado do Módulo 2)" nas Semanas 9, 10 e 11 (Planos de Aula e Slides) para "(construído nesta unidade/semana)". Atualizar PROJECT_ARCHITECTURE.md se a decisão for antecipar o Component.

**Problema 2 (combate nunca ensinado):** ao introduzir `HealthComponent`, incluir a lógica mínima de ataque do `BP_Player` contra `BP_Enemy` (Trace/Overlap chamando `ApplyDamage`), preferencialmente em `Plano_de_Aula_Semana_11.md` (Encontro 2). Atualizar "Introdução da Semana" e "Conteúdos" para não tratar combate como decorrência automática do desafio de animação.

**Problema 3 (Checkpoint sem aula):** adicionar `BP_Checkpoint` como conteúdo explícito em `Plano_de_Aula_Semana_06.md` ou `07.md` (Encontro 1), reaproveitando `BPI_Interactable` + `SaveComponent` já existentes. Remover a formulação condicional "(se já modelados)" da Semana 7 assim que a aula for criada.

**Problema 4 (Desafios Técnicos incompletos):** em `Sistema_de_Avaliacao_Tendencias_de_Motores_de_Jogos.md`, decidir e documentar explicitamente se os desafios das Semanas 7 e 15 entram na nota de Desafios Técnicos ou são absorvidos por outra rubrica (ex.: Semana 7 → Rubrica 4/Code Review; Semana 15 → Feedback Formal).

**Problema 5 (Unidade VI):** em `Cronograma_Tendencias_de_Motores_de_Jogos.md`, renomear "Unidade VI" para estender a "Unidade V" até a Semana 17, eliminando a sexta unidade e alinhando com PROJECT_ARCHITECTURE.md e Sistema de Avaliação.

**Problema 6 (marcação 🔵/🔴):** revisar a legenda do Cronograma para deixar explícito que 🔴 marca apenas encerramento de unidade/módulo, não qualquer Code Review isolado — ou marcar a Semana 12 como 🔴.

---

## Inconsistências Encontradas

1. `HealthComponent` citado como "retomado do Módulo 2" nas Semanas 9, 10 e 11, sem nunca ter sido criado nas Semanas 1–8.
2. Sistema de combate citado como componente já integrado do Vertical Slice nos resumos das Semanas 15, 16 e 17, sem nenhuma aula que o construa.
3. `BP_Checkpoint` presente na arquitetura (seções 6, 7 e 8 do PROJECT_ARCHITECTURE.md) e nos desafios de módulo do COURSE_CONTEXT.md, mas ausente de todo o Cronograma/Planos de Aula como conteúdo ensinado.
4. "NPCs" listados como desafio esperado do Módulo 2 em COURSE_CONTEXT.md, mas nunca aparecem como conteúdo em nenhuma semana.
5. Desafios das Semanas 7 e 15, presentes no Cronograma, ausentes da lista "Aplicação" da Rubrica 2 e da tabela "Distribuição das notas".
6. Estrutura de unidades: Cronograma usa "Unidade VI" (Semana 17) separada de "Unidade V" (Semanas 15–16), enquanto os demais documentos tratam Semanas 15–17 uniformemente como "Módulo 5".
7. Marcação 🔴/🔵 da Semana 12: contém Code Review formal de encerramento mas está marcada 🔵.

---

## Melhorias Opcionais

1. Explicitar no Sistema de Avaliação como o Desenvolvimento Semanal (20%) evita dupla contagem com Desafios Técnicos (15%) quando o desafio da semana é, ele mesmo, o critério "Evolução" da Rubrica 1.
2. Padronizar o texto de "Nota de contingência" (presente de forma inconsistente a partir da Semana 6) em todas as semanas.
3. Adicionar ao PROJECT_ARCHITECTURE.md uma nota explícita ligando `HealthComponent`/combate à semana correta, uma vez corrigido o Problema 1/2.

---

## Parecer Final

**Classificação: Muito Boa**

A disciplina é excepcionalmente bem estruturada em sua concepção pedagógica: a progressão de autonomia é real e verificável aula a aula, a exigência das "quatro perguntas" do CLAUDE.md é cumprida de forma consistente, a bibliografia e ementa oficiais são reproduzidas com fidelidade, e a arquitetura do Vertical Slice funciona de fato como documento de consistência.

No entanto, a auditoria encontrou uma falha **Crítica** e recorrente: o `HealthComponent` (e, por extensão, o sistema de combate simples) é tratado como pré-existente em três semanas consecutivas (9, 10 e 11) sem nunca ter sido efetivamente ensinado — um erro de continuidade que compromete diretamente a entrega esperada do Módulo 3 e a defesa final do Módulo 5. A isso se soma uma falha **Alta** (BP_Checkpoint nunca ensinado) e inconsistências de **Média/Baixa** gravidade entre Cronograma e Sistema de Avaliação.

Nenhum desses problemas exige reescrever a disciplina — todos são correções pontuais e localizadas —, mas o gap do `HealthComponent`/combate é grave o suficiente para impedir a classificação "Excelente" até ser corrigido.
