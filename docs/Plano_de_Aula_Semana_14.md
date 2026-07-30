# Semana 14 🔴

## Introdução da Semana

A Semana 14 encerra a Unidade IV — Produzir como um Pequeno Estúdio. Depois de a Semana 13 ter tratado áudio como resposta a eventos de gameplay e profiling como etapa obrigatória de produção, esta semana conclui o ciclo de produção com o pipeline de Packaging — o processo que transforma o projeto editável em um build distribuível — e uma revisão geral do Vertical Slice sob a perspectiva de um pequeno estúdio, encerrada por Playtest cruzado entre grupos e Code Review de encerramento. O Encontro 1 fundamenta o pipeline de Packaging (configurações, plataformas-alvo, build de produção) e conduz o empacotamento guiado do Vertical Slice de cada grupo. O Encontro 2 realiza o Playtest cruzado — cada grupo testa o build empacotado de outro grupo — e fecha a unidade com Code Review de encerramento sobre os ajustes finais. Nenhum sistema anterior é descartado: `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD`, `BP_Enemy` com Behavior Tree/Blackboard, Material Instances, Foliage e a camada de Áudio da Semana 13 permanecem intactos — esta semana não adiciona gameplay novo, apenas empacota e valida o que já existe.

## Objetivos Gerais

- Compreender o que diferencia um protótipo rodando no editor de um build distribuível.
- Compreender as configurações de Packaging e a escolha de plataforma-alvo como decisões técnicas, não apenas passos operacionais.
- Empacotar o Vertical Slice de cada grupo em um build estável, executável fora do editor.
- Validar o build de um colega através de Playtest cruzado e conduzir o Code Review de encerramento do Módulo 4.

## Resultados Esperados

Ao final da semana, cada grupo terá um build empacotado do seu Vertical Slice, testado tanto pelo próprio grupo quanto por outro grupo via Playtest cruzado, com os bugs e pontos de confusão observados registrados e discutidos no Code Review de encerramento. Essa entrega corresponde à "entrega parcial" da Rubrica 7 (Vertical Slice Final), avaliada formalmente na Semana 14 e reconfirmada na Semana 17.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o que diferencia um protótipo de um build distribuível.
- Identificar as configurações de Packaging relevantes para o projeto (plataforma-alvo, configuração de build, conteúdo incluído).
- Empacotar o Vertical Slice do próprio grupo em um build executável, estável fora do editor.

## Conteúdos

- Pipeline de Packaging: Project Settings relevantes, seleção de plataforma-alvo, configuração de build (Development/Shipping).
- Diferença entre rodar o jogo no editor (Play In Editor) e rodar um build empacotado.
- Empacotamento guiado do Vertical Slice de cada grupo, já otimizado desde a Semana 13.

## Conceitos Fundamentais

O conceito universal desta aula é que todo motor de jogo separa o ambiente de edição do produto final: o editor existe para iterar rapidamente, mas o jogador nunca abre o editor — ele recebe um build compilado, empacotado e independente do ambiente de desenvolvimento. Packaging é o processo que resolve essa separação, compilando o projeto, empacotando os assets referenciados e gerando um executável autônomo para uma plataforma-alvo específica. Esse processo expõe problemas que passam despercebidos no editor — referências quebradas, assets não incluídos, dependências ausentes — e por isso não é um passo burocrático de final de produção, mas o momento em que o projeto é confrontado com as mesmas condições em que o jogador final vai executá-lo. É também o motivo pelo qual o profiling e a otimização da Semana 13 precedem o Packaging: um projeto com gargalos não tratados chega ao build final do mesmo jeito, apenas mais difícil de diagnosticar fora do editor.

## Recursos da Unreal

Project Settings (Packaging), seleção de plataforma-alvo, Build Configuration (Development/Shipping), Package Project, Maps & Modes (mapa inicial do build).

## Comparação com Unity

A Unity resolve o mesmo problema com Build Settings, onde o desenvolvedor escolhe plataforma-alvo e configurações de build (Debug/Release) de forma conceitualmente equivalente ao Packaging da Unreal. O princípio é idêntico nas duas engines — separar o ambiente de edição do produto executável final, compilando e empacotando apenas o necessário para a plataforma escolhida —, mas a Unreal tende a concentrar as configurações relevantes em Project Settings antes de uma única ação de empacotamento, enquanto a Unity expõe a maior parte dessas escolhas diretamente na janela de Build Settings a cada execução. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o Vertical Slice do Módulo 3, a camada visual da Semana 12 e a camada de áudio e otimizações da Semana 13 intactas.
- Configuração de Packaging pré-testada (fora da visão da turma) na máquina/plataforma usada em laboratório, evitando surpresas de tempo de build durante a aula.
- Documentação de Unreal Engine — Packaging Your Project disponível para consulta durante o laboratório.
- Espaço em disco e tempo de build estimados previamente, considerando o tamanho médio dos projetos da turma.
- **Nota de contingência:** o Packaging do build final é pré-requisito do Playtest cruzado do Encontro 2; se necessário, priorizar a conclusão do empacotamento de todos os grupos sobre a profundidade da fundamentação teórica, garantindo que nenhum grupo chegue ao Encontro 2 sem um build gerado.

## Cronograma do Encontro

- 15 min — Revisão do estado atual do Vertical Slice (áudio e otimizações da Semana 13).
- 20 min — Fundamentação: o que diferencia um protótipo de um build distribuível; pipeline de Packaging.
- 30 min — Demonstração: configuração de Project Settings, escolha de plataforma-alvo e empacotamento guiado de um projeto de teste.
- 60 min — Laboratório: cada grupo empacota o próprio Vertical Slice, resolvendo problemas de referência ou conteúdo ausente que surjam no processo.
- 10 min — Feedback: verificação de que cada grupo possui um build executável fora do editor.

## Desenvolvimento

O professor demonstra as configurações de Packaging relevantes — plataforma-alvo, configuração de build, mapa inicial — sobre um projeto de teste, e executa o empacotamento completo, mostrando o build resultante rodando fora do editor. Em seguida, cada grupo aplica o mesmo processo ao próprio Vertical Slice, já otimizado na Semana 13, resolvendo eventuais problemas de referências quebradas ou assets não incluídos que só aparecem durante o empacotamento. O encontro termina quando cada grupo possui um build executável e estável, pronto para o Playtest cruzado do Encontro 2.

## Desafio

Não há desafio de liberdade de solução neste encontro — o empacotamento é demonstração e aplicação guiada sobre o próprio projeto, garantindo que todos os grupos cheguem ao Encontro 2 com um build funcional.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um build empacotado do próprio Vertical Slice, executável fora do editor, sem erros de referência ou conteúdo ausente, preservando intactos todos os sistemas de gameplay e a camada visual e sonora construídos até a Semana 13.

## Evidências para Avaliação

Existência e estabilidade do build empacotado de cada grupo — insumo direto para o critério "Empacotamento" da Rubrica 7 (Vertical Slice Final), que exige que o "build final empacotado (Packaging) roda de forma estável fora do editor, em condições equivalentes às testadas na Semana 14".

## Dificuldades Esperadas

Grupos podem encontrar referências quebradas ou assets não incluídos no build, mesmo funcionando normalmente no editor. Intervenção: conduzir o grupo a identificar se o asset pertence a uma pasta fora da estrutura padrão do PROJECT_ARCHITECTURE.md ou se há uma referência direta a um asset de teste/temporário esquecido no nível. Grupos com tempo de build muito longo devem ser orientados a reduzir a configuração de build utilizada em laboratório (sem comprometer a entrega final), priorizando a conclusão do empacotamento dentro do tempo do encontro.

---

# Encontro 2

## Objetivos de Aprendizagem

- Revisar o Vertical Slice sob a perspectiva de um pequeno estúdio entregando um produto a um público externo.
- Testar o build empacotado de outro grupo e registrar bugs e pontos de confusão observados.
- Conduzir o Code Review de encerramento do Módulo 4, discutindo os ajustes finais necessários.

## Conteúdos

- Revisão geral do projeto sob a perspectiva de produção de um pequeno estúdio.
- Playtest cruzado: cada grupo testa o build empacotado de outro grupo.
- Code Review de encerramento do Módulo 4: discussão dos ajustes finais a partir dos bugs e pontos de confusão registrados no Playtest cruzado.

## Conceitos Fundamentais

O conceito universal desta aula é que nenhuma equipe de desenvolvimento consegue avaliar objetivamente o próprio produto — jogadores que não participaram da construção enxergam confusões, bugs e atritos invisíveis para quem construiu o sistema. O Playtest cruzado formaliza essa perspectiva externa dentro da disciplina: cada grupo passa a ocupar, por um momento, o papel do jogador final de outro grupo, e não do desenvolvedor. Essa prática é universal a qualquer processo de produção de jogos, independentemente da engine, e antecipa o papel do Code Review de encerramento, que não avalia mais sistemas isolados (como nos Code Reviews anteriores do semestre), mas o produto como um todo entregável — coerente com a passagem do Módulo 4 de "construir sistemas" para "produzir como um pequeno estúdio".

## Recursos da Unreal

Build empacotado gerado no Encontro 1, execução do build fora do editor em máquina de outro grupo, revisão de conteúdo via Content Browser durante o Code Review.

## Comparação com Unity

A Unity resolve o mesmo problema de produção com processos equivalentes de build testing e revisão de projeto antes de um marco de entrega, sem uma ferramenta dedicada distinta do que já foi comparado no Encontro 1. O princípio de produção é o mesmo nas duas engines — validar o build fora do ambiente de quem o construiu, antes de considerá-lo pronto —, independentemente de qual engine gerou o executável. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Builds empacotados de todos os grupos, gerados no Encontro 1, prontos para execução cruzada.
- Esquema de rodízio definido previamente (qual grupo testa o build de qual outro grupo).
- Modelo de registro de bugs e pontos de confusão (formulário simples ou checklist) para uso durante o Playtest cruzado.
- Sistema de Avaliação (Rubrica 7 — Vertical Slice Final) disponível para conduzir o Code Review de encerramento.
- **Nota de contingência:** o Code Review de encerramento é o núcleo avaliativo do encontro e não deve ser comprimido; se necessário, reduzir o tempo de Playtest cruzado, mantendo intacto o tempo reservado ao Code Review.

## Cronograma do Encontro

- 10 min — Revisão do Packaging do Encontro 1 e organização do rodízio de Playtest cruzado.
- 15 min — Fundamentação: por que a perspectiva externa do jogador é insubstituível na revisão de um produto.
- 45 min — Playtest cruzado: cada grupo testa o build empacotado de outro grupo, registrando bugs e pontos de confusão.
- 30 min — Ajustes finais: cada grupo trata, quando possível, os problemas mais críticos apontados no Playtest cruzado do próprio build.
- 35 min — Code Review de encerramento do Módulo 4, com base no Sistema de Avaliação (Rubrica 7).

## Desenvolvimento

O professor organiza o rodízio de Playtest cruzado, garantindo que nenhum grupo teste o próprio build, e conduz uma fundamentação breve sobre por que a perspectiva de um jogador externo revela problemas que a equipe de desenvolvimento não percebe. Cada grupo executa o build empacotado de outro grupo, registrando bugs e pontos de confusão observados. Em seguida, cada grupo recebe o registro produzido sobre o próprio build e trata os problemas mais críticos que o tempo permitir. O encontro se encerra com o Code Review de encerramento do Módulo 4, no qual o professor, atuando como diretor técnico, revisa o Vertical Slice de cada grupo à luz da Rubrica 7 (Vertical Slice Final), discutindo arquitetura, organização, qualidade técnica, empacotamento e a capacidade de cada grupo de explicar as decisões tomadas ao longo do módulo.

## Desafio

Cada grupo trata, dentro do tempo disponível, os problemas mais críticos identificados pelo Playtest cruzado no próprio build, priorizando o que compromete a jogabilidade ou a estabilidade sobre ajustes cosméticos — não há lista fechada de correções, cada grupo decide a própria priorização com base no registro recebido.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve ter testado o build de outro grupo com registro de bugs e pontos de confusão, tratado os problemas mais críticos apontados no próprio build dentro do tempo disponível, e participado do Code Review de encerramento do Módulo 4 com capacidade de explicar as decisões técnicas tomadas.

## Evidências para Avaliação

Registro de bugs e pontos de confusão produzido no Playtest cruzado, qualidade dos ajustes finais tratados e desempenho no Code Review de encerramento — insumo direto para a Rubrica 7 (Vertical Slice Final), cujos critérios de Arquitetura, Gameplay, Organização, Qualidade técnica, Polimento, Uso correto dos recursos da Unreal, Consistência, Documentação, Empacotamento e Capacidade de explicar decisões compõem a entrega parcial desta semana, reconfirmada na Semana 17. Não avaliar qualidade artística nem quantidade de assets, conforme aviso explícito do Sistema de Avaliação.

## Dificuldades Esperadas

Grupos podem reagir defensivamente aos bugs apontados pelo Playtest cruzado, tratando as observações como crítica pessoal em vez de dado de produção. Intervenção: reforçar que o objetivo do Playtest cruzado é justamente capturar a perspectiva que a própria equipe não consegue ter, e que o registro de bugs é parte esperada e valiosa do processo, não uma falha do grupo. Grupos podem também tentar corrigir todos os pontos apontados sem priorização, esgotando o tempo disponível em ajustes cosméticos. Intervenção: conduzir o grupo a classificar os problemas registrados por impacto (compromete jogabilidade/estabilidade versus cosmético) antes de iniciar qualquer correção.

---

# Resultado Esperado da Semana

Ao final da Semana 14, cada grupo terá um Vertical Slice empacotado em um build estável, executável fora do editor, testado tanto pelo próprio grupo quanto por outro grupo via Playtest cruzado, com os problemas mais críticos tratados e discutidos no Code Review de encerramento do Módulo 4. Conceitualmente, a turma deve dominar a ideia de que Packaging separa o ambiente de edição do produto final, e que a perspectiva externa de um jogador é insubstituível na revisão de um produto. Todos os sistemas construídos ao longo do semestre — `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD`, `BP_Enemy` com Behavior Tree/Blackboard, Material Instances, Foliage e a camada de Áudio da Semana 13 — permanecem intactos e presentes no build final, que constitui a entrega parcial da Rubrica 7 (Vertical Slice Final), reconfirmada na Semana 17. Encerra-se aqui a Unidade IV — Produzir como um Pequeno Estúdio.

# Preparação para a Próxima Semana

A Semana 15 abre a Unidade V — Comparar Arquiteturas, com metodologia de Reverse Engineering e autonomia muito alta: os estudantes passam a analisar projetos profissionais (Lyra, Stack O Bot, Content Examples) em vez de continuar construindo o próprio Vertical Slice. O build empacotado e estável desta semana serve como ponto de comparação concreto — os próprios grupos poderão contrastar as decisões arquiteturais que tomaram com as decisões observadas nos projetos profissionais analisados a partir da Semana 15.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Packaging Your Project. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução ao pipeline de Packaging e build de produção. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Build Settings, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Packaging; **PrismaticaDev**, para exemplos aplicados de preparação de build final; **Ryan Laley**, para exemplos práticos de checklist de produção antes do empacotamento.
