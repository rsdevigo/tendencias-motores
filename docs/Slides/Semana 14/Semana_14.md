---
marp: true
theme: academic-course
paginate: true
header: 'Semana 14 — Exportação e Consolidação do Vertical Slice Final'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 14

## Exportação e Consolidação do Vertical Slice Final

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade IV — Produzir como um Pequeno Estúdio** (Semanas 12–14)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Semana 🔴** — encerramento da Unidade IV e do Módulo 4. Entrega: Vertical Slice final otimizado e exportado (entrega parcial), Playtest cruzado, Code Review de encerramento

</div>

<!--
A Semana 13 encerrou com o mesmo Vertical Slice jogável desde a Semana 11, agora com som integrado às principais ações de gameplay via AudioStreamPlayer e com ao menos um gargalo de desempenho corrigido a partir de profiling real do próprio projeto.
A Semana 14 fecha o Módulo 4 respondendo a uma pergunta que nenhuma semana anterior precisou responder: o que diferencia um protótipo, que só roda dentro do editor, de um build distribuível, que roda de forma independente em uma máquina de destino?
Metodologia: Studio Based Learning — professor como diretor técnico. Autonomia alta.
-->

---

## Objetivos da Semana

- Compreender exportação de projeto como etapa universal de qualquer pipeline de produção de jogos, distinta de testar o projeto dentro do editor
- Configurar Export Templates e presets de exportação no Godot para gerar um build de produção do Vertical Slice
- Gerar o primeiro executável distribuível do Vertical Slice completo, acumulado desde o Módulo 1
- Realizar Playtest cruzado do build exportado de outro grupo, aplicando critérios de Code Review a um produto fechado
- Consolidar, com ajustes finais pontuais, a entrega do Vertical Slice do Módulo 4 como produto de um pequeno estúdio

<!--
Encontro 1 resolve a exportação. Encontro 2 resolve a validação cruzada e o encerramento do módulo.
Referência: Godot Docs — Exporting Projects, Export Templates; Unity Manual — Build Settings, Publishing Builds.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Pipeline de Exportação e Build de Produção

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o Vertical Slice já validado desde a Semana 13, sem alterar nenhuma mecânica, material, som ou otimização — o objetivo é reempacotar o que já funciona.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 13 (áudio integrado, profiling e otimização aplicada) (15 min)
- Introdução: build de produção vs. projeto no editor, o papel dos Export Templates (20 min)
- Demonstração: configuração de preset de exportação e geração de um build de exemplo (30 min)
- Laboratório: cada grupo configura o próprio preset e exporta o Vertical Slice completo (50 min)
- Feedback e fechamento — verificação de que cada build gerado abre e roda de forma independente (20 min)

<!--
Ciclo pedagógico: Conceito → Demonstração → Construção → Verificação. Nunca inverter.
Não há desafio de solução livre neste encontro — o processo de exportação é guiado; cada grupo decide apenas detalhes de apresentação do próprio build (nome do executável, ícone).
-->

---

<!-- _class: question -->

# O que diferencia um protótipo, que só roda no editor, de um produto que qualquer jogador pode abrir?

Pense em tudo o que o Vertical Slice já faz desde a Semana 1 — e no que muda quando ninguém tem o Godot aberto.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que exportação não é um clique final, mas uma etapa que testa se o projeto sobrevive fora do ambiente de desenvolvimento.
Erro comum: tratar a exportação como formalidade opcional de última hora.
-->

---

## O Problema: Build de Produção vs. Projeto no Editor

- Um projeto aberto no editor depende do próprio Godot instalado na máquina
- Um build exportado precisa rodar de forma independente na máquina de destino
- A mesma distinção entre "rodar em ambiente de desenvolvimento" e "entregar um produto" existe em qualquer pipeline de software

<!--
Conceito universal: exportação separa protótipo de produto distribuível. Presente em qualquer engine de produção antes de uma entrega final.
Referência: Godot Docs — Exporting Projects (resumir, nunca reproduzir trechos).
-->

---

## Export Templates e Presets de Exportação

- Export Templates — binários pré-compilados do motor, necessários para gerar builds sem depender do editor
- Presets de exportação — plataforma-alvo (Windows/Linux/Web), configurações de janela, ícone e nome do executável
- Cada campo do preset é uma decisão de produto, não apenas configuração técnica

<!--
Erro comum: tentar exportar sem os Export Templates da versão correta instalados, causando build que não abre ou fecha imediatamente.
Referência: Godot Docs — Export Templates.
-->

---

<!-- _class: comparison -->

## Exportação no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Export Templates baixados separadamente por versão e plataforma
- Presets de exportação (Project Export) por plataforma-alvo

</div>
<div class="col negative">

### Unity

- Módulos de plataforma instalados via Unity Hub
- Build Settings + Player Settings equivalentes aos presets do Godot

</div>
</div>

<!--
Princípio universal idêntico: um projeto de desenvolvimento precisa ser compilado para uma plataforma específica antes de se tornar um produto distribuível, e esse processo frequentemente expõe problemas que não apareciam dentro do editor.
A diferença está no modelo de distribuição do suporte à plataforma — download separado (Godot) versus módulos do Hub (Unity).
-->

---

## Demonstração — Configuração de Preset e Build de Exemplo

O que será construído:

- Instalação dos Export Templates e criação de um preset de exportação (plataforma-alvo, nome do executável, ícone)
- Um build de exemplo gerado ao vivo e executado fora do editor

Por quê: mostrar o momento exato em que o projeto deixa de depender do Godot aberto.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Preset de referência (ex.: Windows Desktop) já testado pelo professor antes da aula, com build de exemplo gerado previamente.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a diferença entre o projeto rodando dentro do editor do Godot e o mesmo projeto rodando como executável independente.
> Enquadramento: composição dividida em duas metades — à esquerda, a janela do editor do Godot com o botão de "Play" em destaque; à direita, o executável exportado rodando em uma janela própria, sem o editor visível.
> Elementos presentes: ícone do Godot Editor, ícone de executável (.exe), seta de transformação entre as duas metades representando o processo de exportação.
> Destaque visual: a seta central de transformação em cor de destaque, com o rótulo "Export Templates + Preset".
> Legenda sugerida: "Exportar não é só empacotar — é testar se o projeto sobrevive fora do editor."

<!--
Usar esta imagem durante a introdução, antes da demonstração ao vivo do preset e do build de exemplo.
-->

---

## Laboratório — Exportação do Vertical Slice Completo

Cada grupo, no próprio projeto:

1. Instala os Export Templates da versão do Godot em uso (se ainda não instalados)
2. Configura um preset de exportação para a plataforma-alvo disponível no laboratório
3. Exporta o Vertical Slice completo acumulado desde o Módulo 1 e confirma que o build abre de forma independente

<!--
Critério de sucesso: executável exportado, capaz de abrir e rodar de forma independente do editor, sem qualquer regressão de mecânica, áudio ou desempenho em relação à versão validada na Semana 13.
Dificuldade esperada: build não abre ou fecha imediatamente por Export Templates ausentes ou incompatíveis — reforçar verificação da versão dos templates antes de depurar qualquer outra causa.
Dificuldade esperada: recursos que carregavam no editor mas falham no build exportado, geralmente por caminhos de arquivo absolutos — reforçar uso de caminhos relativos ao projeto (`res://`).
Como diretor técnico, o professor circula auxiliando grupos com erros de exportação, tratando cada erro como parte esperada do processo, não como falha do grupo.
-->

---

## Fechamento — Encontro 1

- Cada grupo possui um executável exportado do próprio Vertical Slice completo
- Build capaz de abrir e rodar de forma independente do editor do Godot
- Nenhuma regressão de mecânica, áudio ou desempenho em relação à Semana 13
- Próximo passo: Playtest cruzado e Code Review de encerramento, no Encontro 2

<!--
O build gerado aqui é o objeto avaliado no Playtest cruzado e no Code Review de encerramento do Encontro 2 — pré-requisito direto, sem espaço de compressão (ver Cronograma).
-->

---

<!-- _class: chapter -->

## Encontro 2

# Playtest Cruzado e Code Review de Encerramento

<span class="chapter-number">02</span>

<!--
A turma troca de papel: em vez de testar o próprio projeto, cada grupo faz Playtest cruzado do build exportado de outro grupo, sobre um produto fechado e não mais sobre o projeto aberto no editor.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (build exportado de cada grupo) e explicação do roteiro de Playtest cruzado (15 min)
- Playtest cruzado: cada grupo testa o build exportado de outro grupo e registra observações (55 min)
- Code Review de encerramento: cada grupo revisa a própria organização do projeto (35 min)
- Ajustes finais pontuais no próprio build, a partir do feedback recebido (30 min)

<!--
Reservar tempo real para o Code Review de encerramento — instrumento de avaliação que fecha a Unidade IV (Rubrica 4), não deve ser comprimido (ver Cronograma).
-->

---

<!-- _class: question -->

# Por que um build só está pronto quando validado por alguém que não o construiu?

Pense nos Playtests coletivos já feitos nas Semanas 7 e 11 — o mesmo princípio se aplica agora ao produto fechado.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que quem desenvolveu um sistema deixa de enxergar seus próprios problemas depois de testá-lo repetidamente.
Erro comum: assumir que o próprio grupo já testou o suficiente durante o desenvolvimento.
-->

---

## O Problema: Validar o Próprio Trabalho

- Quem desenvolveu um sistema deixa de enxergar seus próprios problemas depois de testá-lo repetidamente
- Um avaliador externo revela falhas que o próprio grupo não veria
- O build exportado expõe problemas que só aparecem fora do ambiente de desenvolvimento (carregamento de recurso, desempenho, ausência de mensagens de erro do editor)

<!--
Conceito universal: validação externa antes da entrega. Mesmo princípio já praticado nos Playtests das Semanas 7 e 11, agora sobre o produto fechado.
Referência: Godot Docs — Exporting Projects (resumir).
-->

---

## Code Review de Encerramento

- Revisão geral do projeto sob a perspectiva de um pequeno estúdio entregando um produto
- Retoma os princípios já cobrados nas Semanas 7, 10 e 12: organização, ausência de lógica duplicada, local arquitetural único para cada sistema
- Aplicado ao Vertical Slice completo acumulado desde o Módulo 1 (Interactable, SaveData, Inventário, HealthComponent, HUD, IA, materiais, áudio)

<!--
Erro comum: revelar duplicação de lógica acumulada de semanas diferentes sem tempo hábil para refatoração completa — registrar como observação para a Unidade V, sem forçar retrabalho amplo.
Referência: Rubrica 4 (Code Review) do Sistema de Avaliação.
-->

---

<!-- _class: comparison -->

## Validação de Build no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Build exportado testado fora do editor, sem acesso ao projeto
- Playtest cruzado + Code Review de encerramento como prática de produção

</div>
<div class="col negative">

### Unity

- QA/Playtest sobre builds gerados pelo Build Settings
- Frequentemente testados por pessoas fora da equipe de desenvolvimento direto

</div>
</div>

<!--
Princípio universal idêntico: um build só está pronto quando validado por alguém que não o construiu, e problemas de build costumam diferir de problemas vistos no editor.
A diferença está mais no processo de organização de equipe do que na ferramenta — a engine fornece o build, o Playtest cruzado é prática de produção.
-->

---

## Demonstração — Fluxo de Playtest Cruzado

O que será construído:

- Demonstração rápida do fluxo de Playtest cruzado sobre o build de referência do professor, antes da troca entre grupos

Por quê: fixar o roteiro de observação (carregamento, desempenho, áudio, usabilidade, ausência de erros) antes de cada grupo aplicá-lo ao build de outro grupo.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Builds de todos os grupos coletados ao final do Encontro 1, organizados para troca cruzada.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o fluxo de troca cruzada de builds entre grupos, sem acesso ao projeto aberto no editor.
> Enquadramento: diagrama com dois ícones de "Grupo" lado a lado, cada um com um executável saindo em direção ao grupo oposto.
> Elementos presentes: ícone de executável (.exe) para cada grupo, seta cruzada entre os dois grupos, ícone de lista de verificação representando o roteiro de Playtest.
> Destaque visual: as setas cruzadas em cor de destaque, reforçando que nenhum grupo testa o próprio build nesta etapa.
> Legenda sugerida: "Playtest cruzado — cada grupo avalia o build fechado de outro grupo, como um jogador externo avaliaria."

<!--
Usar esta imagem na abertura do Encontro 2, antes da distribuição dos builds entre os grupos.
-->

---

## Laboratório — Playtest Cruzado e Code Review

Cada grupo, no papel de avaliador externo:

1. Testa o build exportado de outro grupo, seguindo o roteiro (carregamento, desempenho, áudio, usabilidade, ausência de erros)
2. Registra os problemas encontrados, distinguindo ajuste pontual de retrabalho fora do escopo

Cada grupo, no próprio projeto:

3. Conduz o Code Review de encerramento, verificando organização e ausência de lógica duplicada entre todos os sistemas acumulados

<!--
Critério de sucesso: build exportado e ajustado, validado por Playtest cruzado de outro grupo e por Code Review de encerramento, sem regressão em nenhuma mecânica, sistema ou otimização já validados.
Dificuldade esperada: avaliar o build de outro grupo com foco em preferência estética pessoal em vez de problemas objetivos — reforçar o roteiro de Playtest como critério, não opinião livre.
Dificuldade esperada: tentar corrigir, nos ajustes finais, problemas que exigiriam retrabalho amplo fora do escopo do tempo restante — reforçar que a entrega desta semana é consolidação pontual.
-->

---

## Arquitetura — Do Editor ao Produto Fechado

- Exportação (Encontro 1) → Vertical Slice reempacotado como build independente do editor
- Playtest cruzado (Encontro 2) → validação do build por um avaliador externo ao grupo que o produziu
- Code Review de encerramento → mesma verificação de organização das Semanas 7, 10 e 12, aplicada ao projeto completo

<!--
Diagrama sugerido: Vertical Slice acumulado (Módulos 1–4) → Export Templates + Preset → Build exportado → Playtest cruzado (outro grupo) → Ajustes finais.
Erro comum: tratar exportação e Playtest cruzado como etapas desconectadas — ambas fazem parte do mesmo encerramento do Módulo 4.
-->

---

<!-- _class: exercise -->

# Entrega da Semana — Vertical Slice Final do Módulo 4

Aplique, no próprio build, os ajustes finais pontuais decorrentes do Playtest cruzado e do Code Review de encerramento.

<div class="objectives">

**Entrega:** Vertical Slice final (Módulo 4) otimizado e exportado (entrega parcial); Playtest cruzado; Code Review de encerramento (Rubrica 4).

</div>

<!--
Liberdade de priorização sobre quais problemas corrigir dentro do tempo disponível, desde que a escolha seja justificada pelo impacto observado.
Dificuldade esperada: priorizar ajustes cosméticos em vez dos problemas de maior impacto observados no Playtest — reforçar a pergunta "qual problema afeta mais a experiência do jogador?".
-->

---

## Boas Práticas — Exportação e Encerramento de Módulo

- Sempre usar caminhos relativos ao projeto (`res://`) em qualquer referência a recurso, evitando falhas exclusivas do build exportado
- Tratar a exportação como parte do pipeline de produção, nunca como etapa opcional de última hora
- Avaliar o build de outro grupo por critérios objetivos do roteiro de Playtest, não por preferência pessoal
- Priorizar, nos ajustes finais, o problema de maior impacto observado, não o mais fácil de corrigir

<!--
Estes são exatamente os pontos observados no Code Review de encerramento da semana.
-->

---

## Fechamento — Encontro 2

- Build exportado e ajustado do Vertical Slice completo, validado por Playtest cruzado de outro grupo
- Code Review de encerramento concluído, sem regressão em nenhum sistema acumulado desde o Módulo 1
- Encerramento da Unidade IV — Produzir como um Pequeno Estúdio
- Próximo passo: Unidade V — Comparar Arquiteturas, a partir da Semana 15

<!--
O build consolidado nesta semana passa a ser o ponto de comparação direto na Unidade V, sem necessidade de retrabalho adicional além dos ajustes já aplicados.
-->

---

## Resultado Esperado da Semana

- Build exportado e executável do Vertical Slice completo, acumulado desde a Semana 1
- Validação por Playtest cruzado de outro grupo e por Code Review de encerramento (mesmos critérios das Semanas 7, 10 e 12)
- Módulo 4 — Produzir como um Pequeno Estúdio — encerrado: projeto tecnicamente pronto, otimizado, sonorizado e empacotado como produto distribuível

<!--
Este resultado corresponde ao encerramento da Unidade IV no roadmap (PROJECT_ARCHITECTURE.md) e antecede a abertura da Unidade V na Semana 15.
-->

---

## Checklist da Semana

- [ ] Build exportado e executável, rodando de forma independente do editor
- [ ] Nenhuma regressão de mecânica, áudio ou desempenho em relação à Semana 13
- [ ] Playtest cruzado do build de outro grupo concluído, com observações registradas
- [ ] Code Review de encerramento concluído (Rubrica 4), sem lógica duplicada entre sistemas
- [ ] Ajustes finais pontuais aplicados a partir do feedback recebido

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 15.
-->

---

## Próximos Passos — Semana 15

A Semana 15 abre a Unidade V — Comparar Arquiteturas — com engenharia reversa de projetos profissionais (Godot Demo Projects, TPS Demo, Platformer 2D Demo). O Vertical Slice consolidado e exportado nesta semana passa a ser o ponto de comparação direto para cada decisão arquitetural tomada ao longo do semestre.

Leitura recomendada: Godot Docs — Exporting Projects, Export Templates; Unity Manual (consulta comparativa) — Build Settings, Publishing Builds.

<!--
Referências completas: ver Plano de Aula Semana 14. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
