# Semana 5

## Introdução da Semana

A Semana 5 dá continuidade à Unidade II — Construir Sistemas — sobre o Gameplay Framework consolidado na Semana 4 (BP_GameMode, BP_GameState, BP_PlayerController, BP_GameInstance). A metodologia permanece Studio Based Learning, com autonomia baixa, mas em ritmo crescente: a Semana 4 já produziu o primeiro desafio de solução aberta da disciplina, e esta semana amplia esse formato. O eixo é a comunicação desacoplada entre sistemas: como um objeto do mundo pode reagir a uma ação do jogador — e como o jogador pode ser avisado dessa reação — sem que Player e objeto conheçam os detalhes internos um do outro. O Encontro 1 constrói a Blueprint Interface `BPI_Interactable` como contrato genérico de interação; o Encontro 2 constrói o Event Dispatcher que reage à ativação, aplicando os dois recursos a um objeto interativo concreto (porta ou equivalente escolhido pelo grupo). A semana fecha com **Feedback Formal**, primeiro instrumento avaliativo desse tipo na disciplina.

## Objetivos Gerais

- Compreender a comunicação desacoplada entre sistemas como problema universal de arquitetura de jogos: como dois objetos interagem sem que um dependa da implementação interna do outro.
- Diferenciar Blueprint Interface (contrato de comunicação) de Event Dispatcher (notificação de evento) como duas ferramentas complementares, não intercambiáveis, para o mesmo problema.
- Implementar `BPI_Interactable` e conectá-la ao `InteractionComponent` de `BP_Player`, definido em PROJECT_ARCHITECTURE.md.
- Implementar um Event Dispatcher acionado por interação e aplicá-lo a um objeto interativo concreto do Vertical Slice (porta ou equivalente escolhido pelo grupo), com liberdade sobre o mecanismo de acionamento.

## Resultados Esperados

Ao final da semana, cada grupo terá um objeto interativo funcional no Vertical Slice — implementando `BPI_Interactable` e reagindo via Event Dispatcher a uma ação do jogador — com o mecanismo de acionamento (alavanca, chave, proximidade ou outro) definido pelo próprio grupo. O Gameplay Framework da Semana 4 permanece intacto e passa a hospedar o primeiro caso de comunicação desacoplada do projeto.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar Blueprint Interfaces como mecanismo de comunicação desacoplada entre Actors que não precisam se conhecer diretamente.
- Comparar Blueprint Interfaces com Interfaces em C# na Unity.
- Criar a interface `BPI_Interactable` e implementá-la em um Actor do nível de teste.

## Conteúdos

- Blueprint Interfaces: contrato de comunicação sem dependência direta de classe.
- Criação de `BPI_Interactable` conforme convenção `BPI_` de PROJECT_ARCHITECTURE.md.
- Implementação da interface em um Actor interativo genérico.

## Conceitos Fundamentais

O conceito universal desta aula é o desacoplamento por contrato. Sempre que um sistema (o Player, via `InteractionComponent`) precisa agir sobre outro sistema (um objeto do mundo) sem conhecer sua implementação específica — pois o mesmo Player deve poder interagir com uma porta, uma alavanca ou um baú de formas completamente diferentes internamente —, toda engine precisa de um mecanismo que garanta apenas que o alvo "responde a uma chamada esperada", sem exigir que o chamador saiba como. A Unreal resolve isso com Blueprint Interfaces: uma interface declara funções sem implementação, e qualquer Actor pode implementá-la, sendo chamado de forma genérica por quem só conhece o contrato — nunca a classe concreta. Isso é o que permite ao `InteractionComponent` de `BP_Player` (PROJECT_ARCHITECTURE.md, seção 7) chamar "interaja" em qualquer Actor próximo, sem um bloco de decisão por tipo de objeto.

## Recursos da Unreal

Blueprint Interfaces, `InteractionComponent` (já referenciado em PROJECT_ARCHITECTURE.md), nível de teste do Vertical Slice.

## Comparação com Unity

Interfaces em C# resolvem o mesmo problema de contrato sem herança de implementação, e o princípio é idêntico: definir o que um objeto deve responder, não como. A diferença arquitetural está na camada de execução — Blueprint Interfaces funcionam nativamente em visual scripting e podem ser chamadas mesmo quando o chamador não tem referência de classe concreta ao alvo (Call Function on Interface), enquanto na Unity o mesmo padrão exige C# e, tipicamente, `GetComponent<IInteragivel>()` para obter a referência tipada pela interface. Não aprofundar mais que isso — a comparação arquitetural mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o Gameplay Framework da Semana 4 (BP_GameMode, BP_GameState, BP_PlayerController, BP_GameInstance) funcional.
- Uma `BPI_Interactable` de exemplo pré-configurada (fora da visão da turma), com uma função de interação simples, implementada em um Actor de demonstração.
- Slides com o diagrama Contrato (Interface) × Implementação concreta (Actor), reforçando que a interface nunca é instanciável por si só.
- PROJECT_ARCHITECTURE.md disponível para reforçar a convenção `BPI_` e a subpasta `Interactables/`.
- Nível de teste com ao menos um Actor candidato a se tornar o objeto interativo do desafio do Encontro 2 (porta, alavanca ou equivalente já modelado no ambiente).

## Cronograma do Encontro

- 15 min — Revisão do Gameplay Framework da Semana 4.
- 20 min — Fundamentação: Blueprint Interfaces como contrato de comunicação desacoplada.
- 35 min — Demonstração: criação guiada de `BPI_Interactable` e implementação em um Actor de exemplo.
- 50 min — Laboratório: cada grupo cria `BPI_Interactable` e a implementa em um Actor próprio do nível de teste.
- 15 min — Feedback: verificação da implementação da interface e da nomenclatura de cada grupo.

## Desenvolvimento

O encontro parte do `InteractionComponent` já previsto na arquitetura do projeto (PROJECT_ARCHITECTURE.md, seção 7) e demonstra por que esse Component não pode conhecer, um a um, todos os tipos de objeto interativo que o Vertical Slice vai acumular ao longo do semestre. O professor cria, ao vivo, a interface `BPI_Interactable` com uma função de interação simples (ex.: `Interact`), implementa essa interface em um Actor de demonstração e mostra a chamada genérica da função via interface a partir de um Blueprint que não conhece a classe concreta do Actor. Cada grupo replica o processo, criando `BPI_Interactable` na subpasta `Interactables/` e implementando-a em um Actor já existente ou recém-criado no próprio nível de teste, preparando a base para o objeto interativo que será desenvolvido no Encontro 2.

## Desafio

Não há desafio de liberdade de solução neste encontro — a criação e implementação da interface é demonstração e adaptação guiada, preparando a base técnica para o desafio do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir `BPI_Interactable` criada e implementada em ao menos um Actor do nível de teste, com nomenclatura conforme a convenção `BPI_` do PROJECT_ARCHITECTURE.md e localizada na subpasta `Interactables/`.

## Evidências para Avaliação

Organização e nomenclatura de `BPI_Interactable` conforme PROJECT_ARCHITECTURE.md, e implementação correta da interface no Actor escolhido (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Preparação).

## Dificuldades Esperadas

Estudantes podem confundir "implementar uma interface" com "herdar de uma classe", tentando duplicar lógica em vez de apenas prover a função exigida pelo contrato. Intervenção: reforçar verbalmente que a interface não carrega implementação nem estado — apenas declara o que deve existir; a lógica pertence inteiramente ao Actor que a implementa. Grupos que não identificarem um Actor candidato no próprio nível devem receber sugestão direta do professor para não atrasar o Encontro 2.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Event Dispatchers como padrão observer para notificação de eventos entre sistemas.
- Comparar Event Dispatchers com UnityEvent/C# Actions.
- Implementar um Event Dispatcher acionado por interação e aplicá-lo a um objeto interativo concreto do Vertical Slice.

## Conteúdos

- Event Dispatchers: padrão observer aplicado a eventos de gameplay.
- Implementação de um Event Dispatcher acionado pela interface `BPI_Interactable`.
- Desafio: objeto interativo (porta ou equivalente) com mecanismo de acionamento definido pelo grupo.

## Conceitos Fundamentais

O conceito universal desta aula complementa o do Encontro 1: se a interface resolve "quem pode ser chamado sem conhecer a classe concreta", o Event Dispatcher resolve o problema inverso — "quem precisa ser avisado quando algo acontece, sem que o emissor do evento precise conhecer os interessados". É o padrão observer: um objeto declara um evento (ex.: "fui ativado"), e qualquer outro sistema pode se inscrever para reagir, sem que o objeto que dispara o evento saiba quantos ou quais sistemas estão ouvindo. Isso é o que permite, por exemplo, que uma porta avise sua própria animação de abertura e, ao mesmo tempo, um sistema de áudio ou de missão, sem que a porta tenha uma lista fixa de "quem reagir".

## Recursos da Unreal

Event Dispatchers, `BPI_Interactable` (do Encontro 1), nível de teste do Vertical Slice.

## Comparação com Unity

UnityEvent e C# Actions (`Action`, `Action<T>`) resolvem o mesmo problema de notificação sem acoplamento direto: um objeto expõe um evento, outros se inscrevem via `AddListener` ou `+=`, e o emissor nunca precisa conhecer os inscritos. A diferença arquitetural relevante é de camada — Event Dispatchers são configuráveis visualmente no Blueprint Editor e podem ser conectados sem escrever código, enquanto UnityEvent exige exposição via Inspector ou código, e C# Actions exigem código puro. O princípio — observer, inversão de controle da notificação — é o mesmo nas duas engines. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `BPI_Interactable` do Encontro 1 implementada.
- Um Event Dispatcher de exemplo pré-configurado (fora da visão da turma), acionado pela chamada da interface e conectado a uma reação simples (ex.: mudança de cor ou movimento do Actor).
- Slides com o diagrama Emissor (Event Dispatcher) × Inscritos (Bind Event), reforçando que o emissor não conhece os inscritos.
- Modelo de Feedback Formal (conforme Sistema de Avaliação, Rubrica correspondente) pronto para uso ao final do encontro — este é o primeiro Feedback Formal da disciplina.
- PROJECT_ARCHITECTURE.md disponível para reforçar `BP_Door`/`BP_Lever` como Actors candidatos ao desafio, e a subpasta `Interactables/`.

## Cronograma do Encontro

- 10 min — Revisão da `BPI_Interactable` do Encontro 1.
- 15 min — Fundamentação: Event Dispatchers como padrão observer para eventos de interação.
- 35 min — Demonstração: criação guiada de um Event Dispatcher acionado pela interface, conectado a uma reação simples.
- 50 min — Laboratório: cada grupo implementa seu objeto interativo (porta ou equivalente) combinando `BPI_Interactable` e Event Dispatcher.
- 25 min — Desafio + Feedback Formal: cada grupo apresenta seu mecanismo de acionamento e recebe feedback formal registrado.

## Desenvolvimento

O encontro continua diretamente do Encontro 1: agora que existe um contrato de interação (`BPI_Interactable`), falta o mecanismo pelo qual o objeto ativado comunica sua própria reação a quem quiser ouvir. O professor cria um Event Dispatcher no Actor de demonstração, dispara esse evento a partir da função de interface implementada, e conecta (`Bind Event`) uma reação simples a esse evento, mostrando que o Actor que dispara o evento não precisa saber quem reage. Cada grupo aplica os dois recursos combinados — Interface + Event Dispatcher — a um objeto interativo concreto do próprio projeto, escolhendo livremente o mecanismo de acionamento (alavanca, chave ou proximidade), conforme o desafio da semana.

## Desafio

Cada grupo implementa um objeto interativo (porta ou equivalente escolhido pelo grupo) usando `BPI_Interactable` + Event Dispatcher, com liberdade sobre o mecanismo de acionamento — alavanca, chave, proximidade ou outra solução própria —, desde que o objeto reaja de forma demonstrável a uma ação do jogador via `InteractionComponent`.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um objeto interativo funcional no nível de teste, implementando `BPI_Interactable`, disparando um Event Dispatcher próprio ao ser ativado, e reagindo de forma visível e demonstrável à ação do jogador, com nomenclatura conforme PROJECT_ARCHITECTURE.md.

## Evidências para Avaliação

Funcionamento demonstrável do objeto interativo, clareza da justificativa do grupo sobre o mecanismo de acionamento escolhido, e organização/nomenclatura conforme PROJECT_ARCHITECTURE.md — registrados no instrumento de Feedback Formal da semana, conforme Sistema de Avaliação.

## Dificuldades Esperadas

Estudantes podem tentar chamar a reação diretamente da função de interface, sem passar pelo Event Dispatcher, resolvendo o desafio "por fora" do padrão ensinado. Intervenção: perguntar "e se outro sistema também precisasse reagir a essa ativação — a solução atual permitiria isso sem alterar o objeto?"; se a resposta for não, reforçar que a reação deve passar pelo Event Dispatcher, não por chamada direta. Grupos que não concluírem o mecanismo de acionamento a tempo devem registrar a interface implementada e o Event Dispatcher criado como pendência, sem bloquear o Feedback Formal — que pode avaliar o raciocínio da solução mesmo incompleta.

---

# Resultado Esperado da Semana

Ao final da Semana 5, cada grupo deve possuir um objeto interativo funcional integrado ao Vertical Slice: um Actor implementando `BPI_Interactable`, disparando um Event Dispatcher próprio ao ser ativado, e reagindo de forma visível a uma ação do jogador via `InteractionComponent`, com mecanismo de acionamento definido pelo grupo. Conceitualmente, a turma deve dominar a distinção entre contrato de comunicação (Interface) e notificação de evento (Event Dispatcher) como duas peças complementares — não substituíveis entre si — do mesmo problema de desacoplamento entre sistemas.

# Preparação para a Próxima Semana

A Semana 6 depende da interação desacoplada consolidada nesta semana como base para introduzir a separação entre dados de design e lógica de gameplay: Data Assets, Data Tables, Structs e Enums serão usados para modelar itens coletáveis (baús, moedas, recursos), reutilizando o mesmo par Interface + Event Dispatcher já implementado para que o ato de coletar um item também seja uma forma de interação. A distinção entre conceito universal e implementação específica, já exercitada nas Semanas 1–5, será retomada ao comparar Data Table/Data Asset com ScriptableObject na Unity.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Blueprints Visual Scripting in Unreal Engine. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Blueprint Interfaces e Event Dispatchers. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Interfaces em C# e UnityEvent, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Blueprint Interfaces e Event Dispatchers; **Mathew Wadstein**, para explicações pontuais de WTF Is? Interface e Event Dispatcher.
