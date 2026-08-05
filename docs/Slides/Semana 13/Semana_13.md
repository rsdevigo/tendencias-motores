---
marp: true
theme: academic-course
paginate: true
header: 'Semana 13 — Áudio (AudioStreamPlayer), Profiling e Optimization'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 13

## Áudio (AudioStreamPlayer), Profiling e Optimization

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade IV — Produzir como um Pequeno Estúdio** (Semanas 12–14)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Desafio Técnico 🔵** — Rubrica 2, com Feedback Formal (não encerra a Unidade IV)

</div>

<!--
A Semana 12 encerrou com o mesmo Vertical Slice jogável desde a Semana 11, agora com materiais reorganizados em base + Material Overrides e a zona externa composta com MultiMeshInstance3D, sem nenhuma alteração de mecânica.
A Semana 13 dá continuidade ao polimento técnico do Módulo 4 em duas frentes conectadas, mas distintas: áudio (Encontro 1) e Profiling/Optimization (Encontro 2).
Metodologia: Studio Based Learning — professor como diretor técnico. Autonomia alta.
-->

---

## Objetivos da Semana

- Compreender `AudioStreamPlayer` como resposta a eventos de gameplay, não como trilha desconectada da ação
- Integrar sons a eventos já existentes no projeto (interação, passos, ambiente), reutilizando Signals e Components de módulos anteriores
- Compreender Profiling e Optimization como etapa obrigatória de produção, não ajuste isolado de última hora
- Usar o Profiler/Debugger nativo do Godot para identificar gargalos reais antes de qualquer otimização
- Propor e justificar, com solução própria, a otimização de um aspecto identificado no profiling do próprio Vertical Slice

<!--
Encontro 1 resolve a camada sonora. Encontro 2 resolve o diagnóstico e a correção de desempenho.
Referência: Godot Docs — Audio; Godot Docs — Optimization (Profiler/Debugger); Unity Manual — Audio Overview, Profiler.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Áudio como Resposta a Eventos de Gameplay

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o Vertical Slice já jogável e visualmente polido desde a Semana 12, sem alterar nenhuma mecânica — a mudança desta semana é uma nova camada de resposta sensorial.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 12 (materiais refatorados, zona externa composta, Code Review) (15 min)
- Introdução: áudio como resposta a eventos de gameplay, não como trilha isolada (20 min)
- Demonstração: `AudioStreamPlayer` reagindo a um Signal de interação já existente e a um evento de passos (30 min)
- Laboratório: cada grupo integra som a interação, passos e ambiente no próprio Vertical Slice (50 min)
- Feedback e fechamento (20 min)

<!--
Ciclo pedagógico: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — a ferramenta é guiada, mas cada grupo escolhe livremente os sons e os pontos exatos de integração.
-->

---

<!-- _class: question -->

# Por que tratar áudio como um sistema à parte, desconectado dos sinais que o jogo já emite?

Pense no mesmo Signal que a Porta já usa desde a Semana 5.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que áudio não precisa de um canal de comunicação novo — o mesmo Signal que already aciona o HUD pode acionar um som.
Erro comum: assumir que som exige lógica própria em vez de reagir a algo que o gameplay já dispara.
-->

---

## O Problema: Áudio Desconectado do Gameplay

- Música/som de fundo tocado sem relação com o que acontece na tela não comunica nada ao jogador
- Áudio, em qualquer engine, deveria ser uma resposta a um evento que o gameplay já dispara
- O projeto já emite os sinais certos desde a Semana 5 (interação) e a Semana 2 (movimentação)

<!--
Conceito universal: som é resposta a evento, não trilha isolada. Mesma lógica de desacoplamento via Signal já ensinada na Semana 5.
Referência: Godot Docs — Audio (resumir, nunca reproduzir trechos).
-->

---

## `AudioStreamPlayer`, `AudioStreamPlayer2D`, `AudioStreamPlayer3D`

- `AudioStreamPlayer` — som não posicional (ex.: UI, música)
- `AudioStreamPlayer2D` / `AudioStreamPlayer3D` — som posicional, com atenuação por distância
- Pergunta-chave para escolher o tipo certo: "esse som deveria mudar de volume se eu me afastar?"

<!--
Erro comum: confundir AudioStreamPlayer (não posicional) com AudioStreamPlayer3D (posicional), aplicando o tipo errado a um som ambiente.
Referência: Godot Docs — Audio.
-->

---

<!-- _class: comparison -->

## Resposta Sonora a Eventos no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `AudioStreamPlayer` / `2D` / `3D` — três classes distintas conforme posicionamento
- Reage a Signals já existentes no projeto (`interacted`, eventos de movimentação)

</div>
<div class="col negative">

### Unity

- `AudioSource` único, configurado por Spatial Blend (2D/3D)
- Reage a `UnityEvent`/C# Actions ou chamada direta de script

</div>
</div>

<!--
Princípio universal idêntico: som é resposta a evento, e a diferença entre som de interface e som de mundo depende de atenuação espacial, não do componente em si.
A diferença está na granularidade da API — classes distintas no Godot versus um componente parametrizado na Unity.
-->

---

## Demonstração — `AudioStreamPlayer` Reagindo a um Signal

O que será construído:

- Um `AudioStreamPlayer` conectado ao Signal `interacted` já existente (Porta ou Alavanca)
- Um segundo exemplo de som não posicional versus posicional aplicado aos passos do Player

Por quê: mostrar que nenhum sistema novo de comunicação é introduzido — apenas um novo "ouvinte" de um sinal já emitido.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Biblioteca de efeitos sonoros livres (ex.: Kenney Audio/Interface Sounds) selecionada previamente pelo professor.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o `AudioStreamPlayer` como um novo "ouvinte" do mesmo Signal `interacted` que já aciona a reação da Porta.
> Enquadramento: diagrama simples com a Porta ao centro emitindo o sinal `interacted`, e duas setas saindo dele — uma para a animação/abertura da Porta (já existente), outra para o novo `AudioStreamPlayer`.
> Elementos presentes: ícone de Porta, ícone de Signal, ícone de alto-falante conectado ao mesmo sinal.
> Destaque visual: a seta para o `AudioStreamPlayer` em destaque (cor diferente), reforçando que é a única novidade da semana.
> Legenda sugerida: "O AudioStreamPlayer não cria um novo canal de comunicação — apenas reage a um Signal que o projeto já emite desde a Semana 5."

<!--
Usar esta imagem logo após a demonstração, antes do laboratório, para reforçar o conceito de "novo ouvinte, não novo sistema".
-->

---

## Laboratório — Integração de Áudio ao Vertical Slice

Cada grupo, no próprio projeto:

1. Integra som a ao menos um evento de interação já existente (Signal `interacted`)
2. Integra som aos passos do Player, escolhendo entre `AudioStreamPlayer` e `AudioStreamPlayer2D/3D`
3. Integra um som ambiente à zona externa ou interna, com liberdade de escolha entre os sons disponíveis

<!--
Critério de sucesso: som integrado a pelo menos um evento de interação, aos passos do Player e a um elemento ambiente, sem alteração de mecânica.
Dificuldade esperada: confundir AudioStreamPlayer com a variante posicional em um som ambiente — reforçar a pergunta "esse som deveria atenuar por distância?".
Dificuldade esperada: tratar áudio como sistema à parte, com lógica própria em vez de reagir a Signals já existentes.
Dificuldade esperada: poluir o Vertical Slice com sons sobrepostos ou volume mal calibrado — reforçar teste auditivo comparativo antes/depois.
Como diretor técnico, o professor orienta qual AudioStreamPlayer usar em cada caso, sem impor a mesma escolha sonora para todos os grupos.
-->

---

## Fechamento — Encontro 1

- Som integrado a pelo menos um evento de interação, aos passos do Player e a um elemento ambiente
- Nenhum sistema novo de comunicação entre objetos — apenas um novo "ouvinte" dos Signals já existentes
- Nenhuma alteração de mecânica ou sistema de gameplay já validado
- Próximo passo: Profiling e Optimization, no Encontro 2

<!--
A integração de áudio conduzida aqui é insumo direto para o profiling do Encontro 2 — o áudio recém-integrado também consome recursos e será avaliado.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Profiling e Optimization

<span class="chapter-number">02</span>

<!--
Retoma o Vertical Slice com áudio integrado do Encontro 1 e introduz profiling como diagnóstico obrigatório antes de qualquer otimização.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (áudio integrado a interação, passos e ambiente) (15 min)
- Demonstração: leitura do Profiler/Debugger em um caso de gargalo conhecido pelo professor (25 min)
- Laboratório: cada grupo faz o profiling do próprio Vertical Slice e implementa uma otimização a partir do diagnóstico (55 min)
- Feedback formal sobre as otimizações realizadas — Desafio Técnico, Rubrica 2 (40 min)

<!--
Reservar tempo real para o Feedback Formal — instrumento de avaliação previsto no Cronograma para esta semana, não deve ser comprimido.
-->

---

<!-- _class: question -->

# Como saber o que otimizar antes de otimizar qualquer coisa?

Pense nos Code Reviews já feitos nas Semanas 7, 10 e 12 — o mesmo princípio se aplica agora ao desempenho.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que otimizar por suposição desperdiça tempo em problemas que podem não ser o gargalo real.
Erro comum: assumir de antemão qual sistema "deve" ser pesado, sem medir.
-->

---

## O Problema: Otimizar sem Medir

- Otimizar por suposição arrisca corrigir um problema que não é o gargalo real do projeto
- Profiling é o mesmo princípio de diagnóstico já praticado nos Code Reviews do semestre, aplicado agora ao desempenho
- O Vertical Slice acumula decisões desde o Módulo 1 (materiais, animação, IA, composição de cena) — o profiling é também uma releitura crítica de tudo isso

<!--
Conceito universal: medir antes de otimizar. Presente em qualquer engine de produção antes de uma entrega final.
Referência: Godot Docs — Optimization (resumir, nunca reproduzir trechos).
-->

---

## Profiler/Debugger do Godot

- Monitor de desempenho (FPS, tempo de frame)
- Monitores de memória, física e renderização
- Identificação de picos de custo por categoria, cruzados com decisões já tomadas em semanas anteriores

<!--
Erro comum: propor uma otimização sem antes consultar o Profiler, baseada apenas em suposição.
Referência: Godot Docs — Optimization (Profiler/Debugger).
-->

---

<!-- _class: comparison -->

## Profiling no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Profiler/Debugger nativo — monitores essenciais compactos (FPS, memória, física, renderização)
- Exige cruzar dados manualmente com mais frequência

</div>
<div class="col negative">

### Unity

- Unity Profiler — módulos mais granulares por sistema (Rendering, Audio, UI em painéis próprios)
- Mesma leitura de gargalos antes de qualquer decisão de otimização

</div>
</div>

<!--
Princípio universal idêntico nas duas engines: medir antes de otimizar, tratando profiling como etapa recorrente de produção, não verificação única.
A diferença está no nível de detalhe e nos módulos exclusivos de cada ferramenta.
-->

---

## Demonstração — Leitura do Profiler em um Gargalo Conhecido

O que será construído:

- Leitura guiada do Profiler/Debugger sobre o projeto de referência do professor, com um gargalo já conhecido de antemão (sem revelar a causa antes do laboratório)

Por quê: fixar o processo de leitura dos monitores antes de cada grupo aplicar o mesmo processo ao próprio projeto.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
O gargalo não deve ser revelado à turma antes do laboratório — o diagnóstico é parte do exercício.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a leitura dos monitores do Profiler/Debugger do Godot antes de qualquer decisão de otimização.
> Enquadramento: captura conceitual do painel do Profiler, com destaque para os monitores de FPS/tempo de frame, memória, física e renderização lado a lado.
> Elementos presentes: gráfico de tempo de frame com um pico visível, indicadores numéricos de memória e física, ícone de lupa sobre o pico de custo.
> Destaque visual: o pico de custo destacado em vermelho, com uma seta apontando para a categoria responsável.
> Legenda sugerida: "Medir antes de otimizar — o Profiler revela onde o tempo de frame e a memória do projeto estão sendo gastos."

<!--
Usar esta imagem durante a demonstração, antes de abrir o Profiler no projeto real do professor.
-->

---

## Laboratório — Profiling e Otimização do Próprio Projeto

Cada grupo, no próprio Vertical Slice:

1. Abre o Profiler/Debugger e identifica ao menos um ponto real de custo elevado (geometria, materiais, iluminação, IA ou lógica de script/Orchestration)
2. Propõe uma otimização específica para esse ponto, com liberdade total de escolha entre os gargalos identificados
3. Implementa a otimização e confirma que nenhuma mecânica ou sistema já validado sofreu regressão

<!--
Critério de sucesso: diagnóstico de profiling com ao menos um gargalo real identificado e uma otimização implementada e funcional, sem regressão.
Dificuldade esperada: otimizar um aspecto de baixo impacto real, ignorando um gargalo maior identificado no mesmo profiling — reforçar leitura completa dos monitores antes de escolher onde agir.
Dificuldade esperada: introduzir uma otimização que compromete a aparência ou o funcionamento já validado em Playtests anteriores (ex.: reduzir densidade de MultiMeshInstance3D a ponto de descaracterizar a composição da Semana 12) — reforçar que otimização é equilíbrio, não redução às custas de qualquer critério.
Como diretor técnico, o professor orienta a leitura correta dos dados, sem indicar de antemão qual é o gargalo — o diagnóstico deve ser do próprio grupo.
-->

---

## Arquitetura — Áudio e Diagnóstico de Desempenho

- Áudio (Encontro 1) → novo "ouvinte" dos Signals já existentes, sem novo canal de comunicação
- Profiling (Encontro 2) → leitura de todo o Vertical Slice acumulado desde o Módulo 1, sob a ótica de desempenho
- Otimização → correção pontual e justificada de um gargalo real, sem alterar mecânica ou geometria

<!--
Diagrama sugerido: Signals existentes (Semana 5) → AudioStreamPlayer (novo ouvinte). Em paralelo: Vertical Slice acumulado (Módulos 1–4) → Profiler/Debugger → Gargalo identificado → Otimização justificada.
Erro comum: tratar áudio e profiling como dois sistemas desconectados — ambos fazem parte da mesma etapa de polimento técnico do Módulo 4.
-->

---

<!-- _class: exercise -->

# Desafio Técnico — Otimização a partir do Profiling

Identifique, no próprio Vertical Slice, ao menos um gargalo real via Profiler/Debugger e implemente uma otimização justificada pelos dados observados.

<div class="objectives">

**Entrega:** Feedback Formal sobre as otimizações realizadas (Desafio Técnico — Rubrica 2): solução proposta, uso correto dos recursos do Godot, criatividade, organização e funcionamento.

</div>

<!--
Mesma exigência de solução própria já praticada nos Desafios Técnicos das Semanas 8, 9, 10 e 11 — cada grupo escolhe o que otimizar e como, e precisa justificar essa escolha.
Dificuldade esperada: dificuldade em justificar por que um gargalo foi priorizado em vez de outro — reforçar a pergunta "por que este e não outro, segundo o que o Profiler mostrou?".
-->

---

## Boas Práticas — Áudio e Desempenho

- Áudio sempre como reação a um Signal já existente, nunca como sistema com lógica própria
- Nenhuma otimização sem consulta prévia ao Profiler/Debugger
- Priorizar o gargalo de maior impacto real, não o mais fácil de corrigir
- Otimização como equilíbrio entre desempenho e resultado já validado em Playtests anteriores

<!--
Estes são exatamente os pontos observados no Feedback Formal de encerramento da semana.
-->

---

## Fechamento — Encontro 2

- Diagnóstico de profiling do próprio projeto, com ao menos um gargalo real identificado
- Otimização implementada e funcional para esse gargalo, sem regressão em nenhuma mecânica
- Feedback Formal sobre as otimizações realizadas (Rubrica 2) concluído
- Próximo passo: exportação do build final do Vertical Slice, na Semana 14

<!--
Dificuldade esperada: tratar a otimização como ajuste isolado de última hora em vez de etapa sistemática de produção — reforçar que profiling é prática recorrente, não verificação única.
-->

---

## Resultado Esperado da Semana

- Vertical Slice com som integrado às principais ações de gameplay (interação, passos, ambiente) via `AudioStreamPlayer`
- Ao menos um gargalo de desempenho identificado por profiling e corrigido por uma otimização própria, justificada tecnicamente
- Nenhuma alteração de mecânica, sistema de gameplay ou geometria do Vertical Slice
- Projeto tecnicamente pronto, em som e desempenho, para a exportação final da Semana 14

<!--
Este resultado corresponde à linha AudioStreamPlayer/Profiler-Optimization do roadmap (PROJECT_ARCHITECTURE.md) e antecede o encerramento da Unidade IV.
-->

---

## Checklist da Semana

- [ ] Som integrado a pelo menos um evento de interação, aos passos do Player e a um elemento ambiente
- [ ] Nenhum sistema novo de comunicação — áudio reage a Signals já existentes
- [ ] Diagnóstico de profiling com ao menos um gargalo real identificado
- [ ] Otimização implementada e funcional, sem regressão em nenhuma mecânica
- [ ] Feedback Formal sobre as otimizações realizadas (Rubrica 2) concluído

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 14.
-->

---

## Próximos Passos — Semana 14

A Semana 14 encerra a Unidade IV e o Módulo 4 com a exportação do build final do Vertical Slice — os ajustes de áudio e as otimizações realizadas nesta semana são parte direta do que será validado no Playtest cruzado entre grupos e no Code Review de encerramento, sem retrabalho de materiais, foliage, áudio ou otimização além de ajustes pontuais identificados nesse Playtest.

Leitura recomendada: Godot Docs — Audio; Godot Docs — Optimization (Profiler/Debugger); Unity Manual (consulta comparativa) — Audio Overview, Profiler; Kenney Assets (kenney.nl).

<!--
Referências completas: ver Plano de Aula Semana 13. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
