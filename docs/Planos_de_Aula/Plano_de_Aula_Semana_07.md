# Semana 7 — Save/Load e consolidação do gameplay do Módulo 2

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7) | **Metodologia:** Studio Based Learning — professor demonstra, aluno adapta. Autonomia baixa. Encerramento de módulo.

## Introdução da Semana

A Semana 6 encerrou com `ItemData` + Enum sustentando um conjunto próprio de itens coletáveis em cada grupo, sobre o `GameManager`, `SaveManager`, contrato `Interactable` e Signals herdados das Semanas 4 e 5. Esta semana fecha a Unidade II em duas frentes complementares: primeiro resolve o problema que faltava — como o progresso do jogador sobrevive ao fechamento do jogo —, construindo `SaveData` (Resource) + FileAccess e o `Checkpoint`; depois integra, em um único fluxo jogável, todos os desafios construídos ao longo do módulo (portas, alavancas, baús, `Checkpoint`). A semana encerra a Unidade II com Code Review e Playtest coletivo, marco de encerramento do Módulo 2 no Cronograma.

## Objetivos Gerais

- Compreender serialização e recuperação de estado de jogo entre sessões como problema universal de qualquer engine.
- Construir `SaveData` (Resource) + FileAccess como mecanismo de persistência real (não apenas entre cenas, como o `SaveManager` da Semana 4).
- Construir `Checkpoint`, reutilizando o contrato `Interactable` e um `SaveComponent`.
- Integrar todos os sistemas do Módulo 2 (GameManager, SaveManager, Interactable, Signals, Resources, save/load) em um único fluxo jogável coerente.

## Resultados Esperados

Ao final da semana, cada grupo possui um Vertical Slice com progresso persistente real entre sessões de jogo — não apenas entre cenas —, com `Checkpoint`s funcionais integrados a portas, alavancas, baús e demais desafios do módulo em um único fluxo. A semana encerra com Code Review dos sistemas implementados e Playtest coletivo, fechando a Unidade II.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar serialização e recuperação de estado de jogo como problema universal de persistência.
- Diferenciar persistência entre cenas (SaveManager, Semana 4) de persistência entre sessões (SaveData + FileAccess).
- Construir `SaveData` (Resource) e um `SaveComponent`, e aplicá-los a um `Checkpoint` que reutiliza o contrato `Interactable`.

## Conteúdos

- O problema de perder todo o progresso ao fechar o jogo, mesmo com o `SaveManager` (Autoload) já mantendo estado entre cenas.
- `SaveData` como Resource customizado que agrega o estado a persistir (itens coletados, checkpoint ativo).
- FileAccess e `ResourceSaver`/`ResourceLoader` como mecanismo nativo de escrita/leitura em disco.
- `SaveComponent` como ponto único de leitura/escrita do `SaveData`, evitando lógica de serialização duplicada entre Scenes.
- `Checkpoint`: Scene que implementa o contrato `Interactable` e aciona o `SaveComponent` ao ser alcançada.

## Conceitos Fundamentais

O `SaveManager` construído na Semana 4 resolve um problema (estado sobrevive à troca de cena), mas não resolve outro: estado sobrevive ao fechamento do processo do jogo. Toda engine com sessões de jogo separadas no tempo — o jogador desliga e volta no dia seguinte — precisa de um mecanismo que transforme estado em memória em algo persistido em disco, e o processo inverso na abertura seguinte. O Godot resolve isso com Resources serializáveis (`ResourceSaver.save`/`ResourceLoader.load`) ou com FileAccess bruto (ex.: JSON), ambos gravando em `user://`, a pasta de dados do usuário isolada do próprio projeto. O `Checkpoint` aplica esse mecanismo a um caso concreto: um ponto do nível que, ao ser alcançado via o mesmo contrato `Interactable` já usado por portas e alavancas, aciona a gravação — reaproveitando desacoplamento, não recriando um sistema de interação próprio.

## Recursos do Godot

`SaveData` (Resource), FileAccess, `ResourceSaver`, `ResourceLoader`, pasta `user://`, `SaveComponent`, contrato `Interactable` (retomado da Semana 5).

## Comparação com Unity

A Unity não tem um equivalente formal único: o padrão mais comum é `PlayerPrefs` para dados simples (chave-valor) ou serialização própria em JSON/binário para dados estruturados, decisão que fica inteiramente a cargo da equipe. O Godot oferece um caminho nativo mais direto para dados estruturados — serializar o próprio `Resource` (`ResourceSaver`/`ResourceLoader`) sem exigir um formato intermediário — mas o FileAccess bruto (equivalente ao JSON manual da Unity) também está disponível quando o formato do arquivo salvo precisa ser legível fora do motor. O conceito universal — transformar estado em memória em dado persistido em disco, e reconstruí-lo na abertura seguinte — é idêntico nas duas engines; a diferença está em qual caminho é o "padrão de fábrica" de cada uma.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 6, com `ItemData` + Enum e um conjunto de itens coletáveis já modelado por grupo.
- Script de referência de `SaveData` (Resource com campos como itens coletados e último checkpoint) já preparado para demonstração.
- Script de referência de `SaveComponent` (métodos de salvar/carregar) e da Scene `Checkpoint` já preparados, sem distribuir antes da aula.
- Slides com o comparativo `SaveData`/FileAccess (Godot) × PlayerPrefs/JSON (Unity).
- Nível de teste com ao menos um ponto candidato a `Checkpoint` já identificado.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 6 (`ItemData` + Enum, Checkpoint de progresso do Módulo 2) |
| 20 min | Introdução: persistência entre cenas (SaveManager) versus persistência entre sessões (SaveData + FileAccess) |
| 40 min | Demonstração: construção de `SaveData`, `SaveComponent` e gravação/leitura em `user://` |
| 40 min | Laboratório: cada grupo implementa seu próprio `SaveData`/`SaveComponent` salvando ao menos um dado real de progresso (itens coletados) |
| 15 min | Construção guiada da Scene `Checkpoint`, reutilizando o contrato `Interactable` |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do projeto herdado da Semana 6 sem alterar `ItemData`, Enum, `GameManager` ou `SaveManager`, adicionando uma camada de persistência real acima do que já existe. O professor demonstra a criação do `SaveData` como Resource, a gravação em disco via `ResourceSaver` (ou FileAccess, conforme a escolha do professor) e a leitura na abertura do projeto. Em seguida, cada grupo implementa seu próprio `SaveComponent` salvando ao menos um dado de progresso já existente (itens coletados na Semana 6). O encontro fecha com a construção guiada do `Checkpoint`, uma Scene que implementa o mesmo contrato `Interactable` da Semana 5 e aciona o `SaveComponent` ao ser alcançada — preparando a integração completa do Encontro 2.

## Desafio

Não há desafio de solução livre neste encontro: a construção de `SaveData`/`SaveComponent`/`Checkpoint` é guiada, pois serve de base direta à integração avaliada do Encontro 2.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, um `SaveData` funcional salvando e recuperando ao menos um dado real de progresso entre sessões (não apenas entre cenas), e uma Scene `Checkpoint` que aciona essa gravação via o contrato `Interactable`.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro. O `SaveData`/`Checkpoint` construídos aqui são pré-requisito direto da integração final avaliada no Encontro 2 (Code Review e Playtest de encerramento do Módulo 2).

## Dificuldades Esperadas

- Confundir o `SaveManager` (Autoload, estado entre cenas) com o `SaveData` (Resource, estado persistido em disco) — reforçar que um mantém estado vivo durante a execução e o outro sobrevive ao fechamento do jogo.
- Gravar em um caminho arbitrário do projeto em vez de `user://` — reforçar que `res://` é o projeto (somente leitura em builds exportados) e `user://` é a pasta de dados do usuário.
- Tentar fazer o `Checkpoint` reimplementar sua própria lógica de interação em vez de reutilizar o contrato `Interactable` já existente — reforçar o princípio de reutilização central da disciplina.

---

# Encontro 2

## Objetivos de Aprendizagem

- Integrar GameManager, contrato Interactable, Signals, Resources e save/load em um único fluxo jogável.
- Justificar, em termos de arquitetura, as escolhas de integração adotadas pelo grupo.
- Reconhecer o estado consolidado do Vertical Slice ao final da Unidade II.

## Conteúdos

- Revisão integrada de todos os sistemas do Módulo 2: `GameManager`/`SaveManager` (Autoload), contrato `Interactable`, Signals, `ItemData`/Enum, `SaveData`/`SaveComponent`, `Checkpoint`.
- Integração final dos desafios do módulo (portas, baús, alavancas, `Checkpoint`) em um único fluxo jogável.
- Code Review dos sistemas implementados.
- Playtest coletivo entre grupos.

## Conceitos Fundamentais

Um Vertical Slice não é a soma isolada de sistemas funcionando cada um em seu próprio teste — é a integração deles em um fluxo único e coerente. O Encontro 2 não introduz nenhum conceito novo: existe para verificar que o desacoplamento ensinado desde a Semana 5 (contrato `Interactable`, Signals) realmente permitiu montar portas, baús, alavancas e `Checkpoint` sem lógica duplicada entre eles, e que os dados de design (`ItemData`/Enum) e a persistência (`SaveData`) sustentam esse fluxo de ponta a ponta. É também o primeiro momento formal em que o grupo precisa justificar, para outra pessoa (o professor no Code Review, os colegas no Playtest), por que cada escolha de arquitetura foi feita — habilidade que a disciplina exige de forma crescente até a Semana 17.

## Recursos do Godot

Revisão de todos os recursos do módulo: Autoload/Singleton, contrato `Interactable`, Signals, Resource customizado, Enum, `SaveData`, FileAccess, `Checkpoint`.

## Comparação com Unity

Nenhuma comparação nova é introduzida neste encontro — é o momento de consolidar, em conjunto, as comparações já feitas nas Semanas 4 a 7: `GameManager` (Autoload) versus a ausência de um equivalente formal direto na Unity; contrato `Interactable` (duck typing/interface do Orchestrator) versus Interfaces em C#; Signals versus UnityEvent/C# Actions; `ItemData`/Enum versus `ScriptableObject`/`enum`; `SaveData`/FileAccess versus PlayerPrefs/JSON. O Code Review deste encontro é o momento de pedir a cada grupo que articule essas comparações com as próprias palavras, não apenas que as reconheça passivamente.

## Preparação do Professor

- Projeto de cada grupo com `SaveData`, `SaveComponent` e `Checkpoint` do Encontro 1 já funcionais.
- Roteiro de Code Review preparado a partir da Rubrica 4 (Code Review) do Sistema de Avaliação — nomenclatura, modularidade, reutilização de contrato `Interactable`, ausência de lógica duplicada entre `Player` e os interativos.
- Roteiro de Playtest coletivo preparado a partir da Rubrica correspondente do Sistema de Avaliação — funcionamento, usabilidade e clareza do fluxo integrado.
- Slides de síntese comparativa Godot × Unity do Módulo 2 (não introduzem comparação nova, apenas consolidam).
- Tempo reservado para rotação entre grupos durante o Playtest coletivo.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão integrada de GameManager, SaveManager, Interactable, Signals, Resources e save/load |
| 60 min | Laboratório: integração final dos desafios do módulo (portas, baús, alavancas, Checkpoint) em um único fluxo jogável |
| 15 min | Preparação de cada grupo para apresentar e justificar sua integração |
| 30 min | Code Review — cada grupo apresenta sua integração completa, justificando as escolhas de arquitetura adotadas |
| 15 min | Playtest coletivo entre grupos e fechamento da Unidade II |

## Desenvolvimento

O encontro não introduz sistema novo: reúne, sob supervisão do professor atuando como diretor técnico, todos os sistemas construídos desde a Semana 4 em um único fluxo jogável por grupo. Cada grupo conecta seus próprios objetos interativos (portas, alavancas, baús) e o `Checkpoint` ao restante do projeto, verificando que o `GameManager`, o `SaveManager` e o `SaveData` sustentam o conjunto sem retrabalho. O professor conduz o Code Review percorrendo a Rubrica 4 do Sistema de Avaliação com cada grupo, seguido do Playtest coletivo, em que os grupos testam o fluxo integrado uns dos outros.

## Desafio

Cada grupo apresenta sua integração completa do Módulo 2, justificando as escolhas de arquitetura adotadas (por que optou por determinado contrato de interação, determinada categoria de Enum, determinado ponto de `Checkpoint`). **Entrega: gameplay funcional consolidado do Módulo 2, avaliado por Code Review e Playtest coletivo.**

## Critérios de Sucesso

Cada grupo possui, ao final da semana, um fluxo jogável único e coerente — sem sistemas isolados — em que `GameManager`, `SaveManager`, contrato `Interactable`, Signals, `ItemData`/Enum e `SaveData`/`Checkpoint` operam juntos, com progresso real persistido entre sessões.

## Evidências para Avaliação

**Code Review** (Rubrica 4 do Sistema de Avaliação) — nomenclatura, modularidade e organização de Scenes/Scripts/Orchestrations; reutilização do contrato `Interactable` sem lógica duplicada entre interativos; ausência de retrabalho de sistemas anteriores.
**Playtest coletivo** (Rubrica correspondente do Sistema de Avaliação) — funcionamento do fluxo integrado de ponta a ponta, usabilidade e clareza para o jogador, avaliado pelos colegas de outros grupos.
Este entregável fecha a Unidade II e compõe, junto ao Checkpoint da Semana 6, a base de avaliação processual do Módulo 2 — não é reavaliado pela Rubrica 2 (Desafios Técnicos), para evitar dupla pontuação sobre o mesmo entregável.

## Dificuldades Esperadas

- Apresentar cada sistema isoladamente no Code Review em vez de demonstrar o fluxo integrado — reforçar que o objetivo da semana é a integração, não a soma de partes.
- Não conseguir justificar por que uma escolha de arquitetura foi feita (ex.: por que aquele Enum, por que aquele ponto de Checkpoint) — usar a pergunta "por que esse caminho e não outro possível?" para calibrar a avaliação, como já indicado na Rubrica 2.
- Retrabalhar sistemas já concluídos (portas ou baús da Semana 5/6) em vez de apenas conectá-los ao fluxo — reforçar que retrabalho desnecessário indica falha de planejamento da integração, não refinamento.

---

# Resultado Esperado da Semana

Ao final da Semana 7, cada grupo possui um Vertical Slice com `GameManager`/`SaveManager` (Autoload), contrato `Interactable`, Signals, `ItemData`/Enum e `SaveData`/`Checkpoint` integrados em um único fluxo jogável, com progresso real persistido entre sessões — não apenas entre cenas. A turma domina serialização e recuperação de estado de jogo via Resource + FileAccess, relaciona esse mecanismo ao equivalente da Unity (PlayerPrefs/JSON), e passou pelo Code Review e Playtest coletivo de encerramento do Módulo 2, fechando a Unidade II — Construir Sistemas.

# Preparação para a Próxima Semana

O gameplay funcional consolidado nesta semana é a base direta da Semana 8, que inicia a Unidade III (Resolver Problemas) com a construção do `HealthComponent` — reutilizando o mesmo padrão de Component já estabelecido pelo `SaveComponent` — e a fundamentação de AnimationTree/BlendSpace para o Player. A metodologia muda de Studio Based Learning para Challenge Based Learning: a partir da Semana 8, o professor apresenta problemas e os grupos propõem soluções com autonomia crescente.

# Referências

- Godot Documentation — Saving Games: https://docs.godotengine.org/en/stable/tutorials/io/saving_games.html
- Godot Documentation — Resources: https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html
- Godot Documentation — File System (FileAccess): https://docs.godotengine.org/en/stable/tutorials/scripting/filesystem.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — PlayerPrefs: https://docs.unity3d.com/Manual/class-PlayerPrefs.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
