# Semana 2 — CharacterBody3D, movimentação e Input Map

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade I — Aprender a Ferramenta** (Semanas 1–3) | **Metodologia:** Scaffolded Learning — professor demonstra, aluno replica. Autonomia muito baixa.

## Introdução da Semana

Na Semana 1 a turma criou o projeto do Vertical Slice (*O Templo Esquecido*) e uma primeira Scene composta por Nodes filhos. Esta semana responde a uma pergunta diferente: como uma engine desacopla a intenção do jogador (apertar uma tecla) da ação que acontece no mundo (o personagem se mover)? Esse desacoplamento é resolvido em duas camadas — um sistema de locomoção física (CharacterBody3D) e uma camada de input abstrata (Input Map) — e nenhuma das duas é exclusiva do Godot: toda engine moderna precisa resolver o mesmo problema.

A Scene criada na Semana 1 não é descartada: o Player desta semana é adicionado como Node filho dentro da mesma estrutura de projeto já organizada.

## Objetivos Gerais

- Compreender por que uma engine separa "o que o jogador quer fazer" de "o que acontece no mundo".
- Configurar um CharacterBody3D controlável usando `move_and_slide`.
- Configurar um Input Map e conectar Actions à movimentação do personagem.

## Resultados Esperados

Ao final da semana, cada estudante terá um Player (CharacterBody3D) movendo-se no nível de teste através de um Input Map próprio, com pelo menos uma Action adicional não demonstrada em aula.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o papel do CharacterBody3D e de `move_and_slide` como sistema universal de locomoção.
- Configurar um CharacterBody3D controlável no nível de teste do Vertical Slice.

## Conteúdos

- CharacterBody3D como Node especializado para personagens físicos.
- `move_and_slide` como resolução de colisão e deslizamento em superfícies.
- Configuração guiada do Player dentro da Scene já existente.

## Conceitos Fundamentais

Qualquer personagem controlável precisa resolver o mesmo problema físico: mover-se no mundo sem atravessar paredes, deslizar suavemente ao encostar em obstáculos e responder a rampas e desníveis. Engines modernas oferecem um Node ou classe dedicada a esse problema para que a equipe não reimplemente física de locomoção do zero a cada projeto. No Godot, esse Node é o CharacterBody3D, e `move_and_slide` é o método que resolve deslocamento e colisão em uma única chamada.

## Recursos do Godot

CharacterBody3D, `move_and_slide`, Orchestrator.

## Comparação com Unity

Na Unity, o mesmo problema costuma ser resolvido combinando um CharacterController (que já resolve colisão de forma parecida ao CharacterBody3D) ou um Rigidbody com um script de movimento próprio — não existe um único Node "pronto" equivalente ao CharacterBody3D com `move_and_slide` embutido. O Godot entrega essa solução de locomoção já pronta dentro do próprio Node; na Unity, a equipe compõe a solução a partir de peças mais genéricas.

## Preparação do Professor

- Projeto do Vertical Slice (retomado da Semana 1) com a Scene do nível de teste aberta.
- Um CharacterBody3D de referência já configurado (CollisionShape3D + MeshInstance3D) para demonstração.
- Orchestrator configurado para a lógica de `move_and_slide`.
- Slides com o comparativo CharacterBody3D/`move_and_slide` × CharacterController/Rigidbody da Unity.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 2 da Semana 1 (Scene com Nodes filhos) |
| 15 min | Introdução: por que engines desacoplam intenção de ação; física de locomoção |
| 35 min | Demonstração: configuração de um CharacterBody3D com CollisionShape3D via Orchestrator |
| 45 min | Laboratório: cada estudante adiciona seu próprio Player à Scene do Vertical Slice |
| 20 min | Desafio: ajustar forma de colisão ou escala do Player, justificando a escolha |
| 10 min | Feedback e fechamento |

## Desenvolvimento

O encontro retoma a Scene da Semana 1 e adiciona um novo Node filho: o Player, um CharacterBody3D. O professor demonstra a montagem — CharacterBody3D com CollisionShape3D e MeshInstance3D como filhos — explicando por que a colisão precisa de uma forma própria, separada da malha visual, e salva o resultado como Scene própria (`scenes/characters/Player.tscn`), reaproveitável em outros níveis do Vertical Slice. A turma replica a montagem dentro do próprio projeto, preparando o terreno para o input, que será conectado no Encontro 2.

## Desafio

Cada estudante ajusta a forma ou o tamanho da CollisionShape3D do próprio Player (por exemplo, cápsula versus caixa, ou uma escala diferente da demonstrada), justificando brevemente a escolha em relação ao personagem que pretende usar no Vertical Slice.

## Critérios de Sucesso

Cada estudante possui um CharacterBody3D funcional na Scene do Vertical Slice, com forma de colisão própria e sem erros ao rodar a Scene (mesmo sem se mover ainda).

## Evidências para Avaliação

Sem instrumento formal nesta semana. A configuração do Player é retomada e observada no Checkpoint de encerramento do Módulo 1, na Semana 3.

## Dificuldades Esperadas

- Confundir a forma de colisão com a malha visual, deixando os dois desalinhados — reforçar visualmente no editor a diferença entre CollisionShape3D e MeshInstance3D.
- Esquecer de que `move_and_slide` ainda não foi conectado a nenhum input — deixar claro que o Player "existir" nesta etapa não significa "se mover" ainda.
- Formas de colisão desproporcionais ao personagem — orientar comparação visual com a malha antes de fechar a etapa.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Input Map e InputEvent como camada de desacoplamento entre dispositivo físico e ação lógica.
- Configurar um Input Map para movimentação.
- Conectar o Input Map ao `move_and_slide` do Player.

## Conteúdos

- Input Map e Actions como abstração entre tecla/botão físico e intenção do jogador.
- InputEvent, deadzones.
- Configuração do Input Map do projeto e conexão com a movimentação do Player.

## Conceitos Fundamentais

Se o código de gameplay lesse diretamente "tecla W pressionada", qualquer remapeamento de controles ou suporte a gamepad exigiria reescrever a lógica do jogo inteira. Por isso engines modernas inserem uma camada de abstração entre o dispositivo físico e a ação lógica: o jogador aperta uma tecla, a engine traduz isso em uma Action nomeada ("mover para frente"), e é essa Action que o código de gameplay consome. No Godot, essa camada é o Input Map, configurado uma vez no projeto e consultado via InputEvent.

## Recursos do Godot

Input Map, InputEvent, CharacterBody3D, `move_and_slide`.

## Comparação com Unity

A Unity resolve o mesmo problema com o Input System (novo), usando Action Maps e um componente Player Input para conectar as Actions ao código — uma solução com mais camadas de configuração (Action Maps, Control Schemes, bindings por dispositivo). O Godot concentra tudo em um único Input Map global do projeto, mais simples de configurar, porém com menos granularidade nativa para múltiplos esquemas de controle simultâneos.

## Preparação do Professor

- Projeto de demonstração com o Player da Semana 2 (Encontro 1) já configurado.
- Input Map de referência pronto para ser recriado ao vivo (Actions: mover para frente/trás/esquerda/direita).
- Orchestrator configurado para ler o Input Map e aplicar velocidade ao `move_and_slide`.
- Slides com o comparativo Input Map/InputEvent × Input System/Action Maps da Unity.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 1 (Player configurado, ainda sem se mover) |
| 20 min | Introdução: por que desacoplar dispositivo físico de ação lógica; Input Map e InputEvent |
| 35 min | Demonstração: configuração do Input Map e conexão com `move_and_slide` via Orchestrator |
| 45 min | Laboratório: cada estudante configura o próprio Input Map e movimenta o Player |
| 20 min | Desafio: adicionar uma Action não demonstrada em aula (correr, agachar ou pular) |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro retoma o Player estático do Encontro 1 e resolve o problema restante: fazê-lo responder ao jogador. O professor demonstra a criação das Actions no Input Map do projeto e a leitura dessas Actions via Orchestrator, aplicando a direção resultante ao `move_and_slide`. A turma replica a configuração no próprio projeto, chegando ao final da semana com um Player efetivamente controlável.

## Desafio

Cada estudante adiciona uma nova Action não demonstrada em aula — correr, agachar ou pular — com liberdade de implementação (por exemplo, correr como multiplicador de velocidade, pular como impulso vertical simples). Não há solução única.

## Critérios de Sucesso

Cada estudante possui, ao final da semana, um Player que se move no nível de teste através de um Input Map próprio configurado, incluindo ao menos uma Action adicional não demonstrada em aula.

## Evidências para Avaliação

Sem instrumento formal nesta semana. O Player e o Input Map construídos aqui compõem, junto com a Scene da Semana 1, a base observada no Checkpoint de encerramento do Módulo 1, na Semana 3.

## Dificuldades Esperadas

- Actions com nomes ambíguos ou duplicados no Input Map, causando comportamento inesperado — reforçar convenção de nomes clara (ex.: `move_forward`, `move_back`).
- Direção de movimento invertida ou câmera desalinhada com os eixos do Player — checar orientação do CharacterBody3D antes de depurar o input.
- Ambiguidade entre a Action nova do desafio (correr/agachar/pular) e as Actions de movimentação já existentes — orientar a manter Actions separadas e nomeadas por intenção.

---

# Resultado Esperado da Semana

Ao final da Semana 2, cada estudante possui um Player (CharacterBody3D) funcional dentro do projeto do Vertical Slice, movendo-se no nível de teste através de um Input Map próprio com ao menos uma Action adicional (correr, agachar ou pular) não demonstrada em aula. A turma domina a distinção entre física de locomoção (CharacterBody3D/`move_and_slide`) e abstração de input (Input Map/InputEvent), relacionando ambas aos equivalentes na Unity (CharacterController/Rigidbody e Input System).

# Preparação para a Próxima Semana

O Player e o nível de teste construídos nesta semana serão a base direta da Semana 3, quando materiais, terreno (Terrain3D), iluminação global (SDFGI/VoxelGI) e a exportação do primeiro build serão adicionados ao mesmo projeto — encerrando o Módulo 1 com o primeiro build executável do Vertical Slice. Nenhum conteúdo desta semana deve ser refeito — apenas ampliado.

# Referências

- Godot Documentation — Physics — CharacterBody3D: https://docs.godotengine.org/en/stable/classes/class_characterbody3d.html
- Godot Documentation — Inputs: https://docs.godotengine.org/en/stable/tutorials/inputs/index.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — Input System: https://docs.unity3d.com/Manual/com.unity.inputsystem.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
