# Semana 16 🔴

## Introdução da Semana

A Semana 16 encerra a Unidade V — Comparar Arquiteturas e fecha o ciclo de Reverse Engineering iniciado na Semana 15. Se a Semana 15 comparou o Vertical Slice da turma a projetos de referência da própria Unreal (Lyra, Stack O Bot, Content Examples), a Semana 16 amplia o horizonte para fora da Unreal: primeiro consolidando, de forma sistemática, a comparação Unreal x Unity que já vem sendo construída de forma pontual desde o Módulo 2 (seção 12 do PROJECT_ARCHITECTURE.md), e depois estendendo essa comparação, quando pertinente, a Godot, O3DE, Stride e CryEngine. Nenhum sistema novo é adicionado ao Vertical Slice nesta semana — `BP_Player`, `BP_Enemy`, o framework de GameMode/GameState/PlayerController/GameInstance, interação, inventário, HUD, IA, combate, materiais, foliage, áudio e o build empacotado da Semana 14 permanecem exatamente como estão. O trabalho da semana é consolidar, por escrito e em quadro comparativo, a transferência de conhecimento entre engines que é o objetivo final da disciplina, preparando diretamente a Apresentação Técnica Final da Semana 17. A semana se encerra com o **Checkpoint de preparação da apresentação técnica final**, marco avaliativo previsto no Cronograma para esta semana.

## Objetivos Gerais

- Consolidar, em um único quadro comparativo, todas as comparações Unreal x Unity construídas ao longo do semestre (gameplay framework, animação, IA, UI, pipeline de produção).
- Identificar o que é conceito universal de motores de jogos e o que é decisão específica de implementação da Unreal.
- Ampliar a comparação arquitetural para pelo menos um motor adicional (Godot, O3DE, Stride ou CryEngine), com justificativa técnica da escolha.
- Preparar a estrutura da Apresentação Técnica Final da Semana 17, articulando Vertical Slice, decisões arquiteturais e comparação entre motores.

## Resultados Esperados

Ao final da semana, cada grupo terá produzido um quadro comparativo sistemático Unreal x Unity cobrindo todos os sistemas construídos no semestre, terá escolhido e justificado um motor adicional (entre Godot, O3DE, Stride e CryEngine) para aprofundar a comparação com o próprio projeto, e terá uma estrutura preliminar da Apresentação Técnica Final pronta para ser refinada na Semana 17. Essa entrega corresponde ao **Checkpoint de preparação da apresentação técnica final** previsto no Cronograma, e reutiliza diretamente o quadro comparativo do Lyra e a justificativa técnica registrados na Semana 15 — nenhum dos dois é descartado ou refeito do zero.

---

# Encontro 1

## Objetivos de Aprendizagem

- Consolidar em um único quadro comparativo todas as correspondências Unreal x Unity identificadas ao longo do semestre.
- Distinguir, para cada sistema do Vertical Slice, o que é conceito universal de motores de jogos e o que é decisão de implementação específica da Unreal.
- Articular a consolidação com a análise arquitetural produzida na Semana 15 (Lyra, Stack O Bot, Content Examples).

## Conteúdos

- Revisão sistemática de todos os sistemas do Vertical Slice construídos desde o Módulo 2: gameplay framework (GameMode/GameState/PlayerController/GameInstance), Enhanced Input, Interaction via Blueprint Interfaces, Event Dispatchers, Inventory (Data Table/Data Asset), SaveGame, Animation Blueprint (State Machine, Blend Space), Behavior Tree/Blackboard, UMG, Materials/Material Instances.
- Consolidação do quadro comparativo Unreal x Unity (seção 12 do PROJECT_ARCHITECTURE.md), expandindo-o com o que foi aprendido na Semana 15 sobre o Lyra.
- Distinção entre conceito universal (o papel arquitetural cumprido) e decisão contextual (como a Unreal resolve esse papel especificamente).

## Conceitos Fundamentais

O conceito universal que fecha esta consolidação é que toda engine de jogos resolve o mesmo conjunto finito de problemas — composição de entidades (Actor/Component na Unreal, GameObject/Component na Unity), desacoplamento entre input físico e ação lógica, um ponto único de regras de partida, comunicação entre sistemas sem acoplamento direto, dados de design separados de lógica, persistência de estado, máquinas de estado para animação, interfaces de usuário em tempo real e estruturas de decisão para agentes não-jogadores. O que muda entre engines não é o problema, mas o grau de formalização nativa da solução: a Unreal formaliza como classe nativa da engine papéis que a Unity resolve por convenção de estúdio (GameMode/GameState versus Manager/Singleton), e oferece nativamente estruturas que a Unity historicamente terceiriza (Behavior Tree nativo versus packages de terceiros). Reconhecer esse padrão — mesmo problema, graus diferentes de formalização — é exatamente a capacidade que permite a um profissional de jogos transitar entre engines sem recomeçar do zero, e é o objetivo final de toda a disciplina.

## Recursos da Unreal

Revisão geral do Vertical Slice completo; PROJECT_ARCHITECTURE.md (seção 12, quadro comparativo base); Unreal Engine Documentation (Gameplay Framework, Enhanced Input, Blueprints, Animation, Behavior Trees, UMG, Materials) como referência de consulta rápida durante a consolidação.

## Comparação com Unity

Esta é a própria atividade do encontro: a seção 12 do PROJECT_ARCHITECTURE.md já registra, sistema a sistema, o que permanece igual e qual é a principal diferença arquitetural entre Unreal e Unity. O trabalho do Encontro 1 é revisar essa tabela em conjunto com a turma, completando eventuais lacunas com base na experiência prática de cada grupo ao longo do semestre e com a documentação oficial da Unity (Unity Manual/Unity Learn) para confirmar terminologia e comportamento atual.

## Preparação do Professor

- Projetar a seção 12 do PROJECT_ARCHITECTURE.md como ponto de partida da consolidação.
- Ter à mão o quadro comparativo do Lyra produzido pelos grupos na Semana 15, Encontro 1.
- Selecionar previamente 2–3 páginas da Unity Manual/Unity Learn para consulta rápida em caso de dúvida terminológica durante a consolidação (ex.: ScriptableObject, Animator Controller, Action Maps).
- Preparar um modelo simples de quadro comparativo consolidado (sistema | Unreal | Unity | o que permanece igual | principal diferença) para os grupos preencherem.

## Cronograma do Encontro

10 min — Revisão da seção 12 do PROJECT_ARCHITECTURE.md e do quadro comparativo do Lyra produzido na Semana 15.

15 min — Introdução: por que consolidar a comparação agora, a uma semana da Apresentação Técnica Final.

40 min — Demonstração: percurso guiado pelo quadro comparativo Unreal x Unity, sistema a sistema, reforçando a distinção entre conceito universal e decisão contextual.

50 min — Laboratório em grupo: cada grupo revisa e completa seu próprio quadro comparativo, incorporando exemplos concretos do próprio Vertical Slice para cada linha da tabela.

20 min — Feedback: cada grupo apresenta brevemente uma linha do quadro que considerou mais reveladora sobre a diferença entre as engines.

## Desenvolvimento

O encontro abre revisando a seção 12 do PROJECT_ARCHITECTURE.md, já familiar à turma desde comparações pontuais feitas em módulos anteriores, e o quadro comparativo do Lyra produzido na Semana 15, que serve de ponte entre a análise interna à Unreal (Semana 15) e a análise entre engines (Semana 16). O professor então conduz uma consolidação guiada, sistema por sistema — gameplay framework, input, interação, inventário, save, animação, IA, UI, materiais — sempre voltando à pergunta central: o que este sistema resolve, independentemente da engine, e como cada engine formaliza essa solução? No laboratório, cada grupo reconstrói o quadro comparativo com exemplos concretos extraídos do próprio Vertical Slice, e não de definições genéricas — por exemplo, não apenas "GameMode versus Manager", mas "o BP_GameMode do nosso projeto controla a condição de vitória ao alcançar o objetivo final; em Unity, isso seria um Singleton próprio chamado, por exemplo, GameManager". O encontro fecha com apresentações curtas destacando a linha do quadro que cada grupo considerou mais reveladora.

## Desafio

Não há desafio formal neste encontro — o Encontro 1 é dedicado à consolidação sistemática, condição de base para a ampliação a outras engines e o desafio proposto no Encontro 2.

## Critérios de Sucesso

Cada grupo produziu um quadro comparativo Unreal x Unity consolidado, cobrindo pelo menos oito sistemas do Vertical Slice, com exemplos concretos do próprio projeto em cada linha e articulação correta entre conceito universal e decisão contextual da Unreal.

## Evidências para Avaliação

O quadro comparativo consolidado alimenta o Checkpoint de preparação da apresentação técnica final, avaliado à luz da Rubrica 7 (arquitetura e consistência do Vertical Slice, em sua dimensão de capacidade de explicar decisões) e da Rubrica 6 (justificativa técnica de decisões).

## Dificuldades Esperadas

Grupos podem reduzir a consolidação a uma cópia da seção 12 do PROJECT_ARCHITECTURE.md sem conectá-la a exemplos concretos do próprio projeto — o professor deve exigir, para cada linha, um exemplo nomeado do próprio Vertical Slice (o Blueprint, o Component, o evento específico), não apenas a categoria genérica. Também é comum confundir "o que permanece igual" com "o que é idêntico na implementação" — o professor deve reforçar que o conceito permanece igual mesmo quando a sintaxe e o grau de abstração mudam completamente.

---

# Encontro 2

## Objetivos de Aprendizagem

- Identificar, entre Godot, O3DE, Stride e CryEngine, o motor mais relevante para comparação com o próprio Vertical Slice, com justificativa técnica.
- Comparar pelo menos um sistema do próprio projeto com a solução equivalente do motor escolhido.
- Estruturar preliminarmente a Apresentação Técnica Final, articulando Vertical Slice, decisões arquiteturais e comparação entre motores.

## Conteúdos

- Panorama comparativo de Godot, O3DE, Stride e CryEngine: modelo de arquitetura, paradigma de scripting, público-alvo e maturidade de cada motor, sempre com a ressalva de que a comparação é pontual e não substitui o aprofundamento dado à dupla Unreal/Unity ao longo do semestre.
- Desafio: escolha justificada de um motor adicional e comparação de pelo menos um sistema do próprio projeto com a solução equivalente nesse motor.
- Estrutura preliminar da Apresentação Técnica Final: o que será apresentado, em que ordem, e que evidências do semestre sustentam cada ponto.

## Conceitos Fundamentais

O conceito universal fechado neste encontro é que a comparação entre engines não precisa ser exaustiva para ser útil — a maturidade profissional está em escolher, entre várias alternativas, a comparação mais relevante para o próprio contexto e justificar essa escolha tecnicamente, exatamente como se decide, no mercado de trabalho real, qual motor adotar para um projeto específico. Godot ilustra um paradigma de código aberto com cena e nó como unidade de composição (equivalente conceitual ao Actor/Component da Unreal); O3DE ilustra um motor open-source de licença permissiva orientado a componentes, com raízes em ferramentas de larga escala; Stride ilustra um motor C#/.NET de escopo mais compacto; CryEngine ilustra uma arquitetura historicamente voltada a fidelidade visual em tempo real. Nenhum desses motores precisa ser dominado pela turma — o objetivo é generalizar, mais uma vez, que o papel arquitetural (composição de entidades, desacoplamento de input, estrutura de dados de design, sistema de IA) é universal, e que a capacidade de identificar rapidamente como um motor novo resolve esses papéis é a competência central que a disciplina se propõe a formar.

## Recursos da Unreal

Revisão geral do Vertical Slice completo, usada como base de comparação; PROJECT_ARCHITECTURE.md (seções 7 e 12) para consulta durante o desafio.

## Comparação com Unity

Breve: a ampliação para Godot, O3DE, Stride e CryEngine não substitui a comparação sistemática com Unity feita no Encontro 1 — ela é um exercício pontual e complementar, escolhido individualmente por cada grupo conforme a relevância para o próprio projeto, e não deve se transformar em uma segunda aula completa de comparação. O professor deve redirecionar a discussão sempre que um grupo tentar aprofundar-se além do necessário para justificar a escolha do desafio.

## Preparação do Professor

- Selecionar previamente uma página de documentação oficial pública de cada motor (Godot Documentation, documentação pública de O3DE, Stride e CryEngine) para consulta rápida durante o laboratório, evitando que os grupos percam tempo apenas localizando a fonte.
- Preparar um roteiro simples da Apresentação Técnica Final (o que apresentar, tempo estimado por seção, evidências do semestre a citar) para orientar a estruturação preliminar.
- Ter à mão o quadro comparativo consolidado do Encontro 1, para servir de base à estrutura da apresentação.

## Cronograma do Encontro

15 min — Revisão do quadro comparativo Unreal x Unity consolidado no Encontro 1.

25 min — Panorama comparativo de Godot, O3DE, Stride e CryEngine: arquitetura, paradigma de scripting e público-alvo de cada um, em nível introdutório.

45 min — Laboratório/Desafio: cada grupo escolhe um motor entre os quatro, compara um sistema do próprio projeto com a solução equivalente nesse motor e registra a justificativa da escolha.

30 min — Estruturação preliminar da Apresentação Técnica Final: cada grupo esboça a ordem dos tópicos e as evidências do semestre que sustentarão a apresentação da Semana 17.

20 min — Feedback: cada grupo apresenta a escolha do motor, a comparação registrada e a estrutura preliminar da apresentação; o professor formaliza o Checkpoint da semana.

## Desenvolvimento

O encontro retoma o quadro comparativo consolidado no Encontro 1 e amplia o horizonte com um panorama rápido de Godot, O3DE, Stride e CryEngine, suficiente para que cada grupo compreenda o paradigma geral de cada motor sem se aprofundar além do necessário. No laboratório, cada grupo escolhe, entre os quatro, o motor mais relevante para comparar com o próprio Vertical Slice — por exemplo, um grupo que valorizou a Behavior Tree nativa da Unreal pode comparar com o sistema de IA do Godot; um grupo que discutiu bastante Data Assets pode comparar com o equivalente em O3DE ou Stride — e registra por escrito a escolha, a comparação de pelo menos um sistema e a justificativa técnica da escolha. Em seguida, cada grupo usa o tempo restante para esboçar a estrutura preliminar da Apresentação Técnica Final da Semana 17, organizando os tópicos (visão geral do Vertical Slice, decisões arquiteturais centrais, comparação Unreal x Unity, comparação com o motor adicional escolhido) e associando cada tópico a evidências concretas produzidas ao longo do semestre. O encontro fecha com apresentações curtas de cada grupo, cobrindo a escolha do motor, a comparação registrada e a estrutura preliminar, e o professor formaliza o Checkpoint de preparação previsto no Cronograma.

## Desafio

Cada grupo escolhe, entre Godot, O3DE, Stride e CryEngine, o motor mais relevante para comparação com o próprio Vertical Slice, registrando por escrito a escolha, a justificativa técnica e a comparação de pelo menos um sistema do próprio projeto com a solução equivalente no motor escolhido. O desafio permite diferentes soluções: não há motor "correto" a ser escolhido, desde que a justificativa relacione a escolha a uma característica concreta do próprio projeto ou do próprio interesse do grupo.

## Critérios de Sucesso

Cada grupo registrou por escrito a escolha de um motor adicional, a justificativa técnica dessa escolha e a comparação de pelo menos um sistema do Vertical Slice com a solução equivalente nesse motor, além de uma estrutura preliminar da Apresentação Técnica Final associando cada tópico a evidências concretas do semestre.

## Evidências para Avaliação

O registro do desafio e a estrutura preliminar da apresentação constituem o Checkpoint de preparação da apresentação técnica final previsto no Cronograma, avaliado pela Rubrica 6 (justificativa técnica de decisões) e pela Rubrica 7 (arquitetura e consistência do Vertical Slice, em sua dimensão de capacidade de explicar decisões), preparando diretamente a Apresentação Técnica Final e o encerramento da disciplina na Semana 17.

## Dificuldades Esperadas

Grupos podem tentar comparar superficialmente com os quatro motores ao mesmo tempo, diluindo a análise — o professor deve exigir a escolha de apenas um motor, reforçando que profundidade em uma comparação vale mais do que superficialidade em quatro. Também é comum que a estruturação da apresentação fique genérica demais ("vamos mostrar o projeto e comparar com Unity") — o professor deve exigir que cada tópico da estrutura preliminar já esteja associado a uma evidência nomeada do semestre (por exemplo, o quadro comparativo do Encontro 1, o registro de decisão da Semana 15, o build empacotado da Semana 14).

---

# Resultado Esperado da Semana

Ao final da Semana 16, cada grupo terá consolidado um quadro comparativo sistemático Unreal x Unity cobrindo todos os principais sistemas do Vertical Slice construído no semestre, terá escolhido e justificado tecnicamente um motor adicional (Godot, O3DE, Stride ou CryEngine) para aprofundar a comparação com o próprio projeto, e terá uma estrutura preliminar da Apresentação Técnica Final associada a evidências concretas produzidas ao longo do semestre. Nenhum sistema novo foi adicionado ao projeto: `BP_Player`, `BP_Enemy`, o framework de GameMode/GameState/PlayerController/GameInstance, os sistemas de interação, inventário, HUD, IA, combate, materiais, foliage, áudio e o build empacotado da Semana 14 permanecem intactos. O estudante domina, ao final da semana, a capacidade de comparar arquiteturas entre motores diferentes de forma sistemática e justificada, encerrando a Unidade V e chegando pronto para a defesa final do Vertical Slice.

# Preparação para a Próxima Semana

A Semana 17 encerra a disciplina com a Apresentação Técnica Final: cada grupo apresenta o Vertical Slice completo, suas decisões arquiteturais e a comparação entre motores construída nas Semanas 15 e 16. O quadro comparativo consolidado no Encontro 1 e a estrutura preliminar da apresentação esboçada no Encontro 2 desta semana são os insumos diretos da apresentação final — nenhum dos dois deve ser descartado ou refeito do zero; a Semana 17 refina o que já foi produzido, não recomeça o trabalho.

# Referências

- Epic Games — Unreal Engine Documentation, Gameplay Framework, Enhanced Input, Blueprints, Animation, Behavior Trees, UMG, Materials.
- Unity Technologies — Unity Manual (https://docs.unity3d.com/Manual/) e Unity Learn (https://learn.unity.com/), para confirmação terminológica durante a consolidação do quadro comparativo.
- Godot Engine — Godot Documentation (https://docs.godotengine.org/), consultada de forma pontual e comparativa.
- Documentação oficial pública de O3DE, Stride e CryEngine, consultada de forma pontual e comparativa, conforme previsto no Cronograma para esta semana.
- PROJECT_ARCHITECTURE.md (seções 7 e 12) como referência de consistência para a consolidação do quadro comparativo.

Vídeos, quando necessários como apoio complementar (nunca como fonte principal): canal oficial Unreal Engine.
