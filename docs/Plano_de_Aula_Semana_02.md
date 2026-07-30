# Semana 2

## Introdução da Semana

A Semana 2 dá continuidade à Unidade I — Aprender a Ferramenta, aprofundando o desacoplamento entre o jogador e o mundo do Vertical Slice. Se a Semana 1 estabeleceu a unidade universal de composição (Actor e Component), esta semana responde a uma pergunta consequente: como uma engine desacopla a intenção do jogador (input) da ação executada no mundo? A turma configura o BP_Player como um Character controlável, dotado de locomoção via Character Movement Component, e conecta esse Character a um esquema de Enhanced Input.

A metodologia permanece Scaffolded Learning, coerente com o Módulo 1 e com a autonomia ainda muito baixa da turma — o professor demonstra, o aluno replica, com um primeiro grau de liberdade restrita apenas no desafio do Encontro 2.

## Objetivos Gerais

- Compreender a distinção entre Pawn e Character e o papel do Character Movement Component como sistema universal de locomoção.
- Configurar um Character controlável no nível de teste do Vertical Slice, a partir do Actor com Components construído na Semana 1.
- Compreender Enhanced Input (Input Actions, Input Mapping Contexts, Triggers, Modifiers) como camada de desacoplamento entre a intenção do jogador e a ação no mundo.
- Implementar movimentação e câmera controláveis via Enhanced Input, incluindo uma Input Action adicional proposta pelo próprio grupo.

## Resultados Esperados

Ao final da semana, cada grupo terá o BP_Player funcional: um Character que se move no nível de teste, controlado por um esquema de Enhanced Input configurado em aula, incluindo ao menos uma ação de input adicional implementada como desafio. O projeto ainda não possui sistemas de gameplay além de locomoção e câmera — o resultado permanece estrutural, preparando a base sobre a qual os módulos seguintes (framework de jogo, interação) serão construídos.

---

# Encontro 1

## Objetivos de Aprendizagem

- Distinguir Pawn de Character e justificar por que Character é uma especialização de Actor voltada a personagens controláveis.
- Explicar o papel do Character Movement Component como sistema universal de locomoção.
- Configurar um Character controlável no nível de teste do Vertical Slice.

## Conteúdos

- Character x Pawn como especializações de Actor.
- Character Movement Component como sistema universal de locomoção.
- Configuração guiada de um Character controlável no nível de teste.

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre a representação de um agente no mundo (Character) e o sistema que resolve sua física de locomoção (Movement Component). Pawn é a classe base de qualquer Actor possuível por um Controller; Character é uma especialização de Pawn que já embute um Character Movement Component pronto para resolver caminhada, corrida, salto e colisão com o solo, sem que o desenvolvedor precise reimplementar essa física do zero. Esse é o mesmo problema que toda engine de terceira pessoa precisa resolver — apenas o grau de solução pronta entregue por padrão varia entre motores. Compreender essa separação prepara a turma para reconhecer, na Semana 4, que GameMode e PlayerController lidam com regras e controle em um nível acima do Character.

## Recursos da Unreal

Character, Pawn, Character Movement Component, nível de teste do Vertical Slice.

## Comparação com Unity

O par Pawn/Character da Unreal não tem equivalente direto único na Unity: o mais próximo é a combinação de um GameObject com CharacterController ou Rigidbody mais um script de movimento próprio. A diferença arquitetural mais relevante é que a Unreal já entrega, por padrão, um Character Movement Component completo (caminhada, corrida, salto, natação, voo, resolução de colisão com rampas e degraus), enquanto a Unity normalmente exige compor essa solução a partir de peças mais genéricas (Rigidbody, CharacterController ou pacotes de terceiros). Não aprofundar mais que isso nesta aula — o ponto será retomado, se necessário, ao comparar a arquitetura completa na Unidade V.

## Preparação do Professor

- Projeto de cada grupo (criado na Semana 1) aberto, com o Actor com Components já implementado.
- Nível de teste (graybox simples) preparado com um piso e obstáculos mínimos para demonstrar locomoção.
- Um BP_Player de exemplo pré-configurado (fora da visão da turma), como subclasse de Character, para demonstração passo a passo.
- Slides com o diagrama Pawn → Character → Character Movement Component e a distinção destes em relação ao Actor da Semana 1.
- PROJECT_ARCHITECTURE.md disponível para reforçar que o BP_Player é o Blueprint central do projeto (seção 7).

## Cronograma do Encontro

- 15 min — Revisão do Actor com Components da Semana 1 e ponte conceitual para o Character.
- 20 min — Fundamentação: Pawn x Character, Character Movement Component como sistema universal de locomoção.
- 35 min — Demonstração: criação guiada do BP_Player como subclasse de Character, ajuste de parâmetros básicos de movimento.
- 50 min — Laboratório: cada grupo cria seu BP_Player e o posiciona controlável no nível de teste.
- 15 min — Feedback: verificação da movimentação básica de cada grupo e dúvidas sobre parâmetros do Character Movement Component.

## Desenvolvimento

O encontro parte do Actor com Components da Semana 1 e mostra por que um personagem controlável exige uma especialização própria (Character), em vez de um Actor genérico. O professor demonstra a criação do BP_Player como subclasse de Character, aponta o Character Movement Component já embutido e ajusta parâmetros simples (velocidade, altura de salto) para tornar a movimentação perceptível. Em seguida, cada grupo replica a criação do próprio BP_Player, posicionando-o no nível de teste e verificando a movimentação básica — ainda sem input customizado, usando o controle padrão do template, que será substituído por Enhanced Input no Encontro 2.

## Desafio

Não há desafio neste encontro — a configuração do BP_Player é demonstração e replicação guiada, coerente com a autonomia muito baixa do Módulo 1. O primeiro desafio da semana ocorre no Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve ter um BP_Player funcional como subclasse de Character, posicionado no nível de teste e capaz de se mover com o controle padrão, com parâmetros de movimento ajustados de forma perceptível em relação ao padrão do template.

## Evidências para Avaliação

Organização e nomenclatura do BP_Player conforme as convenções do PROJECT_ARCHITECTURE.md (Rubrica 1 — Desenvolvimento Semanal, critério Execução).

## Dificuldades Esperadas

Estudantes podem confundir Pawn e Character como sinônimos, ou tentar reimplementar movimentação manualmente em vez de utilizar o Character Movement Component já embutido. Intervenção: reforçar verbalmente que o Character já resolve esse problema por padrão, e redirecionar qualquer tentativa de reimplementação para o ajuste de parâmetros do Component existente.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Enhanced Input (Input Actions, Input Mapping Contexts, Triggers, Modifiers) como camada de desacoplamento entre a intenção do jogador e a ação no mundo.
- Configurar Enhanced Input para movimentação e câmera do BP_Player.
- Implementar uma nova Input Action não demonstrada em aula, com liberdade de solução.

## Conteúdos

- Enhanced Input: Input Actions, Input Mapping Contexts, Triggers e Modifiers.
- Comparação com o Input System da Unity.
- Configuração de Enhanced Input para movimentação e câmera.

## Conceitos Fundamentais

O conceito universal é o desacoplamento entre dispositivo físico e intenção de jogo. Uma Input Action representa uma intenção abstrata ("mover", "pular", "olhar"), independente de qual tecla, botão ou eixo de controle a aciona; um Input Mapping Context define o mapeamento concreto entre dispositivo e Input Action, podendo ser trocado ou combinado em tempo real; Triggers determinam quando um valor de input é considerado acionado (pressionado, mantido, duplo toque); Modifiers alteram o valor bruto do input antes de chegar à lógica de gameplay (inversão de eixo, zona morta, escala). Esse desacoplamento é o mesmo problema que qualquer sistema de input moderno precisa resolver, para que a lógica de gameplay nunca dependa diretamente de qual tecla ou botão foi pressionado.

## Recursos da Unreal

Enhanced Input, Input Actions, Input Mapping Contexts, Triggers, Modifiers.

## Comparação com Unity

Enhanced Input corresponde ao Input System (novo) da Unity: ambos abstraem o dispositivo físico em Actions e permitem múltiplos esquemas de controle combináveis. A diferença arquitetural mais relevante é que a Unreal organiza esses esquemas em Input Mapping Contexts que podem ser adicionados, removidos ou priorizados dinamicamente em runtime (por exemplo, trocar de esquema ao entrar em um veículo), enquanto a Unity resolve um problema equivalente por meio de Action Maps dentro de um único Input Actions Asset, ativados e desativados via código. Não aprofundar mais que isso — o objetivo é reconhecer a equivalência conceitual de desacoplamento, não decorar diferenças de configuração.

## Preparação do Professor

- Projeto de cada grupo com o BP_Player do Encontro 1 aberto e pronto para continuar.
- Input Actions e Input Mapping Context de exemplo pré-configurados (fora da visão da turma) para mover e olhar, para demonstração passo a passo.
- Slides com o diagrama dispositivo → Input Action → Input Mapping Context → lógica de gameplay, e a correspondência com Action Maps da Unity.
- Documentação oficial de Enhanced Input (REFERENCES.md) disponível para consulta durante o laboratório.

## Cronograma do Encontro

- 5 min — Revisão rápida do BP_Player do Encontro 1 e da movimentação padrão obtida.
- 15 min — Fundamentação: Input Actions, Input Mapping Contexts, Triggers e Modifiers.
- 35 min — Demonstração: criação guiada de Input Actions e Input Mapping Context para movimentação e câmera, conectados ao BP_Player.
- 45 min — Laboratório: cada grupo replica a configuração de Enhanced Input no próprio BP_Player.
- 20 min — Desafio: adicionar uma nova Input Action (correr, agachar ou pular) não demonstrada em aula.
- 15 min — Feedback: showcase rápido das ações implementadas e fechamento da semana.

## Desenvolvimento

O encontro retoma o BP_Player configurado no Encontro 1, ainda dependente do controle padrão do template, e substitui essa dependência por um esquema próprio de Enhanced Input. O professor demonstra a criação de Input Actions para movimentação e câmera, a montagem do Input Mapping Context correspondente e a conexão desses eventos à lógica de movimento do Character. Cada grupo replica essa configuração no próprio projeto, consolidando o desacoplamento entre dispositivo e intenção de jogo. O desafio final pede que cada grupo proponha e implemente uma nova Input Action de sua escolha, primeiro exercício de decisão técnica autônoma da disciplina, ainda em escopo estreito e seguro.

## Desafio

Adicionar uma nova Input Action não demonstrada em aula (correr, agachar ou pular), com liberdade de implementação quanto ao Trigger, ao Modifier utilizado e à forma como a ação se manifesta no BP_Player. Deve permitir diferentes soluções, sem gabarito único.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve ter o BP_Player controlável por um esquema próprio de Enhanced Input (movimentação e câmera), acrescido de ao menos uma Input Action adicional resultante do desafio, funcional no nível de teste.

## Evidências para Avaliação

Funcionamento do esquema de Enhanced Input e da Input Action adicional (Rubrica 1 — Desenvolvimento Semanal, critério Execução) e capacidade de propor uma solução própria diante de um desafio de liberdade restrita (Rubrica 2 — Desafios Técnicos, aplicável desde a Semana 2 conforme a Distribuição das Notas do Sistema de Avaliação).

## Dificuldades Esperadas

Estudantes podem confundir Input Action com a tecla física em si, tentando referenciar diretamente "tecla W" na lógica de gameplay em vez de mapear uma intenção abstrata. Intervenção: retomar verbalmente o princípio de desacoplamento antes de auxiliar tecnicamente, redirecionando para a criação de uma Input Action nomeada pela intenção (ex.: IA_Sprint), nunca pelo dispositivo.

---

# Resultado Esperado da Semana

Ao final da Semana 2, cada estudante/grupo deve possuir: um BP_Player funcional como subclasse de Character, controlável no nível de teste do Vertical Slice por um esquema próprio de Enhanced Input (movimentação e câmera), incluindo ao menos uma Input Action adicional implementada no desafio. Conceitualmente, a turma deve dominar a distinção entre Pawn e Character, o papel do Character Movement Component como sistema universal de locomoção e o desacoplamento entre dispositivo físico e intenção de jogo promovido pelo Enhanced Input.

# Preparação para a Próxima Semana

A Semana 3 depende diretamente do BP_Player e do nível de teste consolidados nesta semana: o material simples e o terreno via Landscape serão aplicados ao mesmo nível em que o Character já se move, e o primeiro build empacotado da disciplina exigirá que a locomoção e o input estejam funcionais de ponta a ponta. A distinção entre conceito universal e implementação específica, já exercitada com Enhanced Input, será retomada ao introduzir Nanite e Lumen como soluções específicas da Unreal para problemas universais de renderização.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Enhanced Input in Unreal Engine. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/enhanced-input-in-unreal-engine.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Gameplay Framework in Unreal Engine (Character e Pawn). Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Character Movement e Enhanced Input. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Input System, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Enhanced Input.
