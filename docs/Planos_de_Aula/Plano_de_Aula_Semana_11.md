# Semana 11 — Navigation, Behavior Trees (LimboAI), Blackboards e Combate Simples

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade III — Resolver Problemas** (Semanas 8–11) | **Metodologia:** Challenge Based Learning — professor apresenta problemas, grupos propõem soluções. Autonomia média.
**Encerramento de Módulo (🔴)** — esta semana fecha a Unidade III com Playtest coletivo e Showcase (Rubricas 5 e 6).

## Introdução da Semana

A Semana 10 encerrou com um `InventoryComponent` funcional conectado a um Interaction System ampliado, capaz de coletar, usar e descartar itens, além de um novo tipo de interação proposto por cada grupo. Até aqui, o Vertical Slice não possui nenhum agente que se mova ou decida de forma autônoma no mundo — todo movimento no projeto é do próprio jogador. A Semana 11 resolve esse problema em duas etapas conectadas: primeiro, dá a um agente a capacidade universal de se deslocar de um ponto a outro sem input direto do jogador (Navigation); depois, dá a esse mesmo agente a capacidade de decidir o que fazer com esse deslocamento (Behavior Tree + Blackboard, via addon LimboAI). O encontro final soma a essas duas capacidades um combate simples, que reutiliza sem duplicação o `HealthComponent` construído na Semana 8 — agora aplicado também ao `Enemy`, e não apenas ao `Player`. A semana fecha a Unidade III (Módulo 3) com Playtest coletivo e Showcase, consolidando o Vertical Slice jogável: animação, HUD, inventário, interação ampliada, IA e combate simples integrados em um único fluxo.

## Objetivos Gerais

- Compreender Navigation (NavigationRegion3D/NavigationAgent3D) como base universal de deslocamento autônomo de agentes, independente de engine.
- Compreender Behavior Tree e Blackboard como estrutura de decisão e memória compartilhada de um agente não-jogador, via addon LimboAI.
- Implementar um combate simples que reutiliza o `HealthComponent` já existente, sem duplicar lógica entre `Player` e `Enemy`.
- Propor e implementar, com solução própria, um comportamento autônomo para o `Enemy` do próprio projeto.
- Consolidar e apresentar o Vertical Slice jogável do Módulo 3 em Playtest coletivo e Showcase (encerramento da Unidade III).

## Resultados Esperados

Ao final da semana, cada grupo possui um `Enemy` capaz de se deslocar autonomamente por um `NavigationRegion3D`, decidir entre patrulhar e perseguir via Behavior Tree/Blackboard (LimboAI), e trocar dano com o `Player` por meio de um combate simples que reutiliza o mesmo `HealthComponent` fundamentado na Semana 8 — o conjunto avaliado em Playtest coletivo e apresentado em Showcase como encerramento do Módulo 3.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar por que um agente não-jogador precisa de um sistema dedicado de deslocamento, distinto do `move_and_slide` usado pelo `Player`.
- Configurar um `NavigationRegion3D` que representa a área navegável do nível já existente.
- Movimentar um agente até um ponto usando `NavigationAgent3D`, sem qualquer lógica de decisão associada ainda.

## Conteúdos

- O problema de deslocamento autônomo: por que um `Enemy` não pode simplesmente usar `move_and_slide` com input do teclado, e o que muda quando o "input" é uma decisão da própria engine.
- `NavigationRegion3D` como representação da área navegável de um nível — bake da malha de navegação sobre a geometria já existente do projeto.
- `NavigationAgent3D` como componente de deslocamento — cálculo de rota e movimentação até um ponto-alvo.
- Configuração guiada do `NavigationRegion3D` no nível do Vertical Slice e movimentação de um agente de teste até um ponto fixo.

## Conceitos Fundamentais

Todo agente não-jogador que precisa se mover pelo mundo enfrenta o mesmo problema estrutural, independentemente da engine: calcular uma rota sobre uma superfície navegável e segui-la evitando obstáculos, sem que essa lógica de baixo nível precise ser reescrita a cada novo tipo de agente. O Godot resolve isso com `NavigationRegion3D` (a região navegável, calculada previamente sobre a geometria do nível) e `NavigationAgent3D` (o componente que, dado um ponto-alvo, calcula e segue a rota dentro dessa região). Esse par é deliberadamente introduzido antes de qualquer decisão de IA: primeiro o agente aprende a se mover de A a B de forma confiável, depois — no Encontro 2 — aprende a decidir para onde ir. Separar "como se mover" de "o que decidir" é o mesmo princípio de responsabilidade única já reforçado desde os Components da Semana 4 em diante, agora aplicado ao domínio de agentes autônomos.

## Recursos do Godot

`NavigationRegion3D`, `NavigationAgent3D`, `NavigationServer` (bake da malha de navegação).

## Comparação com Unity

A Unity resolve o mesmo problema com o NavMesh (gerado por bake sobre a geometria do nível, equivalente ao `NavigationRegion3D`) e o `NavMeshAgent` (equivalente ao `NavigationAgent3D`), que calcula e segue rota até um destino. O princípio universal é idêntico nas duas engines: a malha navegável é pré-calculada sobre a geometria estática do nível, e o agente delega a esse sistema o cálculo de rota, sem precisar implementar pathfinding manualmente. A diferença está mais no fluxo de configuração — no Godot o bake é feito diretamente no nó `NavigationRegion3D` dentro do editor; na Unity, historicamente pelo NavMesh Baking do pacote AI Navigation — do que em qualquer diferença conceitual relevante.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 10, com `InventoryComponent` e Interaction System ampliado funcionais.
- Nível do projeto (zona externa e/ou estrutura interna) pronto para bake de `NavigationRegion3D` — geometria estática finalizada o suficiente para gerar uma malha de navegação coerente.
- Cena de agente de teste (CharacterBody3D simples com `NavigationAgent3D`) preparada para demonstração, sem distribuir antes da aula.
- Slides com o comparativo `NavigationRegion3D`/`NavigationAgent3D` (Godot) × NavMesh/NavMeshAgent (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 10 (Interaction System ampliado + inventário) |
| 20 min | Introdução: por que um agente não-jogador precisa de um sistema dedicado de deslocamento |
| 30 min | Demonstração: bake guiado de `NavigationRegion3D` sobre o nível existente e configuração de um `NavigationAgent3D` |
| 55 min | Laboratório: cada grupo faz o bake da navegação no próprio nível e movimenta um agente de teste até um ponto-alvo |
| 15 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do nível já existente do Vertical Slice, sem alterar nenhum sistema de gameplay funcional da Semana 10, introduzindo a camada de navegação como pré-requisito para o `Enemy` que será construído no Encontro 2. O professor demonstra primeiro o problema de deslocamento autônomo de forma isolada — um cubo simples que precisa ir de um ponto a outro sem input direto —, antes de tocar no nível real do projeto. Em seguida, demonstra o bake guiado de um `NavigationRegion3D` sobre a geometria existente e a configuração de um `NavigationAgent3D` em uma cena de teste, movimentando esse agente até um ponto-alvo fixo. Cada grupo replica essa configuração sobre o próprio nível, garantindo que a malha de navegação cubra corretamente as áreas por onde o `Enemy` deverá circular no Encontro 2.

## Desafio

Não há desafio de solução livre neste encontro: a configuração de `NavigationRegion3D`/`NavigationAgent3D` é guiada, servindo de base direta à Behavior Tree e ao combate simples do Encontro 2.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, um `NavigationRegion3D` corretamente calculado sobre o próprio nível e um agente de teste capaz de se deslocar autonomamente até um ponto-alvo fixo, sem colidir com obstáculos da geometria existente.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro (Rubrica 1 — Desenvolvimento Semanal, aplicada de forma contínua). A navegação configurada aqui é pré-requisito direto do `Enemy` construído no Encontro 2.

## Dificuldades Esperadas

- Malha de navegação mal calculada (buracos, áreas inacessíveis) por geometria do nível ainda incompleta ou com colisões inconsistentes — reforçar a checagem visual da malha antes de prosseguir.
- Confundir `NavigationAgent3D` com `move_and_slide` do `Player`, tentando aplicar lógica de input direto ao agente autônomo — reforçar que o agente delega o cálculo de rota ao `NavigationServer`, não ao teclado.
- Agente "tremendo" ou preso perto do ponto-alvo por parâmetros de distância de chegada mal ajustados — reforçar o ajuste do raio de tolerância do `NavigationAgent3D`.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Behavior Tree como estrutura de decisão e Blackboard como memória compartilhada de um agente, via addon LimboAI.
- Implementar uma Behavior Tree simples de patrulha/perseguição para o `Enemy`, reutilizando a navegação do Encontro 1.
- Implementar um combate simples que reutiliza o `HealthComponent` (Semana 8), sem duplicar lógica entre `Player` e `Enemy`.
- Propor e implementar, com solução própria, um comportamento autônomo adicional para o `Enemy`.
- Participar do Playtest coletivo e do Showcase de encerramento do Módulo 3.

## Conteúdos

- Behavior Tree como estrutura de decisão hierárquica (sequências, seletores, folhas de ação/condição) e Blackboard como memória compartilhada entre os nós da árvore, via addon LimboAI — nenhum dos dois é nativo do Godot.
- Implementação guiada de uma Behavior Tree simples de patrulha (deslocamento entre pontos via `NavigationAgent3D`) e perseguição (mudança de alvo ao detectar o `Player`).
- Combate simples: detecção de acerto via `Area3D`/`RayCast3D` do `Player`, chamando `apply_damage` no `HealthComponent` do `Enemy` — reutilizando o mesmo Component fundamentado na Semana 8, sem duplicação de lógica.
- Desafio: cada grupo propõe um comportamento autônomo próprio para o `Enemy` (patrulha, alerta, fuga, interação com o jogador), com liberdade de solução.
- Playtest coletivo e Showcase — encerramento da Unidade III (Rubricas 5 e 6).

## Conceitos Fundamentais

O Encontro 1 resolveu "como" um agente se move. O Encontro 2 resolve "o que" ele decide fazer com esse deslocamento, sem criar um sistema de movimentação paralelo ao já configurado. A Behavior Tree organiza a decisão do `Enemy` em uma estrutura hierárquica de nós (sequências que executam passos em ordem, seletores que tentam alternativas até uma funcionar, folhas que executam ações ou checam condições), enquanto o Blackboard funciona como uma memória compartilhada entre esses nós — por exemplo, a última posição conhecida do `Player`. Nem Behavior Tree nem Blackboard são nativos do Godot: o addon LimboAI resolve esse problema de forma comparável a soluções de terceiros também necessárias na Unity, reforçando que a ausência de uma solução nativa não significa ausência de um padrão universal — apenas que a comunidade, e não o núcleo da engine, mantém a implementação de referência. O combate simples fecha a semana com o mesmo princípio de reutilização cobrado desde a Semana 8: o `HealthComponent` já existe no `Player` e é aplicado ao `Enemy` sem duplicação, apenas com uma nova origem de dano (`Area3D`/`RayCast3D` do `Player`) chamando o mesmo `apply_damage`.

## Recursos do Godot

`NavigationAgent3D` (retomado do Encontro 1), Behavior Trees e Blackboards (addon LimboAI — `BTPlayer`, Blackboard), `Area3D`/`RayCast3D` (detecção de combate), `HealthComponent` (retomado da Semana 8).

## Comparação com Unity

A Unity resolveria a mesma decisão autônoma com um asset de terceiros como Behavior Designer ou NodeCanvas — nenhum dos dois nativo da engine, exatamente como o LimboAI no Godot —, mantendo a mesma lógica de nós de sequência/seletor/folha e uma estrutura de memória compartilhada equivalente ao Blackboard (geralmente resolvida por variáveis do próprio asset ou por um `ScriptableObject` de estado compartilhado). O combate simples seguiria o mesmo princípio na Unity: um `Collider` em modo trigger ou um `Raycast` no `Player`, chamando um método de dano no mesmo componente de vida já usado pelo `Player`, sem duplicar a lógica de vida entre os dois tipos de personagem.

## Preparação do Professor

- Projeto de cada grupo com `NavigationRegion3D`/`NavigationAgent3D` funcionais do Encontro 1.
- Addon LimboAI instalado e verificado previamente em todos os projetos (ou disponibilizado para instalação no início do encontro).
- Cena de exemplo com Behavior Tree simples de patrulha/perseguição e combate via `Area3D`/`RayCast3D` preparada para demonstração, sem distribuir antes da aula.
- Roteiro do desafio preparado: cada grupo escolhe um comportamento autônomo adicional (patrulha, alerta, fuga, interação com o jogador).
- Ficha de Playtest (Rubrica 5) e ficha de Showcase (Rubrica 6) do Sistema de Avaliação, impressas ou digitais.
- Slides com o comparativo Behavior Tree + Blackboard (LimboAI, Godot) × Behavior Designer/NodeCanvas (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (navegação funcional do agente de teste) |
| 30 min | Demonstração: Behavior Tree e Blackboard (LimboAI) — patrulha/perseguição — e combate simples (Área3D/RayCast3D chamando `apply_damage`) |
| 15 min | Apresentação do desafio: cada grupo escolhe um comportamento autônomo adicional para o `Enemy` |
| 45 min | Laboratório/Desafio: cada grupo implementa a Behavior Tree, o combate simples e o comportamento autônomo escolhido |
| 30 min | Playtest coletivo e Showcase — encerramento do Módulo 3 |

## Desenvolvimento

O encontro abre com a demonstração guiada de uma Behavior Tree simples via LimboAI, aplicando o padrão de patrulha (deslocamento entre pontos, reutilizando o `NavigationAgent3D` do Encontro 1) e perseguição (mudança de alvo ao detectar o `Player` via Blackboard), seguida da implementação do combate simples — uma `Area3D` ou `RayCast3D` do `Player` chamando `apply_damage` no `HealthComponent` do `Enemy`, o mesmo Component já existente desde a Semana 8. A partir daí, o professor apresenta o desafio: cada grupo propõe e implementa um comportamento autônomo adicional para o próprio `Enemy` (patrulha, alerta, fuga ou interação com o jogador), com liberdade de solução dentro da estrutura de Behavior Tree/Blackboard já demonstrada. O encontro fecha com o Playtest coletivo, em que os grupos jogam os Vertical Slices uns dos outros avaliando experiência de jogo e clareza (Rubrica 5), seguido do Showcase de apresentação e encerramento formal da Unidade III (Rubrica 6).

## Desafio

Cada grupo propõe um comportamento autônomo próprio para o `Enemy` do seu projeto (patrulha, alerta, fuga ou interação com o jogador), com liberdade de solução dentro da estrutura de Behavior Tree/Blackboard já fundamentada. **Entrega: Vertical Slice jogável (encerramento do Módulo 3)** — Playtest coletivo e Showcase.

## Critérios de Sucesso

Cada grupo possui, ao final da semana, um `Enemy` que se desloca autonomamente via Navigation, decide seu comportamento via Behavior Tree/Blackboard (incluindo o comportamento adicional proposto), e troca dano com o `Player` por meio de um combate simples que reutiliza o `HealthComponent` sem duplicação — com o Vertical Slice completo (animação, HUD, inventário, interação, IA e combate) avaliado em Playtest e apresentado em Showcase.

## Evidências para Avaliação

**Playtest** (Rubrica 5 do Sistema de Avaliação) — experiência efetiva de jogo, funcionamento, usabilidade e clareza para quem joga o Vertical Slice de cada grupo. **Showcase** (Rubrica 6 do Sistema de Avaliação) — apresentação do projeto e capacidade de justificar decisões de arquitetura diante da turma, mesmo instrumento de Showcase aplicado na Semana 3 (a Semana 17 é avaliada pela mesma Rubrica 6, porém como instrumento distinto — Apresentação Técnica Final, não Showcase).

## Dificuldades Esperadas

- Reimplementar deslocamento dentro da própria Behavior Tree (ex.: calcular posição manualmente), em vez de delegar ao `NavigationAgent3D` já configurado no Encontro 1 — reforçar que a árvore decide, o `NavigationAgent3D` executa o deslocamento.
- Duplicar lógica de vida/dano no `Enemy` em vez de reutilizar o `HealthComponent` já existente desde a Semana 8 — reforçar que o mesmo Component se aplica a `Player` e `Enemy` sem reescrita.
- Behavior Tree excessivamente complexa para o escopo do combate simples definido no `PROJECT_ARCHITECTURE.md` — reforçar que o objetivo pedagógico é patrulha/perseguição básicas, não um sistema de IA avançado (fora do escopo da disciplina).

---

# Resultado Esperado da Semana

Ao final da Semana 11, cada grupo possui um Vertical Slice jogável completo — animação (Semana 8), HUD (Semana 9), inventário e interação ampliada (Semana 10), e agora IA (Navigation + Behavior Tree/Blackboard via LimboAI) e combate simples integrados. O `Enemy` se desloca autonomamente por um `NavigationRegion3D`, decide seu comportamento via Behavior Tree/Blackboard — incluindo um comportamento adicional proposto com solução própria — e troca dano com o `Player` reutilizando o `HealthComponent` sem duplicação de lógica. O conjunto foi avaliado em Playtest coletivo e apresentado em Showcase, encerrando formalmente a Unidade III (Módulo 3 — Resolver Problemas).

# Preparação para a Próxima Semana

O Vertical Slice jogável consolidado nesta semana é a base do Módulo 4 (Unidade IV — Produzir como um Pequeno Estúdio), que inicia na Semana 12 com o refinamento de Materials, Material Overrides e Foliage (MultiMeshInstance3D) — nenhum sistema novo de gameplay é introduzido; o foco passa a ser polimento técnico e produção em escala de estúdio, com autonomia alta e o professor atuando como diretor técnico.

# Referências

- Godot Documentation — Navigation: https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_introduction_3d.html
- Godot Documentation — Physics (Area3D, RayCast3D): https://docs.godotengine.org/en/stable/tutorials/physics/physics_introduction.html
- LimboAI — Documentação oficial: https://github.com/limbonaut/limboai
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — NavMesh: https://docs.unity3d.com/Manual/nav-Overview.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
