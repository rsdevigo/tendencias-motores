# Semana 6

## Introdução da Semana

A Semana 6 encerra a fundamentação teórica da Unidade II — Construir Sistemas, retomando o objeto interativo funcional (`BPI_Interactable` + Event Dispatcher) que cada grupo construiu na Semana 5. Até aqui, todo comportamento do Vertical Slice foi definido por lógica dentro de Blueprints. Esta semana introduz o problema inverso: como representar informação de design — o que é um item, quantos tipos existem, quais atributos cada um possui — sem que essa informação fique presa dentro da lógica de um Actor específico. A metodologia permanece Studio Based Learning, com autonomia baixa, mas o desafio de final de semana já exige que cada grupo modele seu próprio conjunto de itens coletáveis, aplicando os dados a um Actor de coleta que reutiliza diretamente `BPI_Interactable` e o Event Dispatcher da Semana 5. O Encontro 1 constrói `DT_Items` como estrutura de dados centralizada; o Encontro 2 introduz Structs e Enums como organizadores tipados dessa mesma tabela e fecha com o **Checkpoint de progresso do Módulo 2**, primeiro checkpoint desde a Semana 3.

## Objetivos Gerais

- Compreender a separação entre dados de design e lógica de gameplay como problema universal de arquitetura de motores.
- Diferenciar Data Table (coleção tabular de dados) de Data Asset (instância de dado independente) como duas estratégias complementares para o mesmo problema.
- Criar `DT_Items` com um Struct tipado (`S_ItemData`) e um Enum de categorização (`E_ItemType`), conforme convenções de PROJECT_ARCHITECTURE.md.
- Aplicar `DT_Items` a um Actor de coleta (`BP_Pickup` ou `BP_Chest`) que reutiliza `BPI_Interactable` e o Event Dispatcher da Semana 5.

## Resultados Esperados

Ao final da semana, cada grupo terá `DT_Items` funcional, estruturada por `S_ItemData` e `E_ItemType`, populada com seu próprio conjunto de itens coletáveis, e um Actor de coleta no Vertical Slice que lê essa tabela ao ser interagido — reutilizando integralmente o par Interface + Event Dispatcher da Semana 5. O Checkpoint de progresso do Módulo 2 verifica esse resultado formalmente.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar Data Tables e Data Assets como mecanismos de separação entre dado de design e lógica de gameplay.
- Comparar Data Table/Data Asset com ScriptableObject na Unity.
- Criar `DT_Items` como tabela centralizada de itens do Vertical Slice.

## Conteúdos

- Data Tables: estrutura tabular de dados reutilizável por múltiplas instâncias.
- Data Assets: instância de dado independente, quando a informação não é tabular por natureza.
- Criação de `DT_Items` conforme convenção `DT_` de PROJECT_ARCHITECTURE.md, na subpasta `Data/DataTables/`.

## Conceitos Fundamentais

O conceito universal desta aula é o desacoplamento entre dado e comportamento. Até a Semana 5, cada Actor interativo carregava sua própria lógica de reação — o que é adequado para comportamento, mas problemático para dado: se "quantidade de vida que uma poção restaura" ou "nome de exibição de um item" estivesem fixados dentro do Blueprint do próprio item, qualquer ajuste de design exigiria abrir e editar Blueprints individualmente, e nenhum sistema (como um futuro Inventário, na Semana 10) poderia consultar esses dados de forma genérica. Toda engine madura precisa de uma camada de dados que exista independentemente da lógica que a consome. A Unreal resolve isso com Data Tables — uma estrutura tabular, editável como planilha, onde cada linha é uma instância de dado — e com Data Assets, quando o dado não se organiza bem em linhas e colunas (por exemplo, um dado único e complexo). Nesta aula, o foco é a Data Table, por ser a ferramenta correta para uma coleção de itens com os mesmos atributos.

## Recursos da Unreal

Data Tables, Data Assets, `BPI_Interactable` e Event Dispatcher (retomados da Semana 5), subpasta `Data/DataTables/`.

## Comparação com Unity

ScriptableObject resolve o mesmo problema de dado desacoplado da lógica, mas por um caminho arquitetural diferente: cada instância de ScriptableObject é um asset independente, e uma coleção de itens normalmente exige que o desenvolvedor organize manualmente uma lista ou array desses assets. A Data Table da Unreal já nasce orientada a coleção — é uma única planilha com uma linha por item, o que a torna mais direta para dados homogêneos em grande quantidade, enquanto o ScriptableObject é mais direto para um dado único e complexo com lógica própria embutida. O princípio — dado como asset, não como variável hardcoded em um Blueprint — é o mesmo nas duas engines. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `BPI_Interactable` e o objeto interativo da Semana 5 funcionais.
- Uma `DT_Items` de exemplo pré-configurada (fora da visão da turma), com duas ou três linhas de itens simples, para demonstração.
- Slides com o diagrama Data Table (coleção tabular) × Data Asset (instância independente), reforçando quando usar cada uma.
- PROJECT_ARCHITECTURE.md disponível para reforçar a convenção `DT_` e a subpasta `Data/DataTables/`.
- **Nota de contingência:** este encontro é compressível em até 20 minutos caso necessário, já que a Data Table é retomada e aprofundada no Encontro 2 com Struct/Enum — a introdução pode ser reduzida sem perda estrutural.

## Cronograma do Encontro

- 15 min — Revisão do objeto interativo da Semana 5 (`BPI_Interactable` + Event Dispatcher).
- 20 min — Fundamentação: Data Tables e Data Assets como separação entre dado e lógica.
- 35 min — Demonstração: criação guiada de `DT_Items` com colunas básicas (nome, descrição, ícone).
- 50 min — Laboratório: cada grupo cria sua própria `DT_Items` na subpasta `Data/DataTables/`.
- 15 min — Feedback: verificação da estrutura e nomenclatura da tabela de cada grupo.

## Desenvolvimento

O encontro parte da constatação de que o objeto interativo da Semana 5 já reage a uma ação do jogador, mas não carrega nenhuma informação estruturada sobre o que está sendo coletado ou ativado. O professor demonstra a criação de `DT_Items` a partir de uma estrutura de linha simples (ainda sem Struct customizado, usando o tipo padrão do editor), populando duas ou três linhas de exemplo, e explica por que essa tabela deve existir de forma independente de qualquer Actor específico. Cada grupo replica o processo, criando sua própria `DT_Items` na subpasta `Data/DataTables/`, preparando o terreno para a tipagem via Struct e Enum que será construída no Encontro 2.

## Desafio

Não há desafio de liberdade de solução neste encontro — a criação da tabela é demonstração e adaptação guiada, preparando a base de dados para o desafio do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir `DT_Items` criada na subpasta `Data/DataTables/`, com nomenclatura conforme a convenção `DT_` de PROJECT_ARCHITECTURE.md e ao menos uma linha de exemplo preenchida.

## Evidências para Avaliação

Organização e nomenclatura de `DT_Items` conforme PROJECT_ARCHITECTURE.md (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Preparação).

## Dificuldades Esperadas

Estudantes podem tentar recriar a mesma informação em variáveis individuais dentro do Actor de coleta, em vez de centralizar na Data Table, por familiaridade com abordagens anteriores da disciplina. Intervenção: perguntar "se este mesmo item aparecer em três baús diferentes do nível, quantos lugares precisariam ser editados na sua solução atual?"; se a resposta for mais de um, reforçar que o dado pertence à tabela, não ao Actor. Grupos com dificuldade para definir as colunas iniciais devem receber sugestão direta do professor (nome, descrição, ícone) para não atrasar o Encontro 2.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Structs e Enums como organizadores de dados tipados dentro de uma Data Table.
- Modelar `S_ItemData` e `E_ItemType` e aplicá-los a `DT_Items`.
- Implementar um conjunto próprio de itens coletáveis aplicado a um Actor de coleta que reutiliza `BPI_Interactable` e Event Dispatcher.

## Conteúdos

- Structs: agrupamento de campos tipados relacionados a uma mesma entidade de dado.
- Enums: conjunto fechado e nomeado de categorias possíveis para um campo.
- Aplicação de `S_ItemData` e `E_ItemType` a `DT_Items`.
- Desafio: modelagem de itens coletáveis próprios (baús, moedas, recursos) aplicados a um Actor de coleta do Vertical Slice.

## Conceitos Fundamentais

O conceito universal desta aula complementa o do Encontro 1: se a Data Table resolve "onde o dado mora", o Struct e o Enum resolvem "que forma esse dado deve ter". Sem tipagem, cada linha da tabela poderia receber qualquer valor em qualquer campo, e categorias como "tipo de item" ficariam sujeitas a erro de digitação (texto livre em vez de uma opção fechada). Um Struct agrupa campos relacionados sob um único tipo nomeado (por exemplo, `S_ItemData` reunindo nome, descrição, ícone e valor), tornando a Data Table fortemente tipada linha a linha. Um Enum restringe um campo a um conjunto fechado e nomeado de opções (por exemplo, `E_ItemType` com valores como Consumível, Chave ou Recurso), eliminando ambiguidade e permitindo que sistemas futuros (como o Inventário, na Semana 10) tomem decisões com base na categoria, não em texto livre. Isso é o que transforma `DT_Items` de uma planilha solta em uma estrutura de dados confiável para o restante do projeto.

## Recursos da Unreal

Structs, Enums, `DT_Items` (do Encontro 1), `BPI_Interactable` e Event Dispatcher (da Semana 5).

## Comparação com Unity

A Unity resolve o mesmo problema de tipagem com classes serializáveis (`[System.Serializable] class`) para o equivalente de um Struct, e com `enum` da própria linguagem C# para o equivalente de um Enum — o princípio de restringir a forma e as opções válidas de um dado é idêntico. A diferença arquitetural está na integração com a ferramenta de edição: na Unreal, o Struct definido em Blueprint já gera automaticamente as colunas correspondentes na Data Table e é editável nativamente no Data Table Editor, enquanto na Unity a exibição de uma classe serializável ou de um enum dentro do Inspector depende de como o campo é declarado e, em alguns casos, de atributos adicionais para aparecer de forma equivalente. O princípio — tipagem forte de dados de design — é o mesmo nas duas engines. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `DT_Items` do Encontro 1 criada.
- Um `S_ItemData` e um `E_ItemType` de exemplo pré-configurados (fora da visão da turma), aplicados à Data Table de demonstração.
- Slides com o diagrama Struct (forma do dado) × Enum (categorias fechadas) × Data Table (coleção de instâncias desse dado).
- Modelo de Checkpoint de progresso (conforme Sistema de Avaliação, Rubrica 3 — Checkpoints) pronto para uso ao final do encontro.
- PROJECT_ARCHITECTURE.md disponível para reforçar as convenções `S_`/`E_`, o Actor `BP_Chest`/`BP_Pickup` como candidato ao desafio, e a subpasta `Data/Structs_Enums/`.

## Cronograma do Encontro

- 10 min — Revisão de `DT_Items` do Encontro 1.
- 15 min — Fundamentação: Structs e Enums como organizadores tipados de dado.
- 35 min — Demonstração: criação guiada de `S_ItemData` e `E_ItemType`, aplicados a `DT_Items`.
- 50 min — Laboratório: cada grupo modela seu conjunto de itens coletáveis e aplica a um Actor de coleta reutilizando `BPI_Interactable` e Event Dispatcher.
- 25 min — Desafio + Checkpoint: apresentação do progresso de cada grupo e registro formal do Checkpoint do Módulo 2.

## Desenvolvimento

O encontro continua diretamente do Encontro 1: agora que `DT_Items` existe, falta garantir que cada linha dessa tabela tenha uma forma confiável. O professor cria `S_ItemData` com campos tipados (nome, descrição, ícone, valor) e `E_ItemType` com categorias fechadas (Consumível, Chave, Recurso), aplica o Struct como tipo de linha de `DT_Items` e popula a tabela de demonstração com itens tipados. Em seguida, conecta essa tabela a um Actor de coleta que já implementa `BPI_Interactable` (reaproveitando o padrão da Semana 5): ao ser interagido, o Actor consulta uma linha da tabela pelo identificador do item e dispara o Event Dispatcher correspondente, sinalizando a coleta. Cada grupo aplica o mesmo padrão ao seu próprio conjunto de itens, escolhendo livremente as categorias e atributos, mas reutilizando obrigatoriamente `BPI_Interactable` e o Event Dispatcher já construídos.

## Desafio

Cada grupo modela seu próprio conjunto de itens coletáveis (baús, moedas, recursos ou outra categoria própria) usando `DT_Items` tipada por `S_ItemData` e `E_ItemType`, com liberdade sobre categorias e atributos, desde que o Actor de coleta reutilize `BPI_Interactable` e o Event Dispatcher da Semana 5 para sinalizar a coleta.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir `DT_Items` tipada por `S_ItemData` e `E_ItemType`, populada com seu próprio conjunto de itens, e um Actor de coleta funcional no nível de teste que consulta essa tabela ao ser interagido, com nomenclatura conforme PROJECT_ARCHITECTURE.md.

## Evidências para Avaliação

Funcionamento demonstrável da consulta à Data Table a partir do Actor de coleta, correção da tipagem via Struct e Enum, e organização/nomenclatura conforme PROJECT_ARCHITECTURE.md — registrados no instrumento de Checkpoint de progresso do Módulo 2, conforme Sistema de Avaliação (Rubrica 3 — Checkpoints, critérios Funcionalidades implementadas e Estabilidade).

## Dificuldades Esperadas

Estudantes podem criar campos redundantes ou não tipados na Data Table (por exemplo, texto livre para categoria em vez de usar `E_ItemType`), reproduzindo o mesmo problema que o Enum resolve. Intervenção: perguntar "se outro estudante do grupo digitar a categoria de forma ligeiramente diferente na próxima linha, o sistema perceberia isso como um erro?"; se a resposta for não, reforçar que qualquer campo de opções fechadas deve ser Enum, nunca texto livre. Grupos que não concluírem a integração completa entre Data Table e Actor de coleta a tempo devem registrar a tabela tipada como pendência no Checkpoint, sem impedir o registro do progresso já alcançado.

---

# Resultado Esperado da Semana

Ao final da Semana 6, cada grupo deve possuir `DT_Items` funcional, tipada por `S_ItemData` e `E_ItemType`, populada com um conjunto próprio de itens coletáveis, e um Actor de coleta integrado ao Vertical Slice que reutiliza `BPI_Interactable` e o Event Dispatcher da Semana 5 para sinalizar a coleta de um item. Conceitualmente, a turma deve dominar a separação entre dado de design (Data Table, Struct, Enum) e lógica de gameplay (Interface, Event Dispatcher) como dois problemas distintos e complementares de arquitetura de motores. O Checkpoint de progresso do Módulo 2 formaliza esse ponto de controle antes do encerramento da Unidade II na Semana 7.

# Preparação para a Próxima Semana

A Semana 7 depende diretamente de `DT_Items` e do Actor de coleta consolidados nesta semana: o SaveGame Object introduzido na Semana 7 precisará serializar exatamente o estado de progresso construído até aqui — quais itens da `DT_Items` já foram coletados por cada grupo. A Semana 7 também integra, em um único fluxo jogável, todos os sistemas construídos desde a Semana 4 (GameMode, GameState, PlayerController, GameInstance, Interfaces, Event Dispatchers, Data Tables, Structs, Enums), encerrando a Unidade II com Code Review e Playtest coletivo.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Gameplay Framework in Unreal Engine (Data Assets e Data Tables). Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Data Tables, Structs e Enums. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — ScriptableObject, classes serializáveis e enums em C#, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Data Tables e Structs; **Mathew Wadstein**, para explicações pontuais de WTF Is? Data Table e Struct.
