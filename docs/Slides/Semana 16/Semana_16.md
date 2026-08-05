---
marp: true
theme: academic-course
paginate: true
header: 'Semana 16 — Comparação Arquitetural Godot x Unity x Unreal x O3DE x Stride'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 16

## Comparação Arquitetural Godot x Unity x Unreal x O3DE x Stride

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade V — Comparar Arquiteturas e Aprender Novos Motores** (Semanas 15–17)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Encerramento de Módulo 🔴** — fecha o núcleo comparativo da Unidade V. Entrega: checkpoint de preparação da apresentação técnica final

</div>

<!--
A Semana 15 abriu a Unidade V com leitura arquitetural guiada do TPS Demo e do Platformer 2D Demo, produzindo paralelos e um feedback formal sobre uma decisão arquitetural própria candidata a revisão.
A Semana 16 muda de escala: em vez de comparar o projeto com outro projeto Godot, cada grupo compara o Godot inteiro — como motor — contra Unity, Unreal, O3DE e Stride, sistema por sistema, ao longo de todos os módulos já cursados.
Nenhuma linha de código é escrita nesta semana; o Vertical Slice permanece no estado consolidado e exportado desde a Semana 14.
Metodologia: Reverse Engineering — discussões, comparações, análises, apresentações. Autonomia muito alta; professor como mediador.
-->

---

## Objetivos da Semana

- Consolidar em um quadro comparativo sistemático as equivalências Godot x Unity identificadas ao longo do semestre, sistema por sistema
- Ampliar a comparação para Unreal Engine, O3DE e Stride, reconhecendo o que é transferível entre engines e o que é específico do Godot
- Escolher, com justificativa técnica própria, o motor mais relevante (Unreal, O3DE ou Stride) para comparação aprofundada com o projeto do grupo
- Estruturar o checkpoint de preparação da apresentação técnica final da Semana 17

<!--
O produto da semana é intelectual: um quadro comparativo sistemático e o checkpoint de preparação, não código novo.
Referência: PROJECT_ARCHITECTURE.md, seção 12 (Comparações com Unity) e seção 6 (Roadmap de Implementação) — insumo direto do quadro.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Consolidação do Quadro Comparativo Godot x Unity

<span class="chapter-number">01</span>

<!--
Encontro dedicado a sistematizar, sistema por sistema, todas as comparações Godot x Unity já praticadas ao longo do semestre. Nenhum recurso novo é aberto no editor.
-->

---

## Agenda do Encontro 1

- Revisão do feedback formal da Semana 15 e abertura da comparação sistemática (15 min)
- Apresentação do modelo de quadro comparativo e do checklist de sistemas construídos (20 min)
- Elaboração em grupo do quadro comparativo Godot x Unity, sistema por sistema (60 min)
- Socialização: cada grupo compartilha um par de linhas mais revelador (30 min)
- Feedback e fechamento do Encontro 1 (10 min)

<!--
Ciclo pedagógico: Conceito → Demonstração → Construção → Desafio → Revisão. Aqui "construção" é a elaboração coletiva do quadro comparativo.
-->

---

<!-- _class: question -->

# Um Autoload e um GameMode resolvem o mesmo problema?

Pense em quantas vezes, desde a Semana 4, você já comparou um recurso do Godot com o equivalente da Unity sem perceber que estava praticando o mesmo método.

<!--
Discussão rápida, 2–3 minutos. Objetivo: mostrar que a comparação sistemática de hoje não é conteúdo novo — é a consolidação de um hábito já praticado desde o Módulo 2.
Erro comum: tratar a pergunta como retórica em vez de puxar exemplos concretos do próprio Vertical Slice.
-->

---

## O Problema: Conceito Universal x Implementação Específica

- Um Autoload no Godot e um GameMode na Unreal resolvem o mesmo problema — estado de partida acessível globalmente — com nomes e sintaxes diferentes
- Uma Signal no Godot e um Event/Delegate na Unity resolvem o mesmo problema de comunicação desacoplada
- Reconhecer o conceito universal por trás de um recurso específico é o que permite localizar o equivalente em qualquer motor novo

<!--
Conceito universal da semana: distinguir "o que todo motor precisa resolver" de "como o Godot resolve isso". Esta é a competência central do Módulo 5.
-->

---

## Estrutura do Quadro Comparativo

- Colunas: Sistema | Módulo | Solução no Vertical Slice (Godot) | Equivalente na Unity | Conceito universal
- Organizado por módulo cursado (1 a 4), não por ordem alfabética — reforça a trilha pedagógica desde a Semana 1
- Preenchido a partir do que o próprio Vertical Slice implementa, nunca de teoria genérica
- Cada linha deve nomear o conceito universal, não apenas listar dois nomes lado a lado
- Base: todos os sistemas listados em PROJECT_ARCHITECTURE.md, seção 6 (Roadmap de Implementação)

<!--
Máximo de cinco bullets. Preparação do professor: modelo de quadro pronto (planilha ou tabela), checklist consolidado dos sistemas do semestre.
-->

---

<!-- _class: comparison -->

## Quadro Comparativo — Amostra (Módulos 1–2)

<div class="columns">
<div class="col positive">

### Godot (no Vertical Slice)

- CharacterBody3D + move_and_slide (Player)
- GameManager / SaveManager (Autoload)
- Contrato Interactable (has_method) + Signals

</div>
<div class="col negative">

### Unity (equivalente)

- CharacterController / Rigidbody + script próprio
- Ausência de equivalente direto — convenção do time (Singleton/ScriptableObject)
- Interfaces C# + UnityEvent/Actions

</div>
</div>

<!--
Esta amostra retoma PROJECT_ARCHITECTURE.md seção 12. O quadro completo elaborado em grupo deve cobrir também animação (AnimationTree x Animator Controller), UI (Control nodes x UGUI/UI Toolkit), IA (LimboAI/Blackboard x Behavior Designer) e demais pares já trabalhados no semestre.
-->

---

## Demonstração — Modelo do Quadro em Uso

O que será construído:

- Nenhum código novo — apenas o preenchimento coletivo do quadro comparativo a partir do checklist de sistemas do semestre

Por quê: fixar o formato do quadro antes da elaboração em grupo.

Resultado esperado: cada grupo sai com o quadro comparativo cobrindo os Módulos 1 a 4, com a coluna de conceito universal preenchida em cada linha.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Preparação do professor: checklist consolidado extraído do Cronograma e de PROJECT_ARCHITECTURE.md, para evitar que algum sistema seja esquecido.
-->

---

> **Imagem sugerida**
>
> Objetivo: apoiar visualmente o preenchimento do quadro comparativo Godot x Unity durante o Encontro 1.
> Enquadramento: tabela em tela cheia, projetada, com cinco colunas (Sistema, Módulo, Solução no Vertical Slice, Equivalente na Unity, Conceito universal).
> Elementos presentes: linhas já preenchidas com exemplos dos Módulos 1 e 2 (GameManager, Contrato Interactable) como referência inicial para os grupos.
> Destaque visual: a coluna "Conceito universal" destacada em cor de acento, reforçando que é a coluna mais importante do quadro.
> Legenda sugerida: "O mesmo problema, nomes diferentes — a coluna que importa é a última."

<!--
Usar esta imagem na abertura da elaboração do quadro, antes dos grupos começarem a preencher.
-->

---

## Checklist de Sistemas do Semestre

- Módulo 1: Player, Input Map, CharacterBody3D, renderização (SDFGI/VoxelGI), build inicial
- Módulo 2: GameManager/SaveManager (Autoload), Contrato Interactable, Signals, ItemData (Resource + Enum), SaveComponent/SaveData
- Módulo 3: HealthComponent, AnimationTree, HUD, InventoryComponent, NavigationRegion3D, LimboAI (Behavior Tree + Blackboard), combate simples
- Módulo 4: Material Overrides, Foliage (MultiMeshInstance3D), áudio, profiling, exportação

<!--
Checklist derivado diretamente de PROJECT_ARCHITECTURE.md, seção 6. Usar como roteiro de verificação para garantir que nenhum sistema seja esquecido no quadro.
Dificuldade esperada: sistemas do Módulo 1 esquecidos por estarem distantes na memória — o professor deve cobrir esses sistemas explicitamente.
-->

---

## Laboratório — Elaboração do Quadro Comparativo

Cada grupo, a partir do checklist:

1. Preenche o quadro comparativo Godot x Unity cobrindo todos os sistemas construídos nos Módulos 1 a 4
2. Nomeia, em cada linha, o conceito universal por trás do par Godot x Unity — não apenas a terminologia

<!--
Critério de sucesso: quadro cobrindo todos os módulos, com a coluna de conceito universal preenchida com o motivo pelo qual o sistema existe em qualquer engine.
Dificuldade esperada: grupos preenchendo o quadro apenas com nomes de classes/nós — insistir na pergunta "por que esse sistema existiria em qualquer engine?".
Dificuldade esperada: grupos tentando reabrir o projeto no editor para "conferir" detalhes — reforçar que o quadro deve vir do que já foi aprendido.
-->

---

## Fechamento — Encontro 1

- Quadro comparativo Godot x Unity elaborado, cobrindo os Módulos 1 a 4
- Coluna de conceito universal preenchida em cada linha do quadro
- Socialização dos pares mais reveladores concluída
- Próximo passo: ampliação da comparação para Unreal, O3DE e Stride, no Encontro 2

<!--
O quadro produzido aqui é retomado na abertura do Encontro 2 e serve de base direta para a ampliação comparativa.
-->

---

<!-- _class: chapter -->

## Encontro 2

# Unreal, O3DE, Stride e o Checkpoint da Apresentação Final

<span class="chapter-number">02</span>

<!--
A turma amplia a comparação para três motores adicionais, escolhe um para aprofundamento e estrutura o checkpoint de preparação da apresentação técnica final da Semana 17.
-->

---

## Agenda do Encontro 2

- Retomada do quadro comparativo Godot x Unity do Encontro 1 (15 min)
- Ampliação guiada da comparação para Unreal, O3DE e Stride (40 min)
- Desafio: escolha e justificativa do motor para comparação aprofundada (15 min)
- Estruturação do checkpoint de preparação da apresentação técnica final (45 min)
- Feedback e fechamento da semana e da Unidade V (20 min)

<!--
Reservar tempo real para a produção do checkpoint — é a entrega avaliativa da semana.
-->

---

<!-- _class: question -->

# Um motor novo confirma ou contradiz o que você já aprendeu?

Pense no par Godot x Unity que seu grupo já mapeou. O que muda quando você olha para Unreal, O3DE ou Stride pelo mesmo sistema?

<!--
Discussão rápida, 2–3 minutos. Objetivo: antecipar que a ampliação para mais motores reforça o padrão já visto, não introduz um problema novo.
-->

---

## O Problema: Confirmação, Não Contradição

- Estado global de partida, comunicação desacoplada, dados de design fora do código, navegação de agentes, empacotamento de build — os mesmos problemas reaparecem em qualquer motor moderno
- Unreal, O3DE e Stride resolvem esses problemas com nomes e convenções próprias, mas com a mesma motivação de design
- A disciplina não ensina Unreal, O3DE ou Stride em profundidade — demonstra que a competência real é reconhecer conceitos universais sob qualquer nome de API

<!--
Conceito universal retomado: a ampliação para múltiplos motores confirma, em vez de contradizer, o que já apareceu no par Godot x Unity.
-->

---

## Demonstração — Panorama Unreal, O3DE, Stride

O que será construído:

- Nenhum código novo — panorama comparativo apenas nos pontos em que cada motor apresenta diferença arquitetural relevante frente ao quadro Godot x Unity já mapeado

Por quê: ampliar o repertório de referência sem tentar ensinar três motores em profundidade no tempo de um encontro.

Resultado esperado: cada grupo situa Unreal, O3DE e Stride em relação ao par Godot x Unity já mapeado, não como comparações isoladas.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Preparação do professor: documentação pública de Unreal, O3DE e Stride organizada por sistema (gameplay framework, animação, IA, UI, packaging).
-->

---

<!-- _class: comparison -->

## Godot x Unity — Ponto de Partida da Ampliação

<div class="columns">
<div class="col positive">

### Godot x Unity (já mapeado)

- Resource customizado + Enum ↔ ScriptableObject
- Ambos resolvem dados de design desacoplados do código

</div>
<div class="col negative">

### Unreal / O3DE / Stride

- Unreal: Data Assets — mesmo problema, mesma motivação
- O3DE: Assets baseados em componentes — mesmo problema
- Stride: Assets serializáveis — mesmo problema

</div>
</div>

<!--
Exemplo do Plano de Aula: "assim como a Unity usa ScriptableObject e o Godot usa Resource, a Unreal usa Data Assets e a O3DE usa Assets baseados em componentes, todos resolvendo o mesmo problema de dados de design desacoplados do código".
Cada grupo deve situar o motor novo em relação ao par Godot x Unity já mapeado, nunca como uma terceira comparação isolada.
-->

---

## Laboratório — Ampliação e Escolha do Motor

Cada grupo:

1. Situa, para cada sistema do próprio quadro, onde Unreal, O3DE ou Stride confirma o padrão já visto ou diverge de forma relevante
2. Escolhe, entre Unreal, O3DE ou Stride, o motor mais relevante para comparação aprofundada com o próprio projeto
3. Redige uma justificativa técnica curta — gênero do jogo, familiaridade prévia da equipe ou qualidade da documentação pública

<!--
Critério de sucesso: justificativa aponta pelo menos um sistema concreto do próprio Vertical Slice que se beneficiaria da comparação com o motor escolhido.
Dificuldade esperada: escolha por familiaridade superficial ("já ouvi falar de Unreal") sem justificativa técnica real.
Dificuldade esperada: grupos tentando cobrir os três motores com a mesma profundidade, esgotando o tempo — a comparação ampliada é panorâmica; profundidade fica reservada ao motor escolhido.
-->

---

## Arquitetura — Do Quadro ao Checkpoint

- Quadro Godot x Unity (Encontro 1) → base sistemática de todos os módulos cursados
- Ampliação Unreal / O3DE / Stride (Encontro 2) → confirmação do padrão, panorâmica
- Escolha justificada de um motor → recorte de aprofundamento próprio de cada grupo
- Checkpoint → recorte do Vertical Slice + decisões arquiteturais + comparação escolhida, como roteiro da Semana 17

<!--
Diagrama sugerido: Quadro Godot x Unity → Ampliação Unreal/O3DE/Stride → Escolha justificada de um motor → Checkpoint de preparação → Apresentação técnica final (Semana 17).
Erro comum: tratar o checkpoint como resumo do semestre inteiro, sem recorte.
-->

---

<!-- _class: exercise -->

# Entrega da Semana — Checkpoint de Preparação da Apresentação Final

Estruture o checkpoint contendo: recorte do Vertical Slice a apresentar, ao menos três decisões arquiteturais centrais, e a comparação entre motores escolhida com justificativa técnica.

<div class="objectives">

**Entrega:** Checkpoint de preparação da apresentação técnica final — avaliação qualitativa da capacidade de síntese comparativa entre motores e de organização da narrativa técnica da Semana 17.

</div>

<!--
Não constitui, isoladamente, uma rubrica numérica formal — alimenta diretamente a apresentação técnica final da Semana 17.
Dificuldade esperada: checkpoint estruturado como resumo do semestre inteiro, sem recorte — a apresentação da Semana 17 tem tempo limitado.
-->

---

## Boas Práticas — Síntese Comparativa entre Motores

- Nomear o conceito universal em cada linha do quadro, nunca apenas listar nomes de classes/nós lado a lado
- Situar cada motor adicional em relação ao par Godot x Unity já mapeado, nunca como comparação isolada
- Justificar a escolha do motor de aprofundamento por um sistema concreto do próprio projeto, nunca por familiaridade superficial
- Recortar o checkpoint com foco no tempo limitado da apresentação, nunca como lista exaustiva de tudo que foi feito

<!--
Estes são os mesmos critérios usados para avaliar o checkpoint desta semana e, por extensão, a apresentação técnica final.
-->

---

## Fechamento — Encontro 2

- Comparação ampliada para Unreal, O3DE e Stride concluída, ancorada no quadro Godot x Unity
- Motor de comparação aprofundada escolhido e justificado por cada grupo
- Checkpoint de preparação da apresentação técnica final estruturado
- Unidade V com núcleo comparativo encerrado — nenhuma alteração feita no Vertical Slice

<!--
O checkpoint produzido aqui é o roteiro direto da apresentação técnica final da Semana 17.
-->

---

## Resultado Esperado da Semana

- Quadro comparativo sistemático Godot x Unity cobrindo todos os sistemas dos Módulos 1 a 4
- Paralelos relevantes registrados com Unreal Engine, O3DE e Stride
- Motor escolhido e justificado para comparação aprofundada com o próprio projeto
- Checkpoint de preparação da apresentação técnica final — recorte, decisões arquiteturais e comparação já estruturados como roteiro
- Nenhuma alteração no Vertical Slice — projeto permanece no estado consolidado e exportado da Semana 14

<!--
Corresponde ao roadmap do Módulo 5 em PROJECT_ARCHITECTURE.md, seção 6: nenhum sistema novo é implementado; o módulo consolida a análise arquitetural do projeto já construído.
-->

---

## Checklist da Semana

- [ ] Quadro comparativo Godot x Unity concluído, cobrindo os Módulos 1 a 4
- [ ] Coluna de conceito universal preenchida em cada linha do quadro
- [ ] Paralelos com Unreal, O3DE e Stride registrados, ancorados no quadro Godot x Unity
- [ ] Motor de comparação aprofundada escolhido, com justificativa técnica
- [ ] Checkpoint de preparação da apresentação técnica final entregue
- [ ] Nenhuma alteração de código realizada no Vertical Slice nesta semana

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 17.
-->

---

## Próximos Passos — Semana 17

A Semana 17 encerra a Unidade V, o Módulo 5 e a disciplina com as apresentações técnicas finais de cada grupo, distribuídas nos dois encontros. O checkpoint produzido nesta semana é o roteiro direto da apresentação; nenhum novo conteúdo de preparação é introduzido entre a Semana 16 e a Semana 17, apenas ensaio e ajuste fino.

Leitura recomendada: PROJECT_ARCHITECTURE.md, seção 12 (Comparações com Unity); documentação oficial de Unreal Engine, O3DE e Stride nos sistemas relevantes ao motor escolhido por cada grupo.

<!--
Referências completas: ver Plano de Aula Semana 16. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
Fontes consultadas para este material: Plano de Aula Semana 16, PROJECT_ARCHITECTURE.md (seções 5, 6 e 12), PEDAGOGICAL_RULES.txt.
-->
