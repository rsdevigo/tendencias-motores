# Semana 11 🔴

## Introdução da Semana

A Semana 11 encerra a Unidade III — Resolver Problemas, mantendo a metodologia de Challenge Based Learning consolidada nas Semanas 8, 9 e 10: o professor apresenta o problema, cada grupo propõe a própria solução, com autonomia média. O eixo conceitual da semana é a autonomia de deslocamento e decisão de agentes não-jogadores, resolvida na Unreal por três recursos que sempre aparecem juntos — Navigation/NavMesh (onde o agente pode andar), Behavior Tree (o que o agente decide fazer) e Blackboard (o que o agente sabe ou lembra). O Encontro 1 fundamenta Navigation e NavMesh, configurando o nível para permitir deslocamento autônomo; o Encontro 2 fundamenta Behavior Tree e Blackboard, implementando um comportamento guiado de patrulha/perseguição em `BP_Enemy`, e fecha o eixo de IA conectando esse `BP_Enemy` a um combate simples — um Trace/Overlap disparado pelo `BP_Player` que chama `ApplyDamage` no `HealthComponent` do inimigo — antes do desafio de propor um comportamento autônomo próprio. A semana encerra com a entrega do Vertical Slice jogável do Módulo 3 — animação, interface, inventário, interação ampliada, IA e combate simples integrados —, Playtest coletivo e Showcase, conforme previsto no Cronograma e no Sistema de Avaliação. Nenhum sistema dos Módulos 1, 2 e do restante do Módulo 3 é descartado: `HealthComponent` (Semana 8), `InteractionComponent`, `InventoryComponent`, `BPI_Interactable` e `WBP_HUD` são todos reutilizados por `BP_Enemy` ou permanecem intactos no Vertical Slice.

## Objetivos Gerais

- Compreender Navigation/NavMesh como base universal de deslocamento autônomo de agentes em qualquer engine.
- Compreender Behavior Tree como estrutura de decisão e Blackboard como memória compartilhada do agente.
- Implementar um `BP_Enemy` com comportamento autônomo simples (patrulha/perseguição), reutilizando o `HealthComponent` já existente.
- Implementar um combate simples: o `BP_Player` ataca `BP_Enemy` por meio de um Trace ou Overlap que chama `ApplyDamage` no `HealthComponent` do alvo.
- Consolidar e apresentar o Vertical Slice jogável do Módulo 3, integrando animação, interface, inventário, interação, IA e combate simples.

## Resultados Esperados

Ao final da semana, cada grupo terá um nível com NavMesh configurado, um `BP_Enemy` funcional capaz de patrulhar e reagir à proximidade do jogador por meio de uma Behavior Tree e um Blackboard próprios, e um combate simples funcional entre `BP_Player` e `BP_Enemy` via `ApplyDamage`, integrado ao Vertical Slice já existente sem substituir nenhum sistema anterior. O Vertical Slice do Módulo 3 terá sido apresentado em Showcase e testado em Playtest coletivo.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar Navigation e NavMesh como base universal de deslocamento autônomo de agentes.
- Comparar a geração de NavMesh na Unreal com o NavMesh da Unity.
- Configurar o NavMesh do nível e movimentar um agente até um ponto definido.

## Conteúdos

- Navigation System como problema universal: como um agente sabe onde pode andar sem colidir com o cenário.
- NavMesh como malha de navegação gerada a partir da geometria do nível.
- Movimentação básica de um agente até um ponto usando o sistema de navegação (`Move To`/`Simple Move to Location`).

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre a geometria visual de um nível (o que o jogador vê e colide) e a geometria de navegação (onde um agente autônomo pode se deslocar). Um NPC não "enxerga" o nível da mesma forma que o motor de física trata colisão de jogador — ele precisa de uma representação simplificada e navegável do espaço, calculada previamente, para poder planejar caminhos até um destino. A Unreal resolve isso com o `NavMesh`, gerado automaticamente a partir da geometria marcada como estática dentro de um volume de navegação (`Nav Mesh Bounds Volume`), sobre o qual um `AIController` pode solicitar deslocamento até qualquer ponto navegável. Este é o primeiro sistema do semestre dedicado exclusivamente a um agente não-jogador — até aqui, todo deslocamento ensinado (Módulo 1) pertencia ao `BP_Player`.

## Recursos da Unreal

Nav Mesh Bounds Volume, NavMesh, AIController, `BP_Enemy` (novo).

## Comparação com Unity

A Unity resolve o mesmo problema com seu próprio sistema de Navigation (NavMesh), gerado via bake sobre a geometria marcada como estática, e um `NavMeshAgent` component que solicita deslocamento até um destino (`SetDestination`), de forma equivalente ao `AIController` da Unreal solicitando movimento sobre o NavMesh. O princípio é idêntico nas duas engines: geometria navegável pré-calculada + um agente que consulta essa geometria para planejar caminho. A diferença está no fluxo de configuração — a Unreal gera o NavMesh em tempo real dentro do volume delimitado, enquanto a Unity normalmente exige um bake explícito antes de rodar o jogo — mas o conceito de "camada de navegação separada da camada visual" transfere-se diretamente entre as duas engines. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o nível do Módulo 2/3 (Dungeon Kit) já modelado e navegável estruturalmente (sem obstáculos que impeçam a geração de NavMesh).
- Um `BP_Enemy` de exemplo pré-configurado (fora da visão da turma), com `AIController` associado e HealthComponent herdado do padrão já usado por `BP_Player`.
- Slides com o diagrama Geometria visual (colisão do jogador) → Nav Mesh Bounds Volume → NavMesh → AIController, reforçando a separação de camadas.
- REFERENCES.md e documentação de Behavior Trees in Unreal Engine (seção de Navigation) disponíveis para consulta durante o laboratório.
- **Nota de contingência:** este é o primeiro encontro da semana e alimenta diretamente o Encontro 2 (Behavior Tree depende de um agente já navegando); não é compressível sem prejudicar a fundamentação — caso falte tempo, priorizar a geração do NavMesh e o deslocamento a um único ponto fixo sobre variações de destino.

## Cronograma do Encontro

- 15 min — Revisão do estado atual do nível (Módulo 2/3) e do `InventoryComponent`/`InteractionComponent` ampliados na Semana 10.
- 20 min — Fundamentação: Navigation e NavMesh como base universal de deslocamento autônomo, e o papel do `AIController` como agente que consulta essa malha.
- 35 min — Demonstração: configuração guiada do `Nav Mesh Bounds Volume`, geração do NavMesh e criação de um `BP_Enemy` com `AIController` que se move até um ponto fixo.
- 50 min — Laboratório: cada grupo configura o NavMesh de seu próprio nível e cria seu `BP_Enemy`, validando o deslocamento até um ponto.
- 15 min — Feedback: verificação da geração do NavMesh e do deslocamento em cada grupo.

## Desenvolvimento

O encontro parte da constatação de que, até aqui, apenas o `BP_Player` se move pelo nível, sempre por comando direto do jogador. O professor demonstra a configuração de um `Nav Mesh Bounds Volume` cobrindo a área jogável, a geração do NavMesh resultante, e a criação de um `BP_Enemy` com `AIController` capaz de se deslocar até um ponto fixo usando o NavMesh gerado. Cada grupo replica o processo em seu próprio nível, validando que seu `BP_Enemy` se move de um ponto a outro sem atravessar paredes ou obstáculos, preparando a estrutura de decisão do Encontro 2.

## Desafio

Não há desafio de liberdade de solução neste encontro — a configuração do NavMesh e do deslocamento básico é demonstração e adaptação guiada, preparando o desafio de maior autonomia do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um NavMesh gerado corretamente sobre seu nível e um `BP_Enemy` capaz de se deslocar até um ponto definido, sem alterar a lógica de nenhum sistema anterior.

## Evidências para Avaliação

Funcionamento demonstrável do deslocamento autônomo e organização/nomenclatura do `BP_Enemy` conforme boas práticas da Unreal 5.6 e do PROJECT_ARCHITECTURE.md (prefixo `BP_` consistente, pasta `Blueprints/Characters/`) — insumo observado para o Playtest e o Showcase do Encontro 2.

## Dificuldades Esperadas

Grupos podem gerar um NavMesh incompleto por não marcar corretamente a geometria do nível como estática ou por delimitar o `Nav Mesh Bounds Volume` menor do que a área jogável. Intervenção: pedir para visualizar o NavMesh em tempo real (tecla de visualização) e comparar visualmente a área verde gerada com a área realmente navegável do nível. Grupos com dificuldade para associar o `AIController` ao `BP_Enemy` devem ser direcionados à documentação oficial antes de receber a resposta direta.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Behavior Tree como estrutura de decisão e Blackboard como memória compartilhada de um agente autônomo.
- Comparar Behavior Tree/Blackboard da Unreal com Behavior Designer/NodeCanvas na Unity.
- Implementar uma Behavior Tree simples de patrulha/perseguição em `BP_Enemy`, reutilizando o `HealthComponent` já existente.
- Implementar um combate simples: `BP_Player` ataca `BP_Enemy` por meio de um Trace ou Overlap que chama `ApplyDamage` no `HealthComponent` do alvo.
- Propor e implementar, com autonomia própria, um comportamento autônomo adicional para o NPC do projeto.

## Conteúdos

- Behavior Tree como árvore de decisão composta por nós de sequência, seletor e tarefa, avaliada continuamente durante o jogo.
- Blackboard como memória compartilhada entre a Behavior Tree e o `AIController`, armazenando dados como localização do jogador ou ponto de patrulha atual.
- Implementação guiada de patrulha entre pontos e transição para perseguição ao detectar o jogador.
- Combate simples: detecção de acerto (Trace ou Overlap) disparada pelo `BP_Player`, chamando `ApplyDamage` no `HealthComponent` de `BP_Enemy`.
- Desafio: proposta de um comportamento autônomo adicional (alerta, fuga, interação com o jogador), com liberdade de solução.

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre decisão (o que fazer) e memória (o que o agente sabe), resolvida por dois artefatos que trabalham em conjunto. A Behavior Tree é uma estrutura hierárquica avaliada repetidamente, na qual nós de seleção escolhem entre ramos alternativos de comportamento (patrulhar ou perseguir) e nós de sequência executam passos em ordem (mover até o ponto, esperar, mover até o próximo); nenhum desses nós, porém, guarda por si só o estado do agente — essa responsabilidade pertence ao Blackboard, uma memória de chave-valor compartilhada (por exemplo, `PontoDePatrulhaAtual` ou `AlvoDetectado`) que a Behavior Tree lê e escreve a cada avaliação. Esse desacoplamento é o mesmo princípio arquitetural já ensinado com `BPI_Interactable`/Event Dispatchers (Semana 5) e com `InteractionComponent`/`InventoryComponent` (Semana 10): uma estrutura de controle não deve guardar internamente o dado que outra parte do sistema também precisa consultar. `BP_Enemy` reutiliza o `HealthComponent` já construído na Semana 8, sem duplicar lógica de vida/dano entre jogador e NPC.

O segundo conceito universal do encontro é a detecção de acerto (hit detection) como problema separado da decisão de comportamento: como uma engine determina que uma ação do jogador efetivamente atingiu um alvo, e como comunica esse acerto ao sistema que já gerencia vida. Um combate simples não precisa de um sistema próprio de dano — ele só precisa de um mecanismo que identifique o alvo atingido (um Trace disparado a partir do Player, ou uma caixa de Overlap ativada momentaneamente durante uma ação de ataque) e, uma vez identificado, chame a função que já existe para esse propósito: `ApplyDamage` no `HealthComponent` do alvo (Semana 8). O `BP_Player` nunca precisa saber como o `HealthComponent` do inimigo armazena ou processa vida — apenas que existe uma função de contrato conhecida para aplicar dano, o mesmo princípio de comunicação através de um ponto único já reforçado desde a Semana 5. Isso mantém o escopo do combate deliberadamente mínimo, conforme PROJECT_ARCHITECTURE.md (seção 4): uma forma de ataque, sem sistema de combos, armas múltiplas ou balanceamento avançado.

## Recursos da Unreal

Behavior Tree, Blackboard, AIController (retomado do Encontro 1), HealthComponent (reutilizado da Semana 8), Line Trace/Overlap para detecção de acerto.

## Comparação com Unity

A Unity não possui um equivalente nativo de mesmo nível a Behavior Tree/Blackboard, dependendo tipicamente de packages de terceiros como Behavior Designer ou NodeCanvas para obter uma estrutura de decisão hierárquica equivalente, com uma solução própria de memória compartilhada (variáveis do asset de comportamento ou um Dictionary interno) cumprindo o papel do Blackboard. O princípio de separação entre estrutura de decisão e memória do agente permanece o mesmo nas duas engines; a diferença está na disponibilidade nativa — a Unreal oferece Behavior Tree e Blackboard integrados ao editor desde o início, enquanto a Unity exige a escolha e integração de uma solução externa. Para a detecção de acerto, a Unity resolve o mesmo problema com `Physics.Raycast`/`Physics.OverlapSphere` (equivalentes ao Trace/Overlap da Unreal) chamando um método público de dano em um script de vida equivalente ao `HealthComponent` — o princípio de "detectar o alvo, depois chamar uma função de contrato conhecida" é idêntico nas duas engines; a diferença é apenas de API e sintaxe. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com NavMesh gerado e `BP_Enemy` funcional do Encontro 1.
- Uma Behavior Tree e um Blackboard de exemplo pré-configurados (fora da visão da turma), com patrulha entre dois pontos e transição para perseguição ao detectar o jogador (Pawn Sensing ou verificação de distância).
- Um exemplo pré-configurado (fora da visão da turma) de combate simples: um Trace ou Overlap disparado por uma ação do `BP_Player`, chamando `ApplyDamage` no `HealthComponent` de `BP_Enemy`.
- Levantamento prévio, por grupo, de quais Actors interativos e sistemas já existem no projeto (inventário, interação, HUD), para orientar o feedback sobre a integração da IA sem indicar a solução do desafio.
- Enunciado do desafio redigido de forma aberta, sem indicar qual comportamento adicional implementar, para preservar a decisão do grupo.
- REFERENCES.md e documentação de Behavior Trees in Unreal Engine disponíveis para consulta durante o laboratório e o desafio.
- Modelo de Avaliação — Playtest e Modelo de Avaliação — Apresentações (Sistema de Avaliação) prontos para uso ao final do encontro.
- **Nota de contingência:** o desafio e a entrega de encerramento do módulo (Playtest + Showcase) são o núcleo do encontro e não devem ser comprimidos; se necessário, reduzir o tempo de demonstração da perseguição ou do combate simples, mantendo intacto o tempo de laboratório do desafio, o Playtest e o Showcase.

## Cronograma do Encontro

- 10 min — Revisão do `BP_Enemy` e do NavMesh construídos no Encontro 1.
- 15 min — Fundamentação: Behavior Tree como estrutura de decisão e Blackboard como memória compartilhada do agente.
- 25 min — Demonstração: construção guiada de uma Behavior Tree de patrulha entre dois pontos, com transição para perseguição ao detectar o jogador via Blackboard.
- 15 min — Combate simples: fundamentação e demonstração guiada de um Trace/Overlap disparado pelo `BP_Player`, chamando `ApplyDamage` no `HealthComponent` de `BP_Enemy`.
- 10 min — Apresentação do desafio: cada grupo propõe um comportamento autônomo adicional para seu `BP_Enemy` (alerta, fuga ou interação com o jogador).
- 30 min — Laboratório do desafio: cada grupo implementa o combate simples e sua própria solução de comportamento autônomo, integrando-as ao Vertical Slice.
- 30 min — Playtest coletivo e Showcase: cada grupo demonstra ao vivo o Vertical Slice jogável do Módulo 3, seguido de feedback formal.

## Desenvolvimento

O professor demonstra a construção de uma Behavior Tree com um nó seletor entre dois ramos — patrulhar entre pontos definidos no Blackboard e perseguir o jogador quando uma chave `AlvoDetectado` do Blackboard é preenchida por uma verificação de distância ou visão. Em seguida, o professor demonstra o combate simples: uma ação de ataque do `BP_Player` dispara um Trace (ou ativa uma caixa de Overlap por um instante), identifica se um `BP_Enemy` foi atingido e, em caso positivo, chama `ApplyDamage` no `HealthComponent` do inimigo — reaproveitando a função já construída na Semana 8, sem qualquer lógica de dano nova dentro do `HealthComponent`. Feitas as duas demonstrações, o professor apresenta o desafio: cada grupo deve propor um comportamento autônomo adicional para o `BP_Enemy` de seu projeto — entrar em estado de alerta antes de perseguir, fugir ao ficar com pouca vida (reutilizando o `HealthComponent`), ou reagir a uma interação do jogador — com liberdade de solução técnica. Cada grupo implementa, no laboratório, tanto o combate simples (guiado) quanto o comportamento adicional (desafio). Encerrado o laboratório, cada grupo apresenta o Vertical Slice completo do Módulo 3 em Showcase, seguido de Playtest coletivo conduzido pelos colegas.

## Desafio

Cada grupo propõe e implementa um comportamento autônomo adicional para seu `BP_Enemy` (alerta, fuga ou interação com o jogador), integrado ao NavMesh, à Behavior Tree e ao Blackboard já construídos, com solução própria, e apresenta a solução no Showcase de encerramento do módulo. A implementação do combate simples (Trace/Overlap + `ApplyDamage`) não é o desafio de liberdade de solução do encontro — é construção guiada, como o restante do combate descrito em "Recursos da Unreal" — mas é pré-requisito funcional para que o comportamento adicional proposto (especialmente a opção de fuga por pouca vida) possa ser testado de ponta a ponta.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um `BP_Enemy` funcional, com patrulha, perseguição e ao menos um comportamento adicional proposto pelo grupo, um combate simples funcional entre `BP_Player` e `BP_Enemy` (Trace/Overlap chamando `ApplyDamage`), integrado ao Vertical Slice completo do Módulo 3 (animação, HUD, inventário, interação ampliada, IA e combate simples), sem alterar a lógica de nenhum sistema anterior, pronto para Playtest e Showcase.

## Evidências para Avaliação

Funcionamento demonstrável da patrulha, perseguição, combate simples e comportamento adicional durante o Playtest coletivo (Rubrica 5 — Funcionamento, Usabilidade, Bugs) e apresentação formal do Vertical Slice no Showcase (Rubrica 6 — Apresentações: Comunicação, Demonstração, Justificativas técnicas, Domínio do projeto, Capacidade de responder perguntas), conforme Sistema de Avaliação (Semana 11, encerramento da Unidade III).

## Dificuldades Esperadas

Grupos podem tentar resolver o comportamento adicional com lógica direta no Event Graph do `BP_Enemy`, fora da Behavior Tree, quebrando o padrão de decisão centralizada. Intervenção: perguntar "se esse NPC precisar de um terceiro comportamento no futuro, essa lógica solta no Event Graph vai crescer de forma organizada?" e reforçar que toda decisão do agente deve passar pela Behavior Tree, com o Blackboard como único ponto de memória compartilhada. Grupos podem também tentar implementar uma lógica de dano própria dentro do combate (por exemplo, reduzindo vida diretamente em vez de chamar `ApplyDamage`), duplicando o que o `HealthComponent` já resolve desde a Semana 8; reforçar que o Trace/Overlap deve apenas identificar o alvo e chamar a função já existente. Grupos que travarem na detecção de proximidade do jogador (transição patrulha → perseguição) ou na configuração do Trace/Overlap do combate devem ser direcionados à documentação oficial antes de receber apoio direto do professor, preservando a autonomia média esperada no Módulo 3. Durante o Playtest, é comum um NPC ficar preso em geometria do nível por NavMesh mal configurado — registrar o bug para correção antes do Módulo 4, sem penalizar o Showcase por esse ponto isoladamente se a IA funcionar na maior parte da sessão.

---

# Resultado Esperado da Semana

Ao final da Semana 11, cada grupo terá um `BP_Enemy` funcional, deslocando-se de forma autônoma sobre um NavMesh gerado no nível do projeto, decidindo entre patrulha e perseguição por meio de uma Behavior Tree e um Blackboard próprios, com ao menos um comportamento adicional proposto pelo grupo, um combate simples funcional entre `BP_Player` e `BP_Enemy` (Trace/Overlap chamando `ApplyDamage`), e reutilizando o `HealthComponent` já construído na Semana 8 sem duplicação de lógica. Conceitualmente, a turma deve dominar a separação entre geometria de navegação (NavMesh), estrutura de decisão (Behavior Tree), memória do agente (Blackboard) e detecção de acerto (combate). A semana encerra a Unidade III com a entrega do Vertical Slice jogável do Módulo 3 — animação, interface, inventário, interação ampliada, IA e combate simples integrados —, avaliado formalmente por Playtest coletivo (Rubrica 5) e Showcase (Rubrica 6).

# Preparação para a Próxima Semana

A Semana 12 abre a Unidade IV — Produzir como um Pequeno Estúdio, na qual a metodologia muda para Studio Based Learning com o professor atuando como diretor técnico, autonomia alta e foco em polimento técnico (materiais parametrizados, áudio integrado a eventos, otimização e empacotamento) sobre o Vertical Slice já consolidado. Nenhum sistema construído até aqui — `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BP_Enemy` com Behavior Tree/Blackboard, combate simples — será substituído; o Módulo 4 refina e otimiza o que já existe, a partir dos bugs e pontos de confusão registrados no Playtest desta semana.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Behavior Trees in Unreal Engine. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Navigation System in Unreal Engine. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-system-in-unreal-engine.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Line Traces (Raycasting) e Overlap Events (detecção de acerto do combate simples). Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/traces-and-overlaps-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a NavMesh, Behavior Tree e Blackboard. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — NavMesh e NavMeshAgent, e Physics.Raycast/Physics.OverlapSphere, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Behavior Tree e NavMesh; **Mathew Wadstein**, para explicações pontuais de WTF Is? Behavior Tree, Blackboard e Line Trace; **Ryan Laley**, para exemplos aplicados de IA de inimigos com Behavior Tree e combate simples.
