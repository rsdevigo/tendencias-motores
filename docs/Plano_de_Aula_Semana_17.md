# Semana 17 🔴

## Introdução da Semana

A Semana 17 encerra a disciplina com a Apresentação Técnica Final do Vertical Slice, marco de encerramento da Unidade VI e do Módulo 5 — Comparação entre Motores. Não há conteúdo novo, sistema novo ou desafio de implementação: a semana consome diretamente os insumos produzidos na Semana 15 (análise arquitetural do Lyra e demais projetos de referência) e na Semana 16 (quadro comparativo Unreal x Unity consolidado, escolha justificada de um motor adicional, estrutura preliminar da apresentação). A metodologia dominante é Reverse Engineering, com autonomia muito alta: o professor atua exclusivamente como revisor e mediador das apresentações, nunca como demonstrador. Cada grupo apresenta o Vertical Slice completo — construído desde a Semana 1 e consolidado no build empacotado da Semana 14 —, justifica suas decisões arquiteturais e articula a comparação entre Unreal, Unity e o motor adicional escolhido. A semana se encerra com a **Apresentação Técnica Final**, instrumento avaliativo de maior peso do semestre, avaliado conjuntamente pela Rubrica 6 (Apresentações) e pela Rubrica 7 (Vertical Slice Final).

## Objetivos Gerais

- Apresentar tecnicamente o Vertical Slice completo, construído ao longo de todo o semestre.
- Justificar as decisões arquiteturais tomadas, com exemplos concretos do próprio projeto.
- Articular a comparação entre Unreal, Unity e o motor adicional escolhido na Semana 16.
- Responder a perguntas técnicas da turma e do professor sobre arquitetura, decisões e limitações do projeto.

## Resultados Esperados

Ao final da semana, cada grupo terá apresentado formalmente o Vertical Slice completo, com defesa oral das decisões arquiteturais e da comparação entre motores, encerrando a disciplina com autonomia demonstrada para transitar entre engines. Essa entrega corresponde à **Apresentação Técnica Final** prevista no Cronograma, avaliada pela Rubrica 6 e pela Rubrica 7, e reutiliza diretamente o quadro comparativo e a estrutura preliminar produzidos na Semana 16 — nenhum dos dois é refeito do zero.

---

# Encontro 1

## Objetivos de Aprendizagem

- Apresentar o Vertical Slice completo perante a turma e o professor, cobrindo gameplay, arquitetura e sistemas construídos ao longo do semestre.
- Justificar tecnicamente as decisões arquiteturais centrais do projeto, com exemplos nomeados do próprio Vertical Slice.
- Comparar explicitamente a arquitetura do projeto com a solução equivalente em Unity, conforme consolidado na Semana 16.

## Conteúdos

- Apresentação técnica final do primeiro grupo de apresentadores (metade da turma, conforme divisão feita previamente pelo professor).
- Demonstração ao vivo do build empacotado da Semana 14, sem alterações não documentadas.
- Defesa das decisões arquiteturais e da comparação Unreal x Unity, com apoio do quadro comparativo consolidado na Semana 16.

## Conceitos Fundamentais

O conceito universal que fecha toda a disciplina nesta apresentação é que dominar uma engine específica não é o objetivo final de um profissional de jogos — o objetivo é dominar os papéis arquiteturais que qualquer engine precisa resolver (composição de entidades, desacoplamento entre input e ação, ponto único de regras, comunicação entre sistemas, dados de design separados de lógica, persistência, máquinas de estado, interfaces em tempo real, estruturas de decisão para agentes) e reconhecer rapidamente como uma engine nova formaliza esses papéis. A apresentação técnica é o momento em que essa autonomia é verificada na prática: um grupo que apenas descreve "onde clicou" não demonstrou domínio; um grupo que explica por que uma decisão arquitetural foi tomada, quais alternativas existiam e como a mesma decisão seria implementada em outra engine demonstrou exatamente a competência que a disciplina se propôs a formar desde a Semana 1.

## Recursos da Unreal

Vertical Slice completo (build empacotado da Semana 14, sem alterações não documentadas); quadro comparativo Unreal x Unity consolidado na Semana 16; registro da comparação com o motor adicional (Godot, O3DE, Stride ou CryEngine) produzido na Semana 16.

## Comparação com Unity

Este é o próprio conteúdo da apresentação de cada grupo, não uma atividade conduzida pelo professor: cada grupo expõe, com base no quadro comparativo consolidado na Semana 16, o que permanece igual entre Unreal e Unity para os sistemas do próprio projeto e qual é a principal diferença arquitetural em cada caso. O professor não introduz conteúdo novo de Unity neste encontro — apenas verifica, nas perguntas, se a comparação apresentada é tecnicamente precisa.

## Preparação do Professor

- Confirmar previamente a ordem e a divisão dos grupos entre Encontro 1 e Encontro 2.
- Testar o build empacotado de cada grupo antes da apresentação (não avaliar apenas a versão no editor).
- Ter em mãos a Rubrica 6 e a Rubrica 7 para preenchimento durante cada apresentação.
- Preparar perguntas técnicas de sondagem para cada grupo, com base no histórico de checkpoints e code reviews do semestre.
- Reservar tempo de troca de equipamento entre apresentações (build, projetor, áudio).

## Cronograma do Encontro

10 min — Abertura: ordem das apresentações, tempo por grupo, critérios de avaliação relembrados (Rubrica 6 e Rubrica 7).

90 min — Apresentações técnicas do primeiro grupo de equipes (tempo fixo por grupo, incluindo demonstração ao vivo do build e perguntas).

25 min — Perguntas finais e feedback formal do professor aos grupos que apresentaram, com apontamentos que orientam eventuais ajustes antes do Encontro 2.

10 min — Encerramento do encontro: síntese das apresentações do dia e organização para o Encontro 2.

## Desenvolvimento

O encontro abre com a reafirmação dos critérios de avaliação — Rubrica 6 para a apresentação em si e Rubrica 7 para o Vertical Slice — e a ordem definida previamente pelo professor. Cada grupo do primeiro bloco apresenta, dentro do tempo estabelecido, o Vertical Slice completo: visão geral do projeto, demonstração ao vivo do build empacotado, justificativa das decisões arquiteturais centrais (por que o gameplay framework foi estruturado daquela forma, por que a interação e o inventário foram implementados daquele jeito, quais trade-offs de polimento e otimização foram feitos no Módulo 4) e a comparação explícita com Unity e com o motor adicional escolhido na Semana 16. Após cada apresentação, o professor e a turma fazem perguntas técnicas, testando se a defesa vai além da descrição de funcionalidades e alcança a justificativa arquitetural. O professor preenche a Rubrica 6 e a Rubrica 7 durante ou imediatamente após cada apresentação, verificando também se o build testado corresponde ao que foi entregue na Semana 14, sem alterações não documentadas. O encontro fecha com feedback formal aos grupos que já apresentaram.

## Desafio

Não há desafio formal — o Encontro 1 é a própria apresentação técnica final do primeiro grupo de equipes, avaliada pelas Rubricas 6 e 7.

## Critérios de Sucesso

Cada grupo do primeiro bloco apresentou o Vertical Slice completo dentro do tempo estabelecido, demonstrou o build empacotado funcionando, justificou tecnicamente pelo menos três decisões arquiteturais centrais com exemplos nomeados do próprio projeto, e articulou a comparação com Unity e com o motor adicional escolhido.

## Evidências para Avaliação

A apresentação de cada grupo é avaliada pela Rubrica 6 (Comunicação, Demonstração, Justificativas técnicas, Domínio do projeto, Capacidade de responder perguntas) e pela Rubrica 7 (Arquitetura, Gameplay, Organização, Qualidade técnica, Polimento, Uso correto dos recursos da Unreal, Consistência, Documentação, Empacotamento, Capacidade de explicar decisões), sem considerar qualidade artística ou quantidade de assets.

## Dificuldades Esperadas

Grupos podem preparar uma apresentação essencialmente descritiva ("o jogador faz isso, depois isso") sem justificativa arquitetural — o professor deve redirecionar com perguntas diretas ("por que essa decisão e não outra?", "como isso seria feito em Unity?") sempre que a apresentação permanecer no nível de funcionalidade. Também é comum que o build apresentado divirja do build entregue na Semana 14 sem aviso — o professor deve perguntar explicitamente se houve alterações desde a entrega e registrar qualquer divergência não documentada como um ponto de atenção na Rubrica 7.

---

# Encontro 2

## Objetivos de Aprendizagem

- Apresentar o Vertical Slice completo perante a turma e o professor, cobrindo gameplay, arquitetura e sistemas construídos ao longo do semestre (grupos restantes).
- Justificar tecnicamente as decisões arquiteturais centrais do projeto, com exemplos nomeados do próprio Vertical Slice.
- Sintetizar, em discussão coletiva final, a autonomia construída ao longo do semestre para aprender e transitar entre motores de jogos.

## Conteúdos

- Apresentação técnica final dos grupos restantes.
- Discussão final coletiva sobre autonomia para aprendizagem de novos motores, encerrando a disciplina.

## Conceitos Fundamentais

Mesmo conceito universal do Encontro 1, agora fechado em discussão coletiva: a disciplina não teve como objetivo formar especialistas em Unreal Engine, mas profissionais capazes de reconhecer, em qualquer motor, os mesmos papéis arquiteturais estudados durante o semestre. A discussão final do Encontro 2 é o espaço em que essa síntese é verbalizada coletivamente — não mais por grupo isolado, mas como turma —, revisitando a trajetória desde o primeiro contato com o editor da Unreal na Semana 1 até a capacidade, demonstrada nas apresentações, de comparar arquiteturas entre engines de forma justificada.

## Recursos da Unreal

Vertical Slice completo (build empacotado da Semana 14, sem alterações não documentadas); quadro comparativo Unreal x Unity consolidado na Semana 16; registro da comparação com o motor adicional produzido na Semana 16.

## Comparação com Unity

Assim como no Encontro 1, a comparação é conduzida por cada grupo durante a própria apresentação, com base no trabalho da Semana 16. Na discussão final, a comparação com Unity (e com os demais motores citados ao longo do semestre) é retomada de forma coletiva e conceitual, não mais projeto a projeto, fechando a generalização buscada por toda a disciplina.

## Preparação do Professor

- Confirmar a ordem dos grupos restantes.
- Testar o build empacotado de cada grupo antes da apresentação.
- Ter em mãos a Rubrica 6 e a Rubrica 7 para preenchimento durante cada apresentação.
- Preparar perguntas de síntese para a discussão final coletiva (o que mudou na forma de pensar arquitetura de jogos ao longo do semestre).
- Preparar o encerramento formal da disciplina (devolutiva geral, lançamento de notas, encaminhamentos finais).

## Cronograma do Encontro

90 min — Apresentações técnicas dos grupos restantes (tempo fixo por grupo, incluindo demonstração ao vivo do build e perguntas).

20 min — Perguntas finais e feedback formal do professor aos grupos que apresentaram neste encontro.

20 min — Discussão final coletiva: autonomia construída ao longo do semestre para aprender e transitar entre motores de jogos.

5 min — Encerramento formal da disciplina.

## Desenvolvimento

O encontro segue exatamente a mesma dinâmica do Encontro 1 para os grupos restantes: apresentação do Vertical Slice completo, demonstração ao vivo do build empacotado, justificativa das decisões arquiteturais e comparação com Unity e com o motor adicional escolhido, seguida de perguntas técnicas e preenchimento das Rubricas 6 e 7 pelo professor. Encerradas todas as apresentações da turma, o encontro se volta para uma discussão coletiva final, conduzida pelo professor, revisitando a trajetória do semestre — do primeiro tour pelo editor na Semana 1 à capacidade de justificar arquitetura e comparar motores demonstrada nas apresentações — e consolidando, com a turma, a resposta à pergunta que orientou toda a disciplina: o que se aprendeu sobre arquitetura de motores de jogos e sobre a autonomia para aprender motores novos. O encontro, e a disciplina, se encerram com a devolutiva formal do professor.

## Desafio

Não há desafio formal — o Encontro 2 é a própria apresentação técnica final dos grupos restantes, seguida da discussão de encerramento da disciplina.

## Critérios de Sucesso

Cada grupo restante apresentou o Vertical Slice completo dentro do tempo estabelecido, demonstrou o build empacotado funcionando, justificou tecnicamente pelo menos três decisões arquiteturais centrais e articulou a comparação com Unity e com o motor adicional escolhido; a turma participou da discussão final de encerramento.

## Evidências para Avaliação

A apresentação de cada grupo é avaliada pela Rubrica 6 e pela Rubrica 7, nos mesmos termos do Encontro 1. A discussão final de encerramento não gera nota, mas encerra formalmente a verificação de autonomia que orientou toda a disciplina.

## Dificuldades Esperadas

As mesmas do Encontro 1: apresentações descritivas sem justificativa arquitetural e divergência não documentada entre o build apresentado e o entregue na Semana 14. Adicionalmente, na discussão final, alunos podem restringir a síntese a "aprendemos Unreal Engine" — o professor deve redirecionar a discussão para o objetivo real da disciplina, reforçando que o aprendizado central foi arquitetural e transferível, com a Unreal como estudo de caso.

---

# Resultado Esperado da Semana

Ao final da Semana 17, todos os grupos terão apresentado tecnicamente o Vertical Slice completo construído ao longo do semestre, com defesa justificada das decisões arquiteturais e comparação explícita entre Unreal, Unity e o motor adicional escolhido na Semana 16. A disciplina se encerra com o Vertical Slice funcional completo, avaliado pela Rubrica 6 (Apresentações) e pela Rubrica 7 (Vertical Slice Final), e com autonomia demonstrada, individual e coletivamente, para reconhecer conceitos universais de arquitetura de motores de jogos e transitar entre engines diferentes.

# Preparação para a Próxima Semana

Não há próxima semana: a Semana 17 encerra o Cronograma e a disciplina. Não há preparação subsequente a indicar.

# Referências

- Epic Games — Unreal Engine Documentation (Gameplay Framework, Blueprints, Animation, Behavior Trees, UMG, Materials, Packaging), consultada de forma pontual para eventuais dúvidas durante as apresentações.
- Unity Technologies — Unity Manual (https://docs.unity3d.com/Manual/) e Unity Learn (https://learn.unity.com/), como referência de apoio à comparação apresentada por cada grupo.
- Documentação oficial pública de Godot, O3DE, Stride e CryEngine, conforme o motor escolhido por cada grupo na Semana 16.
- Sistema_de_Avaliacao_Tendencias_de_Motores_de_Jogos.md — Rubrica 6 (Apresentações) e Rubrica 7 (Vertical Slice Final), instrumentos avaliativos desta semana.
- PROJECT_ARCHITECTURE.md — referência de consistência entre o que é apresentado e o que foi efetivamente construído ao longo do semestre.

Não há indicação de vídeos complementares nesta semana: o conteúdo é inteiramente produzido pelos próprios grupos.
