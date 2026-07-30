# Semana 4

## Introdução da Semana

A Semana 4 abre a Unidade II — Construir Sistemas — e muda o regime de trabalho da turma: até aqui (Semanas 1–3), o Vertical Slice era um protótipo navegável, com locomoção, input e um primeiro build empacotado. A partir de agora, a metodologia passa de Scaffolded Learning para Studio Based Learning — o professor ainda demonstra, mas o aluno adapta em vez de apenas replicar, e a autonomia sobe de "muito baixa" para "baixa". O eixo desta semana é o Gameplay Framework: a estrutura que toda engine precisa para separar regras de partida, estado compartilhado, a ponte entre jogador e personagem, e persistência entre níveis. O Encontro 1 constrói GameMode e GameState; o Encontro 2 constrói PlayerController e GameInstance, fechando a semana com o primeiro desafio de liberdade de solução da disciplina.

## Objetivos Gerais

- Compreender o Gameplay Framework como conjunto de papéis universais que toda engine de jogos precisa resolver, independentemente de como cada uma os nomeia ou estrutura.
- Diferenciar GameMode (regras da partida) de GameState (estado compartilhado) como duas responsabilidades distintas, ainda que frequentemente confundidas por quem vem de engines sem essa separação nativa.
- Diferenciar PlayerController (ponte jogador–Pawn) de GameInstance (persistência entre níveis) como dois problemas de ciclo de vida também distintos entre si.
- Implementar BP_GameMode, BP_GameState, BP_PlayerController e BP_GameInstance customizados no Vertical Slice, com uma variável persistente funcional armazenada no GameInstance.

## Resultados Esperados

Ao final da semana, cada grupo terá o Vertical Slice operando sobre um Gameplay Framework próprio — BP_GameMode, BP_GameState, BP_PlayerController e BP_GameInstance customizados, substituindo as classes padrão da engine — com uma variável definida pelo próprio grupo persistindo corretamente entre a troca de níveis. O nível de teste e o BP_Player continuam os mesmos desde a Semana 1; o que muda é a camada de organização por trás deles, agora visível e sob controle do grupo.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar GameMode e GameState como dois papéis universais e distintos do Gameplay Framework.
- Comparar a ausência de um equivalente direto a GameMode/GameState na Unity com o padrão de Managers/Singletons usado para resolver o mesmo problema.
- Criar BP_GameMode e BP_GameState customizados e atribuí-los ao nível de teste do Vertical Slice.

## Conteúdos

- GameMode: regras da partida.
- GameState: estado compartilhado.
- Atribuição de GameMode/GameState customizados ao nível de teste.

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre regra de partida e estado de partida. Toda engine de jogos multiplayer-ready ou mesmo single-player estruturada precisa responder a duas perguntas distintas: quem decide como a partida começa, termina e é vencida (regra) e o que qualquer sistema do jogo — UI, IA, outro jogador — precisa consultar sobre o estado atual dessa partida (estado). A Unreal resolve isso com duas classes nativas: GameMode, que existe apenas no servidor e concentra a lógica autoritativa de regras, e GameState, que replica para todos os clientes o retrato do estado compartilhado dessa partida. É importante que a turma entenda que essa separação existe mesmo em um projeto single-player como o Vertical Slice desta disciplina — a Unreal formaliza esse papel como arquitetura nativa da engine, independentemente de haver múltiplos jogadores conectados.

## Recursos da Unreal

GameMode, GameState, nível de teste do Vertical Slice, Project Settings (Maps & Modes).

## Comparação com Unity

A Unity não possui uma classe equivalente nativa a GameMode ou GameState: o mesmo problema — centralizar regras de partida e expor estado compartilhado — é resolvido por convenção do próprio time, tipicamente com um GameManager implementado como singleton (MonoBehaviour com instância estática) ou, em projetos mais recentes, com um ScriptableObject de estado compartilhado. A diferença arquitetural relevante não é de capacidade, mas de formalização: a Unreal impõe um lugar único e nomeado para essas responsabilidades desde o primeiro projeto criado, enquanto na Unity essa organização depende inteiramente da disciplina da equipe. Não aprofundar mais que isso nesta semana — a comparação arquitetural mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o build da Semana 3 (Nanite/Lumen ativos, nível de teste consolidado) aberto.
- Um BP_GameMode e um BP_GameState de exemplo pré-configurados (fora da visão da turma), com uma variável simples de estado exposta em cada um, como referência de demonstração.
- Project Settings do projeto de demonstração aberto na aba Maps & Modes, pronto para mostrar onde o GameMode é atribuído ao nível.
- Slides com o diagrama Regra da partida (GameMode) × Estado compartilhado (GameState), e a distinção servidor/replicação em termos simples, sem aprofundar Networking (fora do escopo da disciplina).
- PROJECT_ARCHITECTURE.md disponível para reforçar a convenção `BP_` e a subpasta `Framework/`.

## Cronograma do Encontro

- 15 min — Revisão do build da Semana 3 e abertura da Unidade II.
- 20 min — Fundamentação: GameMode e GameState como papéis universais do Gameplay Framework.
- 35 min — Demonstração: criação guiada de BP_GameMode e BP_GameState customizados, atribuição ao nível de teste via Project Settings.
- 50 min — Laboratório: cada grupo cria seu próprio BP_GameMode/BP_GameState e os atribui ao nível de teste.
- 15 min — Feedback: verificação da atribuição correta e da nomenclatura de cada grupo.

## Desenvolvimento

O encontro parte do nível de teste consolidado na Semana 3 e demonstra por que um jogo — mesmo simples — se beneficia de um ponto único de regras e de um ponto único de estado compartilhado, em vez de espalhar essa lógica dentro do próprio BP_Player. O professor cria, ao vivo, um BP_GameMode customizado (herdando de Game Mode Base) e um BP_GameState customizado (herdando de Game State Base), atribui o GameState ao GameMode e o GameMode ao nível de teste via Project Settings > Maps & Modes, e adiciona uma variável simples de exemplo a cada classe para tornar a separação de responsabilidades concreta. Cada grupo replica o processo no próprio projeto, adaptando os nomes das classes e de uma variável própria à convenção `BP_` da pasta `Framework/`.

## Desafio

Não há desafio de liberdade de solução neste encontro — a criação e atribuição de GameMode/GameState é demonstração e adaptação guiada, coerente com a transição inicial para Studio Based Learning. O desafio da semana concentra-se no Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um BP_GameMode e um BP_GameState customizados, corretamente atribuídos ao nível de teste do Vertical Slice, com nomenclatura conforme a convenção `BP_` do PROJECT_ARCHITECTURE.md e localizados na subpasta `Framework/`.

## Evidências para Avaliação

Organização e nomenclatura de BP_GameMode/BP_GameState conforme PROJECT_ARCHITECTURE.md, e atribuição correta ao nível (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Preparação).

## Dificuldades Esperadas

Estudantes podem esquecer de atribuir o GameMode customizado ao nível (mantendo o padrão da engine ativo sem perceber), ou colocar no GameMode uma variável que deveria estar no GameState (e vice-versa). Intervenção: verificar Project Settings > Maps & Modes de cada grupo durante o laboratório antes do fim do encontro; ao identificar variável no lugar errado, reforçar verbalmente o critério "isso precisa ser consultado por outros sistemas?" — se sim, é GameState; se é regra de decisão da partida, é GameMode.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar PlayerController como a ponte entre o jogador e o Pawn, e GameInstance como o objeto persistente entre níveis.
- Comparar PlayerController e GameInstance com os padrões equivalentes da Unity.
- Implementar uma variável persistente no GameInstance, funcional entre a troca de níveis.

## Conteúdos

- PlayerController: ponte entre jogador e Pawn.
- GameInstance: persistência entre níveis.
- Implementação de uma variável persistente no GameInstance.
- Desafio: definição livre de um dado próprio a persistir.

## Conceitos Fundamentais

O conceito universal desta aula também tem duas partes. A primeira é a separação entre jogador e personagem: PlayerController representa a intenção e a identidade do jogador (input de alto nível, câmera, sessão), enquanto o Pawn/Character é apenas o corpo que ele possui e pode trocar ou perder sem perder a si mesmo — problema que toda engine com possessão de personagem precisa resolver. A segunda é o problema da persistência entre níveis: por padrão, a maioria dos objetos de gameplay é destruída na troca de nível, e toda engine precisa de algum mecanismo que sobreviva a essa transição para guardar dados que não pertencem a nenhum nível específico (progresso, pontuação, configurações). A Unreal resolve isso com o GameInstance, uma única instância que existe durante toda a execução do jogo, do lançamento ao fechamento.

## Recursos da Unreal

PlayerController, GameInstance, nível de teste do Vertical Slice, Project Settings (Maps & Modes).

## Comparação com Unity

O PlayerController da Unreal corresponde, em intenção, ao script de input/câmera atrelado ao GameObject do jogador na Unity — mas a Unity não separa nativamente "quem possui" de "o que é possuído": normalmente o mesmo GameObject concentra corpo e controle, e a separação, quando existe, é uma decisão de arquitetura do time. O GameInstance corresponde ao padrão DontDestroyOnLoad aplicado a um GameObject singleton na Unity (ou a um ScriptableObject persistente): ambos resolvem o mesmo problema de sobreviver à troca de cena/nível, mas a Unreal oferece uma classe dedicada e única para esse papel, enquanto a Unity depende de uma convenção manual do desenvolvedor para não recriar ou destruir esse objeto indevidamente. Não aprofundar mais que isso — o ponto é reconhecer a equivalência conceitual, não decorar diferenças de configuração.

## Preparação do Professor

- Projeto de cada grupo com BP_GameMode/BP_GameState do Encontro 1 prontos.
- Um BP_PlayerController e um BP_GameInstance de exemplo pré-configurados (fora da visão da turma), com uma variável persistente de demonstração (ex.: um contador simples) já funcional entre dois níveis de teste.
- Um segundo nível mínimo (pode ser um level vazio de teste) disponível no projeto de demonstração, apenas para provar a persistência do GameInstance na troca de nível.
- Slides com o diagrama Jogador (PlayerController) × Corpo (Pawn/Character), e Nível A → troca → Nível B → GameInstance permanece.
- Modelo de Feedback Formal (conforme Sistema de Avaliação) pronto para uso ao final do encontro, já que a Semana 5 prevê entrega de feedback formal e este encontro produz o primeiro desafio de solução aberta da disciplina.
- PROJECT_ARCHITECTURE.md disponível para reforçar a convenção `BP_` e a subpasta `Framework/`.

## Cronograma do Encontro

- 15 min — Revisão do BP_GameMode/BP_GameState do Encontro 1.
- 20 min — Fundamentação: PlayerController como ponte jogador–Pawn, e GameInstance como persistência entre níveis.
- 35 min — Demonstração: criação guiada de BP_PlayerController e BP_GameInstance, implementação de uma variável persistente de exemplo, verificada em dois níveis.
- 40 min — Laboratório: cada grupo cria seu BP_PlayerController/BP_GameInstance e implementa uma variável persistente própria.
- 25 min — Desafio + Feedback: cada grupo apresenta o dado escolhido e demonstra sua persistência entre níveis; feedback direto do professor.

## Desenvolvimento

O encontro continua diretamente do Gameplay Framework iniciado no Encontro 1: agora que o nível de teste tem regras (GameMode) e estado (GameState) próprios, falta a ponte entre o jogador humano e o BP_Player que ele controla, e um lugar que sobreviva à troca de nível. O professor cria um BP_PlayerController customizado, atribui-o ao GameMode, e demonstra que ele permanece o mesmo objeto mesmo que o Pawn possuído mude. Em seguida, cria um BP_GameInstance customizado, atribui-o nas Project Settings, adiciona uma variável simples (ex.: um contador) e prova, ao trocar de nível no projeto de demonstração, que o valor permanece. Cada grupo replica os dois processos e, na sequência, assume o desafio da semana.

## Desafio

Cada grupo define e implementa um dado próprio que deve persistir entre níveis — pontuação, item coletado, ou estado de progresso —, com liberdade total de escolha sobre qual dado e como ele é atualizado, desde que a persistência via GameInstance seja demonstrável na troca entre o nível de teste e um segundo nível (pode ser um level mínimo criado apenas para o teste). Este é o primeiro desafio de solução aberta da disciplina, coerente com o início da transição para Studio Based Learning.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir BP_PlayerController e BP_GameInstance customizados corretamente atribuídos, com uma variável definida pelo próprio grupo persistindo de forma verificável entre dois níveis distintos.

## Evidências para Avaliação

Demonstração funcional da persistência do dado escolhido entre níveis, e clareza da justificativa do grupo sobre por que aquele dado pertence ao GameInstance (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Autonomia). O desafio desta semana antecipa o formato de feedback direto que se torna instrumento formal na Semana 5.

## Dificuldades Esperadas

Estudantes podem tentar guardar no GameInstance um dado que deveria estar no GameState (por exemplo, algo que só faz sentido dentro de uma única partida/nível), confundindo os dois papéis construídos nos dois encontros da semana. Intervenção: retomar o critério "esse dado precisa sobreviver à troca de nível, ou só precisa ser compartilhado dentro do nível atual?" — se for o primeiro, GameInstance; se for o segundo, GameState, já construído no Encontro 1. Grupos que não conseguirem demonstrar a persistência a tempo devem registrar o estado do Blueprint (variável criada, mas não testada em dois níveis) como pendência, sem bloquear o andamento da Semana 5.

---

# Resultado Esperado da Semana

Ao final da Semana 4, cada grupo deve possuir um Vertical Slice operando sobre um Gameplay Framework próprio: BP_GameMode e BP_GameState customizados organizando regras e estado do nível de teste, e BP_PlayerController e BP_GameInstance customizados fazendo a ponte com o jogador e garantindo persistência de um dado escolhido pelo grupo entre níveis. Conceitualmente, a turma deve dominar a distinção entre regra de partida e estado compartilhado, entre jogador e corpo possuído, e entre o que pertence a um nível e o que sobrevive a todos eles — quatro papéis universais do Gameplay Framework, cobertos por quatro classes nativas da Unreal sem equivalente direto formalizado na Unity.

# Preparação para a Próxima Semana

A Semana 5 depende do Gameplay Framework consolidado nesta semana como base para introduzir comunicação desacoplada entre sistemas: Blueprint Interfaces e Event Dispatchers serão usados para que um objeto interativo do nível (porta ou equivalente) comunique sua ativação sem depender diretamente do BP_Player, prática que se apoiará no BP_PlayerController já existente como ponto de entrada de input de alto nível (ex.: interagir). A distinção entre conceito universal e implementação específica, já exercitada nas Semanas 1–4, será retomada ao comparar Blueprint Interfaces com Interfaces em C# na Unity.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Gameplay Framework in Unreal Engine. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução ao Gameplay Framework (GameMode, GameState, PlayerController, GameInstance). Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — GameObject, MonoBehaviour, e o padrão DontDestroyOnLoad, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Gameplay Framework; **Mathew Wadstein**, para explicações pontuais de GameMode/GameState/PlayerController/GameInstance.
