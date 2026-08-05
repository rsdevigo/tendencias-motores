---
marp: true
theme: academic-course
paginate: true
header: 'Semana 17 — Apresentação Técnica Final do Vertical Slice'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 17

## Apresentação Técnica Final do Vertical Slice

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade V — Comparar Arquiteturas e Aprender Novos Motores** (Semanas 15–17)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Encerramento de Módulo 🔴** — encerra a Unidade V, o Módulo 5 e a disciplina. Entrega: apresentação e defesa técnica do Vertical Slice

</div>

<!--
A Semana 16 fechou o núcleo comparativo da Unidade V: quadro comparativo Godot x Unity, ampliação para Unreal/O3DE/Stride, escolha justificada de um motor e checkpoint de preparação da apresentação final.
Nenhum sistema novo foi implementado desde a Semana 14; o Vertical Slice permanece consolidado e exportado.
A Semana 17 não introduz conteúdo: é o encontro em que cada grupo apresenta, defende e é arguido sobre o próprio projeto.
Metodologia: Reverse Engineering — apresentações e defesa técnica. Autonomia muito alta; professor como avaliador e mediador da sessão de perguntas.
-->

---

## Objetivos da Semana

- Apresentar tecnicamente o Vertical Slice desenvolvido ao longo do semestre, com recorte definido no checkpoint da Semana 16
- Justificar decisões arquiteturais tomadas em módulos anteriores, articulando o conceito universal por trás de cada escolha de implementação no Godot
- Comparar o projeto e o Godot com a Unity e com o motor adicional escolhido na Semana 16
- Responder a perguntas técnicas da turma e do professor, demonstrando domínio real do projeto

<!--
O produto da semana não é um novo sistema no jogo — é a apresentação técnica final, o instrumento de maior peso do semestre (Apresentações, 10%; Vertical Slice Final, 20%, com defesa arquitetural nesta semana).
Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->

---

<!-- _class: chapter -->

## Encontro 1

# Apresentações Técnicas — Primeiro Bloco

<span class="chapter-number">01</span>

<!--
Metade da turma apresenta e defende o Vertical Slice. Nenhum recurso novo do Godot é aberto no editor; o projeto de cada grupo é usado como evidência da apresentação.
-->

---

## Agenda do Encontro 1

- Abertura, ordem de apresentação e regras da sessão de perguntas (10 min)
- Apresentações técnicas do primeiro bloco de grupos (~95 min)
- Feedback consolidado do professor e fechamento do Encontro 1 (20 min)

<!--
Tempo recomendado por grupo: 10–12 min de apresentação + 5–8 min de perguntas, ajustado ao número de grupos da turma.
-->

---

<!-- _class: question -->

# O que você levaria para outro motor?

Para cada sistema do seu Vertical Slice: qual é o conceito universal, como o Godot resolve, e onde esse mesmo problema aparece em Unity, Unreal, O3DE ou Stride?

<!--
Pergunta de abertura, não retórica — cada grupo deve ter isso pronto antes de apresentar.
Erro comum: tratar a pergunta como aquecimento e não como o próprio roteiro da apresentação.
-->

---

## O Que Está Sendo Avaliado

- Não é um recital de funcionalidades do jogo — é demonstração de raciocínio arquitetural
- Para cada sistema destacado: conceito universal → implementação no Godot → transferência para outro motor
- Clareza técnica na justificativa das decisões, não apenas descrição do que foi feito
- Capacidade de responder perguntas fora do roteiro ensaiado

<!--
Conceito fundamental da semana: a tríade conceito–implementação–transferência, construída desde a Semana 1, agora avaliada diretamente.
Referência: Rubrica de Apresentações e Rubrica de Arquitetura/Justificativa Técnica.
-->

---

## Estrutura Esperada da Apresentação

1. Recorte do Vertical Slice apresentado (definido no checkpoint da Semana 16)
2. Ao menos três decisões arquiteturais centrais, justificadas tecnicamente
3. Comparação Godot x Unity x motor adicional, aplicada ao recorte — não genérica
4. Demonstração ao vivo ou em vídeo/build exportado

<!--
Máximo de cinco bullets no slide; a estrutura completa está detalhada no checkpoint de cada grupo.
Preparação do professor: checklist de itens obrigatórios da apresentação, visível durante a arguição.
-->

---

<!-- _class: comparison -->

## Exemplo de Justificativa Aplicada

<div class="columns">
<div class="col negative">

### Justificativa genérica (evitar)

- "Usamos Autoload porque é assim que se faz no Godot"

</div>
<div class="col positive">

### Justificativa técnica (esperada)

- "Usamos Autoload para o GameManager porque o estado de partida precisa ser acessível globalmente sem acoplar cada sistema ao nó raiz — o mesmo problema que a Unity resolve com um Singleton ou ScriptableObject compartilhado"

</div>
</div>

<!--
Retomado de PROJECT_ARCHITECTURE.md, seção 12. Este é o padrão de resposta esperado na sessão de perguntas.
-->

---

## Demonstração — O Que Acontece em Cada Apresentação

O que será construído: nada — o Vertical Slice já está consolidado desde a Semana 14.

Por quê: o encontro avalia a defesa da arquitetura, não a produção de código novo.

Resultado esperado: cada grupo demonstra o recorte definido no checkpoint, ao vivo ou por vídeo/build, como evidência concreta das decisões que está defendendo.

<!--
Nenhum recurso novo do Godot é aberto no editor. Nunca detalhar passo a passo — sem Tutorial correspondente nesta semana.
-->

---

> **Imagem sugerida**
>
> Objetivo: ilustrar o momento de apresentação técnica final na sala de aula.
> Enquadramento: grupo de estudantes diante da turma, projeção do Vertical Slice em execução ao fundo.
> Elementos presentes: tela com o jogo em execução, integrantes do grupo posicionados lado a lado, professor com rubrica em mãos em primeiro plano.
> Destaque visual: a tela de projeção como centro da composição, com leve destaque de cor sobre o HUD do jogo em exibição.
> Legenda sugerida: "A defesa não é sobre o jogo terminado — é sobre por que ele foi construído assim."

<!--
Usar esta imagem na abertura do Encontro 1, antes da primeira apresentação.
-->

---

## Arquitetura da Sessão de Perguntas

- Após cada apresentação, turma e professor fazem perguntas técnicas
- Perguntas distribuídas entre os integrantes do grupo — nenhuma pessoa concentra todas as respostas
- Professor pode perguntar: "o que aconteceria se essa decisão fosse diferente?"
- Objetivo: verificar domínio real da implementação, além do roteiro ensaiado

<!--
Diagrama sugerido: Apresentação do grupo → Perguntas da turma → Perguntas do professor → Registro nas rubricas → Feedback.
Reforça o Sistema de Avaliação: distribuição de perguntas entre integrantes é critério explícito.
-->

---

## Boas Práticas para a Defesa

- Recortar a apresentação ao tempo disponível, nunca tentar cobrir o semestre inteiro
- Nomear o conceito universal antes de descrever a implementação específica no Godot
- Preparar exemplos concretos do próprio projeto para cada decisão destacada
- Distribuir as respostas da sessão de perguntas entre todos os integrantes do grupo

<!--
Estes são os mesmos critérios usados nas rubricas de Apresentações e de Arquitetura/Justificativa Técnica.
-->

---

## Laboratório — Apresentação e Defesa (Bloco 1)

Cada grupo do primeiro bloco:

1. Apresenta o recorte do Vertical Slice definido no checkpoint da Semana 16
2. Justifica ao menos três decisões arquiteturais centrais
3. Responde às perguntas técnicas da turma e do professor

<!--
Critério de sucesso: recorte respeitado, justificativas técnicas específicas (não genéricas), participação de todos os integrantes na defesa.
Dificuldade esperada: grupos excedendo o tempo por tentar cobrir o semestre inteiro — o professor interrompe com cortesia e redireciona.
Dificuldade esperada: um único integrante concentrando as respostas — reforçar a distribuição.
-->

---

## Fechamento — Encontro 1

- Primeiro bloco de grupos apresentado e arguido
- Evidências registradas nas rubricas de Apresentações e de Arquitetura/Justificativa Técnica
- Feedback consolidado do professor sobre o padrão esperado, entregue antes do Encontro 2
- Próximo passo: segundo bloco de apresentações e discussão final da disciplina

<!--
O feedback imediato do professor reforça o padrão esperado para os grupos que apresentam no Encontro 2.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Apresentações Técnicas — Segundo Bloco e Discussão Final

<span class="chapter-number">02</span>

<!--
Segundo bloco de grupos apresenta com o mesmo padrão do Encontro 1. A disciplina se encerra com a discussão final sobre autonomia para aprender novos motores.
-->

---

## Agenda do Encontro 2

- Apresentações técnicas do segundo bloco de grupos (~85 min)
- Feedback consolidado do professor sobre o bloco apresentado (15 min)
- Discussão final da disciplina: autonomia para aprender novos motores (30 min)
- Encerramento formal da disciplina (5 min)

<!--
Mesmo padrão de defesa e arguição do Encontro 1, aplicado ao segundo bloco.
-->

---

## Laboratório — Apresentação e Defesa (Bloco 2)

Cada grupo do segundo bloco:

1. Apresenta o recorte do Vertical Slice definido no checkpoint da Semana 16
2. Justifica ao menos três decisões arquiteturais centrais
3. Responde às perguntas técnicas da turma e do professor

<!--
Mesmo critério de sucesso do Encontro 1, aplicado ao segundo bloco de grupos.
-->

---

<!-- _class: question -->

# A engine é um estudo de caso — isso se sustentou?

Depois de dezessete semanas em Godot, você abriria Unity, Unreal, O3DE ou outro motor e localizaria com razoável rapidez os mesmos conceitos universais que aprendeu aqui?

<!--
Pergunta de abertura da discussão final. Objetivo: fechar a premissa que abriu a disciplina na Semana 1.
Discussão coletiva, não retórica — provocar a turma a responder com exemplos concretos.
-->

---

## O Que a Turma Deve Nomear

- Estado global de partida (Autoload / Singleton / GameMode)
- Comunicação desacoplada entre sistemas (Signals / Events / Delegates)
- Dados de design fora do código (Resource / ScriptableObject / Data Assets)
- Navegação e decisão autônoma de agentes (NavigationRegion3D / LimboAI / Behavior Trees equivalentes)
- Pipeline de exportação e empacotamento de build

<!--
Estes cinco conceitos atravessam os cinco módulos da disciplina. A discussão pede que a turma os relacione a experiências concretas do próprio Vertical Slice.
-->

---

## Roteiro de Perguntas da Discussão Final

- Qual sistema construído no semestre você reconheceria mais rápido em um motor novo?
- Qual decisão arquitetural do seu projeto você mudaria, sabendo o que sabe hoje?
- O que no Godot foi mais fácil ou mais difícil de aprender do que seria na Unity, e por quê?
- Qual seria seu primeiro passo prático ao abrir um motor totalmente novo pela primeira vez?

<!--
Preparação do professor: roteiro sugerido no Plano de Aula, Encontro 2. Insistir em exemplos concretos, não elogios genéricos ao Godot ou à disciplina.
-->

---

## Boas Práticas para a Discussão Final

- Responder com um sistema específico do próprio projeto, nunca com elogio genérico
- Nomear o conceito universal antes de nomear a ferramenta do Godot que o implementa
- Reconhecer, sem constrangimento, decisões que hoje seriam tomadas de forma diferente
- Equilibrar o fechamento afetivo do semestre com o cumprimento do objetivo técnico da discussão

<!--
Dificuldade esperada: discussão recaindo em elogios genéricos — o professor deve pedir "me dê um sistema específico do seu projeto e me diga onde ele estaria em outro motor".
Dificuldade esperada: ansiedade de fim de semestre esvaziando a participação na discussão — reforçar que ela também compõe a avaliação processual.
-->

---

> **Imagem sugerida**
>
> Objetivo: apoiar visualmente a discussão final da disciplina.
> Enquadramento: quadro ou slide de fechamento com os cinco conceitos universais listados, turma reunida em semicírculo.
> Elementos presentes: os cinco conceitos (estado global, comunicação desacoplada, dados de design, navegação de agentes, pipeline de build) dispostos como um mapa mental simples.
> Destaque visual: uma seta ou conexão visual ligando cada conceito a "Godot", "Unity" e "?" (motor desconhecido), reforçando a ideia de transferência.
> Legenda sugerida: "Cinco conceitos, qualquer motor — o que muda é só o nome."

<!--
Usar esta imagem como pano de fundo da discussão final, antes de abrir para a turma.
-->

---

## Fechamento — Encontro 2

- Segundo bloco de grupos apresentado e arguido
- Discussão final concluída, com os conceitos universais do semestre nomeados coletivamente
- Encerramento formal da disciplina
- Nenhuma alteração no Vertical Slice — build final permanece o consolidado desde a Semana 14

<!--
O encerramento marca o fim da disciplina; encaminhamentos remanescentes são administrativos (registro de notas, avaliação institucional).
-->

---

## Resultado Esperado da Semana

- Todos os grupos apresentaram e defenderam tecnicamente o próprio Vertical Slice
- Decisões arquiteturais centrais justificadas com vocabulário técnico próprio
- Comparação entre Godot, Unity e o motor adicional escolhido articulada por cada grupo
- Discussão final da disciplina concluída, com os conceitos universais do semestre nomeados coletivamente

<!--
Corresponde ao encerramento do roadmap do Módulo 5 em PROJECT_ARCHITECTURE.md — nenhum sistema novo é implementado; a semana consolida a defesa arquitetural do projeto já construído.
-->

---

## Checklist da Semana

- [ ] Todos os grupos do primeiro e do segundo bloco apresentaram e defenderam o Vertical Slice
- [ ] Rubrica de Apresentações aplicada a todos os grupos
- [ ] Rubrica de Arquitetura/Justificativa Técnica aplicada a todos os grupos
- [ ] Discussão final da disciplina realizada, com participação da turma
- [ ] Encerramento formal da disciplina registrado

<!--
Usar este checklist como roteiro de verificação ao final da Semana 17 e da disciplina.
-->

---

## Próximos Passos

Não há próxima semana: a Semana 17 encerra a Unidade V, o Módulo 5 e a disciplina Tendências de Motores de Jogos. Os encaminhamentos remanescentes são administrativos — consolidação de notas de todas as rubricas aplicadas ao longo do semestre, devolutiva individual ou por grupo quando prevista pela coordenação do curso, e registro de encerramento conforme o calendário acadêmico do IFMS.

Leitura recomendada: PROJECT_ARCHITECTURE.md, seção 12 (Comparações com Unity); documentação oficial de Unreal Engine, O3DE e Stride nos sistemas relevantes ao motor escolhido por cada grupo.

<!--
Fontes consultadas para este material: Plano de Aula Semana 17, Semana 16 (referência de formato e conteúdo prévio), PROJECT_ARCHITECTURE.md (seções 6 e 12), PEDAGOGICAL_RULES.txt.
Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2.
Godot Documentation: https://docs.godotengine.org/en/stable/classes/index.html | Orchestrator: https://orchestrator.cratercrash.space/ | Unity Manual: https://docs.unity3d.com/Manual/ | Unreal Engine Documentation: https://dev.epicgames.com/documentation/en-us/unreal-engine | O3DE Documentation: https://docs.o3de.org/ | Stride Documentation: https://doc.stride3d.net/
-->
