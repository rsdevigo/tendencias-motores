# Semana 16 — Comparação Arquitetural Godot x Unity x Unreal x O3DE x Stride

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade V — Comparar Arquiteturas e Aprender Novos Motores** (Semanas 15–17) | **Metodologia:** Reverse Engineering — discussões, comparações, análises, apresentações. Autonomia muito alta; professor atua como mediador de discussão técnica.
**Encerramento de Módulo (🔴)** — esta semana fecha o núcleo comparativo da Unidade V com um Checkpoint de preparação da apresentação técnica final da Semana 17.

## Introdução da Semana

A Semana 15 abriu a Unidade V com leitura arquitetural guiada de dois projetos oficiais do Godot (TPS Demo e Platformer 2D Demo), produzindo registros de paralelo e um feedback formal escrito sobre pelo menos uma decisão arquitetural do próprio Vertical Slice que cada grupo identificou como candidata a revisão. Nenhum sistema novo foi adicionado ao projeto naquela semana — o Vertical Slice permanece no estado consolidado e exportado desde a Semana 14. A Semana 16 muda de escala: em vez de comparar o próprio projeto com outro projeto Godot, cada grupo compara o Godot inteiro — como motor, não como projeto — contra Unity, Unreal Engine, O3DE e Stride, sistema por sistema, ao longo de todos os módulos já cursados (gameplay framework, animação, IA, UI, pipeline de produção). Nenhuma linha de código é escrita nesta semana; nenhum sistema novo é implementado no Vertical Slice. O produto da semana é intelectual: um quadro comparativo sistemático e o checkpoint de preparação da apresentação técnica final, que a Semana 17 vai exigir de cada grupo.

## Objetivos Gerais

- Consolidar, em um quadro comparativo sistemático, as equivalências e diferenças arquiteturais entre Godot e Unity identificadas ao longo de todo o semestre, sistema por sistema.
- Ampliar essa comparação para Unreal Engine, O3DE e Stride, reconhecendo o que é transferível entre engines e o que é específico da implementação do Godot.
- Escolher, com justificativa técnica própria, o motor mais relevante para comparação aprofundada com o projeto de cada grupo (entre Unreal Engine, O3DE e Stride).
- Estruturar o checkpoint de preparação da apresentação técnica final — narrativa, decisões arquiteturais a destacar e comparação entre motores.

## Resultados Esperados

Ao final da semana, cada grupo terá produzido um quadro comparativo Godot x Unity cobrindo todos os sistemas construídos no semestre, terá discutido e registrado paralelos com Unreal Engine, O3DE e Stride quando pertinentes a cada sistema, e terá entregue um checkpoint de preparação da apresentação técnica final — incluindo Vertical Slice, decisões arquiteturais a apresentar e a comparação entre motores escolhida. Nenhuma alteração é feita no Vertical Slice nesta semana; o projeto permanece no estado consolidado da Semana 14.

---

# Encontro 1

## Objetivos de Aprendizagem

- Consolidar sistematicamente, sistema por sistema, a comparação Godot x Unity já praticada ao longo do semestre em cada módulo.
- Elaborar um quadro comparativo Godot x Unity cobrindo gameplay framework, animação, IA, UI e pipeline de produção, com base nos sistemas efetivamente construídos no próprio Vertical Slice.
- Distinguir, em cada linha do quadro, o que é conceito universal de Game Engine e o que é decisão de implementação específica do Godot.

## Conteúdos

- Revisão consolidada, módulo a módulo, das comparações Godot x Unity já feitas ao longo do Cronograma: Autoload/Singleton x GameMode/GameState, Nodes/Components x Actor Components, Signals x Event Dispatchers, Resource x Data Assets, AnimationTree x Animation Blueprint, Control nodes x UMG, NavigationAgent x AI Navigation, LimboAI/Blackboard x Behavior Tree, Material Overrides x Material Instances, MultiMeshInstance3D x Foliage, Export Templates x Packaging.
- Estrutura de um quadro comparativo técnico: sistema, solução no Godot (aplicada no próprio Vertical Slice), solução equivalente na Unity, e o que permanece igual entre as duas (o conceito universal).
- Critério de organização do quadro por módulo cursado, não por ordem alfabética de recurso — reforça a trilha pedagógica percorrida desde a Semana 1.

## Conceitos Fundamentais

O conceito universal desta aula é a distinção entre conceito de Game Engine e implementação de uma engine específica. Um Autoload no Godot e um GameMode na Unreal resolvem o mesmo problema — estado de partida acessível globalmente — com nomes, sintaxe e limitações diferentes; uma Signal no Godot e um Event/Delegate na Unity resolvem o mesmo problema de comunicação desacoplada entre sistemas. A competência central do Módulo 5 é reconhecer esse padrão repetidamente: quando um estudante consegue nomear o conceito universal por trás de um recurso específico do Godot, ele já tem o vocabulário necessário para localizar o recurso equivalente em qualquer motor novo, mesmo sem ainda conhecer a sintaxe daquele motor.

## Recursos do Godot

- Revisão geral do Vertical Slice completo — nenhum recurso novo é aberto no editor nesta semana; o Godot é usado apenas como referência de consulta para preencher o quadro comparativo.
- Documentação oficial do Godot (Class Reference) como fonte de consulta rápida para confirmar terminologia exata de cada sistema já construído.

## Comparação com Unity

Este encontro é, por definição, inteiramente sobre a comparação com Unity — não há "comparação com Unity" isolada como seção lateral, porque a comparação é o próprio conteúdo do encontro. O quadro comparativo deve cobrir, no mínimo, os pares já trabalhados no semestre: Autoload x GameMode/GameState/GameInstance, Node composition x Actor Components, Signals x C# Events/UnityEvents, Resource x ScriptableObject, AnimationTree/BlendSpace x Animator Controller/Blend Trees, Control nodes x UGUI/UI Toolkit, NavigationAgent3D x NavMesh Agent, LimboAI/Blackboard x Behavior Designer ou soluções equivalentes de terceiros, Material Overrides x Material Instances/Property Blocks, MultiMeshInstance3D x GPU Instancing/terrain foliage, Export Templates x Build Settings/Player Settings.

## Preparação do Professor

- Modelo de quadro comparativo (planilha ou tabela) com colunas Sistema | Módulo | Solução no Vertical Slice (Godot) | Equivalente na Unity | Conceito universal, pronto para ser preenchido em aula.
- Lista consolidada de todos os sistemas construídos no semestre, extraída do Cronograma e do PROJECT_ARCHITECTURE.md, para servir de checklist e evitar que algum sistema seja esquecido no quadro.
- Documentação oficial do Godot e da Unity Manual/Unity Learn abertas para consulta rápida durante a sessão.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 15 min | Revisão do feedback formal produzido na Semana 15 e abertura da comparação sistemática |
| 20 min | Apresentação do modelo de quadro comparativo e do checklist de sistemas construídos no semestre |
| 60 min | Elaboração em grupo do quadro comparativo Godot x Unity, sistema por sistema, módulo por módulo |
| 30 min | Socialização: cada grupo apresenta rapidamente um par de linhas do próprio quadro que considerou mais revelador |
| 10 min | Feedback e fechamento do Encontro 1 |

## Desenvolvimento

O encontro abre retomando o feedback formal da Semana 15 — a decisão arquitetural que cada grupo identificou como candidata a revisão é o primeiro item a entrar no quadro comparativo, como ponto de partida concreto. O professor apresenta o modelo de quadro e o checklist de sistemas construídos desde a Semana 1, e os grupos passam a maior parte do encontro preenchendo o quadro comparativo, sistema por sistema, sempre alimentados pelo que o próprio Vertical Slice implementa (não por teoria genérica). O encontro fecha com uma rodada de socialização breve, em que cada grupo compartilha o par Godot x Unity que considerou mais revelador — geralmente aquele em que a diferença de implementação escondia, ou revelava com mais clareza, o mesmo conceito universal.

## Desafio

Não há desafio de implementação neste encontro — o desafio é a completude e a profundidade do quadro comparativo: cada grupo deve cobrir todos os módulos cursados (1 a 4), sem pular sistemas, e cada linha do quadro deve nomear explicitamente o conceito universal por trás do par Godot x Unity, não apenas listar os dois nomes lado a lado.

## Critérios de Sucesso

Cada grupo produz, ao final do encontro, um quadro comparativo Godot x Unity cobrindo todos os sistemas construídos nos Módulos 1 a 4, com a coluna de conceito universal preenchida em cada linha — não apenas terminologia, mas o motivo pelo qual o sistema existe em qualquer engine.

## Evidências para Avaliação

Quadro comparativo Godot x Unity de cada grupo, insumo direto para o Checkpoint de preparação previsto como entrega da Semana 16 — não constitui, isoladamente, uma rubrica numérica formal, mas alimenta diretamente a apresentação técnica final da Semana 17.

## Dificuldades Esperadas

- Grupos preenchendo o quadro apenas com nomes de classes/nós, sem articular o conceito universal — o professor deve insistir na pergunta "por que esse sistema existiria em qualquer engine?" para cada linha.
- Sistemas de módulos mais antigos (Semanas 1–3) sendo esquecidos por já estarem distantes na memória — o checklist do professor deve cobrir explicitamente esses sistemas.
- Grupos tentando reabrir o projeto no editor para "conferir" detalhes de implementação — reforçar que o quadro deve ser preenchido a partir do que já foi aprendido, não de nova exploração no editor.

---

# Encontro 2

## Objetivos de Aprendizagem

- Ampliar a comparação sistemática para Unreal Engine, O3DE e Stride, quando pertinente a cada sistema já mapeado no quadro Godot x Unity.
- Escolher e justificar, entre Unreal Engine, O3DE e Stride, o motor mais relevante para comparação aprofundada com o próprio projeto.
- Estruturar o checkpoint de preparação da apresentação técnica final, articulando Vertical Slice, decisões arquiteturais e comparação entre motores.

## Conteúdos

- Panorama comparativo de Unreal Engine, O3DE e Stride frente aos sistemas já mapeados no quadro Godot x Unity — apenas nos pontos em que cada motor apresenta uma diferença arquitetural relevante, não uma varredura exaustiva de todos os recursos de cada engine.
- Critérios para escolha do motor de comparação aprofundada: gênero do Vertical Slice do grupo, familiaridade prévia (Unreal costuma ser mais conhecida da turma via disciplinas anteriores), e disponibilidade de documentação pública de qualidade.
- Estrutura do checkpoint de preparação da apresentação técnica final: recorte do Vertical Slice a apresentar, decisões arquiteturais centrais a destacar, e a comparação entre motores escolhida como fio condutor da apresentação da Semana 17.

## Conceitos Fundamentais

O conceito universal retomado neste encontro é que a ampliação da comparação para múltiplos motores confirma, em vez de contradizer, o que já apareceu no par Godot x Unity: os mesmos problemas — estado global de partida, comunicação desacoplada entre sistemas, dados de design fora do código, navegação e decisão autônoma de agentes, composição de cena em escala, empacotamento de build — reaparecem em Unreal, O3DE e Stride com nomes e convenções próprias, mas com a mesma motivação de design. A disciplina não pretende ensinar Unreal, O3DE ou Stride em profundidade; pretende demonstrar, com evidência acumulada de múltiplos motores, que a competência real desenvolvida no semestre foi a de reconhecer conceitos universais de Game Engine sob qualquer nome de API.

## Recursos do Godot

- Nenhum recurso novo do Godot é explorado neste encontro — o Vertical Slice consolidado desde a Semana 14 continua sendo o objeto de referência central da comparação e da apresentação em preparação.

## Comparação com Unity

A comparação com Unity, já consolidada no Encontro 1, permanece como eixo de referência: ao introduzir Unreal, O3DE e Stride, cada grupo deve situar o novo motor em relação ao par Godot x Unity já mapeado, não tratá-lo como uma terceira comparação isolada — por exemplo, "assim como a Unity usa ScriptableObject e o Godot usa Resource, a Unreal usa Data Assets e a O3DE usa Assets baseados em componentes, todos resolvendo o mesmo problema de dados de design desacoplados do código".

## Preparação do Professor

- Quadros comparativos produzidos pelos grupos no Encontro 1, retomados como base deste encontro.
- Documentação pública de Unreal Engine, O3DE e Stride organizada por sistema (gameplay framework, animação, IA, UI, packaging), pronta para consulta rápida quando um grupo escolher aprofundar um desses motores.
- Modelo/roteiro do checkpoint de preparação da apresentação técnica final (recorte do Vertical Slice, decisões arquiteturais a destacar, comparação entre motores escolhida), para orientar a produção escrita dos grupos.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 15 min | Retomada do quadro comparativo Godot x Unity produzido no Encontro 1 |
| 40 min | Ampliação guiada da comparação para Unreal Engine, O3DE e Stride, nos pontos em que cada motor diverge de forma relevante |
| 15 min | Desafio: cada grupo escolhe e justifica o motor mais relevante para comparação aprofundada com o próprio projeto |
| 45 min | Estruturação do checkpoint de preparação da apresentação técnica final |
| 20 min | Feedback e fechamento da semana e da Unidade V |

## Desenvolvimento

O encontro retoma o quadro comparativo do Encontro 1 e amplia a discussão para Unreal Engine, O3DE e Stride, sempre ancorado nos sistemas já mapeados — o professor conduz essa ampliação apontando, sistema por sistema, onde cada motor adicional confirma o padrão já visto (ex.: todo motor moderno tem algum mecanismo de estado global de partida) e onde a implementação diverge de forma pedagogicamente relevante (ex.: Blueprint visual scripting na Unreal como equivalente mais direto ao Orchestrator do que ao C# da Unity). Em seguida, cada grupo cumpre o desafio da semana: escolher, entre Unreal, O3DE ou Stride, o motor mais relevante para uma comparação aprofundada com o próprio projeto, justificando a escolha por gênero, familiaridade ou qualidade de documentação disponível. O encontro fecha com a produção do checkpoint de preparação da apresentação técnica final — cada grupo estrutura o recorte do Vertical Slice que vai apresentar, as decisões arquiteturais centrais a destacar e a comparação entre motores que vai servir de fio condutor da apresentação da Semana 17.

## Desafio

Cada grupo escolhe, entre Unreal Engine, O3DE ou Stride, o motor mais relevante para comparação aprofundada com o próprio projeto, redigindo uma justificativa técnica curta para a escolha (gênero do jogo, familiaridade prévia da equipe, ou qualidade da documentação pública disponível) — sem exigência de implementação nesta semana; o registro escrito, junto ao checkpoint, é o produto do desafio.

## Critérios de Sucesso

Cada grupo entrega, ao final da semana, um checkpoint de preparação da apresentação técnica final contendo: o recorte do Vertical Slice a ser apresentado, ao menos três decisões arquiteturais centrais a destacar, e a comparação entre motores escolhida (Unreal, O3DE ou Stride) com justificativa técnica — pronto para servir de roteiro direto da apresentação da Semana 17.

## Evidências para Avaliação

**Checkpoint de preparação da apresentação técnica final**, conforme previsto no Cronograma para a Semana 16 — avaliação qualitativa da capacidade de síntese comparativa entre motores e de organização da narrativa técnica que será apresentada na Semana 17, não associada a uma rubrica numérica formal isolada.

## Dificuldades Esperadas

- Grupos tentando cobrir Unreal, O3DE e Stride com a mesma profundidade, esgotando o tempo do encontro — reforçar que a comparação ampliada é panorâmica; a profundidade fica reservada ao motor escolhido no desafio.
- Escolha do motor de comparação aprofundada feita por familiaridade superficial ("já ouvi falar de Unreal") sem justificativa técnica real — exigir que a justificativa aponte pelo menos um sistema concreto do próprio projeto que se beneficiaria da comparação com o motor escolhido.
- Checkpoint estruturado como resumo do semestre inteiro, sem recorte — reforçar que a apresentação da Semana 17 tem tempo limitado, e o checkpoint deve já vir com um recorte claro do que será mostrado, não uma lista exaustiva de tudo que foi feito.

---

# Resultado Esperado da Semana

Ao final da Semana 16, cada grupo terá produzido um quadro comparativo sistemático Godot x Unity cobrindo todos os sistemas construídos nos Módulos 1 a 4, terá discutido e registrado paralelos relevantes com Unreal Engine, O3DE e Stride, terá escolhido e justificado um desses três motores para comparação aprofundada com o próprio projeto, e terá entregue um checkpoint de preparação da apresentação técnica final — recorte do Vertical Slice, decisões arquiteturais centrais e comparação entre motores já estruturados como roteiro. Nenhuma alteração é feita no Vertical Slice nesta semana; o projeto permanece no estado consolidado e exportado desde a Semana 14. A Unidade V está com seu núcleo comparativo encerrado: a turma articula, com vocabulário próprio, o que é conceito universal de Game Engine e o que é decisão de implementação específica de cada motor.

# Preparação para a Próxima Semana

A Semana 17 encerra a Unidade V, o Módulo 5 e a disciplina com as apresentações técnicas finais de cada grupo, distribuídas nos dois encontros. O checkpoint de preparação produzido nesta semana — recorte do Vertical Slice, decisões arquiteturais a destacar e comparação entre motores escolhida — é o roteiro direto da apresentação; nenhum novo conteúdo de preparação é introduzido entre a Semana 16 e a Semana 17, apenas o ensaio e o ajuste fino de cada grupo sobre o que já foi estruturado.

# Referências

- Godot Documentation — Class Reference: https://docs.godotengine.org/en/stable/classes/index.html
- Godot Demo Projects (repositório oficial): https://github.com/godotengine/godot-demo-projects
- Unity Manual: https://docs.unity3d.com/Manual/
- Unity Learn: https://learn.unity.com/
- Unreal Engine Documentation: https://dev.epicgames.com/documentation/en-us/unreal-engine
- O3DE Documentation: https://docs.o3de.org/
- Stride Documentation: https://doc.stride3d.net/
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
