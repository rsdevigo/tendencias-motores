# Semana 5 — Contrato Interactable e Signals

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7) | **Metodologia:** Studio Based Learning — professor demonstra, aluno adapta. Autonomia baixa.

## Introdução da Semana

A Semana 4 encerrou com dois Autoloads funcionais — `GameManager` e `SaveManager` — sustentando estado de partida e persistência entre cenas. Esta semana mantém o projeto intacto e resolve um problema diferente: como um objeto do mundo (uma porta, uma alavanca) comunica ao Player que pode ser acionado, e como reage a esse acionamento, sem que Player e objeto precisem se conhecer diretamente. A resposta é o contrato `Interactable`, complementado por Signals — o par que vai sustentar todo objeto interativo do Vertical Slice até a Semana 17, incluindo a ampliação prevista para a Semana 10.

## Objetivos Gerais

- Compreender o contrato `Interactable` como mecanismo de comunicação desacoplada entre Player e objetos do mundo.
- Compreender Signals como padrão observer para reação a eventos de interação.
- Implementar um objeto interativo concreto (porta ou equivalente) usando contrato Interactable + Signal.

## Resultados Esperados

Ao final da semana, cada estudante possui, além do `GameManager` e `SaveManager` herdados da Semana 4, um contrato `Interactable` implementado por ao menos uma Scene do Vertical Slice, com um Signal disparado por interação e conectado a uma reação concreta.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o contrato `Interactable` como mecanismo de comunicação desacoplada entre sistemas.
- Diferenciar comunicação por contrato de comunicação por referência direta (`get_node`).
- Criar um contrato `Interactable` genérico e implementá-lo em uma Scene do Vertical Slice.

## Conteúdos

- O problema da comunicação acoplada entre sistemas que não deveriam se conhecer.
- Contrato `Interactable` via duck typing/`has_method("interact")` em GDScript, ou nó de interface do Orchestrator.
- Criação guiada de uma Scene que implementa o contrato.

## Conceitos Fundamentais

Toda engine de jogos com múltiplos sistemas independentes precisa resolver o mesmo problema: como um sistema chama outro sem depender do tipo concreto dele. Se o `InteractionComponent` do Player precisasse conhecer explicitamente a classe `Door`, `Lever`, `Chest` e cada novo objeto interativo criado depois, cada adição exigiria alterar o Player — um acoplamento que não escala. O contrato `Interactable` resolve isso definindo apenas um comportamento esperado (responder a `interact()`), sem exigir uma hierarquia de herança comum entre os objetos que o implementam. O Godot expressa esse contrato via duck typing — checando `has_method("interact")` em tempo de execução — ou, no Orchestrator, por um nó de interface dedicado, sem precisar de uma linguagem de interfaces formal como a Unity/C# usa.

## Recursos do Godot

Contrato Interactable, GDScript (`has_method`), Orchestrator (nó de interface), Area3D (detecção de proximidade).

## Comparação com Unity

A Unity resolve o mesmo problema com `interface` formal de C# (`IInteractable`), implementada por qualquer `MonoBehaviour` que declare os métodos exigidos — uma checagem de tipo em tempo de compilação. O Godot, ao usar duck typing via `has_method`, faz a mesma checagem em tempo de execução: mais flexível (qualquer Node pode implementar o contrato sem declarar formalmente que o faz) mas sem a garantia do compilador de que o método existe antes de rodar. Vale destacar essa diferença à turma sem transformar isso em uma aula de C#: o conceito universal — contrato de comportamento sem herança compartilhada — é o mesmo nas duas engines, muda apenas o momento em que o contrato é verificado.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 4, com `GameManager` e `SaveManager` já registrados como Autoload.
- Script de referência do contrato `Interactable` e de uma Scene de exemplo (`Door.tscn`) já preparados para demonstração (não distribuídos antes da aula).
- Slides com o comparativo contrato via duck typing (Godot) × `IInteractable` (Unity/C#).
- Área de teste no nível existente com espaço para posicionar um objeto interativo.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 4 (`GameManager` e `SaveManager` como Autoload) |
| 20 min | Introdução: o problema da comunicação acoplada entre sistemas |
| 35 min | Demonstração: criação do contrato `Interactable` e implementação em uma Scene (`Door.tscn`) |
| 45 min | Laboratório: cada estudante cria seu próprio contrato e implementa uma Scene interativa no Vertical Slice |
| 15 min | Desafio: adaptar a reação da Scene interativa para um comportamento próprio |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro retoma o projeto herdado da Semana 4 sem alterar `GameManager` ou `SaveManager`, adicionando um novo tipo de comunicação ao Vertical Slice. O professor demonstra a definição do contrato `Interactable` (via `has_method("interact")` ou nó de interface do Orchestrator) e sua implementação em uma Scene concreta — uma porta que reage ao ser interagida. A turma replica a criação do contrato e implementa sua própria Scene interativa, preparando o terreno para a conexão via Signal no Encontro 2.

## Desafio

Cada estudante adapta a reação da própria Scene interativa a um comportamento não demonstrado em aula (por exemplo, alternar entre dois estados visuais, ou emitir uma mensagem de depuração própria), mantendo o contrato `Interactable` como ponto de entrada.

## Critérios de Sucesso

Cada estudante possui, ao final do encontro, um contrato `Interactable` definido e implementado por ao menos uma Scene do Vertical Slice, respondendo corretamente a uma chamada de `interact()`.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro. O contrato `Interactable` construído aqui é pré-requisito direto do desafio avaliado (Rubrica 2) do Encontro 2 e do Checkpoint de progresso da Semana 6.

## Dificuldades Esperadas

- Implementar a reação da Scene diretamente no corpo do contrato em vez de na Scene concreta — reforçar que o contrato apenas define o método esperado; a lógica de reação pertence a cada Scene que o implementa.
- Usar `get_node`/referência direta para chamar a Scene interativa a partir do Player em vez de checar o contrato via `has_method` — reforçar que isso reintroduz o acoplamento que o contrato existe para evitar.
- Esquecer de testar a chamada de `interact()` a partir de uma segunda Scene interativa diferente da demonstrada — orientar teste com pelo menos duas instâncias antes de encerrar a etapa.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Signals como padrão observer para reação a eventos de interação.
- Diferenciar chamada direta de método de emissão de Signal.
- Implementar um Signal disparado por interação e conectá-lo a uma reação concreta em uma Scene do grupo.

## Conteúdos

- Signals como padrão observer: emissor não conhece quem reage ao evento.
- Conexão de um Signal de interação a uma função de reação.
- Desafio: objeto interativo próprio (porta ou equivalente) usando contrato Interactable + Signal.

## Conceitos Fundamentais

O contrato `Interactable` resolve "como um objeto responde a uma chamada"; Signals resolvem um problema complementar: "como um objeto avisa que algo aconteceu, sem saber quem está ouvinte". Esse é o padrão observer, presente em praticamente toda engine de jogos moderna. No Godot, um Signal é declarado na Scene emissora e conectado — via editor ou código — a uma ou mais funções de reação em outras Scenes, sem que o emissor precise conhecer o receptor. Combinado ao contrato `Interactable`, isso permite que um objeto interativo dispare uma reação (abrir uma porta, acionar uma alavanca) sem acoplamento direto entre a lógica de interação e a lógica de reação — a mesma separação que sustentará a ampliação da interação conectada ao Inventário na Semana 10.

## Recursos do Godot

Signals, contrato Interactable, Área de detecção (Area3D/RayCast3D), GDScript/Orchestrator.

## Comparação com Unity

A Unity resolve o mesmo padrão observer com `UnityEvent` (configurável pelo Inspector, semelhante à conexão de Signal pelo editor do Godot) ou com `event`/`Action` de C# (mais próximo da conexão via código). A diferença arquitetural relevante para a turma não é a sintaxe, mas o fato de o Godot tratar Signals como um mecanismo de primeira classe do editor — declarado, listado e conectado visualmente em qualquer Node — enquanto na Unity o mesmo resultado depende de qual das duas abordagens (`UnityEvent` ou `event`/`Action`) a equipe escolheu adotar como convenção própria.

## Preparação do Professor

- Projeto de demonstração com o contrato `Interactable` do Encontro 1 já implementado em uma Scene.
- Script de referência de um Signal de interação e sua conexão a uma função de reação já preparados para demonstração.
- Slides com o comparativo Signal (Godot) × `UnityEvent`/`event`/`Action` (Unity).
- Área de teste no nível existente com espaço para pelo menos dois objetos interativos distintos (ex.: porta e alavanca).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 1 (contrato `Interactable` implementado em uma Scene) |
| 20 min | Introdução: Signals como padrão observer e o problema de avisar sem conhecer quem escuta |
| 35 min | Demonstração: declaração de um Signal de interação e conexão a uma função de reação |
| 50 min | Laboratório e Desafio: cada grupo implementa seu objeto interativo (porta ou equivalente) usando contrato Interactable + Signal, com liberdade de acionamento (alavanca, chave, proximidade) |
| 20 min | Feedback formal sobre as soluções de interação apresentadas pelos grupos |

## Desenvolvimento

O encontro completa a semana conectando o contrato `Interactable` do Encontro 1 a um Signal disparado pela interação. O professor demonstra a declaração do Signal na Scene interativa e sua conexão a uma função de reação (por exemplo, abrir a porta ao ser acionada). Em seguida, cada grupo implementa seu próprio objeto interativo — porta ou equivalente escolhido pelo grupo — combinando contrato `Interactable` e Signal, com liberdade para definir o mecanismo de acionamento (alavanca, chave, proximidade). O encontro fecha com Feedback formal sobre as soluções apresentadas, avaliado pela Rubrica 2 (Desafios Técnicos).

## Desafio

Cada grupo implementa um objeto interativo (porta ou equivalente escolhido pelo grupo) usando contrato Interactable + Signal, permitindo diferentes soluções de acionamento (alavanca, chave, proximidade). **Entrega: Feedback formal** sobre as soluções apresentadas.

## Critérios de Sucesso

Cada grupo possui, ao final da semana, pelo menos um objeto interativo funcional no Vertical Slice, implementando o contrato `Interactable`, disparando um Signal próprio na interação e reagindo a esse Signal com um comportamento visível.

## Evidências para Avaliação

Feedback formal sobre as soluções de interação apresentadas pelos grupos, avaliado pela Rubrica 2 — Desafios Técnicos (Solução proposta, Uso correto do Godot, Criatividade, Organização, Funcionamento). O contrato `Interactable` e os Signals aqui construídos também compõem a base avaliada no Checkpoint de progresso da Semana 6 e no Code Review de encerramento do Módulo 2 (Semana 7).

## Dificuldades Esperadas

- Chamar a função de reação diretamente em vez de emitir o Signal, reintroduzindo acoplamento entre interação e reação — reforçar que o Signal deve mediar a chamada, não substituí-la por uma chamada direta disfarçada.
- Conectar o Signal apenas pelo editor sem entender a conexão equivalente em código, dificultando reuso em objetos criados dinamicamente — mostrar brevemente a conexão via código como alternativa.
- Confundir o papel do Signal (avisar que a interação ocorreu) com o papel do contrato Interactable (responder à chamada de interação) — reforçar que os dois mecanismos são complementares, não substitutos um do outro.

---

# Resultado Esperado da Semana

Ao final da Semana 5, cada estudante possui, sobre o projeto herdado da Semana 4, um contrato `Interactable` implementado por ao menos uma Scene do Vertical Slice e um Signal de interação conectado a uma reação concreta — cada grupo com seu próprio objeto interativo (porta, alavanca ou equivalente) e mecanismo de acionamento. A turma domina o contrato `Interactable` como mecanismo de comunicação desacoplada e Signals como padrão observer, relaciona os dois ao equivalente da Unity (`IInteractable` e `UnityEvent`/`event`/`Action`), e recebeu Feedback formal sobre as soluções de interação apresentadas.

# Preparação para a Próxima Semana

O contrato `Interactable` e os Signals construídos nesta semana são pré-requisito direto da Semana 6, que introduz `ItemData` (Resource customizado) e Enums para separar dados de design da lógica de gameplay — os itens coletáveis modelados na Semana 6 poderão, por exemplo, ser associados a objetos interativos (baús) que já implementam o contrato desta semana. O par Interactable/Signal também será retomado e ampliado na Semana 10, quando a interação passar a se conectar ao Inventário.

# Referências

- Godot Documentation — Signals: https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html
- Godot Documentation — GDScript (métodos, `has_method`): https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/index.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — Events: https://docs.unity3d.com/Manual/UnityEvents.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
