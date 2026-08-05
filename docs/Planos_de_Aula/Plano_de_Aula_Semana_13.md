# Semana 13 — Áudio (AudioStreamPlayer), Profiling e Optimization

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade IV — Produzir como um Pequeno Estúdio** (Semanas 12–14) | **Metodologia:** Studio Based Learning — professor atua como diretor técnico. Muito laboratório, feedback contínuo, playtests, code reviews. Autonomia alta.
**Desafio Técnico (🔵)** — esta semana aplica a Rubrica 2 (Desafios Técnicos) sobre a otimização proposta no Encontro 2, e o Feedback Formal previsto no Cronograma, mas não fecha a Unidade IV (encerramento apenas na Semana 14).

## Introdução da Semana

A Semana 12 encerrou com o mesmo Vertical Slice jogável desde a Semana 11, agora com materiais reorganizados em base + Material Overrides e a zona externa composta com MultiMeshInstance3D, sem nenhuma alteração de mecânica. A Semana 13 dá continuidade ao polimento técnico do Módulo 4 em duas frentes conectadas, mas distintas. No Encontro 1, o projeto ganha uma camada que até aqui nunca foi tratada em nenhuma semana anterior — o áudio —, integrado diretamente a eventos de gameplay que já existem (interação, passos, ambiente), nunca como trilha genérica de fundo desconectada do que acontece na tela. No Encontro 2, a disciplina introduz Profiling e Optimization como etapa obrigatória de qualquer produção — não um ajuste opcional de última hora, mas uma prática sistemática de identificar gargalos reais no próprio projeto antes de qualquer decisão de otimização. Os dois encontros seguem a mesma lógica do restante do Módulo 4: nenhuma geometria, mecânica ou sistema de gameplay é alterado — apenas camadas de apresentação e desempenho sobre o Vertical Slice que já roda de ponta a ponta desde a Semana 11.

## Objetivos Gerais

- Compreender AudioStreamPlayer como mecanismo universal de integração de áudio a eventos de gameplay, distinto de tocar música de fundo desconectada da jogabilidade.
- Integrar sons a ações já existentes no Vertical Slice (interação, passos, ambiente), reutilizando os próprios sinais e eventos já implementados desde módulos anteriores.
- Compreender Profiling e Optimization como etapa obrigatória de produção, não como ajuste isolado de última hora.
- Utilizar o Profiler/Debugger nativo do Godot para identificar gargalos reais no próprio projeto, antes de propor qualquer otimização.
- Propor e justificar, com solução própria, a otimização de um aspecto específico identificado no profiling do próprio Vertical Slice.

## Resultados Esperados

Ao final da semana, cada grupo possui o próprio Vertical Slice com som integrado às principais ações de gameplay (interação, passos, ambiente) via AudioStreamPlayer, um diagnóstico de profiling do próprio projeto e ao menos uma otimização implementada e justificada a partir desse diagnóstico — avaliada como Desafio Técnico (Rubrica 2) e comunicada como Feedback Formal.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar AudioStreamPlayer (e suas variantes 2D/3D) como camada de resposta sonora a um evento de gameplay, não como trilha desconectada da ação.
- Identificar, no próprio projeto, quais eventos já existentes (interação, passos, ambiente) devem receber resposta sonora.
- Integrar sons a ao menos três categorias de eventos do próprio Vertical Slice (interação, passos, ambiente), reutilizando os sinais e Components já existentes.

## Conteúdos

- O problema do áudio como camada de resposta a eventos, não como trilha isolada: som de interação, som de passos e som ambiente respondem a algo que já acontece no jogo, e não devem ser tratados como um sistema à parte.
- `AudioStreamPlayer` (som não posicional, ex.: música/UI), `AudioStreamPlayer2D` e `AudioStreamPlayer3D` (som posicional no espaço do nível) — quando cada um se aplica.
- Reaproveitamento dos pontos de integração já existentes no projeto: o Signal de interação (Semana 5), o `move_and_slide` do Player (Semana 2) como gatilho de passos, e a ambientação da zona externa/interna (Semana 3) como base do som ambiente.
- Integração guiada de som a um evento de interação já existente (ex.: `Door` ou `Lever`) e a um evento de passos do Player.

## Conceitos Fundamentais

Áudio, em qualquer engine, não é um sistema separado do gameplay — é uma resposta a eventos que o gameplay já dispara. O mesmo Signal que a Semana 5 usou para desacoplar a reação de um objeto interativo do conhecimento direto do Player é reutilizado aqui: em vez de o `Door` "saber" tocar um som, ele apenas emite `interacted`, e o `AudioStreamPlayer` reage a esse mesmo sinal, exatamente como o HUD já reage a sinais de vida e inventário desde a Semana 9. A diferença entre `AudioStreamPlayer` e suas variantes posicionais (`AudioStreamPlayer2D`/`3D`) é a mesma diferença universal entre som de interface (não posicional, sempre no mesmo volume) e som de mundo (posicional, com atenuação por distância) — presente em qualquer engine que separe áudio de UI de áudio diegético. Como o Módulo 4 mantém autonomia alta, a integração de som não introduz nenhum sistema novo de comunicação entre objetos: ela apenas conecta um novo tipo de "ouvinte" (o `AudioStreamPlayer`) aos sinais que o projeto já emite desde módulos anteriores.

## Recursos do Godot

`AudioStreamPlayer`, `AudioStreamPlayer2D`, `AudioStreamPlayer3D`, Signals já existentes no projeto (interação, movimentação).

## Comparação com Unity

A Unity resolve o mesmo problema com `AudioSource` (não posicional ou 3D, conforme a configuração de Spatial Blend) reagindo a eventos de gameplay disparados por `UnityEvent`/C# Actions ou chamados diretamente de scripts — o princípio universal é idêntico: som é resposta a evento, e a diferença entre som de interface e som de mundo depende de atenuação espacial, não do componente em si. A diferença está na granularidade da API: o Godot separa explicitamente `AudioStreamPlayer` (2D lógico), `AudioStreamPlayer2D` (2D posicional) e `AudioStreamPlayer3D` (posicional em profundidade), enquanto a Unity resolve as três situações com um único `AudioSource` configurado por parâmetros (Spatial Blend, 2D/3D Sound Settings) em vez de por classes distintas.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 12, com Vertical Slice jogável completo, materiais refatorados e zona externa composta.
- Biblioteca curta de efeitos sonoros livres de direitos (ex.: Kenney Audio/Interface Sounds, mesma filosofia de assets gratuitos já usada para arte) selecionada previamente para interação, passos e ambiente.
- Cena de exemplo com `AudioStreamPlayer` reagindo a um Signal, preparada para demonstração, sem distribuir antes da aula.
- Slides com o comparativo `AudioStreamPlayer`/`2D`/`3D` (Godot) × `AudioSource`/Spatial Blend (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 12 (materiais refatorados, zona externa composta, Code Review) |
| 20 min | Introdução: áudio como resposta a eventos de gameplay, não como trilha isolada |
| 30 min | Demonstração: `AudioStreamPlayer` reagindo a um Signal de interação já existente e a um evento de passos |
| 50 min | Laboratório: cada grupo integra som a interação, passos e ambiente no próprio Vertical Slice |
| 20 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do Vertical Slice já validado na Semana 12, sem alterar nenhuma mecânica de gameplay — a mudança desta semana é uma nova camada de resposta sensorial sobre o que já funciona. O professor demonstra primeiro, isoladamente, um `AudioStreamPlayer` conectado a um Signal já conhecido da turma (o mesmo `interacted` da Semana 5), reforçando que nenhum sistema novo de comunicação está sendo introduzido — apenas um novo "ouvinte" do sinal. Em seguida, demonstra a diferença entre som não posicional e posicional em um segundo exemplo (passos do Player). Cada grupo integra sons próprios (escolhidos livremente dentro da biblioteca disponibilizada) a ao menos três pontos do próprio projeto: um evento de interação, os passos do Player e um som ambiente da zona externa ou interna — como diretor técnico, o professor orienta decisões de qual `AudioStreamPlayer` usar em cada caso, sem impor a mesma escolha sonora para todos os grupos.

## Desafio

Não há desafio de solução livre com liberdade ampla neste encontro: a integração de áudio é guiada quanto à ferramenta (`AudioStreamPlayer` e variantes), mas cada grupo escolhe livremente quais sons usar e a quais eventos do próprio projeto associá-los, além dos três pontos mínimos exigidos.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, som integrado a pelo menos um evento de interação, aos passos do Player e a um elemento ambiente do próprio Vertical Slice, sem qualquer alteração de mecânica ou sistema de gameplay já validado.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro (Rubrica 1 — Desenvolvimento Semanal, aplicada de forma contínua). A integração de áudio conduzida aqui é insumo para o profiling do Encontro 2.

## Dificuldades Esperadas

- Confundir `AudioStreamPlayer` (não posicional) com `AudioStreamPlayer3D` (posicional), aplicando o tipo errado a um som ambiente que deveria atenuar por distância — reforçar a pergunta "esse som deveria mudar de volume se eu me afastar?" antes de escolher o Node.
- Tratar o áudio como sistema à parte, criando lógica própria em vez de reagir aos Signals já existentes desde a Semana 5 — reforçar que o `AudioStreamPlayer` deve ser um novo "ouvinte" de um sinal já emitido, nunca uma nova cadeia de dependência direta.
- Poluir o Vertical Slice com sons sobrepostos ou volume mal calibrado, comprometendo a clareza da experiência validada em Playtests anteriores — reforçar teste auditivo comparativo antes/depois de cada integração.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Profiling e Optimization como etapa obrigatória de produção, distinta de um ajuste isolado de última hora.
- Utilizar o Profiler/Debugger nativo do Godot para identificar gargalos reais no próprio Vertical Slice.
- Propor e implementar, com solução própria, a otimização de um aspecto específico identificado no profiling do próprio projeto, justificando a escolha.

## Conteúdos

- O papel do Profiling em qualquer pipeline de produção: medir antes de otimizar, para não gastar tempo corrigindo um problema que não é o gargalo real do projeto.
- O Profiler/Debugger nativo do Godot: monitor de desempenho (FPS, tempo de frame), monitores de memória, física e renderização, e identificação de picos de custo por categoria.
- Leitura guiada do profiling do próprio Vertical Slice, cruzando os dados do Profiler com decisões já tomadas em semanas anteriores (materiais, MultiMeshInstance3D, IA, animação).
- Otimização guiada de um caso identificado durante a leitura do profiling (ex.: ajuste de densidade de MultiMeshInstance3D, revisão de um material, ajuste de raio de detecção da IA).

## Conceitos Fundamentais

Profiling é o mesmo princípio de diagnóstico já praticado nos Code Reviews do semestre (Semanas 7, 10 e 12), aplicado agora ao desempenho em vez de à organização do código: não se otimiza por suposição, otimiza-se a partir de evidência medida. O Profiler do Godot expõe, em tempo real, onde o tempo de frame e a memória do projeto estão sendo gastos — a mesma pergunta que qualquer engine de produção precisa responder antes da entrega final. Como o Vertical Slice já acumula, desde o Módulo 1, decisões de materiais (Semana 3, 12), animação (Semana 8), IA (Semana 11) e composição de cena (Semana 12), o profiling desta semana é também um exercício de releitura crítica de todo o projeto sob a ótica de desempenho, não a introdução de um sistema novo. O desafio de otimização retoma, no domínio de performance, a mesma exigência de solução própria já praticada nos Desafios Técnicos anteriores (Semanas 8, 9, 10 e 11): cada grupo escolhe, a partir do próprio diagnóstico, o que otimizar e como, e precisa justificar essa escolha.

## Recursos do Godot

Profiler/Debugger (Monitor de desempenho, memória, física, renderização), instancing, LOD, occlusion culling.

## Comparação com Unity

A Unity resolve o mesmo problema com o Unity Profiler, que expõe categorias equivalentes de custo (CPU, GPU, memória, física, renderização) e permite a mesma leitura de gargalos antes de qualquer decisão de otimização — o princípio universal é idêntico nas duas engines: medir antes de otimizar, e tratar profiling como etapa recorrente de produção, não como verificação única. A diferença está no nível de detalhe e nos módulos exclusivos de cada ferramenta — o Unity Profiler tradicionalmente oferece módulos mais granulares por sistema (ex.: Rendering, Audio, UI separados em painéis próprios), enquanto o Profiler/Debugger do Godot concentra as mesmas categorias essenciais de forma mais compacta, exigindo do desenvolvedor cruzar os dados manualmente com mais frequência.

## Preparação do Professor

- Projetos de cada grupo com áudio integrado do Encontro 1.
- Projeto de referência do professor já rodando com o Profiler aberto, com ao menos um gargalo conhecido de antemão para a demonstração (sem revelar a causa antes do laboratório).
- Ficha de Desafio Técnico (Rubrica 2) do Sistema de Avaliação, para apresentar aos grupos.
- Slides com o comparativo Profiler/Debugger (Godot) × Unity Profiler.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (áudio integrado a interação, passos e ambiente) |
| 25 min | Demonstração: leitura do Profiler/Debugger em um caso de gargalo conhecido pelo professor |
| 55 min | Laboratório: cada grupo faz o profiling do próprio Vertical Slice e implementa uma otimização a partir do diagnóstico |
| 40 min | Feedback formal sobre as otimizações realizadas (Desafio Técnico — Rubrica 2) |

## Desenvolvimento

O encontro abre com a demonstração guiada do Profiler/Debugger sobre um caso de gargalo já conhecido pelo professor, mostrando como ler os monitores de desempenho, memória, física e renderização antes de decidir o que otimizar. Cada grupo repete esse processo sobre o próprio Vertical Slice, acumulado desde o Módulo 1: abre o Profiler, identifica ao menos um ponto real de custo elevado (geometria, materiais, iluminação, IA, ou lógica de script/Orchestration) e propõe uma otimização específica para esse ponto, dentro do que o próprio grupo julgar mais relevante entre os identificados. Como diretor técnico, o professor circula orientando a leitura correta dos dados do Profiler, sem indicar de antemão qual é o gargalo — o diagnóstico deve ser do próprio grupo. O encontro fecha com o Feedback Formal, em que cada grupo apresenta o gargalo identificado, a otimização escolhida e a justificativa técnica para essa escolha.

## Desafio

Cada grupo otimiza um aspecto específico identificado no profiling do próprio Vertical Slice (geometria, materiais, iluminação, lógica de script/Orchestration), com liberdade total de escolha sobre qual gargalo priorizar, desde que a escolha seja justificada pelos dados observados no Profiler. **Entrega: Feedback Formal sobre as otimizações realizadas.**

## Critérios de Sucesso

Cada grupo apresenta, ao final da semana, um diagnóstico de profiling do próprio projeto, com ao menos um gargalo real identificado e uma otimização implementada e funcional para esse gargalo, sem regressão em nenhuma mecânica ou sistema já validado em semanas anteriores.

## Evidências para Avaliação

**Desafio Técnico** (Rubrica 2 do Sistema de Avaliação) — solução proposta, uso correto dos recursos do Godot, criatividade, organização e funcionamento aplicados à otimização escolhida por cada grupo, com **Feedback Formal** sobre as otimizações realizadas, conforme já previsto no Cronograma para a Semana 13.

## Dificuldades Esperadas

- Propor uma otimização sem antes consultar o Profiler, baseada apenas em suposição sobre o que "deve" ser pesado — reforçar que toda otimização desta semana precisa partir de um dado observado, não de uma hipótese não verificada.
- Otimizar um aspecto de baixo impacto real (ex.: um único material pouco usado) ignorando um gargalo maior identificado no mesmo profiling — reforçar a leitura completa dos monitores antes de escolher onde agir.
- Introduzir uma otimização que compromete a aparência ou o funcionamento já validado em Playtests anteriores (ex.: reduzir densidade de MultiMeshInstance3D a ponto de descaracterizar a composição da Semana 12) — reforçar que otimização é um equilíbrio entre desempenho e resultado, não redução às custas de qualquer critério.

---

# Resultado Esperado da Semana

Ao final da Semana 13, cada grupo possui o mesmo Vertical Slice jogável e visualmente polido desde a Semana 12, agora com som integrado às principais ações de gameplay (interação, passos, ambiente) via AudioStreamPlayer, e com ao menos um gargalo de desempenho identificado por profiling e corrigido por uma otimização própria, justificada tecnicamente em Feedback Formal. O projeto está tecnicamente pronto, em termos de apresentação sonora e desempenho, para a exportação final da Semana 14.

# Preparação para a Próxima Semana

A Semana 14 encerra a Unidade IV e o Módulo 4 com a exportação do build final do Vertical Slice — os ajustes de áudio e as otimizações realizadas nesta semana são parte direta do que será validado no Playtest cruzado entre grupos e no Code Review de encerramento, e nenhum retrabalho de materiais, foliage, áudio ou otimização deve ser necessário além de ajustes pontuais identificados nesse Playtest.

# Referências

- Godot Documentation — Audio: https://docs.godotengine.org/en/stable/tutorials/audio/index.html
- Godot Documentation — Optimization (Profiler/Debugger): https://docs.godotengine.org/en/stable/tutorials/performance/index.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — Audio Overview: https://docs.unity3d.com/Manual/AudioOverview.html
- Unity Manual (consulta comparativa) — Profiler: https://docs.unity3d.com/Manual/Profiler.html
- Kenney Assets (CC0), incluindo bibliotecas de áudio: https://kenney.nl/
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
