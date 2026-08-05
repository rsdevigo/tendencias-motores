# Semana 14 — Exportação e Consolidação do Vertical Slice Final

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade IV — Produzir como um Pequeno Estúdio** (Semanas 12–14) | **Metodologia:** Studio Based Learning — professor atua como diretor técnico. Muito laboratório, feedback contínuo, playtests, code reviews. Autonomia alta.
**Semana 🔴** — encerramento da Unidade IV e do Módulo 4. Entrega: Vertical Slice final (Módulo 4) otimizado e exportado (entrega parcial), Playtest cruzado, Code Review de encerramento.

## Introdução da Semana

A Semana 13 encerrou com o mesmo Vertical Slice jogável desde a Semana 11, agora com som integrado às principais ações de gameplay via AudioStreamPlayer e com ao menos um gargalo de desempenho corrigido a partir de profiling real do próprio projeto. A Semana 14 fecha o Módulo 4 respondendo a uma pergunta que nenhuma semana anterior precisou responder: o que diferencia um protótipo, que só roda dentro do editor, de um build distribuível, que roda de forma independente em uma máquina de destino? No Encontro 1, o projeto retoma o pipeline de exportação já introduzido no Checkpoint de encerramento do Módulo 1 (Semana 3) — Export Templates, presets e build de produção —, mas agora aplicado pela primeira vez ao Vertical Slice completo, acumulado desde o Módulo 1, e não mais a um nível de teste simples. No Encontro 2, a turma troca de papel: em vez de testar o próprio projeto, cada grupo faz Playtest cruzado do build exportado de outro grupo, aplicando o mesmo olhar crítico de Code Review já praticado nas Semanas 7, 10 e 12, agora sobre um produto fechado e não mais sobre o projeto aberto no editor. Nenhuma geometria, mecânica ou sistema de gameplay é alterado nesta semana — o Vertical Slice construído desde o Módulo 1 é, pela primeira vez, empacotado e validado como entrega.

## Objetivos Gerais

- Compreender exportação de projeto como etapa universal de qualquer pipeline de produção de jogos, distinta de testar o projeto dentro do editor.
- Configurar Export Templates e presets de exportação no Godot para gerar um build de produção do Vertical Slice.
- Gerar o primeiro executável distribuível do Vertical Slice completo, acumulado desde o Módulo 1.
- Realizar Playtest cruzado do build exportado de outro grupo, aplicando critérios de Code Review a um produto fechado.
- Consolidar, com ajustes finais pontuais, a entrega do Vertical Slice do Módulo 4 como produto de um pequeno estúdio.

## Resultados Esperados

Ao final da semana, cada grupo possui um build exportado e executável do próprio Vertical Slice, testado de forma cruzada por outro grupo, com ajustes finais aplicados a partir desse Playtest e de um Code Review de encerramento — entregando a versão consolidada do Módulo 4.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar a diferença entre rodar um projeto no editor e rodar um build exportado, e por que essa diferença importa para qualquer estúdio.
- Configurar Export Templates e ao menos um preset de exportação (plataforma-alvo) no Godot.
- Gerar um build de produção executável do Vertical Slice completo do próprio grupo.

## Conteúdos

- O problema do build de produção: um projeto aberto no editor depende do próprio Godot instalado; um build exportado precisa rodar de forma independente na máquina de destino — a mesma distinção entre "rodar em ambiente de desenvolvimento" e "entregar um produto" de qualquer pipeline de software.
- Export Templates: binários pré-compilados do motor necessários para gerar builds sem depender do editor.
- Presets de exportação: plataforma-alvo (Windows/Linux/Web, conforme disponibilidade do laboratório), configurações de janela, ícone e nome do executável.
- Exportação guiada do Vertical Slice completo do próprio grupo, acumulado desde a Semana 1 — reaproveitando o mesmo pipeline de Export Templates e presets já praticado no Checkpoint da Semana 3, agora aplicado ao produto final e não a um nível de teste.

## Conceitos Fundamentais

Exportação é a etapa que separa um protótipo funcional de um produto distribuível — o mesmo protótipo que já rodava no editor desde a Semana 1 precisa, agora, ser reempacotado para rodar sem o editor, sem acesso ao código-fonte das cenas e sem qualquer dependência do ambiente de desenvolvimento. Os Export Templates cumprem, no Godot, o mesmo papel que qualquer engine de produção precisa resolver: compilar o motor e o projeto em um binário autocontido para a plataforma-alvo. Como o Vertical Slice já acumula, desde o Módulo 1, todas as decisões de arquitetura, materiais, áudio e otimização das treze semanas anteriores, a exportação desta semana não introduz nenhum sistema novo de gameplay — ela testa, pela primeira vez, se tudo o que foi construído continua funcionando fora do ambiente do editor, o que frequentemente revela dependências implícitas (caminhos de arquivo, referências a recursos) que passavam despercebidas durante o desenvolvimento.

## Recursos do Godot

Export Templates, Project Export (presets), plataformas-alvo (Windows/Linux/Web).

## Comparação com Unity

A Unity resolve o mesmo problema com Build Settings, selecionando uma plataforma-alvo e gerando um build a partir de Player Settings equivalentes aos presets do Godot — o princípio universal é idêntico nas duas engines: um projeto de desenvolvimento precisa ser compilado para uma plataforma específica antes de se tornar um produto distribuível, e esse processo frequentemente expõe problemas que não apareciam dentro do editor. A diferença está no modelo de distribuição do motor: o Godot depende de Export Templates baixados separadamente por versão e plataforma, enquanto a Unity resolve a mesma necessidade através de módulos de plataforma instalados via Unity Hub — a mesma exigência (ter o suporte à plataforma-alvo disponível antes de exportar) é resolvida por fluxos de instalação diferentes.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 13, com Vertical Slice jogável completo, áudio integrado e ao menos uma otimização aplicada.
- Export Templates da versão do Godot 4.7 em uso já baixados e testados previamente no laboratório, para evitar depender da rede durante a aula.
- Preset de exportação de referência (ex.: Windows Desktop) já configurado e testado pelo professor antes da aula, com um build de exemplo gerado previamente para demonstração.
- Slides com o comparativo Export Templates/Project Export (Godot) × Build Settings/Player Settings (Unity).

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 13 (áudio integrado, profiling e otimização aplicada) |
| 20 min | Introdução: build de produção vs. projeto no editor, o papel dos Export Templates |
| 30 min | Demonstração: configuração de preset de exportação e geração de um build de exemplo |
| 50 min | Laboratório: cada grupo configura o próprio preset e exporta o Vertical Slice completo |
| 20 min | Feedback e fechamento — verificação de que cada build gerado abre e roda de forma independente |

## Desenvolvimento

O encontro parte do Vertical Slice já validado na Semana 13, sem alterar nenhuma mecânica, material, som ou otimização — o objetivo é reempacotar o que já funciona. O professor demonstra primeiro a instalação dos Export Templates e a criação de um preset de exportação, explicando cada campo (plataforma-alvo, nome do executável, ícone) como decisão de produto, não apenas configuração técnica. Em seguida, gera ao vivo um build de exemplo e o executa fora do editor, mostrando à turma o momento em que o projeto deixa de depender do Godot aberto. Cada grupo repete o processo sobre o próprio projeto: instala os templates (se ainda não instalados na máquina), configura o preset e exporta o Vertical Slice completo acumulado desde o Módulo 1. Como diretor técnico, o professor circula auxiliando grupos que encontrarem erros de exportação — tipicamente causados por caminhos de arquivo ou recursos referenciados de forma incorreta —, tratando cada erro encontrado como parte esperada do processo de empacotamento, não como falha do grupo.

## Desafio

Não há desafio de solução livre neste encontro: a exportação é guiada quanto ao processo (Export Templates, preset, geração do build), mas cada grupo decide os detalhes de apresentação do próprio build (nome do executável, ícone), dentro do que a plataforma-alvo escolhida permitir.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, um executável exportado do próprio Vertical Slice completo, capaz de abrir e rodar de forma independente do editor do Godot, sem qualquer regressão de mecânica, áudio ou desempenho em relação à versão validada na Semana 13.

## Evidências para Avaliação

Insumo direto para a entrega da semana (Vertical Slice final do Módulo 4, otimizado e exportado). Sem instrumento formal isolado neste encontro; o build gerado aqui é o objeto avaliado no Playtest cruzado e no Code Review de encerramento do Encontro 2.

## Dificuldades Esperadas

- Build exportado não abre ou fecha imediatamente por Export Templates ausentes ou incompatíveis com a versão do Godot em uso — reforçar a verificação da versão dos templates antes de depurar qualquer outra causa.
- Recursos (texturas, sons, cenas) que carregavam corretamente no editor mas falham no build exportado, geralmente por caminhos de arquivo referenciados de forma absoluta ou fora da pasta do projeto — reforçar o uso de caminhos relativos ao projeto (`res://`) em qualquer referência a recurso.
- Grupos tratando a exportação como etapa opcional de última hora em vez de parte do pipeline de produção — reforçar que um Vertical Slice que só roda no editor não é, para os fins desta unidade, um produto entregável.

---

# Encontro 2

## Objetivos de Aprendizagem

- Realizar Playtest do build exportado de outro grupo, sem acesso ao projeto aberto no editor.
- Aplicar critérios de Code Review já praticados no semestre (Semanas 7, 10 e 12) a um produto fechado, identificando problemas visíveis apenas fora do ambiente de desenvolvimento.
- Consolidar o próprio Vertical Slice com ajustes finais pontuais a partir do Playtest cruzado e do Code Review de encerramento.

## Conteúdos

- Playtest cruzado: cada grupo testa o build exportado de outro grupo, sem qualquer explicação prévia de quem desenvolveu, reproduzindo a experiência de um jogador ou avaliador externo.
- Code Review de encerramento: revisão geral do projeto sob a perspectiva de um pequeno estúdio entregando um produto, retomando os princípios de organização e ausência de lógica duplicada já cobrados nas Semanas 7, 10 e 12.
- Registro estruturado de problemas encontrados no Playtest cruzado (bugs, quedas de desempenho, falhas de áudio, problemas de usabilidade), distinguindo o que é ajuste pontual do que exigiria retrabalho fora do escopo desta semana.
- Aplicação de ajustes finais no próprio build, a partir do feedback recebido, dentro do tempo disponível do encontro.

## Conceitos Fundamentais

O Playtest cruzado retoma, sobre o produto final, o mesmo princípio já praticado em Playtests anteriores do semestre: quem desenvolveu um sistema deixa de enxergar seus próprios problemas depois de testá-lo repetidamente, e um avaliador externo revela falhas que o próprio grupo não veria. A diferença desta semana é o objeto avaliado — não mais o projeto aberto no editor, mas o build exportado, que expõe problemas que só aparecem fora do ambiente de desenvolvimento (erros de carregamento de recurso, comportamento diferente de performance, ausência de mensagens de erro do editor). O Code Review de encerramento generaliza, para o projeto completo acumulado desde o Módulo 1, os mesmos critérios já aplicados isoladamente nas Semanas 7 (SaveData), 10 (Interactable/Inventário) e 12 (materiais e composição de cena): organização, ausência de duplicação e local arquitetural único para cada sistema. Encerrar o Módulo 4 desta forma reforça, pela última vez no semestre antes da Unidade V, que produzir como um pequeno estúdio significa validar o produto sob a ótica de quem não o construiu, não apenas sob a ótica de quem o construiu.

## Recursos do Godot

Build exportado (executável), Export Templates/Project Export (revisão), Profiler/Debugger (se necessário para investigar problema reportado no Playtest).

## Comparação com Unity

A Unity resolve o mesmo problema de validação de build com QA/Playtest sobre builds gerados pelo Build Settings, frequentemente testados por pessoas fora da equipe de desenvolvimento direto — o princípio universal é idêntico: um build só está pronto quando validado por alguém que não o construiu, e problemas de build costumam diferir de problemas vistos no editor. A diferença está mais no processo de organização de equipe do que na ferramenta em si: tanto Godot quanto Unity dependem do mesmo ciclo de exportar, testar de forma cruzada e corrigir antes da entrega — a engine fornece o build, mas o processo de Playtest cruzado é uma prática de produção, não um recurso técnico específico de nenhuma das duas.

## Preparação do Professor

- Builds exportados de todos os grupos, coletados ao final do Encontro 1 (ou no início deste encontro), organizados para troca cruzada entre grupos.
- Ficha de Code Review (Sistema de Avaliação, Rubrica 4) para orientar a revisão de encerramento.
- Roteiro breve de Playtest cruzado (o que observar: carregamento, desempenho, áudio, usabilidade, ausência de erros) para orientar os grupos avaliadores.
- Projeto de referência do professor com um build já exportado, para demonstrar rapidamente o fluxo de Playtest cruzado antes de distribuir os builds entre os grupos.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (build exportado de cada grupo) e explicação do roteiro de Playtest cruzado |
| 55 min | Playtest cruzado: cada grupo testa o build exportado de outro grupo e registra observações |
| 35 min | Code Review de encerramento: cada grupo revisa a própria organização do projeto sob os critérios já praticados no semestre |
| 30 min | Ajustes finais pontuais no próprio build, a partir do feedback recebido |

## Desenvolvimento

O encontro abre com a troca cruzada dos builds exportados no Encontro 1 — cada grupo recebe o executável de outro grupo, sem acesso ao projeto aberto no editor, e conduz um Playtest seguindo o roteiro fornecido pelo professor. Enquanto testa, cada grupo registra problemas encontrados (bugs, desempenho, áudio, usabilidade), reproduzindo a experiência de um avaliador externo ao pequeno estúdio que produziu aquele build. Em seguida, cada grupo retorna ao próprio projeto e conduz o Code Review de encerramento, aplicando ao Vertical Slice completo os mesmos critérios de organização já cobrados nas Semanas 7, 10 e 12 — verificando se cada sistema (Interactable, SaveData, Inventário, HealthComponent, HUD, IA, materiais, áudio) permanece no local arquitetural correto, sem lógica duplicada entre cenas. O encontro fecha com cada grupo aplicando ajustes finais pontuais no próprio build, priorizando o feedback recebido no Playtest cruzado dentro do tempo restante — sem reabrir escopo além do que já foi construído ao longo do semestre.

## Desafio

Cada grupo aplica, no próprio Vertical Slice, os ajustes finais pontuais decorrentes do Playtest cruzado e do Code Review de encerramento, com liberdade de priorização sobre quais problemas corrigir dentro do tempo disponível, desde que a escolha seja justificada pelo impacto observado. **Entrega: Vertical Slice final (Módulo 4) otimizado e exportado (entrega parcial); Playtest cruzado; Code Review de encerramento.**

## Critérios de Sucesso

Cada grupo entrega, ao final da semana, um build exportado e ajustado do Vertical Slice completo, validado por Playtest cruzado de outro grupo e por Code Review de encerramento, sem regressão em nenhuma mecânica, sistema ou otimização já validados em semanas anteriores.

## Evidências para Avaliação

**Code Review** (Rubrica 4 do Sistema de Avaliação) — organização do projeto, ausência de lógica duplicada, local arquitetural correto de cada sistema acumulado desde o Módulo 1, aplicado ao projeto completo como revisão de encerramento da Unidade IV, conforme já previsto no Cronograma para a Semana 14. O Playtest cruzado é insumo direto para essa revisão, não um instrumento formal separado.

## Dificuldades Esperadas

- Grupos avaliando o build de outro grupo com foco em preferência estética pessoal em vez de problemas objetivos (bugs, desempenho, usabilidade) — reforçar o roteiro de Playtest como critério, não opinião livre.
- Tentar corrigir, nos ajustes finais, problemas que exigiriam retrabalho amplo fora do escopo do tempo restante — reforçar que a entrega desta semana é consolidação pontual, não uma nova rodada de desenvolvimento.
- Code Review de encerramento revelando duplicação de lógica acumulada de semanas diferentes (ex.: lógica de interação repetida em mais de uma cena) sem tempo hábil para refatoração completa — registrar o problema identificado como observação para a Unidade V, sem forçar retrabalho amplo nesta semana.

---

# Resultado Esperado da Semana

Ao final da Semana 14, cada grupo possui um build exportado e executável do Vertical Slice completo, acumulado desde a Semana 1, validado por Playtest cruzado de outro grupo e por Code Review de encerramento sob os mesmos critérios de organização já praticados nas Semanas 7, 10 e 12. O Módulo 4 — Produzir como um Pequeno Estúdio — está encerrado: o projeto está tecnicamente pronto, otimizado, sonorizado e empacotado como produto distribuível, sem pendências de gameplay, apresentação ou desempenho para além dos ajustes pontuais já aplicados nesta semana.

# Preparação para a Próxima Semana

A Semana 15 abre a Unidade V — Comparar Arquiteturas — com engenharia reversa de projetos profissionais (Godot Demo Projects, TPS Demo, Platformer 2D Demo). O Vertical Slice consolidado e exportado nesta semana passa a ser o ponto de comparação direto: cada decisão arquitetural tomada pelo próprio grupo ao longo do semestre (Signals, Autoload/Singleton, Resource customizado, Components, Behavior Tree, materiais, áudio, otimização) será confrontada com as soluções adotadas em projetos de referência oficiais, sem necessidade de qualquer retrabalho adicional no projeto além do que já foi ajustado nesta semana.

# Referências

- Godot Documentation — Exporting Projects: https://docs.godotengine.org/en/stable/tutorials/export/index.html
- Godot Documentation — Export Templates: https://docs.godotengine.org/en/stable/tutorials/export/exporting_projects.html
- Unity Manual (consulta comparativa) — Build Settings: https://docs.unity3d.com/Manual/BuildSettings.html
- Unity Manual (consulta comparativa) — Publishing Builds: https://docs.unity3d.com/Manual/PublishingBuilds.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
