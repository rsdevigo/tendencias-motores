---
marp: true
theme: academic-course
paginate: true
header: 'Semana 15 — Engenharia Reversa de Projetos Profissionais (Godot Demo Projects)'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 15

## Engenharia Reversa de Projetos Profissionais (Godot Demo Projects)

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade V — Comparar Arquiteturas e Aprender Novos Motores** (Semanas 15–17)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Semana 🔵** — abertura da Unidade V; não fecha módulo. Entrega: feedback formal sobre as análises arquiteturais

</div>

<!--
A Semana 14 encerrou a Unidade IV com o Vertical Slice de cada grupo exportado, validado por Playtest cruzado e por Code Review de encerramento.
A partir da Semana 15, a pergunta muda: não mais "o que falta construir?", mas "como uma equipe profissional estrutura a arquitetura de um jogo em produção real, e o que isso revela sobre as próprias escolhas do grupo?".
Metodologia: Reverse Engineering — discussões, comparações, análises. Autonomia muito alta; professor como mediador de discussão técnica.
-->

---

## Objetivos da Semana

- Compreender engenharia reversa de código como método de aprendizagem: ler a arquitetura de um projeto profissional para entender decisões de design, não para copiar implementação
- Analisar a estrutura do TPS Demo oficial do Godot, identificando padrões já praticados pelo grupo (Signals, Autoload, Resource customizado, Components)
- Comparar as soluções arquiteturais dos projetos de referência com as soluções do próprio grupo
- Identificar, no próprio Vertical Slice, ao menos uma decisão arquitetural que poderia ser refeita à luz dos projetos analisados

<!--
Encontro 1 resolve a leitura do TPS Demo. Encontro 2 resolve a leitura do Platformer 2D Demo e a consolidação do feedback formal.
Referência: Godot Demo Projects (github.com/godotengine/godot-demo-projects) — TPS Demo, Platformer 2D Demo.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Leitura Arquitetural Guiada — TPS Demo

<span class="chapter-number">01</span>

<!--
Encontro guiado por roteiro de perguntas norteadoras. Nenhuma alteração de código é feita no Vertical Slice nesta semana — apenas leitura e registro de paralelos.
-->

---

## Agenda do Encontro 1

- Revisão do Módulo 4 encerrado na Semana 14 e abertura da Unidade V (15 min)
- Introdução ao método de engenharia reversa de código como prática de aprendizagem (20 min)
- Leitura arquitetural guiada do TPS Demo, seguindo o roteiro de perguntas norteadoras (50 min)
- Paralelo em pequenos grupos: mapear no próprio Vertical Slice os equivalentes (ou ausências) do TPS Demo (40 min)
- Feedback e fechamento do Encontro 1 (10 min)

<!--
Ciclo pedagógico: Conceito → Demonstração → Construção → Desafio → Revisão. Aqui "construção" é substituída por leitura guiada — não há implementação nesta semana.
Não há desafio de solução livre: o "desafio" é interpretativo (ver Desafio do Plano de Aula).
-->

---

<!-- _class: question -->

# O que muda quando você abre um projeto que não foi escrito pela sua equipe?

Pense em como você leria a árvore de cenas e os scripts de um projeto pronto, sem poder perguntar a quem o construiu.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que engenharia reversa é uma leitura ativa, não uma navegação passiva de arquivos.
Erro comum: tratar a leitura do projeto de referência como um passeio superficial pela árvore de cenas, sem examinar Signals e conexões reais.
-->

---

## O Problema: Ler Antes de Mexer

- Um profissional frequentemente entra em um projeto já existente, com decisões arquiteturais já tomadas por outra equipe
- "Entender antes de mexer" é uma competência tão universal quanto qualquer padrão de design isolado
- Engenharia reversa de arquitetura é uma habilidade transferível para qualquer engine, linguagem ou stack

<!--
Conceito universal: ler a arquitetura de um projeto pronto para reconstruir as decisões de design por trás dele. O TPS Demo é o veículo, não o objetivo — o que se ensina é o método de leitura.
-->

---

## Método: Engenharia Reversa como Leitura Arquitetural

- Ler a árvore de cenas, os scripts e as conexões de Signals de um projeto pronto
- Reconstruir o raciocínio arquitetural por trás dele, sem executar refatoração
- Usar o próprio código-fonte do projeto de referência como documentação primária
- Recorrer à documentação oficial do Godot apenas quando um recurso específico não for familiar

<!--
Máximo de cinco bullets — este slide resume o método antes da leitura guiada em si.
Referência: Godot Demo Projects (repositório oficial) — https://github.com/godotengine/godot-demo-projects
-->

---

<!-- _class: comparison -->

## Projetos de Referência no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Godot Demo Projects — repositório GitHub aberto, código-fonte completo
- TPS Demo e Platformer 2D Demo como exemplos oficiais de gênero

</div>
<div class="col negative">

### Unity

- Templates oficiais de Third Person e sample projects via Unity Learn / Package Manager
- Mesma prática de engenharia reversa sobre projetos de amostra

</div>
</div>

<!--
Princípio universal idêntico: um projeto de referência oficial da própria engine mostra convenções e padrões idiomáticos que a documentação de API isolada não revela.
A diferença está na distribuição — repositório GitHub aberto (Godot) versus Package Manager e Unity Learn (Unity) — não no método de leitura em si.
-->

---

## Demonstração — Estrutura do TPS Demo

O que será construído:

- Nenhum código novo — apenas leitura em tela da estrutura de cenas, gameplay framework (player, câmera, armas, inimigos) e Signals do TPS Demo

Por quê: fixar o roteiro de perguntas norteadoras antes do paralelo em pequenos grupos.

Resultado esperado: a turma reconhece, na estrutura do TPS Demo, padrões já praticados no próprio Vertical Slice (Signals, Autoload, Components, State Machine).

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Preparação do professor: cópia local do TPS Demo já aberta no editor; roteiro de leitura arquitetural guiada projetado (onde está o Autoload? Como o player se comunica com a arma? Que Signals existem e quem os escuta?).
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a tela dividida usada na leitura arquitetural guiada do TPS Demo lado a lado com o Vertical Slice da turma.
> Enquadramento: composição dividida em duas metades — à esquerda, o FileSystem dock e a Scene dock do TPS Demo aberto no editor do Godot; à direita, a Scene dock do Vertical Slice da turma.
> Elementos presentes: ícones de nós representando Player, Câmera, Armas e Inimigos no TPS Demo; ícones equivalentes no Vertical Slice.
> Destaque visual: linhas tracejadas conectando nós equivalentes dos dois projetos, em cor de destaque.
> Legenda sugerida: "Ler antes de mexer — o mesmo problema, duas soluções possíveis."

<!--
Usar esta imagem na abertura da leitura arquitetural guiada, antes de navegar pelo TPS Demo em tela.
-->

---

## Roteiro de Perguntas Norteadoras — TPS Demo

- Onde está o Autoload e o que ele gerencia?
- Como o player se comunica com a arma? Que Signals existem e quem os escuta?
- Que outros padrões já praticados pela turma aparecem na solução oficial (Components, Resource customizado, State Machine)?
- Onde o TPS Demo resolve o mesmo tipo de problema do Vertical Slice — de forma igual, similar ou diferente?

<!--
Este roteiro conduz os 50 minutos de leitura guiada. Forçar a leitura das conexões de Signals, não apenas dos nomes de arquivos e nós.
-->

---

## Laboratório — Paralelo com o Próprio Vertical Slice

Cada grupo, em pequenos grupos:

1. Mapeia, no próprio Vertical Slice, os equivalentes (ou ausências) dos padrões identificados no TPS Demo
2. Registra por escrito ao menos três pontos de paralelo — convergência ou divergência — com justificativa técnica para cada um

<!--
Critério de sucesso: registro escrito com ao menos três paralelos arquiteturais, cada um justificado em termos dos padrões já praticados no semestre (Signals, Autoload, Components, Resource customizado, State Machine/Behavior Tree).
Dificuldade esperada: grupos tentando "corrigir" o próprio projeto durante a leitura — reforçar que nenhuma alteração de código é esperada nesta semana.
Dificuldade esperada: grupos cujo Vertical Slice diverge muito do TPS Demo por escopo ou gênero — divergência justificada é um paralelo tão válido quanto convergência.
-->

---

## Fechamento — Encontro 1

- Roteiro de leitura arquitetural do TPS Demo concluído
- Registro escrito com ao menos três paralelos arquiteturais entre o TPS Demo e o próprio Vertical Slice
- Nenhuma alteração de código realizada — apenas leitura e registro
- Próximo passo: leitura do Platformer 2D Demo e consolidação do feedback formal, no Encontro 2

<!--
Os registros produzidos aqui são retomados na abertura do Encontro 2 e servem de insumo direto para o feedback formal da semana.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Platformer 2D Demo e Consolidação do Feedback Formal

<span class="chapter-number">02</span>

<!--
A turma amplia o repertório de soluções examinadas com um segundo projeto de referência (2D), complementar ao TPS Demo (3D), e fecha a semana produzindo o feedback formal escrito.
-->

---

## Agenda do Encontro 2

- Revisão dos paralelos registrados no Encontro 1 (TPS Demo) (15 min)
- Leitura arquitetural guiada do Platformer 2D Demo e de outros Godot Demo Projects relevantes (45 min)
- Comparação consolidada: cruzar os paralelos do TPS Demo e do Platformer 2D Demo com o próprio Vertical Slice (40 min)
- Desafio: redação do feedback formal — decisão arquitetural própria a ser refeita, com justificativa (25 min)
- Feedback e fechamento da semana (10 min)

<!--
Reservar tempo real para a produção do feedback formal — é a entrega avaliativa da semana (ver Cronograma e Evidências para Avaliação do Plano de Aula).
-->

---

<!-- _class: question -->

# Arquitetura de software tem uma única solução correta?

Pense no TPS Demo, no Platformer 2D Demo e no próprio Vertical Slice — três soluções distintas para problemas semelhantes.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a reconhecer trade-offs arquiteturais, não a buscar uma resposta "certa" única.
Erro comum: confundir "decisão que poderia ser refeita" com "erro cometido".
-->

---

## O Problema: Trade-offs, Não Respostas Únicas

- TPS Demo, Platformer 2D Demo e o próprio Vertical Slice resolvem problemas semelhantes de formas distintas
- Comunicação entre sistemas, gerenciamento de estado e organização de cena admitem múltiplas soluções válidas
- A competência da semana não é "replicar a solução oficial", mas reconhecer trade-offs e justificar uma escolha própria

<!--
Conceito universal ampliado: quanto mais amostras de solução profissional um desenvolvedor examina, mais nítido fica o espaço de trade-offs arquiteturais disponível — independentemente da engine.
-->

---

## Demonstração — Estrutura do Platformer 2D Demo

O que será construído:

- Leitura em tela da organização de cenas e do gameplay framework 2D do Platformer 2D Demo, e de outros Godot Demo Projects relevantes ao escopo da turma

Por quê: ampliar o repertório de soluções examinadas com um gênero (2D) complementar ao TPS Demo (3D).

Resultado esperado: a turma cruza os paralelos do TPS Demo e do Platformer 2D Demo com as próprias decisões do Vertical Slice.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Preparação do professor: cópia local do Platformer 2D Demo aberta no editor; registros de paralelo do Encontro 1 retomados no início.
-->

---

<!-- _class: comparison -->

## Comparação de Soluções × Unity

<div class="columns">
<div class="col positive">

### Godot

- TPS Demo (3D) e Platformer 2D Demo (2D) como amostras complementares de solução oficial
- Comparação direta contra o próprio Vertical Slice do grupo

</div>
<div class="col negative">

### Unity

- Templates oficiais equivalentes para gêneros 2D via Unity Learn
- Mesma prática de comparar múltiplas amostras contra o próprio projeto

</div>
</div>

<!--
O princípio universal é idêntico nas duas engines: examinar múltiplos projetos de referência revela o espaço de trade-offs disponível, muito além de um único exemplo isolado.
-->

---

## Laboratório — Comparação Consolidada e Feedback Formal

Cada grupo:

1. Cruza os paralelos do TPS Demo e do Platformer 2D Demo com as próprias decisões tomadas desde o Módulo 1
2. Identifica ao menos uma decisão arquitetural própria que poderia ser refeita à luz da análise
3. Redige uma justificativa técnica curta para a mudança proposta — sem implementá-la nesta semana

<!--
Critério de sucesso: feedback formal escrito com pelo menos uma decisão arquitetural própria identificada, justificada em termos de trade-off técnico, não de opinião estética.
Dificuldade esperada: propostas vagas ("deveríamos organizar melhor o projeto") sem justificativa técnica específica — exigir um trade-off concreto observado no projeto de referência.
Dificuldade esperada: grupos com pouco tempo tentando cobrir múltiplos pontos superficialmente — reforçar que a qualidade da justificativa importa mais que a quantidade.
-->

---

## Arquitetura — Do Vertical Slice à Leitura Comparativa

- TPS Demo (Encontro 1) → paralelos registrados com o Vertical Slice em 3D
- Platformer 2D Demo (Encontro 2) → paralelos registrados com o Vertical Slice em 2D/gameplay geral
- Consolidação → cruzamento dos dois conjuntos de paralelos com as decisões do próprio grupo desde o Módulo 1

<!--
Diagrama sugerido: Vertical Slice acumulado (Módulos 1–4) → Leitura do TPS Demo → Leitura do Platformer 2D Demo → Paralelos consolidados → Feedback formal.
Erro comum: tratar os dois projetos de referência como leituras isoladas — a consolidação do Encontro 2 é o que produz o feedback formal.
-->

---

<!-- _class: exercise -->

# Entrega da Semana — Feedback Formal sobre as Análises Arquiteturais

Redija, por escrito, ao menos uma decisão arquitetural própria que seria refeita à luz do TPS Demo e do Platformer 2D Demo, com justificativa técnica.

<div class="objectives">

**Entrega:** Feedback formal sobre as análises arquiteturais — avaliação qualitativa da capacidade de leitura arquitetural comparativa e de autocrítica técnica fundamentada.

</div>

<!--
Não constitui, isoladamente, uma rubrica formal de Code Review — alimenta a avaliação qualitativa da Unidade V.
Dificuldade esperada: confundir "decisão que poderia ser refeita" com "erro cometido" — trade-offs válidos na época (ex.: Semana 3) podem legitimamente não escalar até a Semana 14, sem indicar erro do grupo.
-->

---

## Boas Práticas — Engenharia Reversa de Arquitetura

- Ler a árvore de cenas e as conexões de Signals antes de julgar uma solução — nunca avaliar por nomes de arquivo isoladamente
- Registrar convergência e divergência com o mesmo rigor — divergência justificada é um paralelo tão válido quanto convergência
- Justificar qualquer proposta de mudança por um trade-off técnico concreto, nunca por preferência estética
- Tratar o projeto de referência como documentação primária, complementada pela documentação oficial apenas quando necessário

<!--
Estes são os mesmos critérios usados para avaliar o feedback formal desta semana.
-->

---

## Fechamento — Encontro 2

- Leitura arquitetural guiada do TPS Demo e do Platformer 2D Demo concluída
- Paralelos consolidados entre os dois projetos de referência e o próprio Vertical Slice
- Feedback formal escrito, com ao menos uma decisão arquitetural própria justificada
- Unidade V aberta — nenhuma alteração feita no Vertical Slice, que permanece no estado exportado da Semana 14

<!--
O feedback formal produzido aqui serve de insumo direto para a comparação arquitetural ampliada da Semana 16.
-->

---

## Resultado Esperado da Semana

- Leitura arquitetural guiada de dois projetos de referência oficiais do Godot (TPS Demo e Platformer 2D Demo)
- Registros de paralelo comparando essas soluções com as do próprio Vertical Slice construído desde a Semana 1
- Feedback formal escrito identificando e justificando ao menos uma decisão arquitetural própria que seria refeita à luz da análise
- Nenhuma alteração no Vertical Slice — o projeto permanece no estado consolidado e exportado da Semana 14

<!--
Este resultado corresponde à abertura da Unidade V no roadmap (PROJECT_ARCHITECTURE.md) — a turma domina o método de engenharia reversa como prática transferível para qualquer projeto profissional.
-->

---

## Checklist da Semana

- [ ] Roteiro de leitura arquitetural do TPS Demo concluído, com ao menos três paralelos registrados
- [ ] Roteiro de leitura arquitetural do Platformer 2D Demo concluído
- [ ] Paralelos do TPS Demo e do Platformer 2D Demo cruzados com as decisões do próprio Vertical Slice
- [ ] Feedback formal escrito, com ao menos uma decisão arquitetural própria justificada tecnicamente
- [ ] Nenhuma alteração de código realizada no Vertical Slice nesta semana

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 16.
-->

---

## Próximos Passos — Semana 16

A Semana 16 encerra a Unidade V com a comparação arquitetural sistemática Godot x Unity x Unreal x O3DE x Stride, consolidando em quadro comparativo todos os sistemas construídos ao longo do semestre e preparando o checkpoint da apresentação técnica final da Semana 17.

Leitura recomendada: Godot Demo Projects (github.com/godotengine/godot-demo-projects) — TPS Demo, Platformer 2D Demo; Godot Docs — Best Practices / Project Organization.

<!--
Referências completas: ver Plano de Aula Semana 15. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
Os paralelos e o feedback formal produzidos nesta semana — especialmente a decisão arquitetural candidata a revisão — servem de insumo direto para a comparação ampliada da Semana 16.
-->
