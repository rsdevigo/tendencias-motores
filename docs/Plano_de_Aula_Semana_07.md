# Semana 7 🔴

## Introdução da Semana

A Semana 7 encerra a Unidade II — Construir Sistemas. É uma semana de encerramento de módulo: não introduz apenas um recurso novo isolado, mas fecha o ciclo iniciado na Semana 4 (GameMode, GameState, PlayerController, GameInstance) e ampliado nas Semanas 5 e 6 (Interfaces, Event Dispatchers, Data Tables, Structs, Enums). O eixo conceitual do Encontro 1 é a serialização de estado — como uma engine grava e recupera o progresso de um jogador entre sessões — aplicada diretamente ao que já existe no Vertical Slice: os itens de `DT_Items` coletados via `BPI_Interactable` e Event Dispatcher, e um novo `BP_Checkpoint` que aplica esse mesmo par (Interface + persistência) a um ponto concreto de progresso. O Encontro 2 não introduz nenhum recurso novo da Unreal: é dedicado à revisão integrada de todos os sistemas do Módulo 2 e à integração final dos desafios acumulados (portas, alavancas, baús, checkpoints) em um único fluxo jogável, encerrando com Code Review e Playtest coletivo — os primeiros instrumentos desse tipo na disciplina. A metodologia permanece Studio Based Learning, mas a autonomia do Encontro 2 se aproxima do limite superior do módulo: cada grupo já deve ser capaz de justificar tecnicamente as próprias decisões de arquitetura.

## Objetivos Gerais

- Compreender a serialização e recuperação de estado como problema universal de persistência entre sessões de jogo.
- Implementar `BP_SaveGame` e `SaveComponent`, conforme PROJECT_ARCHITECTURE.md, para gravar e recuperar o progresso de coleta de itens.
- Implementar `BP_Checkpoint`, reutilizando `BPI_Interactable` e o `SaveComponent`, como ponto concreto de gravação de progresso.
- Integrar, em um único fluxo jogável, todos os sistemas construídos no Módulo 2: GameMode, GameState, PlayerController, GameInstance, `BPI_Interactable`, Event Dispatchers, `DT_Items`, `BP_Checkpoint` e SaveGame.
- Justificar tecnicamente, em Code Review, as decisões de arquitetura adotadas ao longo do módulo.

## Resultados Esperados

Ao final da semana, cada grupo terá um SaveGame funcional que grava e recupera o progresso de coleta de itens do Vertical Slice, um `BP_Checkpoint` funcional que aciona essa gravação ao ser alcançado/interagido, e terá integrado portas, alavancas, baús, checkpoints e o próprio SaveGame em um único fluxo jogável testável de ponta a ponta. O módulo se encerra com Code Review dos sistemas implementados e Playtest coletivo, conforme Rubricas 4 e 5 do Sistema de Avaliação.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o SaveGame Object como mecanismo de serialização e recuperação de estado de jogo.
- Comparar SaveGame Object com PlayerPrefs e serialização própria em JSON na Unity.
- Implementar `BP_SaveGame` e `SaveComponent` para gravar e recuperar o progresso de coleta de itens.
- Implementar `BP_Checkpoint`, reutilizando `BPI_Interactable` (Semana 5) e o `SaveComponent` recém-construído, como ponto concreto de gravação de progresso.

## Conteúdos

- SaveGame Object: classe dedicada à serialização de estado entre sessões de jogo.
- `SaveComponent` como ponto único de leitura/escrita do `BP_SaveGame`, conforme PROJECT_ARCHITECTURE.md.
- Aplicação do SaveGame ao progresso de coleta de itens de `DT_Items` (Semana 6).
- `BP_Checkpoint`: Actor que implementa `BPI_Interactable` (Semana 5) e, ao ser alcançado/interagido pelo jogador, aciona o `SaveComponent` para gravar o progresso — a primeira aplicação concreta do par Interface + persistência no mesmo objeto.

## Conceitos Fundamentais

O conceito universal desta aula é a persistência de estado além do tempo de execução. Até aqui, todo o progresso do jogador — itens coletados, portas abertas — existe apenas enquanto o jogo está rodando; ao fechar o editor ou o build, esse estado desaparece. Toda engine madura precisa de um mecanismo que capture uma fração do estado em memória e a grave em um formato recuperável, para que o jogador retome de onde parou. A Unreal resolve isso com o SaveGame Object: uma classe que existe fora do fluxo normal de Actors, pensada exclusivamente para ser serializada em disco e desserializada de volta. O princípio arquitetural relevante, reforçado por PROJECT_ARCHITECTURE.md, é que nenhum Actor deve implementar sua própria lógica de leitura/escrita de arquivo — essa responsabilidade é centralizada em `SaveComponent`, evitando que a lógica de serialização se espalhe pelo projeto à medida que novos sistemas persistentes forem adicionados (como o Inventário, na Semana 10). O `BP_Checkpoint` é a aplicação mais direta desse princípio: em vez de reinventar um mecanismo próprio de gravação, ele apenas implementa `BPI_Interactable` (exatamente como `BP_Door`/`BP_Lever` na Semana 5) e, ao ser interagido, aciona o `SaveComponent` já existente — reaproveitando tanto o contrato de interação quanto o ponto único de persistência, sem duplicar lógica de nenhum dos dois.

## Recursos da Unreal

SaveGame Object, `BP_SaveGame`, `SaveComponent`, `BP_Checkpoint` (novo), `DT_Items` e `BPI_Interactable`/Event Dispatcher (retomados das Semanas 5 e 6).

## Comparação com Unity

A Unity resolve o mesmo problema de persistência principalmente de duas formas: `PlayerPrefs`, adequado apenas a dados simples e pequenos (chave-valor), e serialização própria em JSON (via `JsonUtility` ou bibliotecas externas) para estados mais complexos, exigindo que o próprio desenvolvedor defina o formato e a gravação em arquivo. A Unreal, por sua vez, já oferece uma classe dedicada (`USaveGame`) com suporte nativo a serialização binária de propriedades marcadas, sem exigir que o desenvolvedor defina o formato do arquivo. O princípio — isolar o estado que deve persistir em uma estrutura própria, separada da lógica de gameplay em tempo real — é o mesmo nas duas engines; a diferença está no grau de suporte nativo da ferramenta. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `DT_Items`, `BPI_Interactable` e Event Dispatcher das Semanas 5 e 6 funcionais.
- Um `BP_SaveGame` de exemplo pré-configurado (fora da visão da turma), gravando e recuperando uma lista simples de itens coletados.
- Um `BP_Checkpoint` de exemplo pré-configurado (fora da visão da turma), implementando `BPI_Interactable` e acionando o `SaveComponent` ao ser interagido.
- Slides com o diagrama Estado em memória (runtime) × Estado serializado (SaveGame Object), reforçando o papel do `SaveComponent` como ponto único de acesso.
- PROJECT_ARCHITECTURE.md disponível para reforçar a convenção de nomenclatura, a responsabilidade do `SaveComponent` e a subpasta `Interactables/` de `BP_Checkpoint`.
- **Nota de contingência:** este é um encontro de fundamentação técnica que alimenta diretamente a integração do Encontro 2; não é compressível sem prejudicar a consolidação do módulo — caso falte tempo, priorizar a gravação sobre a recuperação, e o `BP_Checkpoint` sobre a persistência de itens individuais, retomando o que faltar no início do Encontro 2.

## Cronograma do Encontro

- 15 min — Revisão de `DT_Items`, `BPI_Interactable` e Event Dispatcher (Semanas 5 e 6).
- 15 min — Fundamentação: SaveGame Object como serialização de estado entre sessões.
- 30 min — Demonstração: criação guiada de `BP_SaveGame` e `SaveComponent`, gravando e recuperando o progresso de coleta de um item, seguida da aplicação do `SaveComponent` a um `BP_Checkpoint` que implementa `BPI_Interactable`.
- 50 min — Laboratório: cada grupo implementa `BP_SaveGame` e `SaveComponent` aplicados ao próprio conjunto de itens de `DT_Items`, e constrói seu próprio `BP_Checkpoint`.
- 25 min — Feedback: verificação da gravação e recuperação funcional em cada grupo, incluindo o funcionamento do `BP_Checkpoint`.

## Desenvolvimento

O encontro parte da constatação de que, embora cada grupo já colete itens de `DT_Items` desde a Semana 6, esse progresso se perde a cada nova sessão de teste. O professor demonstra a criação de `BP_SaveGame` com uma propriedade simples (lista de identificadores de itens coletados), cria `SaveComponent` como ponto único de gravação e leitura, e conecta esse componente ao Event Dispatcher já existente no Actor de coleta — de modo que, ao coletar um item, o `SaveComponent` grava o progresso, e ao carregar o nível, o mesmo componente recupera e reaplica o estado salvo. Em seguida, o professor cria `BP_Checkpoint`, implementando `BPI_Interactable` exatamente como fez com `BP_Door`/`BP_Lever` na Semana 5, e conecta a função de interação diretamente ao `SaveComponent`, de modo que alcançar/interagir com o checkpoint dispara a gravação do progresso — sem que o `BP_Checkpoint` implemente qualquer lógica própria de arquivo. Cada grupo replica o processo em seu próprio projeto, aplicando `SaveComponent` ao Actor de coleta e ao Player, construindo seu próprio `BP_Checkpoint`, e validando a persistência com um teste de fechar e reabrir o nível.

## Desafio

Não há desafio de liberdade de solução neste encontro — a implementação do SaveGame e do `BP_Checkpoint` é demonstração e adaptação guiada, preparando a integração final do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir `BP_SaveGame` e `SaveComponent` funcionais, gravando e recuperando corretamente o progresso de coleta de itens de `DT_Items`, e um `BP_Checkpoint` funcional que implementa `BPI_Interactable` e aciona o `SaveComponent` ao ser alcançado/interagido, com nomenclatura conforme PROJECT_ARCHITECTURE.md.

## Evidências para Avaliação

Funcionamento demonstrável da gravação e recuperação de progresso, funcionamento demonstrável do `BP_Checkpoint`, e organização/nomenclatura de `BP_SaveGame`/`SaveComponent`/`BP_Checkpoint` conforme PROJECT_ARCHITECTURE.md (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Preparação).

## Dificuldades Esperadas

Estudantes podem tentar gravar o estado diretamente dentro do Actor de coleta ou do Player, duplicando lógica de serialização em vários lugares do projeto. Intervenção: perguntar "se o próximo sistema persistente (o Inventário, na Semana 10) precisar salvar dados, ele vai duplicar essa mesma lógica de gravação?"; se a resposta for sim, reforçar que toda leitura/escrita deve passar pelo `SaveComponent`, nunca ser implementada localmente em cada Actor. Estudantes também podem tentar dar ao `BP_Checkpoint` sua própria lógica de gravação, em vez de acionar o `SaveComponent` já existente — reforçar que o checkpoint é apenas mais um Actor que implementa `BPI_Interactable`, como qualquer outro interativo da Semana 5. Grupos com dificuldade para testar a persistência (por não saberem como forçar o recarregamento do nível) devem receber orientação direta do professor sobre o fluxo de teste.

---

# Encontro 2

## Objetivos de Aprendizagem

- Revisar de forma integrada GameMode, GameState, PlayerController, GameInstance, `BPI_Interactable`, Event Dispatchers, `DT_Items` e SaveGame.
- Integrar os desafios acumulados do módulo (portas, alavancas, baús, `BP_Checkpoint`) em um único fluxo jogável.
- Justificar tecnicamente, em Code Review, as decisões de arquitetura adotadas.

## Conteúdos

- Revisão integrada de todos os sistemas construídos nas Semanas 4 a 7.
- Integração final dos desafios do módulo em um único fluxo jogável.
- Code Review dos sistemas implementados (Rubrica 4).
- Playtest coletivo (Rubrica 5).

## Conceitos Fundamentais

Este encontro não introduz um conceito universal novo — ele consolida a ideia que atravessou todo o Módulo 2: um Vertical Slice funcional não é a soma de sistemas isolados, mas a integração coerente entre eles. GameMode e GameState fornecem o contexto de partida; PlayerController e GameInstance fazem a ponte entre jogador e persistência entre níveis; `BPI_Interactable` e Event Dispatchers desacoplam a comunicação entre Player e objetos do mundo; `DT_Items` separa dado de lógica; e o SaveGame, recém-construído, garante que tudo isso sobreviva entre sessões. O Code Review formaliza a verificação dessa integração sob a perspectiva de boas práticas (organização, nomenclatura, modularidade, reutilização, comunicação desacoplada), e o Playtest verifica a mesma integração sob a perspectiva da experiência do jogador — as duas faces complementares de "o sistema funciona corretamente" que qualquer estúdio profissional avalia antes de considerar um módulo encerrado.

## Recursos da Unreal

GameMode, GameState, PlayerController, GameInstance, `BPI_Interactable`, Event Dispatchers, `DT_Items`, `BP_SaveGame`, `SaveComponent`, `BP_Checkpoint` — todos retomados das Semanas 4 a 7.

## Comparação com Unity

Não há novo recurso da Unreal a comparar neste encontro. A discussão comparativa retoma, de forma breve, o quadro já construído nas Semanas 4 a 7: a ausência de um equivalente direto a GameMode/GameState na Unity (resolvido por convenção de Managers/Singletons), Interfaces em C# para `BPI_Interactable`, UnityEvent/Actions para Event Dispatchers, ScriptableObject para Data Table, e PlayerPrefs/JSON para SaveGame. O objetivo aqui não é aprofundar cada comparação novamente, mas reforçar que a integração entre múltiplos sistemas desacoplados — não apenas cada peça isoladamente — é o que diferencia um protótipo de um gameplay funcional, princípio válido em qualquer engine.

## Preparação do Professor

- Projeto de cada grupo com todos os sistemas do Módulo 2 (Semanas 4 a 7) implementados, incluindo `BP_SaveGame`/`SaveComponent` do Encontro 1.
- Modelo de Code Review (Sistema de Avaliação, Rubrica 4) impresso ou digital, um por grupo.
- Modelo de Playtest (Sistema de Avaliação, Rubrica 5) impresso ou digital, um por grupo, com identificação de jogadores externos ao próprio grupo (idealmente colegas de outro grupo).
- PROJECT_ARCHITECTURE.md disponível para consulta durante o Code Review, especialmente as seções 7 (Arquitetura de Alto Nível) e 10 (Boas Práticas).
- Organização prévia da sala para permitir rodízio de grupos durante o Playtest coletivo.
- **Nota de contingência:** este encontro concentra os instrumentos avaliativos de encerramento do módulo e não deve ser comprimido; se necessário, reduzir o tempo de integração livre, nunca o tempo de Code Review ou Playtest.

## Cronograma do Encontro

- 15 min — Revisão rápida, em conjunto com a turma, de todos os sistemas do Módulo 2 (GameMode a SaveGame).
- 60 min — Laboratório de integração: cada grupo conecta portas, alavancas, baús, o `BP_Checkpoint` do Encontro 1 e SaveGame em um único fluxo jogável no nível de teste.
- 30 min — Code Review: o professor percorre os grupos, abrindo os Blueprints ao vivo e aplicando a Rubrica 4.
- 30 min — Playtest coletivo: rodízio entre grupos, com um jogador externo testando o fluxo integrado de cada projeto, aplicando a Rubrica 5.

## Desenvolvimento

O encontro não introduz nada novo tecnicamente — é dedicado a fechar as pontas soltas do módulo. Cada grupo revisa seu próprio projeto e conecta, em um único percurso jogável, os objetos interativos construídos ao longo das Semanas 5 e 6 (a porta ou equivalente da Semana 5, os baús/itens da Semana 6) e o `BP_Checkpoint` do Encontro 1 ao SaveGame, de modo que o progresso completo — objetos ativados, itens coletados e checkpoint alcançado — seja gravado e recuperado de forma consistente. Em seguida, o professor conduz o Code Review grupo a grupo, pedindo que cada grupo explique suas próprias decisões de arquitetura (por que um Actor usa Interface em vez de referência direta, por que um dado está em `DT_Items` e não hardcoded), aplicando a Rubrica 4. Por fim, ocorre o Playtest coletivo: um jogador externo ao grupo testa o fluxo integrado, sem explicação prévia além do mínimo necessário, e o professor registra funcionamento, usabilidade, bugs e clareza conforme a Rubrica 5.

## Desafio

Cada grupo apresenta sua integração completa do Módulo 2 — todos os objetos interativos, coleta de itens e SaveGame funcionando em um único fluxo — justificando tecnicamente, durante o Code Review, as escolhas de arquitetura adotadas (uso de Interfaces, Event Dispatchers, Data Table, e centralização da persistência no `SaveComponent`).

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um fluxo jogável único no nível de teste, integrando portas/alavancas, baús/itens, `BP_Checkpoint` e SaveGame, com o progresso completo persistindo corretamente entre sessões, e deve ter passado pelo Code Review e pelo Playtest coletivo conforme as Rubricas 4 e 5.

## Evidências para Avaliação

Organização, nomenclatura, modularidade, reutilização e comunicação desacoplada entre sistemas, registradas no instrumento de Code Review (Rubrica 4); funcionamento, usabilidade, bugs, feedback visual e clareza de interface, registrados no instrumento de Playtest (Rubrica 5) — ambos instrumentos de encerramento formal do Módulo 2, conforme Sistema de Avaliação.

## Dificuldades Esperadas

Grupos podem ter implementado sistemas individualmente funcionais nas semanas anteriores, mas nunca testados em conjunto, revelando conflitos de integração apenas neste encontro (por exemplo, o SaveGame não reconhecendo o estado de um objeto interativo específico). Intervenção: tratar esses conflitos como parte esperada do processo de integração, não como falha — orientar o grupo a isolar qual sistema não está se comunicando corretamente e revisar se a comunicação passa pelos padrões corretos (Interface/Event Dispatcher) antes de qualquer ajuste emergencial. Grupos que não concluírem a integração completa a tempo do Playtest devem apresentar o fluxo parcial, registrando as pendências no Code Review para acompanhamento nos módulos seguintes, sem impedir o registro do progresso já alcançado.

---

# Resultado Esperado da Semana

Ao final da Semana 7, cada grupo deve possuir um gameplay funcional consolidado: GameMode, GameState, PlayerController e GameInstance como framework de base; `BPI_Interactable` e Event Dispatchers permitindo comunicação desacoplada entre Player e objetos do mundo; `DT_Items` (com `S_ItemData` e `E_ItemType`) como dado de design centralizado; `BP_SaveGame`/`SaveComponent` persistindo o progresso de coleta entre sessões; e `BP_Checkpoint`, aplicando esse mesmo par (Interface + persistência) a um ponto concreto de progresso — tudo integrado em um único fluxo jogável testado via Code Review e Playtest coletivo. Conceitualmente, a turma deve dominar a distinção entre regras de partida, estado compartilhado, comunicação desacoplada, dado de design e persistência como cinco problemas complementares de arquitetura de motores, todos resolvidos de forma integrada — não isolada — em um mesmo projeto. Este resultado encerra a Unidade II — Construir Sistemas.

# Preparação para a Próxima Semana

A Semana 8 abre a Unidade III — Resolver Problemas, com a introdução de Animation Blueprint, Blend Spaces e Montages, que passam a atuar sobre o `BP_Player` já consolidado nas Semanas 1 a 7. A metodologia muda de Studio Based Learning para Challenge Based Learning: a partir da Semana 8, o professor apresenta problemas e os grupos propõem soluções com autonomia crescente, sem tutoriais passo a passo, retomando o gameplay funcional consolidado nesta semana como base estável sobre a qual a animação, a interface, o inventário e a IA serão construídos até a Semana 11.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Saving and Loading Your Game. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-loading-your-game-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a SaveGame Object. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — PlayerPrefs e serialização com JsonUtility, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Save/Load; **Mathew Wadstein**, para explicações pontuais de WTF Is? Save Game.
