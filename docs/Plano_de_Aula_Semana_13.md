# Semana 13 🔵

## Introdução da Semana

A Semana 13 dá continuidade à Unidade IV — Produzir como um Pequeno Estúdio, mantendo a metodologia de Studio Based Learning com autonomia alta em que o professor atua como diretor técnico. Depois de a Semana 12 ter refinado a camada visual do Vertical Slice (Material Instances e Foliage), esta semana trata de dois eixos complementares de produção: integrar áudio a eventos de gameplay já existentes — não como elemento decorativo, mas como parte da experiência — e tratar Optimization e Profiling como etapa obrigatória antes de qualquer entrega final, retomando diretamente a discussão de custo de densidade de foliage iniciada na Semana 12. O Encontro 1 integra som a ações que já existem no projeto (interação, passos, ambiente), sem criar nenhum sistema novo de gameplay. O Encontro 2 fundamenta profiling como prática de produção, conduz cada grupo a identificar gargalos no próprio projeto e propõe um desafio de otimização com solução própria por grupo, encerrando com feedback formal. Nenhum sistema anterior é descartado: `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD`, `BP_Enemy` com Behavior Tree/Blackboard, Material Instances e Foliage permanecem intactos — a semana refina a camada sonora e a saúde técnica do mesmo Vertical Slice, preparando diretamente o Packaging final da Semana 14.

## Objetivos Gerais

- Compreender a integração de áudio a eventos de gameplay como parte da experiência de jogo, e não como camada acessória adicionada ao final.
- Compreender Optimization e Profiling como etapa obrigatória de produção, capaz de identificar gargalos antes de qualquer entrega.
- Integrar sons a ações já existentes no projeto (interação, passos, ambiente), sem alterar nenhum sistema de gameplay.
- Realizar profiling do próprio Vertical Slice, identificar pelo menos um gargalo real e tratá-lo, justificando a escolha técnica.

## Resultados Esperados

Ao final da semana, cada grupo terá integrado áudio às ações de interação, locomoção e ambiente já existentes no Vertical Slice, organizado em `Audio/` conforme o PROJECT_ARCHITECTURE.md, e terá executado profiling do próprio projeto, identificando e tratando ao menos um gargalo (geometria, materiais, iluminação ou lógica de Blueprint), com a decisão registrada e justificada. O encontro se encerra com Feedback formal sobre as otimizações realizadas, preparando diretamente o Packaging do build final na Semana 14.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar por que áudio é parte estrutural da experiência de jogo, e não um acréscimo cosmético de final de produção.
- Associar eventos sonoros a ações de gameplay já existentes no projeto (interação, passos, ambiente).
- Integrar sons a essas ações sem alterar a lógica de nenhum sistema já construído.

## Conteúdos

- Áudio como resposta a eventos de gameplay: interação, movimentação, ambiente.
- Diferença entre som pontual (disparado por um evento) e som contínuo/ambiente (associado a um espaço ou estado).
- Integração guiada de sons às ações já existentes: `InteractionComponent`, locomoção do `BP_Player`, ambientação dos níveis de Exploração e Dungeon.

## Conceitos Fundamentais

O conceito universal desta aula é que o áudio, em uma engine, não é um arquivo tocado isoladamente, mas uma resposta a um evento que já existe no fluxo de gameplay — a mesma lógica de evento que já dispara a interação via `BPI_Interactable` ou a atualização do `WBP_HUD` também pode disparar um som, sem exigir nenhum sistema novo. Por isso, a aula não introduz um "sistema de áudio" separado: ela conecta pontos de disparo sonoro aos eventos que o `InteractionComponent`, a locomoção do `BP_Player` e a ambientação dos níveis já produzem desde os Módulos 2 e 3. Essa integração tardia e deliberada — depois que o gameplay já está estável — reforça o princípio de que áudio comunica estado e reforça feedback (uma porta que range ao abrir confirma a interação tanto quanto a animação), e antecipa o tema de Profiling do Encontro 2: sons mal gerenciados (excesso de sons simultâneos, sem prioridade ou distância de corte) também custam performance.

## Recursos da Unreal

Sound Cue / Sound Base (conforme versão do projeto), Audio Component, disparo de som via Blueprint (Play Sound at Location / Play Sound 2D), integração com Event Dispatchers já existentes no `InteractionComponent`.

## Comparação com Unity

A Unity resolve o mesmo problema com `AudioSource` e `AudioClip`, disparados a partir de eventos de script (`OnTriggerEnter`, chamadas diretas de método) de forma conceitualmente equivalente ao Audio Component da Unreal disparado a partir de Event Dispatchers. O princípio é idêntico nas duas engines — som como resposta a um evento de gameplay já existente, não como sistema autônomo —, mas a Unreal tende a centralizar a composição sonora mais complexa (mixagem, randomização, atenuação) em assets dedicados (Sound Cue/MetaSounds) editáveis visualmente, enquanto a Unity historicamente resolve variações semelhantes com mais lógica em código sobre o próprio `AudioSource`. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o Vertical Slice do Módulo 3 e a camada visual da Semana 12 (Material Instances, Foliage) intactos.
- Conjunto de assets de áudio de prototipagem (passos, interação — porta, alavanca, baú —, ambiente) disponibilizado previamente a todos os grupos (fonte livre/CC0, compatível com REFERENCES.md).
- Um exemplo pré-configurado (fora da visão da turma) de som de interação disparado a partir do Event Dispatcher já existente no `InteractionComponent`, e de som de passos associado à locomoção do `BP_Player`.
- Estrutura de pasta `Audio/` (PROJECT_ARCHITECTURE.md, seção 8) revisada previamente em cada projeto de grupo.
- REFERENCES.md e documentação de Unreal Engine — Audio Overview disponíveis para consulta durante o laboratório.
- **Nota de contingência:** este encontro não depende de nenhum sistema novo e pode ser comprimido reduzindo o número de eventos sonorizados por grupo, priorizando a integração de som à interação (evento mais evidente para o Code Review) sobre a cobertura completa de passos e ambiente.

## Cronograma do Encontro

- 15 min — Revisão do estado atual do Vertical Slice (Semana 12) e dos eventos de gameplay já disponíveis para disparo sonoro.
- 20 min — Fundamentação: áudio como resposta a evento, não como sistema autônomo; som pontual versus som ambiente.
- 35 min — Demonstração: integração guiada de som ao evento de interação (via Event Dispatcher do `InteractionComponent`) e de som de passos à locomoção do `BP_Player`.
- 50 min — Laboratório: cada grupo integra som às suas próprias ações de interação, passos e ambiente, organizando os assets em `Audio/`.
- 15 min — Feedback: verificação da integração sonora e da coerência entre evento e som disparado em cada grupo.

## Desenvolvimento

O professor retoma o `InteractionComponent` e a locomoção do `BP_Player`, já estáveis desde os Módulos 2 e 3, e demonstra como associar um som ao evento já disparado por essas ações, sem tocar na lógica de gameplay existente. Em seguida, demonstra a diferença entre som pontual (disparado uma vez, como o clique de uma alavanca) e som ambiente (associado a uma região do nível, como o ambiente da Dungeon). Cada grupo aplica a mesma lógica às suas próprias interações — portas, alavancas, baús —, à locomoção do próprio `BP_Player` e à ambientação de seus níveis de Exploração e Dungeon, organizando os assets de áudio em `Audio/` conforme o PROJECT_ARCHITECTURE.md.

## Desafio

Não há desafio de liberdade de solução neste encontro — a integração de áudio a eventos existentes é demonstração e adaptação guiada, preparando a autonomia do desafio de otimização do Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir som integrado a pelo menos uma ação de interação, à locomoção do `BP_Player` e a um elemento de ambiente do nível, organizados em `Audio/`, sem alterar nenhum sistema de gameplay existente.

## Evidências para Avaliação

Coerência entre evento de gameplay e som disparado, e organização dos assets em `Audio/` conforme o PROJECT_ARCHITECTURE.md — insumo para o Feedback formal do Encontro 2, junto com as otimizações realizadas.

## Dificuldades Esperadas

Grupos podem tratar áudio como adição isolada, disparando sons soltos sem vínculo com o Event Dispatcher já existente, duplicando lógica de disparo. Intervenção: perguntar "esse som está reagindo a um evento que já existe no projeto, ou você está criando um gatilho novo só para o som?" e reconduzir ao Event Dispatcher do `InteractionComponent`. Grupos podem também sonorizar excessivamente o ambiente, sem critério de distância ou prioridade, antecipando um problema de performance a ser evidenciado no profiling do Encontro 2.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Optimization e Profiling como etapa obrigatória de produção, e não como correção de emergência.
- Executar profiling do próprio Vertical Slice e identificar ao menos um gargalo real (geometria, materiais, iluminação ou lógica de Blueprint).
- Tratar o gargalo identificado e justificar tecnicamente a escolha de otimização feita.

## Conteúdos

- Profiling como prática sistemática de identificação de gargalos, comparada ao Profiler da Unity.
- Fontes comuns de gargalo em um Vertical Slice deste porte: densidade de foliage (retomando a Semana 12), draw calls, complexidade de materiais, iluminação dinâmica, lógica de Blueprint em Tick.
- Desafio de otimização: cada grupo trata um gargalo específico identificado no próprio profiling.
- Feedback formal sobre as otimizações realizadas.

## Conceitos Fundamentais

O conceito universal desta aula é que nenhuma decisão de otimização é válida sem medição prévia — otimizar por intuição tende a gastar esforço em partes do projeto que não são, de fato, o gargalo. A Unreal expõe essa medição através de ferramentas de profiling (como Stat commands e o Session Frontend/Unreal Insights, conforme disponibilidade da versão 5.6 usada em aula) que revelam onde o tempo de frame está sendo consumido — geometria, materiais, iluminação ou lógica de Blueprint — antes de qualquer ação corretiva. Este encontro retoma diretamente a densidade de foliage discutida na Semana 12 como primeiro candidato a gargalo mensurável, mas amplia a discussão para as demais camadas construídas ao longo do semestre. O desafio pede que cada grupo escolha, com base em dados reais do próprio projeto, qual aspecto otimizar — não há solução única, porque o gargalo real depende do que cada grupo construiu, o que é coerente com a autonomia alta do Módulo 4.

## Recursos da Unreal

Stat commands (`stat fps`, `stat unit`, `stat scenerendering`), Unreal Insights ou Session Frontend (conforme disponibilidade), revisão de Materials/Material Instances e Foliage (Semana 12), revisão de lógica de Blueprint (Tick versus Event-driven).

## Comparação com Unity

A Unity resolve o mesmo problema com o Profiler integrado ao Editor, que expõe consumo de CPU, GPU, memória e renderização por frame de forma equivalente às ferramentas de profiling da Unreal. O princípio é o mesmo nas duas engines — medir antes de otimizar, e tratar profiling como etapa obrigatória de produção, não como correção pontual —, mas a Unreal tende a expor esses dados de forma mais granular por sistema (renderização, materiais, Blueprint) através de múltiplas ferramentas complementares, enquanto o Profiler da Unity concentra essas visões em um único painel unificado. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com áudio integrado do Encontro 1 e toda a camada visual da Semana 12 intacta.
- Ambiente pré-configurado (fora da visão da turma) demonstrando o uso de `stat fps`, `stat unit` e, se disponível, Unreal Insights, sobre uma cena de teste com gargalo proposital (foliage em densidade excessiva).
- Modelo de Feedback formal (conforme Sistema de Avaliação, Semana 13) pronto para uso ao final do encontro.
- REFERENCES.md e documentação de Unreal Engine — Optimization Guide disponíveis para consulta durante o laboratório.
- **Nota de contingência:** o Feedback formal de encerramento é o núcleo avaliativo do encontro e não deve ser comprimido; se necessário, reduzir o escopo do gargalo tratado por grupo a um único aspecto, mantendo intacto o tempo reservado ao Feedback.

## Cronograma do Encontro

- 15 min — Revisão da integração de áudio do Encontro 1 e do estado atual do Vertical Slice.
- 20 min — Fundamentação: Optimization e Profiling como etapa obrigatória, comparando com o Profiler da Unity.
- 30 min — Demonstração: profiling guiado de uma cena de teste com gargalo proposital, usando stat commands.
- 50 min — Laboratório/Desafio: cada grupo realiza profiling do próprio projeto, identifica um gargalo (geometria, materiais, iluminação ou lógica de Blueprint) e o trata, justificando a escolha.
- 20 min — Feedback formal sobre as otimizações realizadas em cada grupo.

## Desenvolvimento

O professor demonstra o uso de stat commands (e Unreal Insights, se disponível) sobre uma cena de teste com um gargalo proposital de densidade de foliage, mostrando como os dados de profiling apontam a causa antes de qualquer correção. Cada grupo então executa o mesmo processo sobre seu próprio Vertical Slice, identificando um gargalo real entre geometria, materiais, iluminação ou lógica de Blueprint — podendo ser a própria densidade de foliage da Semana 12, uma Material Instance mal configurada, iluminação dinâmica custosa ou lógica de Tick evitável em algum Blueprint. Cada grupo trata o gargalo identificado e prepara uma justificativa técnica curta da escolha, apresentada durante o Feedback formal que encerra o encontro.

## Desafio

Cada grupo otimiza um aspecto específico identificado no profiling do seu próprio Vertical Slice (geometria, materiais, iluminação ou lógica de Blueprint), justificando tecnicamente a escolha com base nos dados de profiling coletados — não há solução única, e diferentes grupos podem legitimamente identificar e tratar gargalos distintos.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve ter executado profiling do próprio projeto, identificado ao menos um gargalo real com dados concretos, tratado esse gargalo e apresentado uma justificativa técnica coerente durante o Feedback formal, sem regressão em nenhum sistema de gameplay ou visual já construído.

## Evidências para Avaliação

Feedback formal sobre as otimizações realizadas, avaliando a qualidade da medição (profiling real, não suposição), a pertinência da escolha de otimização e a clareza da justificativa técnica apresentada pelo grupo — insumo direto para o critério "Qualidade técnica" do Sistema de Avaliação, que passa a considerar explicitamente os gargalos identificados no profiling da Semana 13.

## Dificuldades Esperadas

Grupos podem tentar otimizar por suposição, sem antes medir com stat commands, revertendo à intuição em vez de dado. Intervenção: recusar validar qualquer otimização proposta sem o dado de profiling correspondente, reforçando que a medição é pré-requisito, não etapa opcional. Grupos com dificuldade para localizar o gargalo real em meio a múltiplas camadas (geometria, materiais, iluminação, Blueprint) devem ser direcionados a isolar variáveis uma de cada vez (por exemplo, ocultando temporariamente a foliage para verificar impacto no `stat fps`) antes de receber a resposta direta.

---

# Resultado Esperado da Semana

Ao final da Semana 13, cada grupo terá integrado áudio a eventos de interação, locomoção e ambiente já existentes no Vertical Slice, organizado em `Audio/`, e terá executado profiling do próprio projeto, identificando e tratando ao menos um gargalo real com justificativa técnica registrada. Conceitualmente, a turma deve dominar a ideia de que áudio é resposta a evento de gameplay, e que otimização exige medição antes de ação. Nenhum sistema de gameplay ou visual dos Módulos 1 a 4 — `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD`, `BP_Enemy` com Behavior Tree/Blackboard, Material Instances e Foliage — foi alterado; a semana adiciona a camada sonora e trata a saúde técnica do mesmo Vertical Slice, avaliada formalmente por Feedback (Semana 13).

# Preparação para a Próxima Semana

A Semana 14 encerra a Unidade IV com o pipeline de Packaging do Vertical Slice final — configurações, plataformas-alvo e build de produção — diretamente dependente do trabalho de otimização desta semana: um projeto com gargalos não tratados compromete o empacotamento e o Playtest cruzado entre grupos que encerra o módulo. A justificativa técnica das otimizações da Semana 13 também alimenta a revisão geral do projeto sob a perspectiva de um pequeno estúdio, conduzida no Encontro 2 da Semana 14.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Audio Overview. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Optimization Guide. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Audio e a ferramentas de Profiling. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — AudioSource/AudioClip e Profiler, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Audio e Profiling; **PrismaticaDev**, para exemplos aplicados de otimização de cena; **Ryan Laley**, para exemplos práticos de integração de áudio a eventos de gameplay.
