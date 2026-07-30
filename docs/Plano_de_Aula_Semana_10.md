# Semana 10 🔵

## Introdução da Semana

A Semana 10 dá continuidade à Unidade III — Resolver Problemas, mantendo a metodologia de Challenge Based Learning já consolidada nas Semanas 8 e 9: o professor apresenta o problema, cada grupo propõe a própria solução, com autonomia média. O eixo conceitual da semana é a estruturação de dados coletados ao longo do jogo em um sistema de Inventário, e a retomada do Interaction System introduzido na Semana 5 para suportar múltiplos tipos de interação conectados a esse inventário. O Encontro 1 introduz padrões de Inventory System (armazenamento, adição/remoção, exibição), reutilizando diretamente os itens já modelados em `DT_Items` (Data Table + Struct + Enum) na Semana 6; o Encontro 2 retoma o `InteractionComponent` e a interface `BPI_Interactable` da Semana 5, ampliando-os para responder de forma diferenciada a múltiplos tipos de interação (coletar, usar, descartar) conectados ao inventário recém-construído. Nenhum sistema dos Módulos 1 e 2 é descartado: `DT_Items`, `BPI_Interactable`, `InteractionComponent` e o `WBP_HUD` da Semana 9 são todos reutilizados e ampliados, não recriados. A semana encerra com Code Review dos sistemas de inventário e interação, conforme previsto no Sistema de Avaliação.

## Objetivos Gerais

- Compreender padrões universais de Inventory System (armazenamento, adição/remoção, exibição) como problema recorrente em qualquer engine.
- Estruturar um `InventoryComponent` funcional, reutilizando os itens já modelados em `DT_Items` na Semana 6.
- Retomar e ampliar o `InteractionComponent` e a interface `BPI_Interactable` da Semana 5 para suportar múltiplos tipos de interação.
- Conectar o Interaction System ao Inventário (coletar, usar, descartar), propondo, com autonomia própria, um novo tipo de interação.

## Resultados Esperados

Ao final da semana, cada grupo terá um `InventoryComponent` funcional, armazenando e exibindo os itens definidos em `DT_Items`, conectado a um `InteractionComponent` ampliado capaz de responder a múltiplos tipos de interação (ao menos coletar e um segundo tipo proposto pelo grupo), sem substituir nenhum sistema construído nos Módulos 1 e 2.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar padrões universais de Inventory System — armazenamento, adição/remoção e exibição de itens.
- Comparar a estruturação de inventário na Unreal (Data Assets/Data Tables + Component) com o equivalente em Unity (ScriptableObjects + MonoBehaviour).
- Estruturar um `InventoryComponent` inicial, reutilizando os itens modelados em `DT_Items` na Semana 6.

## Conteúdos

- Inventory System como problema universal: onde armazenar os itens, como adicionar/remover, como expor o estado para exibição.
- `InventoryComponent` como Component dedicado ao armazenamento, seguindo o mesmo padrão de composição já usado por `HealthComponent` e `InteractionComponent`.
- Reutilização de `DT_Items` (Data Table + Struct + Enum, Semana 6) como fonte de dados dos itens armazenáveis.

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre o dado do item (o que ele é — nome, tipo, atributos, já modelado em `DT_Items` na Semana 6) e o estado de posse do item (quais itens, e em que quantidade, um jogador possui em determinado momento). Um Inventory System não redefine o que é um item; ele apenas gerencia uma coleção de referências a itens já definidos, com operações de adicionar, remover e consultar. A Unreal resolve isso com um `InventoryComponent`, seguindo exatamente o mesmo padrão arquitetural de composição já ensinado com `HealthComponent` (Semana 8) e `InteractionComponent` (Semana 5): um Component isolado, anexado ao `BP_Player`, que mantém uma coleção interna (Array ou Map) de referências às linhas de `DT_Items`, expondo funções de adicionar, remover e consultar itens sem que o restante do projeto precise conhecer a estrutura interna dessa coleção. Este é o quarto Component construído pela turma seguindo o mesmo princípio de encapsulamento (depois de `InteractionComponent`, `SaveComponent` e `HealthComponent`) — o padrão já deve ser reconhecível pelos grupos, o que permite maior autonomia na implementação.

## Recursos da Unreal

Components, `DT_Items` (retomado da Semana 6), Arrays/Maps de Blueprint, `InventoryComponent` (novo).

## Comparação com Unity

A Unity resolve o mesmo problema tipicamente com um `MonoBehaviour` de inventário anexado ao jogador, mantendo uma `List<T>` ou `Dictionary` de referências a `ScriptableObjects` de item — os `ScriptableObjects` cumprindo o mesmo papel do `DT_Items`, como dado de item desacoplado da lógica. O princípio é idêntico nas duas engines: o Component/script de inventário nunca redefine o que é um item, apenas gerencia posse e quantidade de itens já definidos em outro lugar. A diferença está na estrutura de dados de origem — Data Table (linhas tipadas por Struct) na Unreal versus um asset por item (ScriptableObject) na Unity — mas o padrão de composição do inventário como Component/script isolado é o mesmo. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `DT_Items` funcional (Semana 6) e `HealthComponent`/`InteractionComponent`/`WBP_HUD` consolidados.
- Um `InventoryComponent` de exemplo pré-configurado (fora da visão da turma), com função de adicionar item por referência a uma linha de `DT_Items` e um Array interno de itens possuídos.
- Slides com o diagrama Item (dado em `DT_Items`) → posse (`InventoryComponent`) → exibição (`WBP_HUD`/`WBP_Inventory`), reforçando a separação de responsabilidades.
- REFERENCES.md e documentação de Gameplay Framework (Data Assets aplicados a inventário) disponíveis para consulta durante o laboratório.
- **Nota de contingência:** este é o primeiro encontro da semana e alimenta diretamente o Encontro 2 (ampliação da interação); não é compressível sem prejudicar a fundamentação — caso falte tempo, priorizar a função de adicionar item sobre a de remover/descartar, que pode ser retomada no início do Encontro 2.

## Cronograma do Encontro

- 15 min — Revisão do estado atual de `DT_Items` (Semana 6) e do `InteractionComponent` (Semana 5).
- 20 min — Fundamentação: padrões universais de Inventory System (armazenamento, adição/remoção, exibição) e o papel do `InventoryComponent` como Component dedicado.
- 35 min — Demonstração: criação guiada de um `InventoryComponent` com função de adicionar item por referência a `DT_Items` e Array interno de itens possuídos.
- 50 min — Laboratório: cada grupo estrutura seu próprio `InventoryComponent`, reutilizando os itens já modelados na Semana 6, e implementa adição e remoção básica.
- 15 min — Feedback: verificação do armazenamento e da consulta de itens em cada grupo.

## Desenvolvimento

O encontro parte da constatação de que os itens já estão modelados em `DT_Items` desde a Semana 6, mas nenhum sistema registra quais itens o jogador possui. O professor demonstra a criação de um `InventoryComponent`, com uma coleção interna de itens possuídos e uma função de adicionar item por referência a uma linha de `DT_Items`. Cada grupo replica o processo em seu próprio projeto, estruturando seu `InventoryComponent` e validando que itens podem ser adicionados e consultados, preparando a conexão com o Interaction System no Encontro 2.

## Desafio

Não há desafio de liberdade de solução neste encontro — a estruturação do `InventoryComponent` é demonstração e adaptação guiada, preparando o desafio de maior autonomia do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um `InventoryComponent` funcional, capaz de armazenar e consultar itens referenciados em `DT_Items`, sem alterar a lógica de nenhum sistema anterior.

## Evidências para Avaliação

Funcionamento demonstrável do armazenamento e organização/nomenclatura do `InventoryComponent` conforme boas práticas da Unreal 5.6 e do PROJECT_ARCHITECTURE.md (prefixo de Component consistente com `HealthComponent`/`InteractionComponent`) — insumo observado para o Code Review do Encontro 2 (Rubrica 4 — Code Review, critérios Nomenclatura e Reutilização).

## Dificuldades Esperadas

Estudantes podem tentar recriar os dados dos itens diretamente dentro do `InventoryComponent` (duplicando atributos já definidos em `DT_Items`), em vez de armazenar apenas referências. Intervenção: perguntar "se um item mudar de nome ou de dano no `DT_Items`, quantos lugares do projeto precisariam ser atualizados manualmente?" e reforçar que o inventário guarda posse, não a definição do item. Grupos com dificuldade para referenciar uma linha de Data Table a partir do Component devem ser direcionados à documentação oficial antes de receber a resposta direta.

---

# Encontro 2

## Objetivos de Aprendizagem

- Retomar e ampliar o `InteractionComponent` e a interface `BPI_Interactable` da Semana 5 para suportar múltiplos tipos de interação.
- Conectar o Interaction System ao `InventoryComponent` (coletar, usar, descartar).
- Propor e implementar, com autonomia própria, um novo tipo de interação conectado ao inventário.

## Conteúdos

- Retomada do `InteractionComponent` e de `BPI_Interactable` (Semana 5): detecção e comunicação desacoplada.
- Ampliação da interação para múltiplos tipos de resposta (coletar, usar, descartar), em vez de uma única reação genérica.
- Desafio: expansão do sistema de interação para um novo tipo (empilhar, combinar ou interação com cooldown), conectado ao inventário.

## Conceitos Fundamentais

O conceito universal desta aula é a evolução de um sistema de comunicação desacoplada de uma única reação genérica para múltiplas reações diferenciadas por tipo. Na Semana 5, o `InteractionComponent` detectava um objeto interativo e disparava uma única chamada via `BPI_Interactable`, com cada Actor definindo sua própria reação (abrir porta, acionar alavanca). Nesta semana, o mesmo padrão arquitetural é reaproveitado, mas o problema muda: agora a interação precisa distinguir tipos de resposta — coletar um item (adicioná-lo ao `InventoryComponent`), usar um item (aplicar seu efeito) e descartar um item (removê-lo do inventário e devolvê-lo ao mundo) — sem que o `InteractionComponent` precise conhecer os detalhes internos de cada um desses casos. O princípio de desacoplamento ensinado na Semana 5 não muda; o que muda é a granularidade da resposta, permanecendo a interface `BPI_Interactable` como ponto único de comunicação entre `InteractionComponent` e qualquer objeto do mundo, agora incluindo objetos coletáveis que dialogam diretamente com o `InventoryComponent`.

## Recursos da Unreal

`InteractionComponent`, `BPI_Interactable`, Event Dispatchers (retomados da Semana 5), `InventoryComponent` (do Encontro 1).

## Comparação com Unity

A Unity resolveria a ampliação do mesmo modo que resolveu a interação básica na Semana 5 — por meio de uma interface C# (equivalente a `BPI_Interactable`) implementada por diferentes componentes de objeto interativo, com um script central de interação (equivalente ao `InteractionComponent`) detectando e chamando o método da interface. A distinção entre múltiplos tipos de interação normalmente é resolvida por parâmetros do método da interface (por exemplo, um enum de tipo de interação) ou por múltiplas interfaces especializadas, escolha que também está disponível na Unreal através de `BPI_Interactable` com parâmetros ou de interfaces adicionais. O princípio de comunicação desacoplada permanece idêntico nas duas engines; a decisão de design (um método genérico parametrizado versus múltiplas interfaces) é a mesma decisão que um estúdio enfrentaria em qualquer engine. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `InventoryComponent` funcional do Encontro 1 e `InteractionComponent`/`BPI_Interactable` consolidados da Semana 5.
- Um exemplo pré-configurado (fora da visão da turma) de um `BP_Pickup` que implementa `BPI_Interactable` e, ao ser interagido, adiciona seu item ao `InventoryComponent` do jogador.
- Levantamento prévio, por grupo, de quais Actors interativos já existem no projeto (porta, alavanca, baú da Semana 6/7), para orientar o feedback sem indicar a solução do desafio.
- Enunciado do desafio redigido de forma aberta, sem indicar qual novo tipo de interação implementar, para preservar a decisão do grupo.
- REFERENCES.md e documentação de Gameplay Framework (Data Assets aplicados a inventário) disponíveis para consulta durante o laboratório e o desafio.
- Modelo de Avaliação — Code Review (Sistema de Avaliação) pronto para uso ao final do encontro.
- **Nota de contingência:** o desafio é o núcleo do encontro e não deve ser comprimido; se necessário, reduzir o tempo de demonstração da coleta conectada ao inventário, mantendo intacto o tempo de laboratório do desafio e o Code Review final.

## Cronograma do Encontro

- 15 min — Revisão do `InventoryComponent` construído no Encontro 1 e do `InteractionComponent`/`BPI_Interactable` da Semana 5.
- 20 min — Fundamentação: ampliação da interação para múltiplos tipos de resposta (coletar, usar, descartar), reaproveitando o padrão de desacoplamento já conhecido.
- 25 min — Demonstração: conexão guiada entre um Actor interativo (`BP_Pickup`) e o `InventoryComponent`, implementando a interação de coletar.
- 15 min — Apresentação do desafio: cada grupo expande seu sistema de interação para suportar um novo tipo (empilhar itens, combinar itens ou interação com cooldown).
- 45 min — Laboratório do desafio: cada grupo implementa sua própria solução de ampliação da interação.
- 15 min — Desafio + Code Review: cada grupo apresenta sua solução e recebe Code Review formal dos sistemas de inventário e interação.

## Desenvolvimento

O professor demonstra a conexão entre um Actor interativo existente (`BP_Pickup`) e o `InventoryComponent`, implementando a interação de coletar: ao interagir, o `BP_Pickup` chama `BPI_Interactable`, o `InteractionComponent` do jogador recebe o evento, e o item é adicionado ao `InventoryComponent`. Feita a demonstração, o professor apresenta o desafio: cada grupo deve expandir seu sistema de interação para suportar um novo tipo de interação além de coletar — empilhar itens do mesmo tipo, combinar itens diferentes em um novo item, ou uma interação com tempo de espera (cooldown) antes de poder ser repetida — conectada ao `InventoryComponent` já existente, propondo a própria solução técnica.

## Desafio

Cada grupo expande seu sistema de interação para suportar um novo tipo de interação (empilhar itens, combinar itens ou interação com cooldown), conectado ao `InventoryComponent`, com solução própria, e apresenta a solução ao final do encontro para o Code Review.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um `InteractionComponent` ampliado, suportando ao menos coletar e um segundo tipo de interação conectados ao `InventoryComponent`, sem alterar a lógica de nenhum sistema do Módulo 2, com organização e nomenclatura adequadas para o Code Review.

## Evidências para Avaliação

Funcionamento demonstrável da coleta e do novo tipo de interação, e avaliação formal via Rubrica 4 — Code Review (Organização dos Blueprints, Nomenclatura, Modularidade, Reutilização, Comunicação entre sistemas, Boas práticas gerais), aplicada aos sistemas de inventário e interação conforme Sistema de Avaliação (Semana 10).

## Dificuldades Esperadas

Grupos podem tentar resolver o novo tipo de interação com referências diretas (`Cast to`) entre o Actor interativo e o `InventoryComponent`, contornando `BPI_Interactable`. Intervenção: perguntar "se amanhã existir um segundo tipo de objeto coletável totalmente diferente, o `InteractionComponent` precisaria conhecer os dois?" e reforçar que a interface deve continuar sendo o único ponto de contato, exatamente como ensinado na Semana 5. Grupos que travarem na lógica de empilhar ou combinar itens devem ser direcionados à documentação oficial antes de receber apoio direto do professor, preservando a autonomia média esperada no Módulo 3. Durante o Code Review, é comum encontrar duplicação de lógica entre os diferentes tipos de interação (coletar, usar, descartar) — priorizar feedback sobre modularização dessas funções, conforme orientação do Sistema de Avaliação para o Code Review.

---

# Resultado Esperado da Semana

Ao final da Semana 10, cada grupo terá um `InventoryComponent` funcional, armazenando e exibindo os itens definidos em `DT_Items` (Semana 6), conectado a um `InteractionComponent` ampliado que suporta múltiplos tipos de interação (coletar e ao menos um tipo adicional proposto pelo grupo — empilhar, combinar ou cooldown), tudo comunicado através de `BPI_Interactable`, sem substituir nenhum sistema anterior. Conceitualmente, a turma deve dominar a distinção entre dado de item (`DT_Items`), posse de item (`InventoryComponent`) e comunicação de interação (`BPI_Interactable`/`InteractionComponent`), e deve ter recebido Code Review formal desses dois sistemas, terceira aplicação da Rubrica 4 no semestre (após a Semana 7).

# Preparação para a Próxima Semana

A Semana 11 introduz Navigation, Behavior Trees e Blackboards, encerrando a Unidade III com a entrega do Vertical Slice jogável do Módulo 3 — animação, interface, inventário, interação ampliada e IA integrados —, seguido de Playtest coletivo e Showcase. O `InventoryComponent` e a interação ampliada construídos nesta semana servirão de contexto para o comportamento autônomo de NPCs (por exemplo, reagir à proximidade do jogador ou a itens específicos), e o padrão de comunicação desacoplada via `BPI_Interactable`/Event Dispatchers será reaproveitado na integração entre IA e os demais sistemas do Vertical Slice.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Gameplay Framework in Unreal Engine (Data Assets aplicados a inventário). Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Data Assets, Data Tables e padrões de inventário. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — ScriptableObjects e padrões de inventário, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Data Assets e inventário; **Mathew Wadstein**, para explicações pontuais de WTF Is? Data Table e Struct; **PrismaticaDev**, para exemplos aplicados de sistemas de inventário.
