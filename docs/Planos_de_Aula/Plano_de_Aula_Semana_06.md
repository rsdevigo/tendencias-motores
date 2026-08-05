# Semana 6 — Resource customizado (ItemData) e Enums

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7) | **Metodologia:** Studio Based Learning — professor demonstra, aluno adapta. Autonomia baixa.

## Introdução da Semana

A Semana 5 encerrou com o contrato `Interactable` e Signals sustentando pelo menos um objeto interativo funcional (porta, alavanca ou equivalente) em cada grupo. Esta semana mantém o projeto intacto e resolve um problema diferente: onde vivem os dados de um item de jogo — nome, ícone, valor, categoria — sem misturá-los à lógica que os manipula. A resposta é o Resource customizado `ItemData`, complementado por Enums para tipar categorias. O par sustentará todo item do Vertical Slice até a ampliação do Inventário na Semana 10.

## Objetivos Gerais

- Compreender Resource customizado como estrutura de dados desacoplada da lógica de gameplay.
- Compreender Enums como organizadores de dados tipados dentro de um Resource.
- Modelar um conjunto de itens coletáveis do Vertical Slice usando `ItemData` + Enum.

## Resultados Esperados

Ao final da semana, cada grupo possui, além do `GameManager`, `SaveManager`, contrato `Interactable` e Signals herdados das Semanas 4 e 5, um Resource customizado `ItemData` com pelo menos um Enum de categoria, aplicado a um conjunto próprio de itens coletáveis do Vertical Slice — consolidando o Checkpoint de progresso do Módulo 2.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar Resource customizado como estrutura de dados desacoplada da lógica de gameplay.
- Diferenciar dado de design (Resource) de comportamento de gameplay (Node/script).
- Criar um Resource customizado (`ItemData`) para itens/entidades do projeto.

## Conteúdos

- O problema de misturar dados de design (nome, valor, ícone de um item) com a lógica que os manipula.
- Resource customizado no Godot (`class_name` estendendo `Resource`) como estrutura de dados serializável e reutilizável.
- Criação guiada de um Resource `ItemData` com campos exportados (`@export`).

## Conceitos Fundamentais

Toda engine de jogos com conteúdo além do mínimo precisa resolver o mesmo problema: como permitir que quem projeta o conteúdo (itens, inimigos, fases) trabalhe sem editar código a cada novo item. Se cada item coletável exigisse uma classe própria ou valores hardcoded no script do objeto, adicionar um item novo significaria mexer em lógica, não em dado. O Resource customizado resolve isso definindo uma estrutura de dados serializável, independente de qualquer Scene ou Node específico — o mesmo `ItemData` pode ser reutilizado por um baú, uma prateleira de loja ou um slot de inventário, todos lendo os mesmos campos sem duplicar a definição.

## Recursos do Godot

Resource customizado, `class_name`, `@export`, FileSystem Dock (arquivos `.tres`).

## Comparação com Unity

A Unity resolve o mesmo problema com `ScriptableObject` — um equivalente quase direto do Resource do Godot: ambos são estruturas de dados serializáveis, editáveis pelo Inspector, independentes de instância em cena. A diferença arquitetural relevante para a turma é sutil: no Godot, Resource é a mesma classe-base usada internamente por texturas, cenas e scripts, então customizar um Resource é estender um mecanismo já onipresente no motor; na Unity, `ScriptableObject` é uma classe-base separada, criada especificamente para esse padrão de dado-como-asset. O conceito universal — dado de design como asset independente de lógica — é idêntico nas duas engines.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 5, com contrato `Interactable` e Signals já implementados em pelo menos uma Scene por grupo.
- Script de referência do Resource `ItemData` (campos `nome`, `icone`, `valor` ou equivalente) já preparado para demonstração (não distribuído antes da aula).
- Slides com o comparativo Resource customizado (Godot) × `ScriptableObject` (Unity).
- Exemplos de arquivos `.tres` de itens já criados para mostrar o resultado final da demonstração.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 5 (objeto interativo com contrato `Interactable` + Signal) |
| 20 min | Introdução: o problema de misturar dado de design e lógica de gameplay |
| 35 min | Demonstração: criação do Resource `ItemData` e de instâncias `.tres` |
| 45 min | Laboratório: cada estudante cria seu próprio `ItemData` e ao menos duas instâncias de itens |
| 15 min | Desafio: adicionar um campo próprio ao `ItemData` não demonstrado em aula |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro retoma o projeto herdado da Semana 5 sem alterar o contrato `Interactable` ou os Signals já implementados, adicionando uma nova camada ao Vertical Slice: dados de item desacoplados de lógica. O professor demonstra a criação da classe `ItemData` estendendo `Resource`, com campos exportados básicos, e a instanciação de dois ou três itens como arquivos `.tres` distintos. A turma replica a criação da classe e modela suas próprias instâncias, preparando o terreno para a tipagem via Enum no Encontro 2.

## Desafio

Cada estudante adiciona ao próprio `ItemData` um campo não demonstrado em aula (por exemplo, peso, raridade ou descrição), mantendo a estrutura de Resource como ponto de entrada dos dados.

## Critérios de Sucesso

Cada estudante possui, ao final do encontro, uma classe `ItemData` (Resource customizado) definida e pelo menos duas instâncias `.tres` de itens distintos criadas a partir dela.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro. O `ItemData` construído aqui é pré-requisito direto do desafio avaliado (Checkpoint de progresso) do Encontro 2.

## Dificuldades Esperadas

- Colocar lógica de gameplay (ex.: efeito ao coletar) dentro do próprio `ItemData` em vez de em um script de comportamento — reforçar que o Resource guarda apenas dado, a reação pertence à Scene que o consome.
- Confundir a classe `ItemData` com uma instância `.tres` — reforçar que a classe define a estrutura e cada `.tres` é um dado concreto preenchido a partir dela.
- Esquecer de exportar (`@export`) os campos, tornando-os invisíveis no Inspector ao criar a instância — orientar verificação no Inspector antes de seguir para o próximo item.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Enums como organizadores de dados tipados dentro de um Resource.
- Diferenciar um campo tipado por Enum de um campo livre (string ou número mágico).
- Modelar um conjunto próprio de itens coletáveis usando `ItemData` + Enum.

## Conteúdos

- Enums como forma de restringir um campo a um conjunto fechado e nomeado de valores.
- Aplicação de um Enum de categoria (ex.: `Categoria { MOEDA, RECURSO, CHAVE }`) dentro do `ItemData`.
- Desafio: conjunto próprio de itens coletáveis (baús, moedas, recursos) usando `ItemData` + Enum.

## Conceitos Fundamentais

O `ItemData` do Encontro 1 resolve "onde vive o dado"; o Enum resolve um problema complementar: "como impedir que um campo de categoria aceite qualquer string digitada livremente, sujeita a erro de digitação ou inconsistência entre itens". Enums existem em praticamente toda linguagem de programação porque o mesmo problema — um conjunto fechado e conhecido de opções — aparece em qualquer domínio, não apenas em jogos. No Godot, um Enum é declarado dentro do script do Resource e passa a aparecer como um menu suspenso no Inspector, eliminando a possibilidade de um valor fora do conjunto esperado. Combinado ao `ItemData`, isso permite modelar categorias de item (moeda, recurso, chave) de forma tipada e consistente entre todas as instâncias do projeto.

## Recursos do Godot

Enums (`enum`), Resource customizado (`ItemData`), Inspector (menu suspenso gerado a partir do Enum).

## Comparação com Unity

A Unity resolve o mesmo padrão com `enum` de C#, aplicado a um campo público ou `[SerializeField]` de um `ScriptableObject` — mecanismo praticamente idêntico ao do Godot: declaração de um conjunto fechado de valores nomeados, exposto no Inspector como menu suspenso. A diferença relevante para a turma não está no conceito, mas em GDScript tratar Enums como valores inteiros nomeados dentro do próprio script, sem a necessidade de um arquivo de definição separado — o C# permite (mas não exige) declarar o `enum` fora da classe que o usa. O conceito universal — restringir um campo a um conjunto fechado e nomeado de opções — é idêntico nas duas engines.

## Preparação do Professor

- Projeto de demonstração com a classe `ItemData` do Encontro 1 já criada e com instâncias de exemplo.
- Script de referência de um Enum de categoria já preparado para demonstração, aplicado ao campo de categoria do `ItemData`.
- Slides com o comparativo Enum (Godot/GDScript) × `enum` (Unity/C#).
- Conjunto de referência de 3 a 4 categorias de item sugeridas (moeda, recurso, chave, consumível) para orientar o desafio dos grupos.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 1 (`ItemData` criado e instâncias `.tres` de itens) |
| 20 min | Introdução: Enums como organizadores de um conjunto fechado de valores |
| 35 min | Demonstração: declaração de um Enum de categoria e aplicação ao `ItemData` |
| 50 min | Laboratório e Desafio: cada grupo modela seu próprio conjunto de itens coletáveis (baús, moedas, recursos) usando `ItemData` + Enum, com liberdade de categorias e atributos |
| 20 min | Checkpoint de progresso do Módulo 2 — apresentação rápida dos conjuntos de itens de cada grupo |

## Desenvolvimento

O encontro completa a semana conectando o `ItemData` do Encontro 1 a um Enum de categoria. O professor demonstra a declaração do Enum dentro do script do Resource e sua aplicação ao campo de categoria, mostrando o menu suspenso resultante no Inspector. Em seguida, cada grupo modela seu próprio conjunto de itens coletáveis — baús, moedas, recursos ou equivalente escolhido pelo grupo — combinando `ItemData` e Enum, com liberdade para definir categorias e atributos adicionais. O encontro fecha com o Checkpoint de progresso do Módulo 2, em que cada grupo apresenta rapidamente seu conjunto de itens.

## Desafio

Cada grupo modela seu próprio conjunto de itens coletáveis (baús, moedas, recursos ou equivalente) usando `ItemData` + Enum, com liberdade de categorias e atributos. **Entrega: Checkpoint de progresso** do Módulo 2.

## Critérios de Sucesso

Cada grupo possui, ao final da semana, uma classe `ItemData` com pelo menos um Enum de categoria e um conjunto de três ou mais instâncias de itens distintos, coerentes com o tema do próprio Vertical Slice.

## Evidências para Avaliação

Checkpoint de progresso do Módulo 2 — verificação do `ItemData` com Enum de categoria aplicado a um conjunto de itens coletáveis. Não substitui a Rubrica formal, mas compõe a base avaliada no Code Review de encerramento do Módulo 2 (Semana 7).

## Dificuldades Esperadas

- Usar uma string livre em vez do Enum para representar a categoria, reintroduzindo o risco de inconsistência que o Enum existe para evitar — reforçar que toda categoria fechada e conhecida de antemão deve ser um Enum, não uma string.
- Criar um Enum excessivamente granular (uma categoria por item individual) em vez de um conjunto pequeno e reutilizável de categorias — orientar a pensar em categorias, não em identificadores únicos.
- Esquecer de salvar as instâncias `.tres` no FileSystem do projeto antes de encerrar o laboratório, perdendo o trabalho ao fechar a cena — orientar salvamento explícito de cada instância criada.

---

# Resultado Esperado da Semana

Ao final da Semana 6, cada grupo possui, sobre o projeto herdado das Semanas 4 e 5, uma classe `ItemData` (Resource customizado) com pelo menos um Enum de categoria, aplicada a um conjunto próprio de itens coletáveis do Vertical Slice (baús, moedas, recursos ou equivalente). A turma domina Resource customizado como estrutura de dados desacoplada da lógica e Enums como organizadores de dados tipados, relaciona os dois ao equivalente da Unity (`ScriptableObject` e `enum` de C#), e passou pelo Checkpoint de progresso do Módulo 2.

# Preparação para a Próxima Semana

O `ItemData` e o Enum de categoria construídos nesta semana são pré-requisito direto da Semana 7, que introduz `SaveData` (Resource) + FileAccess para serializar e recuperar o estado de progresso do jogador, incluindo os itens coletados. A Semana 7 também integra, em um único fluxo jogável, todos os desafios do Módulo 2 (portas, baús, alavancas, `Checkpoint`), encerrando a Unidade II com Code Review e Playtest coletivo. O par `ItemData`/Enum também será retomado na ampliação do Inventário na Semana 10.

# Referências

- Godot Documentation — Resources: https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html
- Godot Documentation — GDScript (Enums): https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html#enums
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — ScriptableObjects: https://docs.unity3d.com/Manual/class-ScriptableObject.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
