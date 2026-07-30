# Semana 8 🔵

## Introdução da Semana

A Semana 8 abre a Unidade III — Resolver Problemas, e com ela muda a própria lógica da disciplina: da Semana 4 à Semana 7, o professor demonstrava e os grupos adaptavam (Studio Based Learning); a partir de agora, o professor apresenta problemas e cada grupo propõe a própria solução, com autonomia média (Challenge Based Learning). Antes de entrar no eixo conceitual da semana, o Encontro 1 abre com a construção de um sistema pequeno, mas estrutural, que ficou pendente do Módulo 2: o `HealthComponent`, um Component mínimo de vida/dano que passa a existir desde já, para que `BP_Player` (e, mais adiante, `BP_Enemy`) tenham um ponto único de gerenciamento de vida antes de qualquer sistema depender dele (o HUD da Semana 9, o combate da Semana 11). O eixo conceitual central da semana é a transição e a combinação de animações — como uma engine decide qual animação um personagem deve exibir a cada instante, e como combina múltiplas animações sem que uma substitua abruptamente a outra. O restante do Encontro 1 introduz Animation Blueprint e State Machines para resolver o primeiro problema de animação (transição entre estados de locomoção do `BP_Player` já consolidado no Módulo 1 e 2); o Encontro 2 introduz Blend Spaces e Montages para resolver o segundo problema (interpolação direcional e animações pontuais sobrepostas), fechando com um desafio de liberdade real de solução — cada grupo escolhe, entre Blend Space ou Montage, a ferramenta mais adequada ao problema que propõe resolver. Nenhum sistema do Módulo 2 é descartado: a animação e o `HealthComponent` passam a atuar sobre o `BP_Player` e sobre o fluxo jogável já integrados na Semana 7.

## Objetivos Gerais

- Implementar um `HealthComponent` mínimo (vida atual/máxima, `ApplyDamage`, evento de morte), reutilizável por `BP_Player` e por futuros agentes não-jogadores.
- Compreender Animation Blueprint e State Machine como mecanismo universal de transição de estados de animação.
- Implementar uma State Machine básica (idle, andar, correr) sobre o `BP_Player` já existente.
- Compreender Blend Spaces como interpolação multidimensional e Montages como animações pontuais sobrepostas.
- Propor e implementar, com autonomia própria, uma animação contextual (reação a dano, interação ou ataque) escolhendo a ferramenta adequada ao problema.

## Resultados Esperados

Ao final da semana, o `BP_Player` de cada grupo possuirá um `HealthComponent` funcional, e exibirá transições fluidas entre idle, andar e correr por meio de uma State Machine, um Blend Space direcional funcional, e uma solução própria de animação contextual (Blend Space ou Montage, à escolha do grupo), integrada ao Vertical Slice sem substituir nenhum sistema construído no Módulo 2.

---

# Encontro 1

## Objetivos de Aprendizagem

- Implementar um `HealthComponent` mínimo (vida atual/máxima, `ApplyDamage`, evento de morte/`OnDeath`), seguindo o mesmo padrão de composição já usado por `InteractionComponent` e `SaveComponent`.
- Explicar Animation Blueprint e State Machine como mecanismo de transição de estados de animação.
- Comparar Animation Blueprint/State Machine com o Animator Controller da Unity.
- Implementar uma State Machine básica (idle, andar, correr) sobre o `BP_Player`.

## Conteúdos

- `HealthComponent`: Component dedicado a vida/dano/morte, seguindo o padrão de encapsulamento já ensinado com `InteractionComponent` (Semana 5) e `SaveComponent` (Semana 7).
- Animation Blueprint como camada de decisão de animação, separada da lógica de gameplay do `BP_Player`.
- State Machine como estrutura de estados e transições de animação.
- Aplicação da State Machine aos estados de locomoção já existentes no `BP_Player` (idle, andar, correr).

## Conceitos Fundamentais

Antes de entrar no conceito central da aula, o encontro resolve um problema pendente que qualquer jogo com risco ou desafio precisa resolver: onde vive o estado de "quanto dano um personagem pode receber antes de morrer" — e quem tem permissão de alterá-lo. Se cada sistema que causa dano (uma armadilha, um inimigo, uma queda) escrever diretamente em uma variável de vida espalhada pelo `BP_Player`, o projeto acumula pontos de acesso descoordenados ao mesmo dado crítico, exatamente o problema que `InteractionComponent` (Semana 5) e `SaveComponent` (Semana 7) já resolveram para interação e persistência. A Unreal resolve isso da mesma forma: um `HealthComponent` — Component isolado, anexável a qualquer Actor — concentra vida atual, vida máxima, a função `ApplyDamage` (único ponto de entrada para reduzir vida) e um evento de morte (`OnDeath`) disparado quando a vida chega a zero, notificando quem estiver inscrito sem que o `HealthComponent` precise conhecer o que acontece depois (fim de jogo, tela de derrota, remoção do Actor). Por ser construído como Component genérico desde já, o mesmo `HealthComponent` poderá ser anexado a `BP_Enemy` na Semana 11, sem duplicar lógica de vida entre jogador e inimigo.

O conceito universal do restante da aula é a separação entre lógica de gameplay e lógica de apresentação visual do movimento. O `BP_Player` já sabe, desde o Módulo 1, se está parado, andando ou correndo — essa informação existe como velocidade e input processados pelo Character Movement Component. O que falta é uma camada dedicada a traduzir esse estado interno em uma animação visível, e a decidir como transitar de uma animação para outra sem cortes abruptos. Toda engine de jogos precisa resolver esse problema, porque misturar decisão de animação com lógica de gameplay dentro do próprio Character tornaria o código de movimento acoplado a detalhes de apresentação que deveriam ser intercambiáveis (por exemplo, trocar o esqueleto ou o conjunto de animações sem tocar na lógica de input). A Unreal resolve isso com o Animation Blueprint, um asset separado do Character que lê variáveis expostas por ele (como velocidade) e usa uma State Machine — estados discretos (Idle, Walk, Run) conectados por regras de transição — para decidir qual animação reproduzir a cada instante.

## Recursos da Unreal

`HealthComponent` (novo), Animation Blueprint, State Machine, `BP_Player` (retomado dos Módulos 1 e 2).

## Comparação com Unity

A Unity resolve o problema de vida/dano tipicamente com um `MonoBehaviour` próprio (por exemplo, uma classe `Health`) anexado ao GameObject do personagem, expondo um método equivalente a `ApplyDamage` e um `UnityEvent`/`Action` disparado na morte — o mesmo princípio de concentrar vida em um único ponto de acesso, sem uma classe nativa dedicada como o `HealthComponent` da Unreal; a solução, nas duas engines, depende do próprio time definir esse Component/script. Já para o problema de animação, a Unity resolve com o Animator Controller, um asset conceitualmente equivalente ao Animation Blueprint: também organiza estados de animação e regras de transição por meio de parâmetros expostos pelo script do personagem (Float, Bool, Trigger), de forma visual, em uma máquina de estados. O princípio é idêntico nas duas engines — isolar a decisão de "qual animação tocar agora" em um asset dedicado, alimentado por variáveis de gameplay, nunca decidido dentro do próprio script/Blueprint de movimento. A diferença prática está na integração: na Unreal, o Animation Blueprint acessa diretamente propriedades do Character via nós de Blueprint; na Unity, o Animator Controller é acionado via `SetFloat`/`SetBool`/`SetTrigger` a partir do script. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com `BP_Player` funcional (Módulos 1 e 2), incluindo Character Movement Component configurado.
- Um `HealthComponent` de exemplo pré-configurado (fora da visão da turma), com vida atual/máxima, função `ApplyDamage` e evento `OnDeath` disparando uma reação simples de teste.
- Um esqueleto e um conjunto mínimo de animações (idle, andar, correr) compatíveis com o `BP_Player`, disponibilizados a todos os grupos (asset pack padronizado, para não consumir tempo de aula com retargeting).
- Um Animation Blueprint de exemplo pré-configurado (fora da visão da turma), com State Machine de três estados e transições por velocidade.
- Slides com o diagrama Character (dado de gameplay: velocidade) → Animation Blueprint (decisão) → State Machine (estados e transições), reforçando a separação de responsabilidades.
- REFERENCES.md e documentação de Animation Blueprints e de Actor Components disponíveis para consulta durante o laboratório.
- **Nota de contingência:** este é o primeiro encontro da Unidade III e alimenta diretamente o Encontro 2 (Blend Space); não é compressível sem prejudicar a fundamentação — caso falte tempo, priorizar o `HealthComponent` e a transição idle↔andar sobre a inclusão de correr, retomando a transição completa no início do Encontro 2.

## Cronograma do Encontro

- 10 min — Revisão do estado atual do `BP_Player` e do fluxo jogável consolidado na Semana 7.
- 20 min — Fundamentação e construção guiada do `HealthComponent` (vida atual/máxima, `ApplyDamage`, evento `OnDeath`), seguindo o mesmo padrão de `InteractionComponent`/`SaveComponent`.
- 15 min — Fundamentação: Animation Blueprint e State Machine como camada de decisão de animação.
- 30 min — Demonstração: criação guiada de uma State Machine de três estados (idle, andar, correr) conectada à velocidade do `BP_Player`.
- 45 min — Laboratório: cada grupo implementa o `HealthComponent` e anexa-o ao `BP_Player`, e implementa a State Machine no próprio `BP_Player`.
- 15 min — Feedback: verificação do `HealthComponent` e das transições de animação em cada grupo.

## Desenvolvimento

O encontro abre com a constatação de que nenhum sistema construído até a Semana 7 gerencia vida ou dano — um problema que precisa existir antes de qualquer combate ou reação a dano ser construído nos módulos seguintes. O professor cria `HealthComponent` como um novo Component, com variáveis de vida atual e vida máxima, a função `ApplyDamage` (recebendo a quantidade de dano e reduzindo a vida, sem permitir valores negativos) e um Event Dispatcher `OnDeath` disparado quando a vida chega a zero. Cada grupo replica o processo, criando seu próprio `HealthComponent` na subpasta `Blueprints/Components/` e anexando-o ao `BP_Player`, validando `ApplyDamage` com um teste temporário (uma tecla de debug, por exemplo). Em seguida, o encontro muda de eixo: o `BP_Player` já se move corretamente desde o Módulo 1, mas ainda não exibe nenhuma animação de locomoção. O professor demonstra a criação de um Animation Blueprint associado ao esqueleto do personagem, expõe a velocidade do Character como variável lida pela State Machine, e constrói os três estados (Idle, Walk, Run) com transições baseadas em faixas de velocidade. Cada grupo replica o processo em seu próprio projeto, associando o Animation Blueprint ao `BP_Player` e validando visualmente a transição entre os três estados em diferentes situações de movimento.

## Desafio

Não há desafio de liberdade de solução neste encontro — a construção do `HealthComponent` e da State Machine básica é demonstração e adaptação guiada, preparando os problemas de maior autonomia do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um `HealthComponent` funcional anexado ao `BP_Player`, com `ApplyDamage` reduzindo vida corretamente e `OnDeath` disparando ao chegar a zero, e o `BP_Player` deve exibir transições visuais corretas entre idle, andar e correr, comandadas por uma State Machine dentro de um Animation Blueprint, sem interromper o fluxo jogável consolidado na Semana 7.

## Evidências para Avaliação

Funcionamento demonstrável do `HealthComponent` (`ApplyDamage`/`OnDeath`) e das transições de animação, e organização/nomenclatura do `HealthComponent`/Animation Blueprint conforme boas práticas da Unreal 5.6 e do PROJECT_ARCHITECTURE.md (Rubrica 1 — Desenvolvimento Semanal, critérios Execução e Evolução).

## Dificuldades Esperadas

Estudantes podem tentar reduzir a vida diretamente de fora do `HealthComponent` (alterando a variável em vez de chamar `ApplyDamage`), reabrindo o mesmo problema de acesso descoordenado que o Component deveria resolver. Intervenção: perguntar "se três sistemas diferentes puderem escrever diretamente na variável de vida, quem garante que nenhum valor inválido será escrito?" e reforçar que `ApplyDamage` deve ser o único ponto de entrada. Estudantes também podem configurar transições de animação com faixas de velocidade que se sobrepõem ou deixam lacunas, causando animações que "travam" em um estado intermediário ou alternam de forma instável entre dois estados. Intervenção: pedir ao grupo que leia em voz alta as condições de transição de cada seta da State Machine e identifique sobreposições ou lacunas antes de qualquer ajuste, reforçando que a State Machine é uma leitura direta de uma variável de gameplay, não um conjunto de regras arbitrárias. Grupos com dificuldade para localizar a variável de velocidade exposta pelo Character Movement Component devem ser direcionados à documentação oficial antes de receber a resposta direta.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Blend Spaces como interpolação multidimensional entre animações e Montages como animações pontuais sobrepostas.
- Comparar Blend Spaces com Blend Trees da Unity.
- Propor e implementar, com autonomia própria, uma animação contextual escolhendo entre Blend Space ou Montage conforme o problema apresentado.

## Conteúdos

- Blend Space como interpolação direcional entre múltiplas animações (ex.: andar para frente, lateral, diagonal).
- Montage como animação pontual sobreposta ao estado corrente, sem substituir a State Machine.
- Desafio: proposta e implementação de uma animação contextual própria de cada grupo.

## Conceitos Fundamentais

O conceito universal desta aula é a diferença entre dois problemas de animação que parecem semelhantes, mas exigem soluções distintas: combinar continuamente várias animações de acordo com uma direção (interpolação multidimensional) e sobrepor pontualmente uma animação a um estado já em curso, sem interromper o fluxo normal da State Machine (ação pontual sobreposta). Uma State Machine de estados discretos, por si só, não resolve bem o primeiro problema — andar para frente, para os lados e na diagonal não são estados isolados, mas pontos ao longo de um espaço contínuo de direções, e forçar isso em estados discretos geraria transições artificiais. O Blend Space resolve esse problema interpolando entre animações-base de acordo com coordenadas (direção, velocidade). Já o segundo problema — uma reação a dano, um ataque, uma interação pontual — não deve alterar permanentemente o estado da State Machine; precisa apenas ser reproduzido uma vez, sobreposto ao que já está acontecendo, e depois devolver o controle à State Machine. O Montage resolve esse segundo problema. A escolha entre as duas ferramentas depende da natureza do problema: contínuo e direcional (Blend Space) ou pontual e sobreposto (Montage) — e essa distinção é exatamente o que o desafio deste encontro pede que cada grupo identifique por conta própria.

## Recursos da Unreal

Blend Spaces, Montages, Animation Blueprint e State Machine (retomados do Encontro 1).

## Comparação com Unity

A Unity resolve o problema de interpolação multidimensional com Blend Trees dentro do Animator Controller, que também combinam animações de acordo com um ou mais parâmetros contínuos (tipicamente velocidade e direção). A diferença arquitetural mais relevante é que, na Unreal, o Blend Space é multidimensional por padrão (um espaço 1D ou 2D de direção/velocidade configurado visualmente), enquanto na Unity o Blend Tree exige configuração manual equivalente para alcançar o mesmo resultado multidimensional. Para animações pontuais sobrepostas, a Unity não possui um equivalente direto e nomeado como o Montage; o efeito equivalente é obtido combinando camadas de Animator (Layers) com Avatar Masks, ou disparando clipes via `Animator.Play` sobre uma camada adicional. O princípio geral — separar animação contínua de locomoção de animação pontual de ação — é o mesmo nas duas engines; o grau de suporte nativo dedicado é maior na Unreal. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com a State Machine do Encontro 1 funcional.
- Um conjunto mínimo de animações direcionais (frente, lateral, trás) e ao menos uma animação de ação pontual (reação a dano, interação ou ataque simples) disponibilizado a todos os grupos.
- Um Blend Space de exemplo e uma Montage de exemplo pré-configurados (fora da visão da turma).
- Enunciado do desafio redigido de forma aberta, sem indicar qual ferramenta usar, para preservar a decisão do grupo entre Blend Space e Montage.
- Modelo de Desafios Técnicos (Sistema de Avaliação, Rubrica 2) impresso ou digital, um por grupo.
- REFERENCES.md e documentação de Animation Blueprints disponíveis para consulta durante o laboratório e o desafio.
- **Nota de contingência:** o desafio é o núcleo do encontro e não deve ser comprimido; se necessário, reduzir o tempo de demonstração do Blend Space, mantendo intacto o tempo de laboratório do desafio.

## Cronograma do Encontro

- 10 min — Revisão da State Machine do Encontro 1.
- 15 min — Fundamentação: Blend Space (interpolação multidimensional) e Montage (animação pontual sobreposta).
- 30 min — Demonstração: configuração guiada de um Blend Space direcional e de uma Montage de ação simples.
- 15 min — Apresentação do desafio: cada grupo escolhe, entre Blend Space ou Montage, a ferramenta adequada à animação contextual que propõe implementar.
- 45 min — Laboratório do desafio: cada grupo implementa sua própria solução.
- 20 min — Feedback: apresentação breve de cada grupo, justificando a escolha entre Blend Space e Montage.

## Desenvolvimento

O professor demonstra primeiro um Blend Space direcional simples (frente, lateral, trás) associado à State Machine já existente, e em seguida uma Montage disparada por um evento de teste (por exemplo, uma tecla de ação), mostrando que a Montage sobrepõe a animação corrente sem interromper a State Machine. Feita a demonstração, o professor apresenta o desafio: cada grupo deve propor e implementar sua própria animação contextual — reação a dano, interação com um objeto do mundo (retomando `BPI_Interactable` da Semana 5) ou um ataque simples — decidindo, com base no problema que escolher, se a solução exige um Blend Space (variação contínua e direcional) ou uma Montage (ação pontual sobreposta). Não há indicação prévia de qual ferramenta usar; a decisão correta faz parte do desafio.

## Desafio

Cada grupo propõe e implementa uma animação contextual própria (reação a dano, interação ou ataque), escolhendo entre Blend Space ou Montage conforme a natureza do problema que decidir resolver, e apresenta ao final do encontro a justificativa técnica da escolha feita.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir uma animação contextual funcional, integrada ao `BP_Player` e à State Machine já existentes, implementada com a ferramenta (Blend Space ou Montage) tecnicamente adequada ao problema escolhido, sem interromper o fluxo jogável do Módulo 2.

## Evidências para Avaliação

Adequação da ferramenta escolhida ao problema proposto, funcionamento da solução e capacidade de justificar tecnicamente a escolha entre Blend Space e Montage, registradas conforme a Rubrica 2 — Desafios Técnicos (critérios Solução proposta, Uso correto da Unreal e Criatividade).

## Dificuldades Esperadas

Grupos podem escolher Montage para um problema que é, na verdade, contínuo e direcional (ou o inverso), produzindo uma solução tecnicamente funcional mas conceitualmente inadequada. Intervenção: não corrigir diretamente a escolha; perguntar "essa animação muda de forma contínua conforme uma direção, ou acontece uma vez e depois volta ao normal?" e deixar o grupo re-avaliar a própria decisão a partir da resposta. Grupos que travarem na configuração técnica (eixos do Blend Space, slot da Montage) devem ser direcionados à documentação oficial antes de receber apoio direto do professor, preservando a autonomia média esperada no Módulo 3.

---

# Resultado Esperado da Semana

Ao final da Semana 8, o `BP_Player` de cada grupo possuirá um `HealthComponent` funcional (vida atual/máxima, `ApplyDamage`, `OnDeath`), exibirá uma State Machine funcional (idle, andar, correr), um Blend Space direcional e uma solução própria de animação contextual (Blend Space ou Montage, conforme escolha justificada do grupo), tudo integrado ao Vertical Slice consolidado no Módulo 2, sem substituir nenhum sistema anterior. Conceitualmente, a turma deve dominar a distinção entre gerenciamento de estado crítico centralizado (`HealthComponent`), decisão de estado (State Machine), interpolação contínua (Blend Space) e ação pontual sobreposta (Montage) como problemas complementares — e, por ser a primeira semana de Challenge Based Learning, deve começar a exercitar a decisão autônoma de qual ferramenta aplicar a qual problema, sem depender de indicação prévia do professor.

# Preparação para a Próxima Semana

A Semana 9 introduz UMG e HUD para comunicar em tempo real o estado de jogo ao jogador, reutilizando dados de gameplay já existentes (como a vida exposta pelo `HealthComponent` construído nesta semana e o progresso persistido pelo `SaveComponent` da Semana 7). A metodologia permanece Challenge Based Learning, com o desafio de HUD reforçando a mesma autonomia de decisão exercitada nesta semana: cada grupo deve escolher quais dados de gameplay compõem o HUD e propor a própria solução visual e de binding.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Animation Blueprints in Unreal Engine. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Actors and Components (base conceitual do `HealthComponent`). Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-actors.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Animation Blueprint, State Machines, Blend Spaces e Montages. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Animator Controller e Blend Trees, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Animation Blueprint; **Mathew Wadstein**, para explicações pontuais de WTF Is? State Machine, Blend Space, Montage e Actor Component; **PrismaticaDev**, para exemplos aplicados de animação de personagem.
