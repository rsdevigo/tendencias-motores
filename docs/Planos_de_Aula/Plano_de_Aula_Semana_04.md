# Semana 4 — GameManager e SaveManager (Autoload/Singleton)

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7) | **Metodologia:** Studio Based Learning — professor demonstra, aluno adapta. Autonomia baixa.

## Introdução da Semana

A Semana 3 encerrou o Módulo 1 com o primeiro build executável do Vertical Slice: um nível de teste com Player controlável, terreno, material e iluminação global. Esta semana abre o Módulo 2 (Construir Sistemas) e desloca o foco de composição visual para arquitetura de gameplay — a primeira pergunta deixa de ser "como o mundo aparece" e passa a ser "onde vive o estado que uma partida precisa compartilhar entre cenas". Nada do nível, do Player ou do build da Semana 3 é refeito: o mesmo projeto recebe dois sistemas novos, construídos como Autoload/Singleton, que passam a coordenar regras de partida e persistência para todo o restante do semestre.

## Objetivos Gerais

- Compreender Autoload/Singleton como mecanismo nativo do Godot para estado global compartilhado entre cenas.
- Construir um `GameManager` que centraliza regras de partida e estado compartilhado.
- Construir um `SaveManager` que centraliza persistência de dados entre cenas.

## Resultados Esperados

Ao final da semana, cada estudante possui, além do projeto herdado das Semanas 1–3, um `GameManager` e um `SaveManager` configurados como Autoload, com pelo menos um dado de progresso próprio persistindo corretamente entre cenas.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar Autoload/Singleton como mecanismo nativo de estado global no Godot.
- Diferenciar o papel do `GameManager` (regras de partida e estado compartilhado) de um Node comum de cena.
- Criar um `GameManager` customizado como Autoload no projeto do Vertical Slice.

## Conteúdos

- Autoload/Singleton no Godot: registro, ciclo de vida e escopo global.
- Papel do `GameManager` como ponto único de regras de partida e estado compartilhado.
- Criação guiada do script e registro do `GameManager` como Autoload.

## Conceitos Fundamentais

Toda engine de jogos que trabalha com múltiplas cenas precisa resolver o mesmo problema: onde vive um dado ou uma regra que não pertence a nenhuma cena específica, mas que todas precisam acessar — pontuação da partida, condição de vitória, referência ao jogador ativo. O Godot resolve isso de forma nativa e formal com Autoload/Singleton: um script registrado nas configurações do projeto é instanciado automaticamente na raiz da árvore de cenas e permanece acessível globalmente, sobrevivendo à troca de cenas. O `GameManager` construído nesta semana ocupa esse papel — reunindo em um único ponto o que a Unreal separa formalmente em GameMode (regras) e GameState (estado compartilhado), sem que o Godot precise de dois conceitos distintos para isso.

## Recursos do Godot

Autoload/Singleton, Project Settings (aba Autoload), GDScript, Orchestrator.

## Comparação com Unity

A Unity não possui um mecanismo formal equivalente ao Autoload — o mesmo problema de estado global é resolvido por convenção do próprio time, tipicamente com `DontDestroyOnLoad` aplicado a um GameObject, ou com um singleton implementado manualmente em C# (por vezes apoiado em um ScriptableObject). O Godot formaliza esse padrão como um recurso de primeira classe do editor, registrado explicitamente em Project Settings, o que reduz a chance de implementações inconsistentes entre membros de uma mesma equipe — uma diferença arquitetural que vale destacar à turma, não apenas mencionar de passagem.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 3, com nível de teste, Player e build já configurados.
- Script de referência de um `GameManager` mínimo já preparado para demonstração (não distribuído antes da aula).
- Project Settings aberto na aba Autoload da máquina de demonstração, pronto para registrar o script ao vivo.
- Slides com o comparativo Autoload/Singleton × `DontDestroyOnLoad`/singleton manual da Unity.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 3 (build exportado, encerramento do Módulo 1) |
| 20 min | Introdução: onde vive o estado que não pertence a nenhuma cena específica |
| 35 min | Demonstração: criação do script `GameManager` e registro como Autoload em Project Settings |
| 45 min | Laboratório: cada estudante cria e registra seu próprio `GameManager` no projeto do Vertical Slice |
| 15 min | Desafio: adicionar uma variável de estado de partida própria ao `GameManager` |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro abre o Módulo 2 retomando o projeto herdado da Semana 3 sem alterar nada do que já existe — nível, Player e build permanecem intactos. O professor demonstra a criação de um script `GameManager` simples e seu registro na aba Autoload de Project Settings, explicando por que esse registro transforma o script em um Singleton acessível globalmente a partir de qualquer outra cena ou script do projeto. A turma replica a criação e o registro no próprio projeto, preparando o `GameManager` para receber, no Encontro 2, o `SaveManager` e a lógica de persistência entre cenas.

## Desafio

Cada estudante adiciona ao `GameManager` uma variável de estado de partida própria, não demonstrada em aula (por exemplo, um contador de tentativas, um estado de progresso simples ou uma flag de evento), justificando brevemente sua escolha em relação ao Vertical Slice.

## Critérios de Sucesso

Cada estudante possui, ao final do encontro, um `GameManager` registrado como Autoload no projeto, acessível a partir de qualquer cena, contendo ao menos uma variável de estado além da demonstrada em aula.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro. O `GameManager` construído aqui é pré-requisito direto do Checkpoint de progresso da Semana 6 e do encerramento do Módulo 2 na Semana 7.

## Dificuldades Esperadas

- Registrar o script como Autoload sem defini-lo corretamente como `class_name` ou sem testar o acesso a partir de outra cena — orientar um teste rápido de acesso ao `GameManager` a partir do Player antes de encerrar a etapa.
- Confundir Autoload com um Node comum adicionado manualmente à Scene do nível — reforçar que o Autoload vive fora da árvore de cenas do nível e é configurado exclusivamente em Project Settings.
- Duplicar responsabilidades já cobertas por variáveis locais do Player (por exemplo, vida ou inventário) dentro do `GameManager` — reforçar que o `GameManager` guarda apenas estado de partida compartilhado, não estado interno de um Node específico.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar a centralização de input de alto nível no próprio Player como característica arquitetural do Godot.
- Explicar o `SaveManager` (Autoload) como mecanismo de persistência de dados entre cenas.
- Implementar uma variável persistente no `SaveManager` e validar sua persistência entre trocas de cena.

## Conteúdos

- Centralização de input de alto nível no Player, na ausência de uma separação nativa Pawn/Controller.
- `SaveManager` (Autoload) como ponto único de persistência entre cenas.
- Implementação guiada de uma variável persistente e teste de troca de cena.

## Conceitos Fundamentais

O Godot não separa formalmente "quem controla" de "o que é controlado" como a Unreal faz com Pawn e Controller: o próprio Node do Player concentra a leitura de input de alto nível (ações de gameplay, não apenas movimentação) e a lógica que reage a ele, o que é uma escolha arquitetural válida e não uma limitação. Paralelamente, toda engine multi-cena precisa de um lugar para guardar dados que sobrevivem à troca de cena antes mesmo de qualquer gravação em disco — esse é o papel do `SaveManager`: um segundo Autoload, independente do `GameManager`, dedicado exclusivamente a manter dados persistentes entre cenas e centralizar o slot de save ativo, preparando o terreno para a serialização em disco que será construída na Semana 7.

## Recursos do Godot

Autoload/Singleton, SaveManager, GameManager, GDScript.

## Comparação com Unity

A centralização de input de alto nível no próprio Player, sem uma separação nativa equivalente a Pawn/Controller, aproxima o Godot da forma como a maioria dos projetos em Unity já lida com input de gameplay — tipicamente concentrado no próprio script do personagem ou em um Input System conectado diretamente a ele, sem um objeto de controle formalmente separado. Já para persistência entre cenas, a Unity resolve o problema de forma equivalente a um Autoload por meio de um singleton manual (muitas vezes o mesmo objeto usado para o `GameManager`, com `DontDestroyOnLoad`), enquanto o Godot separa esse papel em um segundo Autoload dedicado — uma decisão de organização que reforça a especialização de responsabilidades entre `GameManager` e `SaveManager`.

## Preparação do Professor

- Projeto de demonstração com o `GameManager` do Encontro 1 já registrado como Autoload.
- Script de referência de um `SaveManager` mínimo já preparado para demonstração.
- Duas cenas de teste no projeto de demonstração para validar a persistência de uma variável entre trocas de cena.
- Slides com o comparativo de input centralizado no Player (Godot) × Input System conectado ao personagem (Unity), e persistência via Autoload × singleton com `DontDestroyOnLoad`.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 1 (`GameManager` registrado como Autoload) |
| 20 min | Introdução: centralização de input no Player e o problema da persistência entre cenas |
| 35 min | Demonstração: criação do `SaveManager` e implementação de uma variável persistente |
| 45 min | Laboratório: cada estudante cria seu `SaveManager` e testa a persistência entre duas cenas |
| 20 min | Desafio: cada grupo define e implementa um dado próprio que deve persistir entre cenas |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro completa o Módulo 2 desta semana adicionando o `SaveManager` como segundo Autoload do projeto, independente do `GameManager` construído no Encontro 1. O professor demonstra a criação do script, seu registro em Project Settings e a implementação de uma variável simples que precisa sobreviver à troca entre duas cenas de teste, validando o comportamento ao vivo. A turma replica a criação do próprio `SaveManager` e testa a persistência da variável trocando de cena no projeto do Vertical Slice, encerrando a semana com os dois Autoloads que sustentarão gameplay, interação e save/load nas semanas seguintes.

## Desafio

Cada grupo define e implementa, no `SaveManager`, um dado próprio que deve persistir entre cenas — pontuação, item coletado ou estado de progresso, à escolha do grupo —, validando a persistência com uma troca de cena real dentro do projeto.

## Critérios de Sucesso

Cada estudante possui, ao final da semana, um `GameManager` e um `SaveManager` registrados como Autoload, com ao menos uma variável de estado de partida no primeiro e um dado de progresso próprio persistindo corretamente entre cenas no segundo.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro. `GameManager` e `SaveManager` compõem a base avaliada no Checkpoint de progresso do Módulo 2 (Semana 6) e no Code Review/Playtest de encerramento do Módulo 2 (Semana 7).

## Dificuldades Esperadas

- Implementar a variável persistente diretamente na cena do nível em vez do `SaveManager`, perdendo o dado ao trocar de cena — orientar teste explícito de troca de cena antes de considerar a etapa concluída.
- Confundir o papel do `SaveManager` (persistência entre cenas, em memória) com gravação em disco — reforçar que a serialização em arquivo só será introduzida na Semana 7, e que esta semana resolve apenas a persistência durante a sessão de jogo.
- Sobrepor responsabilidades entre `GameManager` e `SaveManager` (por exemplo, guardar o mesmo dado nos dois Autoloads) — reforçar a separação de papéis: regras/estado de partida no primeiro, dados que precisam sobreviver à troca de cena no segundo.

---

# Resultado Esperado da Semana

Ao final da Semana 4, cada estudante possui, sobre o projeto herdado do Módulo 1, dois Autoloads funcionais — `GameManager`, com regras e estado de partida compartilhado, e `SaveManager`, com ao menos um dado de progresso persistindo corretamente entre cenas. A turma domina Autoload/Singleton como mecanismo nativo de estado global do Godot, relaciona esse mecanismo à ausência de um equivalente formal na Unity (resolvido por convenção via `DontDestroyOnLoad` ou singleton manual), e compreende a centralização de input de alto nível no próprio Player como escolha arquitetural válida diante da separação Pawn/Controller da Unreal. Esses dois sistemas abrem a Unidade II — Construir Sistemas e sustentam toda a arquitetura de gameplay das semanas seguintes.

# Preparação para a Próxima Semana

O `GameManager` e o `SaveManager` construídos nesta semana são pré-requisito direto da Semana 5, que introduz o contrato `Interactable` e Signals para comunicação desacoplada entre sistemas — o primeiro objeto interativo do Vertical Slice (porta ou equivalente) poderá, por exemplo, consultar ou atualizar estado mantido no `GameManager` ao ser acionado.

# Referências

- Godot Documentation — Nodes and Scene Instances (Autoload): https://docs.godotengine.org/en/stable/tutorials/scripting/singletons_autoload.html
- Godot Documentation — GDScript: https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/index.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — DontDestroyOnLoad: https://docs.unity3d.com/ScriptReference/Object.DontDestroyOnLoad.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
