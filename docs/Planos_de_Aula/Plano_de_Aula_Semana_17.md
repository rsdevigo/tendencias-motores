# Semana 17 — Apresentação Técnica Final do Vertical Slice

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade V — Comparar Arquiteturas e Aprender Novos Motores** (Semanas 15–17) | **Metodologia:** Reverse Engineering — apresentações e defesa técnica. Autonomia muito alta; professor atua como avaliador e mediador da sessão de perguntas.
**Encerramento de Módulo (🔴)** — esta semana encerra a Unidade V, o Módulo 5 e a disciplina inteira. Não há conteúdo novo: é a apresentação técnica final de cada grupo.

## Introdução da Semana

A Semana 16 fechou o núcleo comparativo da Unidade V: cada grupo produziu um quadro comparativo sistemático Godot x Unity cobrindo os Módulos 1 a 4, ampliou a comparação para Unreal Engine, O3DE e Stride, escolheu e justificou um desses três motores para aprofundamento, e entregou um checkpoint de preparação — recorte do Vertical Slice, decisões arquiteturais centrais e comparação entre motores escolhida como fio condutor. Nenhum sistema novo foi implementado desde a Semana 14; o projeto permanece no estado consolidado e exportado como Vertical Slice final. A Semana 17 não introduz conteúdo: é o encontro em que cada grupo apresenta, defende e é arguido sobre o próprio projeto, distribuído nos dois encontros da semana. O produto da semana não é um novo sistema no jogo, é a apresentação técnica final — o instrumento de maior peso do semestre, conforme o Sistema de Avaliação (Apresentações, 10%; Vertical Slice Final, 20%, com defesa arquitetural nesta semana).

## Objetivos Gerais

- Apresentar tecnicamente o Vertical Slice desenvolvido ao longo do semestre, com recorte claro definido no checkpoint da Semana 16.
- Justificar decisões arquiteturais tomadas em módulos anteriores, articulando o conceito universal de Game Engine por trás de cada escolha de implementação no Godot.
- Comparar o projeto e o Godot com a Unity e com o motor adicional (Unreal Engine, O3DE ou Stride) escolhido na Semana 16.
- Responder a perguntas técnicas da turma e do professor, demonstrando domínio real do projeto, não apenas do roteiro de apresentação.

## Resultados Esperados

Ao final da semana, todos os grupos terão apresentado e defendido tecnicamente o próprio Vertical Slice, terão sido arguidos pela turma e pelo professor sobre decisões arquiteturais específicas, e terão articulado, com vocabulário próprio, a comparação entre Godot, Unity e o motor adicional escolhido. A disciplina se encerra com a discussão final sobre autonomia para aprendizagem de novos motores — a competência central que atravessou os cinco módulos.

---

# Encontro 1

## Objetivos de Aprendizagem

- Apresentar o Vertical Slice do primeiro grupo de apresentações, com recorte definido no checkpoint da Semana 16.
- Justificar oralmente, com clareza técnica, ao menos três decisões arquiteturais centrais do projeto.
- Responder a perguntas técnicas sobre a implementação e as escolhas de arquitetura, demonstrando domínio real do projeto.

## Conteúdos

- Apresentações técnicas finais dos grupos do primeiro bloco (metade da turma, conforme distribuição definida pelo professor com base no número total de grupos e no tempo disponível no encontro).
- Estrutura de apresentação já roteirizada no checkpoint da Semana 16: recorte do Vertical Slice, decisões arquiteturais centrais, comparação entre motores.
- Sessão de perguntas técnicas após cada apresentação, conduzida pela turma e pelo professor.

## Conceitos Fundamentais

Não há conceito novo de Game Engine introduzido neste encontro. O conceito fundamental em jogo é a síntese de todo o semestre: a capacidade de nomear, para qualquer sistema construído no Vertical Slice, o conceito universal que ele resolve, a implementação específica adotada no Godot, e ao menos um motor alternativo em que o mesmo problema aparece sob outro nome. Essa tríade — conceito, implementação, transferência — é a competência que a disciplina construiu desde a Semana 1 e que a apresentação técnica final avalia diretamente, não como recital de funcionalidades, mas como demonstração de raciocínio arquitetural.

## Recursos do Godot

- Vertical Slice completo de cada grupo, executado ao vivo ou demonstrado em vídeo/build exportado, conforme a infraestrutura disponível na sala.
- Nenhum recurso novo do Godot é aberto no editor; o projeto de cada grupo é usado como evidência da apresentação, não como objeto de nova exploração.

## Comparação com Unity

Cada apresentação deve conter a comparação Godot x Unity estruturada no quadro da Semana 16, aplicada especificamente às decisões arquiteturais que o grupo escolheu destacar — não uma repetição genérica do quadro comparativo, mas sua aplicação concreta ao recorte apresentado (por exemplo, ao justificar o uso de Autoload para o GameManager, o grupo situa essa escolha frente ao padrão de Managers/Singletons da Unity).

## Preparação do Professor

- Ordem de apresentação dos grupos e tempo definido por grupo (recomenda-se 10–12 minutos de apresentação e 5–8 minutos de perguntas por grupo, ajustado ao número de grupos da turma).
- Rubrica de Apresentações e Rubrica de Vertical Slice Final (Sistema de Avaliação) impressas ou abertas para preenchimento durante cada apresentação.
- Projetor, som e acesso aos builds exportados de cada grupo testados antes do início do encontro, para evitar perda de tempo com problemas técnicos.
- Perguntas de arguição preparadas por grupo, com base no checkpoint da Semana 16 e no histórico de decisões de cada projeto ao longo do semestre.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| 10 min | Abertura do encontro, ordem de apresentação e regras da sessão de perguntas |
| ~105 min | Apresentações técnicas do primeiro bloco de grupos (tempo dividido conforme número de grupos) |
| 20 min | Feedback consolidado do professor sobre o bloco apresentado e fechamento do Encontro 1 |

## Desenvolvimento

O encontro abre com a definição da ordem de apresentação e das regras da sessão de perguntas — cada grupo apresenta o recorte do Vertical Slice definido no checkpoint da Semana 16, justifica as decisões arquiteturais destacadas e situa o projeto na comparação Godot x Unity x motor adicional escolhido. Após cada apresentação, a turma e o professor fazem perguntas técnicas, distribuídas entre os integrantes do grupo para garantir que a defesa não recaia sobre uma única pessoa. O professor registra, ao longo das apresentações, as evidências para as rubricas de Apresentações e de Vertical Slice Final. O encontro fecha com feedback consolidado do professor sobre o bloco apresentado, sem aguardar o encerramento de todas as apresentações da disciplina — o feedback imediato reforça o padrão esperado para os grupos que apresentam no Encontro 2.

## Desafio

Não há desafio de implementação nesta semana. O desafio do encontro é a própria defesa técnica: cada grupo deve responder a perguntas não previstas no roteiro do checkpoint, demonstrando que o domínio do projeto vai além do que foi ensaiado.

## Critérios de Sucesso

Cada grupo do primeiro bloco apresenta o recorte definido no checkpoint, justifica ao menos três decisões arquiteturais com clareza técnica, articula a comparação com Unity e com o motor adicional escolhido, e responde às perguntas da sessão de arguição demonstrando domínio real da implementação.

## Evidências para Avaliação

Rubrica de Apresentações (10% da nota final) e Rubrica de Vertical Slice Final (20%, critérios de Arquitetura e de Capacidade de Explicar Decisões), aplicadas em conjunto nesta semana conforme previsto no Sistema de Avaliação — a defesa oral é o principal instrumento de evidência para ambas.

## Dificuldades Esperadas

- Grupos excedendo o tempo de apresentação por tentar cobrir o semestre inteiro em vez do recorte definido no checkpoint — o professor deve interromper com cortesia e redirecionar para o tempo restante.
- Um único integrante do grupo concentrando todas as respostas da sessão de perguntas — reforçar a distribuição de perguntas entre os integrantes, conforme já indicado no Sistema de Avaliação.
- Justificativas de arquitetura genéricas ("usamos porque é assim que se faz") em vez de justificativas técnicas específicas — o professor deve perguntar diretamente "o que aconteceria se essa decisão fosse diferente?" para forçar a articulação do raciocínio.

---

# Encontro 2

## Objetivos de Aprendizagem

- Apresentar o Vertical Slice do segundo grupo de apresentações, com o mesmo padrão de defesa técnica do Encontro 1.
- Participar da discussão final da disciplina sobre autonomia para aprendizagem de novos motores de jogos.
- Consolidar, coletivamente, o que a turma aprendeu sobre arquitetura de Game Engines ao longo do semestre.

## Conteúdos

- Apresentações técnicas finais dos grupos do segundo bloco (restante da turma).
- Discussão final da disciplina: o que é transferível entre motores e o que foi, de fato, aprendido sobre autonomia para aprender um motor novo.
- Encerramento formal da disciplina.

## Conceitos Fundamentais

O conceito fundamental deste encontro é o fechamento da premissa que abriu a disciplina na Semana 1: a engine é um estudo de caso, não o objetivo. Depois de dezessete semanas construindo um único Vertical Slice em Godot, a discussão final pergunta à turma, de forma direta, se essa premissa se sustentou — se, de fato, cada estudante sairia desta disciplina capaz de abrir Unity, Unreal, O3DE ou qualquer outro motor e localizar, com razoável rapidez, onde vivem os mesmos conceitos universais que aprendeu aqui: estado global de partida, comunicação desacoplada entre sistemas, dados de design fora do código, navegação e decisão autônoma de agentes, pipeline de exportação. A resposta a essa pergunta é o verdadeiro produto final da disciplina, mais do que o próprio Vertical Slice.

## Recursos do Godot

- Vertical Slice completo dos grupos do segundo bloco.
- Nenhum recurso novo do Godot é aberto no editor; o Godot aparece, na discussão final, como um dos motores possíveis, não como o centro exclusivo da conversa.

## Comparação com Unity

Assim como no Encontro 1, cada apresentação do segundo bloco deve conter a comparação Godot x Unity aplicada ao recorte apresentado. Na discussão final, a comparação se amplia deliberadamente: a pergunta não é mais "como isso funciona no Godot e na Unity", mas "o que eu levo desta disciplina que me serve em qualquer motor que eu vier a usar depois de formado".

## Preparação do Professor

- Continuação da ordem de apresentação e da rubrica iniciada no Encontro 1.
- Roteiro de perguntas para a discussão final: por exemplo, "qual sistema construído no semestre você reconheceria mais rápido em um motor novo?", "qual decisão arquitetural do seu projeto você mudaria sabendo o que sabe hoje?", "o que no Godot foi mais fácil ou mais difícil de aprender do que na Unity, e por quê?".
- Planilha ou documento consolidado de notas/feedback de todas as rubricas do semestre, para eventual devolutiva individual ou por grupo após o encerramento.
- Encaminhamentos administrativos de encerramento da disciplina (registro de notas, avaliação institucional, entrega final de artefatos), conforme calendário acadêmico do IFMS.

## Cronograma do Encontro

| Duração | Atividade |
|---|---|
| ~85 min | Apresentações técnicas do segundo bloco de grupos (tempo dividido conforme número de grupos) |
| 15 min | Feedback consolidado do professor sobre o bloco apresentado |
| 30 min | Discussão final da disciplina: autonomia para aprender novos motores |
| 5 min | Encerramento formal da disciplina |

## Desenvolvimento

O encontro dá continuidade às apresentações técnicas com o segundo bloco de grupos, seguindo exatamente o mesmo padrão de defesa e arguição do Encontro 1. Encerradas as apresentações, o professor conduz a discussão final da disciplina, provocando a turma a nomear, em voz alta, os conceitos universais de Game Engine que reconhecem hoje independentemente de qual motor os implementou — estado global, comunicação desacoplada, dados de design, navegação de agentes, pipeline de build — e a relacionar cada um a uma experiência concreta vivida no próprio Vertical Slice ao longo do semestre. A discussão fecha com um convite explícito à reflexão sobre autonomia: cada estudante é convidado a nomear qual seria, hoje, seu primeiro passo prático ao abrir um motor totalmente novo pela primeira vez. O encerramento formal marca o fim da disciplina.

## Desafio

Não há desafio de implementação. O desafio do encontro, para os grupos do segundo bloco, é o mesmo do Encontro 1: sustentar a defesa técnica sob perguntas não previstas no roteiro.

## Critérios de Sucesso

Cada grupo do segundo bloco apresenta e defende o próprio Vertical Slice com o mesmo padrão de qualidade técnica do primeiro bloco. A turma, na discussão final, articula coletivamente ao menos os principais conceitos universais trabalhados no semestre, relacionando-os a experiências concretas do próprio processo de desenvolvimento.

## Evidências para Avaliação

Rubrica de Apresentações e Rubrica de Vertical Slice Final, aplicadas aos grupos do segundo bloco. A participação na discussão final não gera nota isolada, mas compõe a avaliação processual de participação ativa prevista no Sistema de Avaliação ao longo de toda a disciplina.

## Dificuldades Esperadas

- Ansiedade de fim de semestre concentrando a atenção da turma apenas na própria apresentação, esvaziando a discussão final — reforçar que a discussão final também é avaliada como parte da participação processual da disciplina.
- Discussão final recaindo em elogios genéricos ao Godot ou à disciplina, sem articulação técnica real — o professor deve insistir em exemplos concretos ("me dê um sistema específico do seu projeto e me diga onde ele estaria em outro motor").
- Encerramento emocional do semestre atropelando o tempo reservado à discussão técnica final — o professor deve equilibrar o fechamento afetivo do semestre com o cumprimento do objetivo pedagógico da discussão.

---

# Resultado Esperado da Semana

Ao final da Semana 17, todos os grupos terão apresentado e defendido tecnicamente o próprio Vertical Slice perante a turma, terão justificado decisões arquiteturais centrais tomadas ao longo do semestre e terão situado o projeto na comparação entre Godot, Unity e o motor adicional escolhido na Semana 16. A disciplina se encerra com a turma capaz de nomear, com vocabulário técnico próprio, os conceitos universais de Game Engine trabalhados nos cinco módulos e de reconhecer, de forma justificada, o que é transferível para qualquer motor novo e o que é específico da implementação do Godot. Nenhuma alteração é feita no Vertical Slice nesta semana; o build final permanece o consolidado e exportado desde a Semana 14, agora acompanhado da defesa arquitetural que completa sua avaliação.

# Preparação para a Próxima Semana

Não há próxima semana: a Semana 17 encerra a Unidade V, o Módulo 5 e a disciplina Tendências de Motores de Jogos. Os encaminhamentos remanescentes são administrativos — consolidação de notas de todas as rubricas aplicadas ao longo do semestre, devolutiva individual ou por grupo quando prevista pela coordenação do curso, e registro de encerramento conforme o calendário acadêmico do IFMS.

# Referências

- Godot Documentation — Class Reference: https://docs.godotengine.org/en/stable/classes/index.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual: https://docs.unity3d.com/Manual/
- Unity Learn: https://learn.unity.com/
- Unreal Engine Documentation: https://dev.epicgames.com/documentation/en-us/unreal-engine
- O3DE Documentation: https://docs.o3de.org/
- Stride Documentation: https://doc.stride3d.net/
- Sistema de Avaliação da disciplina (Rubrica 6 — Apresentações; Rubrica 7 — Vertical Slice Final) — Sistema_de_Avaliacao_Tendencias_de_Motores_de_Jogos.md
