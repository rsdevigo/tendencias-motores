# Semana 15 — Engenharia Reversa de Projetos Profissionais (Godot Demo Projects)

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade V — Comparar Arquiteturas e Aprender Novos Motores** (Semanas 15–17) | **Metodologia:** Reverse Engineering — discussões, comparações, análises, apresentações. Autonomia muito alta; professor atua como mediador de discussão técnica.
**Abertura de Unidade (🔵)** — a Semana 15 abre a Unidade V; não fecha módulo.

## Introdução da Semana

A Semana 14 encerrou a Unidade IV com o Vertical Slice de cada grupo exportado, validado por Playtest cruzado e por Code Review de encerramento — um produto tecnicamente pronto, otimizado e empacotado. A partir da Semana 15, a disciplina muda de pergunta outra vez: não mais "o que falta construir?" nem "como produzir em escala de estúdio?", mas "como uma equipe profissional estrutura a arquitetura de um jogo em produção real, e o que isso revela sobre as próprias escolhas do grupo?". Nenhum sistema novo é adicionado ao Vertical Slice nesta semana. O projeto de cada grupo, consolidado na Semana 14, passa a ser o ponto de comparação direto contra projetos de referência oficiais do Godot — os Godot Demo Projects, com foco no TPS Demo (Third Person Shooter) e no Platformer 2D Demo. A metodologia muda de produção para leitura arquitetural guiada e discussão comparativa.

## Objetivos Gerais

- Compreender engenharia reversa de código como método de aprendizagem: ler a arquitetura de um projeto profissional para entender decisões de design, não para copiar implementação.
- Analisar a estrutura do TPS Demo oficial do Godot, identificando como Signals, Autoload, Resource customizado, Components e outros padrões já praticados pelo grupo aparecem (ou não) na solução oficial.
- Comparar as soluções arquiteturais dos projetos de referência com as soluções adotadas pelo próprio grupo ao longo do semestre.
- Identificar, no próprio Vertical Slice, ao menos uma decisão arquitetural que poderia ser refeita à luz dos projetos de referência analisados.

## Resultados Esperados

Ao final da semana, cada grupo terá conduzido a leitura arquitetural guiada de dois projetos de referência oficiais do Godot (TPS Demo e Platformer 2D Demo), identificado paralelos e divergências entre essas soluções e as do próprio Vertical Slice, e produzido um feedback formal sobre pelo menos uma decisão arquitetural própria que seria refeita à luz da análise — sem qualquer alteração de código exigida nesta semana.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o que é engenharia reversa de código como prática de aprendizagem, distinguindo-a de cópia de implementação.
- Identificar, na estrutura de cenas e scripts do TPS Demo, os padrões arquiteturais equivalentes aos já praticados no próprio Vertical Slice (Signals, Autoload/Singleton, Components, State Machine/Behavior Tree).
- Traçar paralelos explícitos entre decisões do TPS Demo e decisões tomadas pelo próprio grupo desde o Módulo 1.

## Conteúdos

- Engenharia reversa como método: ler a árvore de cenas, os scripts e as conexões de sinais de um projeto pronto para reconstruir o raciocínio arquitetural por trás dele, sem executar refatoração.
- Estrutura geral do TPS Demo (Third Person Shooter) — organização de cenas, gameplay framework (player, câmera, armas, inimigos), uso de Signals e Autoload.
- Paralelo guiado com o Vertical Slice da turma: onde o TPS Demo resolve o mesmo tipo de problema (comunicação entre sistemas, estado do personagem, gerenciamento de estado global) com uma solução igual, similar ou diferente da adotada pelo grupo.
- Documentação como ponto de partida da leitura: uso do próprio código-fonte do TPS Demo como documentação primária, complementado pela documentação oficial do Godot quando um recurso específico não for familiar.

## Conceitos Fundamentais

O conceito universal desta aula é engenharia reversa de arquitetura de software como ferramenta de aprendizagem contínua — a capacidade de ler um projeto pronto (não escrito pelo próprio time) e reconstruir as decisões de design por trás dele é uma habilidade transferível para qualquer engine, qualquer linguagem e qualquer stack, muito além do Godot. Em qualquer motor de jogos, um profissional frequentemente entra em um projeto já existente, com decisões arquiteturais já tomadas por outra equipe — a competência de "entender antes de mexer" é tão universal quanto qualquer padrão de design isolado. O TPS Demo é o veículo, não o objetivo: o que se ensina é o método de leitura, aplicável a qualquer código-base profissional que o estudante encontrará depois da disciplina.

## Recursos do Godot

- Godot Demo Projects (repositório oficial) — TPS Demo.
- Editor do Godot em modo de leitura: FileSystem dock, Scene dock e Script editor usados para navegação e leitura, não para edição.
- Debugger/Remote Scene Tree (opcional) para observar a árvore de nós do TPS Demo em execução.

## Comparação com Unity

A Unity Learn e o Asset Store oferecem projetos de referência equivalentes (ex.: templates oficiais de Third Person, Unity Learn sample projects), e a prática de engenharia reversa sobre projetos de amostra é igualmente comum na comunidade Unity — a diferença está mais na organização dos exemplos oficiais (Unity tende a distribuir templates via Package Manager e Unity Learn; Godot distribui via repositório GitHub aberto) do que no método de leitura em si. O princípio universal é idêntico nas duas engines: um projeto de referência oficial da própria engine mostra convenções e padrões idiomáticos que a documentação de API isolada não revela.

## Preparação do Professor

- Cópia local do TPS Demo (Godot Demo Projects, github.com/godotengine/godot-demo-projects) já aberta no editor, pronta para navegação em tela.
- Vertical Slice de referência do professor (ou de um grupo, com autorização prévia) aberto lado a lado para o paralelo em tempo real.
- Roteiro de leitura arquitetural guiada (perguntas norteadoras: onde está o Autoload? Como o player se comunica com a arma? Que Signals existem e quem os escuta?) impresso ou projetado.
- Projetor/tela dividida para exibir TPS Demo e Vertical Slice simultaneamente durante o paralelo.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Módulo 4 encerrado na Semana 14 e abertura da Unidade V — o que muda na pergunta orientadora do semestre |
| 20 min | Introdução ao método de engenharia reversa de código como prática de aprendizagem |
| 50 min | Leitura arquitetural guiada do TPS Demo, seguindo o roteiro de perguntas norteadoras |
| 40 min | Paralelo em pequenos grupos: cada grupo mapeia, no próprio Vertical Slice, os equivalentes (ou ausências) dos padrões identificados no TPS Demo |
| 10 min | Feedback e fechamento do Encontro 1 |

## Desenvolvimento

O encontro abre reconhecendo a virada de módulo: da Semana 1 à Semana 14 a pergunta foi "que sistema construir a seguir?"; a partir de agora a pergunta é "o que a leitura de projetos profissionais revela sobre as escolhas já feitas?". O professor apresenta o método de engenharia reversa de código — não como uma técnica exclusiva do Godot, mas como uma prática universal de leitura de arquitetura de software — e então conduz a turma pela estrutura do TPS Demo, seguindo o roteiro de perguntas norteadoras: como o projeto organiza suas cenas principais, onde estão os Autoloads e o que eles gerenciam, como Signals conectam player, armas e inimigos, e que outros padrões já praticados pela turma (Components, Resource customizado, State Machine) aparecem na solução oficial. Em seguida, os grupos se voltam para o próprio Vertical Slice e, em pequenos grupos, mapeiam explicitamente os paralelos: onde o próprio projeto resolve o mesmo problema de forma igual, similar ou diferente do TPS Demo, registrando essas observações para retomada no Encontro 2.

## Desafio

Não há desafio de implementação neste encontro — o "desafio" é interpretativo: cada grupo deve identificar, no roteiro de leitura, ao menos três pontos de paralelo (convergência ou divergência) entre a arquitetura do TPS Demo e a do próprio Vertical Slice, com justificativa técnica para cada ponto, não apenas observação superficial.

## Critérios de Sucesso

Cada grupo produz, ao final do encontro, um registro escrito com ao menos três paralelos arquiteturais identificados entre o TPS Demo e o próprio Vertical Slice, cada um justificado em termos dos padrões já praticados durante o semestre (Signals, Autoload, Components, Resource customizado, State Machine/Behavior Tree).

## Evidências para Avaliação

Registro de paralelos arquiteturais de cada grupo, insumo direto para o feedback formal sobre as análises arquiteturais previsto como entrega da Semana 15 — não constitui, isoladamente, uma rubrica formal de Code Review, mas alimenta a avaliação qualitativa da Unidade V.

## Dificuldades Esperadas

- Grupos tentando "corrigir" o próprio projeto durante a leitura, em vez de apenas registrar o paralelo — reforçar que nenhuma alteração de código é esperada nesta semana.
- Leitura superficial do TPS Demo, limitada a nomes de arquivos sem examinar Signals e conexões reais — o roteiro de perguntas norteadoras deve forçar a leitura das conexões, não apenas da árvore de cenas.
- Grupos cujo Vertical Slice diverge muito da estrutura do TPS Demo (por escopo ou gênero) tendo dificuldade de traçar paralelo direto — reforçar que divergência justificada é um paralelo tão válido quanto convergência.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar a estrutura do Platformer 2D Demo e de outros Godot Demo Projects relevantes ao escopo dos Vertical Slices da turma.
- Comparar as soluções arquiteturais dos projetos de referência (TPS Demo e Platformer 2D Demo) com as soluções adotadas pelo próprio grupo ao longo do semestre.
- Identificar e justificar, no próprio Vertical Slice, ao menos uma decisão arquitetural que poderia ser refeita à luz dos projetos de referência analisados.

## Conteúdos

- Estrutura geral do Platformer 2D Demo — organização de cenas, gameplay framework 2D, e outros Godot Demo Projects relevantes conforme o escopo dos Vertical Slices presentes na turma.
- Consolidação comparativa: retomada dos paralelos registrados no Encontro 1 (TPS Demo) somados aos novos paralelos identificados no Platformer 2D Demo.
- Formulação do feedback formal — cada grupo estrutura por escrito ao menos uma decisão arquitetural própria que seria refeita à luz da análise, com justificativa técnica.

## Conceitos Fundamentais

O conceito universal retomado e ampliado neste encontro é o de que arquitetura de software não tem uma única solução correta — projetos profissionais diferentes (TPS Demo, Platformer 2D Demo, e o próprio Vertical Slice de cada grupo) resolvem problemas semelhantes (comunicação entre sistemas, gerenciamento de estado, organização de cena) de formas distintas, cada uma com trade-offs próprios. A competência que a Semana 15 desenvolve não é "replicar a solução oficial", mas "reconhecer trade-offs arquiteturais e justificar uma escolha própria diante de alternativas conhecidas" — uma habilidade que permanece idêntica em qualquer engine ou stack de desenvolvimento de software.

## Recursos do Godot

- Godot Demo Projects (repositório oficial) — Platformer 2D Demo e outros projetos relevantes ao escopo da turma.
- Vertical Slice de cada grupo, consolidado na Semana 14, como objeto de comparação.

## Comparação com Unity

Assim como no Encontro 1, a Unity oferece equivalentes em Unity Learn e templates oficiais para gêneros 2D — a prática de comparar múltiplos projetos de referência contra o próprio projeto, em vez de estudar apenas um exemplo isolado, é igualmente válida em qualquer engine: quanto mais amostras de solução profissional um desenvolvedor examina, mais nítido fica o espaço de trade-offs arquiteturais disponível, independentemente de a engine ser Godot, Unity ou outra.

## Preparação do Professor

- Cópia local do Platformer 2D Demo (e de outros Godot Demo Projects pertinentes ao escopo predominante dos Vertical Slices da turma) já aberta no editor.
- Registros de paralelo arquitetural produzidos pelos grupos no Encontro 1, retomados no início deste encontro.
- Modelo/roteiro do feedback formal (uma decisão arquitetural própria a ser refeita, com justificativa) para orientar a produção escrita dos grupos.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 15 min | Revisão dos paralelos registrados no Encontro 1 (TPS Demo) |
| 45 min | Leitura arquitetural guiada do Platformer 2D Demo e de outros Godot Demo Projects relevantes ao escopo da turma |
| 40 min | Comparação consolidada: cada grupo cruza os paralelos do TPS Demo e do Platformer 2D Demo com as soluções do próprio Vertical Slice |
| 25 min | Desafio: cada grupo redige o feedback formal — ao menos uma decisão arquitetural própria que seria refeita à luz da análise, com justificativa |
| 10 min | Feedback e fechamento da semana |

## Desenvolvimento

O encontro retoma os registros de paralelo produzidos no Encontro 1 e estende a leitura arquitetural guiada ao Platformer 2D Demo — escolhido por cobrir um gênero (2D) que complementa o TPS Demo (3D) e amplia o repertório de soluções examinadas — além de outros Godot Demo Projects que o professor julgar relevantes ao escopo predominante dos Vertical Slices da turma. Com os dois projetos de referência já lidos, cada grupo consolida a comparação: cruza os paralelos identificados no TPS Demo e no Platformer 2D Demo com as próprias decisões tomadas desde o Módulo 1 (Signals, Autoload/Singleton, Resource customizado, Components, Behavior Tree, materiais, áudio, otimização), buscando pontos em que a solução de referência é mais robusta, mais simples, ou resolve um trade-off de forma diferente da adotada pelo grupo. O encontro fecha com a produção do desafio da semana — o feedback formal escrito.

## Desafio

Cada grupo identifica, no próprio Vertical Slice, ao menos uma decisão arquitetural que poderia ser refeita à luz dos projetos de referência analisados (TPS Demo e Platformer 2D Demo), redigindo uma justificativa técnica curta para a mudança proposta — sem exigência de implementá-la nesta semana; o registro escrito é o produto do desafio.

## Critérios de Sucesso

Cada grupo entrega, ao final da semana, um feedback formal escrito identificando pelo menos uma decisão arquitetural própria que seria refeita à luz da análise dos projetos de referência, com justificativa técnica fundamentada nos paralelos levantados nos dois encontros — não uma opinião estética, mas uma análise de trade-off arquitetural.

## Evidências para Avaliação

**Feedback formal sobre as análises arquiteturais**, conforme previsto no Cronograma para a Semana 15 — avaliação qualitativa da capacidade de leitura arquitetural comparativa e de autocrítica técnica fundamentada, não associada a uma rubrica numérica formal de Code Review.

## Dificuldades Esperadas

- Grupos propondo mudanças arquiteturais vagas ("deveríamos organizar melhor o projeto") sem justificativa técnica específica — exigir que a proposta aponte um trade-off concreto observado no projeto de referência.
- Confundir "decisão que poderia ser refeita" com "erro cometido" — reforçar que trade-offs arquiteturais válidos na época da decisão (ex.: Semana 3, com escopo menor) podem legitimamente não escalar até a Semana 14, sem que isso indique um erro do grupo.
- Grupos com pouco tempo restante tentando cobrir múltiplos pontos superficialmente em vez de aprofundar um único ponto — reforçar que a qualidade da justificativa importa mais que a quantidade de pontos levantados.

---

# Resultado Esperado da Semana

Ao final da Semana 15, cada grupo terá conduzido a leitura arquitetural guiada de dois projetos de referência oficiais do Godot (TPS Demo e Platformer 2D Demo), produzido registros de paralelo comparando essas soluções com as do próprio Vertical Slice construído desde a Semana 1, e entregue um feedback formal escrito identificando e justificando ao menos uma decisão arquitetural própria que seria refeita à luz dessa análise. Nenhuma alteração é feita no Vertical Slice nesta semana — o projeto permanece no estado consolidado e exportado da Semana 14. A Unidade V está aberta: a turma domina o método de engenharia reversa de arquitetura de software como prática transferível para qualquer projeto profissional, dentro ou fora do Godot.

# Preparação para a Próxima Semana

A Semana 16 encerra a Unidade V com a comparação arquitetural sistemática Godot x Unity x Unreal x O3DE x Stride, consolidando em quadro comparativo todos os sistemas construídos ao longo do semestre (gameplay framework, animação, IA, UI, pipeline de produção) e preparando o checkpoint da apresentação técnica final da Semana 17. Os paralelos e o feedback formal produzidos nesta semana — especialmente a decisão arquitetural que cada grupo identificou como candidata a revisão — servem de insumo direto para essa comparação ampliada e para a narrativa da apresentação final.

# Referências

- Godot Demo Projects (repositório oficial): https://github.com/godotengine/godot-demo-projects
- Godot Demo Projects — TPS Demo (Third Person Shooter): https://github.com/godotengine/godot-demo-projects/tree/master/3d/third_person_shooter
- Godot Demo Projects — Platformer 2D Demo: https://github.com/godotengine/godot-demo-projects/tree/master/2d/platformer
- Godot Documentation — Best Practices / Project Organization: https://docs.godotengine.org/en/stable/tutorials/best_practices/index.html
- Unity Learn (consulta comparativa) — Sample Projects: https://learn.unity.com/
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
