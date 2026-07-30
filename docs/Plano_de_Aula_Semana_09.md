# Semana 9 🔵

## Introdução da Semana

A Semana 9 dá continuidade à Unidade III — Resolver Problemas, mantendo a metodologia de Challenge Based Learning inaugurada na Semana 8: o professor apresenta o problema, cada grupo propõe a própria solução, com autonomia média. O eixo conceitual da semana muda de animação para comunicação com o jogador: como uma engine comunica, em tempo real, o estado interno do jogo — vida, itens, progresso — sem que essa camada de apresentação se misture com a lógica de gameplay já construída. O Encontro 1 introduz UMG (Widgets, Canvas Panel, binding de dados) como sistema universal de interface em tempo real, aplicado a uma única variável de gameplay já existente; o Encontro 2 introduz HUD como camada de organização de múltiplos Widgets, fechando com um desafio de liberdade real: cada grupo decide quais dados de gameplay já existentes (vida do `HealthComponent`, itens do futuro Inventário, progresso do `SaveComponent`) devem compor o HUD, propondo a própria solução visual e de binding. Nenhum sistema dos Módulos 1 e 2, nem o `HealthComponent` construído na Semana 8, é descartado: o HUD passa a expor, em tela, dados que já existem no `BP_GameState` e no `SaveComponent` (consolidados até a Semana 7) e no `HealthComponent` (construído na Semana 8).

## Objetivos Gerais

- Compreender UMG como sistema universal de interface em tempo real e o binding de dados como mecanismo de exibição de estado de gameplay na UI.
- Criar um Widget simples vinculado a uma variável de gameplay já existente no projeto.
- Compreender HUD como camada de organização de múltiplos Widgets sobre a tela de jogo.
- Propor e implementar, com autonomia própria, um HUD que exiba os dados de gameplay que o grupo julgar relevantes, justificando a escolha visual e de binding.

## Resultados Esperados

Ao final da semana, cada grupo terá um `WBP_HUD` funcional, exibindo em tempo real ao menos os dados de gameplay que o próprio grupo escolheu (vida, itens, progresso ou combinação destes), vinculados por binding aos sistemas já existentes, sem alterar a lógica de nenhum sistema do Módulo 2.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar UMG como sistema universal de interface em tempo real, incluindo Widgets, Canvas Panel e binding de dados.
- Comparar UMG com UI Toolkit/uGUI da Unity.
- Criar um Widget simples vinculado a uma variável de gameplay já existente no projeto.

## Conteúdos

- UMG como camada de apresentação de interface, separada da lógica de gameplay.
- Widget Blueprint, Canvas Panel e elementos básicos de UI (Text, Progress Bar).
- Binding de uma propriedade de Widget a uma variável de gameplay já existente (ex.: vida do `HealthComponent`).

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre o dado de gameplay e sua representação visual em tela. Um valor de vida, de itens coletados ou de progresso já existe internamente no projeto — no `HealthComponent`, no `BP_GameState` ou no `SaveComponent` — antes de qualquer interface ser criada; o problema que toda engine precisa resolver é como expor esse dado ao jogador em tempo real, de forma que a interface se atualize automaticamente quando o dado mudar, sem que o sistema de gameplay precise conhecer detalhes de como a informação é desenhada na tela. A Unreal resolve isso com UMG (Unreal Motion Graphics): um Widget Blueprint organiza elementos visuais (texto, barras, imagens) sobre um Canvas Panel, e o binding conecta uma propriedade do elemento visual (por exemplo, o valor de uma Progress Bar) a uma função que lê o dado de gameplay a cada frame, sem exigir que o sistema de gameplay dispare eventos de atualização manualmente. Essa camada é deliberadamente desacoplada: o `HealthComponent` continua funcionando de forma idêntica exista ou não um Widget lendo seus dados.

## Recursos da Unreal

UMG, Widget Blueprint, Canvas Panel, binding de dados, `HealthComponent` (construído na Semana 8).

## Comparação com Unity

A Unity resolveu historicamente o mesmo problema de duas formas: uGUI, sistema mais antigo baseado em Canvas e componentes de UI escritos em C#, e UI Toolkit, sistema mais recente baseado em UXML/USS, inspirado em tecnologias web. Em ambos os casos, a atualização da interface a partir de um dado de gameplay normalmente exige código explícito (um script que lê a variável e escreve no componente de texto ou barra a cada mudança), diferente do binding declarativo do UMG, que permite conectar visualmente uma propriedade do Widget a uma função de leitura de dados sem escrever a lógica de atualização manualmente. O princípio geral é o mesmo nas duas engines — a interface lê o estado de gameplay e nunca o contrário —, mas o grau de suporte visual/declarativo nativo é maior no UMG. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `HealthComponent` funcional (Semana 8) e `BP_GameState`/`SaveComponent` consolidados na Semana 7.
- Um Widget Blueprint de exemplo pré-configurado (fora da visão da turma), com uma Progress Bar vinculada por binding à vida do `HealthComponent`.
- Slides com o diagrama Dado de gameplay (`HealthComponent`) → binding → elemento visual (Widget), reforçando a separação de responsabilidades.
- REFERENCES.md e documentação de UMG UI Designer disponíveis para consulta durante o laboratório.
- **Nota de contingência:** este é o primeiro encontro da semana e alimenta diretamente o Encontro 2 (HUD); não é compressível sem prejudicar a fundamentação — caso falte tempo, priorizar o binding de um único dado (vida) sobre a exploração de múltiplos elementos de Canvas Panel.

## Cronograma do Encontro

- 15 min — Revisão do estado atual do `BP_GameState` e do `SaveComponent` (consolidados na Semana 7) e do `HealthComponent` (construído na Semana 8).
- 20 min — Fundamentação: UMG, Widget Blueprint, Canvas Panel e binding de dados como camada de interface desacoplada da lógica de gameplay.
- 35 min — Demonstração: criação guiada de um Widget simples com uma Progress Bar vinculada por binding à vida do `HealthComponent`.
- 50 min — Laboratório: cada grupo cria seu próprio Widget e vincula um elemento visual a uma variável de gameplay já existente no projeto.
- 15 min — Feedback: verificação da atualização em tempo real do Widget em cada grupo.

## Desenvolvimento

O encontro parte da constatação de que o `HealthComponent` já gerencia vida corretamente desde a Semana 8, mas nenhum dado de gameplay é exibido em tela. O professor demonstra a criação de um Widget Blueprint, a montagem de uma Progress Bar sobre um Canvas Panel, e o binding dessa Progress Bar à função que lê a vida atual do `HealthComponent`. Cada grupo replica o processo em seu próprio projeto, escolhendo um dado de gameplay já existente (vida, ou outro dado disponível) para vincular a um elemento visual simples, validando que a interface se atualiza automaticamente quando o dado muda em tempo de jogo.

## Desafio

Não há desafio de liberdade de solução neste encontro — a criação do Widget simples com binding é demonstração e adaptação guiada, preparando o desafio de maior autonomia do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um Widget funcional, exibido em tela durante o gameplay, com ao menos um elemento visual atualizado por binding a uma variável de gameplay já existente, sem alterar a lógica de nenhum sistema do Módulo 2.

## Evidências para Avaliação

Funcionamento demonstrável do binding e organização/nomenclatura do Widget conforme boas práticas da Unreal 5.6 e do PROJECT_ARCHITECTURE.md (prefixo `WBP_`) (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Evolução).

## Dificuldades Esperadas

Estudantes podem tentar atualizar o Widget escrevendo diretamente no elemento visual a partir do `HealthComponent` (referência direta), em vez de usar binding, acoplando novamente gameplay e interface. Intervenção: perguntar "se a vida mudar em três lugares diferentes do projeto, quantas vezes esse código de atualização de tela precisaria ser escrito?" e reforçar que o binding lê o dado sempre que necessário, sem exigir que o sistema de gameplay dispare a atualização manualmente. Grupos com dificuldade para localizar a variável ou função exposta pelo `HealthComponent` devem ser direcionados à documentação oficial antes de receber a resposta direta.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar HUD como camada de organização de múltiplos Widgets sobre a tela de jogo.
- Propor e implementar, com autonomia própria, um HUD que combine os dados de gameplay que o grupo julgar relevantes.
- Justificar tecnicamente as escolhas de quais dados exibir e como estruturar o binding de cada um.

## Conteúdos

- HUD como Widget de nível superior que organiza e posiciona múltiplos elementos de interface.
- Reutilização do binding de dados do Encontro 1 aplicado a múltiplos dados de gameplay (vida, itens, progresso).
- Desafio: proposta e implementação de um HUD próprio de cada grupo.

## Conceitos Fundamentais

O conceito universal desta aula é a organização de múltiplos elementos de interface em uma única camada coerente. Um único Widget com um elemento vinculado, como o construído no Encontro 1, resolve a exibição de um dado isolado; um jogo real, porém, precisa comunicar vários dados simultaneamente — vida, itens, objetivo — sem que a tela se torne uma colagem desorganizada de Widgets independentes. O HUD resolve esse problema como um Widget "container", posicionado permanentemente em tela durante o gameplay, que agrupa e organiza os demais elementos (ou os próprios bindings) em um layout único. O problema que este encontro apresenta não tem uma resposta fechada: cada grupo possui um conjunto diferente de dados de gameplay já implementados (todos possuem `HealthComponent`; alguns podem ter avançado mais no progresso do `SaveComponent`), e cabe a cada grupo decidir quais desses dados comunicar e como organizá-los visualmente — decisão que é, em si, o núcleo do desafio.

## Recursos da Unreal

UMG, HUD, Widget Blueprint, Canvas Panel e binding de dados (retomados do Encontro 1).

## Comparação com Unity

A Unity não possui uma classe nomeada equivalente ao conceito de "HUD" como Widget de nível superior; o mesmo resultado é obtido organizando um Canvas raiz (uGUI) ou um documento UXML raiz (UI Toolkit) que agrupa os elementos de interface do jogo, geralmente instanciado e mantido por um script de gerenciamento de UI equivalente a um Game Manager. O princípio é o mesmo nas duas engines — um único ponto de organização visual concentra os elementos de interface ativos durante o gameplay —, mas a Unreal nomeia e trata esse papel de forma mais explícita através da convenção de HUD como Widget dedicado. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o Widget do Encontro 1 funcional.
- Levantamento prévio, por grupo, de quais dados de gameplay já estão disponíveis (vida, itens do inventário ainda em construção, progresso do `SaveComponent`), para orientar o feedback sem indicar a solução.
- Um `WBP_HUD` de exemplo pré-configurado (fora da visão da turma), combinando dois elementos (vida e um segundo dado), fora da vista da turma.
- Enunciado do desafio redigido de forma aberta, sem indicar quais dados exibir nem o layout, para preservar a decisão do grupo.
- Modelo de Feedback Formal (conforme Sistema de Avaliação, Rubrica correspondente) pronto para uso ao final do encontro.
- REFERENCES.md e documentação de UMG UI Designer disponíveis para consulta durante o laboratório e o desafio.
- **Nota de contingência:** o desafio é o núcleo do encontro e não deve ser comprimido; se necessário, reduzir o tempo de demonstração do HUD combinado, mantendo intacto o tempo de laboratório do desafio.

## Cronograma do Encontro

- 15 min — Revisão do Widget e do binding construídos no Encontro 1.
- 20 min — Fundamentação: HUD como camada de organização de múltiplos Widgets.
- 25 min — Demonstração: montagem guiada de um HUD combinando dois elementos vinculados por binding.
- 15 min — Apresentação do desafio: cada grupo decide quais dados de gameplay já existentes devem compor seu HUD.
- 45 min — Laboratório do desafio: cada grupo implementa sua própria solução de HUD.
- 15 min — Desafio + Feedback Formal: cada grupo apresenta seu HUD e recebe feedback formal registrado, justificando a escolha dos dados exibidos e do layout.

## Desenvolvimento

O professor demonstra a montagem de um `WBP_HUD` que combina, em um único Canvas Panel, dois elementos já conhecidos do Encontro 1 (por exemplo, vida e um segundo dado simples), reforçando que o HUD é apenas um Widget organizador, não um conceito tecnicamente novo além do já aprendido. Feita a demonstração, o professor apresenta o desafio: cada grupo deve decidir, entre os dados de gameplay já existentes em seu próprio projeto (vida do `HealthComponent`, progresso do `SaveComponent` ou outros disponíveis), quais compor no HUD, propondo a própria solução visual (layout, posicionamento, elementos gráficos) e de binding. Não há indicação prévia de quais dados exibir ou como organizá-los; a decisão faz parte do desafio.

## Desafio

Cada grupo define quais dados de gameplay já existentes (vida, itens, progresso) devem compor o HUD, propondo a própria solução visual e de binding, e apresenta ao final do encontro a justificativa técnica das escolhas feitas.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um `WBP_HUD` funcional, exibido em tela durante o gameplay, combinando ao menos dois dados de gameplay vinculados por binding, com layout e escolha de dados justificados tecnicamente pelo grupo, sem alterar a lógica de nenhum sistema do Módulo 2.

## Evidências para Avaliação

Adequação dos dados escolhidos e do layout ao propósito de comunicação com o jogador, funcionamento do binding e capacidade de justificar tecnicamente as escolhas, registradas conforme o instrumento de Feedback Formal da semana (Sistema de Avaliação).

## Dificuldades Esperadas

Grupos podem tentar exibir todos os dados disponíveis de uma vez, produzindo um HUD poluído e sem hierarquia visual clara. Intervenção: não indicar diretamente quais dados remover; perguntar "qual desses dados o jogador precisa ver a cada segundo, e qual só precisa ver ocasionalmente?" e deixar o grupo re-avaliar a própria composição a partir da resposta. Grupos que travarem na configuração técnica do binding para um dado específico devem ser direcionados à documentação oficial antes de receber apoio direto do professor, preservando a autonomia média esperada no Módulo 3.

---

# Resultado Esperado da Semana

Ao final da Semana 9, cada grupo terá um `WBP_HUD` funcional, exibindo em tempo real os dados de gameplay que o próprio grupo escolheu comunicar (vida, itens, progresso ou combinação destes), vinculados por binding ao `BP_GameState`/`SaveComponent` (consolidados no Módulo 2) e ao `HealthComponent` (construído na Semana 8), sem substituir nenhum sistema anterior. Conceitualmente, a turma deve dominar a distinção entre Widget (elemento de interface com binding) e HUD (camada de organização de múltiplos Widgets), e deve ter exercitado, pela segunda vez no Módulo 3, a decisão autônoma de qual solução (dados exibidos, layout) aplicar a um problema aberto.

# Preparação para a Próxima Semana

A Semana 10 introduz o Inventário, reutilizando os itens modelados em Data Table/Struct na Semana 6, e amplia o Interaction System introduzido na Semana 5 para suportar múltiplos tipos de interação conectados ao inventário (coletar, usar, descartar). O `WBP_HUD` construído nesta semana será o destino natural da exibição dos itens do inventário, e o binding aprendido nesta semana será diretamente reutilizado para exibir dados de itens. A metodologia permanece Challenge Based Learning, encerrando com Code Review dos sistemas de inventário e interação.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — UMG UI Designer. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-ui-designer.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a UMG, Widget Blueprint e binding de dados. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — uGUI e UI Toolkit, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de UMG; **Mathew Wadstein**, para explicações pontuais de WTF Is? Widget Blueprint e Binding; **PrismaticaDev**, para exemplos aplicados de HUD de gameplay.
