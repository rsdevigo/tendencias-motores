---
marp: true
theme: academic-course
paginate: true
header: 'Semana 7 — Save/Load e consolidação do gameplay do Módulo 2'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 7

## Save/Load e consolidação do gameplay do Módulo 2

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
Retomar o projeto da Semana 6 já aberto, com GameManager/SaveManager (Autoload), contrato Interactable, Signals e ItemData + Enum sustentando o conjunto próprio de itens de cada grupo. Nada desse trabalho é alterado — apenas ampliado.
Esta semana fecha a Unidade II em duas frentes: SaveData + FileAccess (Encontro 1) e integração final de todos os sistemas do módulo em um único fluxo, com Code Review e Playtest (Encontro 2).
Metodologia: Studio Based Learning, autonomia baixa — professor demonstra, aluno adapta. Encerramento de módulo.
-->

---

## Objetivos da Semana

- Compreender serialização e recuperação de estado de jogo entre sessões como problema universal de qualquer engine
- Construir `SaveData` (Resource) + FileAccess como mecanismo de persistência real, e um `Checkpoint` que reutiliza o contrato `Interactable`
- Integrar todos os sistemas do Módulo 2 em um único fluxo jogável coerente, com Code Review e Playtest coletivo

<!--
Encontro 1 cobre SaveData, SaveComponent e Checkpoint. Encontro 2 não introduz nada novo — integra tudo em um fluxo único e avalia via Code Review e Playtest.
Resultado esperado ao final: Vertical Slice com progresso persistente real entre sessões, encerrando a Unidade II.
Referência: Godot Docs — Saving Games, Resources, FileSystem; Unity Manual — PlayerPrefs.
-->

---

<!-- _class: chapter -->

## Encontro 1

# SaveData, SaveComponent e Checkpoint

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o projeto da Semana 6 sem alterar GameManager, SaveManager, contrato Interactable ou ItemData/Enum — apenas adiciona uma camada de persistência real acima do que já existe.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 6 (`ItemData` + Enum, Checkpoint de progresso do Módulo 2) (15 min)
- Introdução: persistência entre cenas (`SaveManager`) versus persistência entre sessões (`SaveData` + FileAccess) (20 min)
- Demonstração: construção de `SaveData`, `SaveComponent` e gravação/leitura em `user://` (40 min)
- Laboratório: cada grupo implementa seu `SaveData`/`SaveComponent` salvando um dado real de progresso (40 min)
- Construção guiada da Scene `Checkpoint`, reutilizando o contrato `Interactable` (15 min)
- Feedback e fechamento (5 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — SaveData/SaveComponent/Checkpoint são construção guiada, base direta da integração avaliada do Encontro 2.
-->

---

<!-- _class: question -->

# Se o jogo é fechado e reaberto no dia seguinte, o progresso do jogador sobrevive?

Pense no que o `SaveManager` (Semana 4) já resolve — e no que ele não resolve.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que o SaveManager mantém estado vivo apenas enquanto o processo do jogo está rodando, mesmo trocando de cena — mas esse estado desaparece ao fechar o jogo.
Erro comum: achar que o SaveManager (Autoload) já resolve persistência em disco, sem perceber que é apenas persistência em memória entre cenas.
-->

---

## O Problema: Persistência Entre Sessões, Não Só Entre Cenas

- Toda engine com sessões de jogo separadas no tempo precisa transformar estado em memória em algo persistido em disco — e o processo inverso ao reabrir
- O `SaveManager` (Semana 4) resolve estado entre cenas; não resolve estado entre execuções do processo
- O Godot resolve isso com Resources serializáveis (`ResourceSaver`/`ResourceLoader`) ou FileAccess bruto, gravando em `user://`

<!--
Conceito universal, não específico do Godot. Reforçar o hábito da disciplina: perguntar "que problema universal isso resolve?" antes de "como se usa no Godot?".
Referência: Godot Docs — Saving Games, File System (user://).
-->

---

## `SaveData`: o Resource que Representa o Progresso

- Resource customizado, assim como `ItemData` (Semana 6) — mas grava e lê dinamicamente em `user://`, fora do projeto (`res://`)
- Campos exportados: itens coletados, último checkpoint alcançado
- Não é uma instância `.tres` criada manualmente — é instanciado e preenchido em tempo de execução pelo `SaveComponent`

<!--
Reforçar: res:// é o projeto (somente leitura em builds exportados); user:// é a pasta de dados do usuário, gravável em tempo de execução.
Erro comum: criar SaveData como Node em vez de Resource — apenas Resources são serializáveis com ResourceSaver/ResourceLoader.
-->

---

<!-- _class: comparison -->

## Persistência em Disco no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `SaveData` (Resource) serializado nativamente via `ResourceSaver`/`ResourceLoader`
- FileAccess bruto disponível quando o arquivo precisa ser legível fora do motor

</div>
<div class="col negative">

### Unity

- `PlayerPrefs` para dados simples (chave-valor)
- Serialização própria em JSON/binário para dados estruturados — decisão inteiramente da equipe

</div>
</div>

<!--
O conceito universal — transformar estado em memória em dado persistido em disco — é idêntico nas duas engines. O Godot oferece um caminho nativo mais direto para dados estruturados; a Unity não tem um equivalente formal único.
Não transformar isso em aula de C#.
-->

---

## Demonstração — `SaveData` e `SaveComponent`

O que será construído:

- Classe `SaveData` (Resource) com campos `itens_coletados` e `ultimo_checkpoint`
- `SaveComponent`, centralizando `salvar()` e `carregar()` via `ResourceSaver`/`ResourceLoader` em `user://`
- Teste de gravação e leitura, confirmando persistência entre execuções

Por quê: evita lógica de serialização duplicada entre Scenes — qualquer ponto do jogo que precise salvar conversa apenas com o `SaveComponent`.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 7, Encontro 1).
Reforçar: SaveComponent conhece apenas SaveData, nunca Nodes específicos da cena.
-->

---

> **Imagem sugerida**
>
> Objetivo: contrastar persistência entre cenas e persistência entre sessões.
> Enquadramento: diagrama de duas colunas.
> Elementos presentes: à esquerda, "SaveManager (Autoload)" com seta circular entre duas cenas do jogo em execução; à direita, "SaveData + FileAccess" com seta entre o jogo em execução e a pasta `user://`, e outra seta de volta ao reabrir o jogo.
> Destaque visual: a pasta `user://` como o elemento que sobrevive ao fechamento do processo.
> Legenda sugerida: "SaveManager mantém estado entre cenas; SaveData + FileAccess mantém estado entre sessões, gravando em disco."

<!--
Usar esta imagem na introdução do encontro, antes da demonstração ao vivo.
-->

---

## Arquitetura — `SaveComponent` como Ponto Único de Gravação

- `SaveComponent` (Node): único responsável por `ResourceSaver`/`ResourceLoader` e pelo caminho `user://save_data.tres`
- Quem monta os dados a salvar (itens coletados, checkpoint) é responsabilidade de quem chama `salvar()`, não do Component
- Nenhuma Scene chama `ResourceSaver`/FileAccess diretamente — sempre através do `SaveComponent`

<!--
Diagrama sugerido: Checkpoint → SaveComponent.salvar() → SaveData (Resource) → user://save_data.tres.
Erro comum: instanciar mais de um SaveComponent ativo na mesma árvore de cena, criando ambiguidade sobre a fonte de verdade.
-->

---

## `Checkpoint`: o Contrato `Interactable` Aplicado à Persistência

- Scene que implementa o mesmo contrato `Interactable` já usado por `Door` e `Lever` desde a Semana 5
- Ao ser alcançado, aciona `SaveComponent.salvar()` — sem nenhuma lógica de interação própria
- Testa o desacoplamento ensinado na disciplina: um novo tipo de interativo não exige alteração no `InteractionComponent` do Player nem no contrato

<!--
Erro comum: reimplementar detecção de proximidade dentro do Checkpoint em vez de reutilizar o InteractionComponent e o contrato já existente.
Referência: PROJECT_ARCHITECTURE.md, seção 8 (scenes/interactables/).
-->

---

## Laboratório — `SaveData`, `SaveComponent` e `Checkpoint`

Cada grupo replica, no próprio projeto:

1. `SaveData` (Resource) em `scripts/resources/save_data.gd`, com `itens_coletados` e `ultimo_checkpoint`
2. `SaveComponent` em `scripts/components/save_component.gd`, com `salvar()` e `carregar()`
3. Teste de gravação/leitura, confirmando o arquivo em `user://`
4. Scene `Checkpoint`, reutilizando o contrato `Interactable`, acionando `salvar()`

<!--
Erro comum: gravar em res:// em vez de user://.
Erro comum: esquecer FileAccess.file_exists() antes de ResourceLoader.load(), causando erro na primeira execução.
-->

---

## Boas Práticas — Save/Load

- Manter o caminho do arquivo de save em uma única constante (`CAMINHO_SAVE`), nunca repetida como string literal
- `SaveData` enxuto: apenas dados que precisam sobreviver ao fechamento do jogo, nunca referências diretas a Nodes
- Um único `SaveComponent` ativo por vez, assim como um único `SaveManager`
- Dar feedback visual ou sonoro simples ao alcançar um `Checkpoint`

<!--
Esses hábitos evitam retrabalho na integração do Encontro 2 e sustentam a Rubrica 4 (Code Review).
-->

---

## Fechamento — Encontro 1

- `SaveData` (Resource) e `SaveComponent` funcionais, salvando e recuperando progresso real entre sessões
- Ao menos uma Scene `Checkpoint`, implementando o contrato `Interactable` e acionando o `SaveComponent`
- GameManager, SaveManager, contrato Interactable, Signals e ItemData/Enum das Semanas 4 a 6 sem nenhuma alteração
- Próximo passo: integração completa do Módulo 2, no Encontro 2

<!--
Dificuldade esperada: confundir SaveManager (entre cenas) com SaveData (entre sessões) — reforçar a diferença.
Este resultado corresponde à conclusão dos itens "SaveComponent / SaveData (Resource)" e "Checkpoint" do roadmap (PROJECT_ARCHITECTURE.md, seção 6).
-->

---

<!-- _class: chapter -->

## Encontro 2

# Integração Final e Encerramento da Unidade II

<span class="chapter-number">02</span>

<!--
Encontro não introduz sistema novo. Reúne, sob supervisão do professor como diretor técnico, todos os sistemas construídos desde a Semana 4 em um único fluxo jogável por grupo.
-->

---

## Agenda do Encontro 2

- Revisão integrada de GameManager, SaveManager, Interactable, Signals, Resources e save/load (15 min)
- Laboratório: integração final dos desafios do módulo em um único fluxo jogável (60 min)
- Preparação de cada grupo para apresentar e justificar sua integração (15 min)
- Code Review — cada grupo apresenta e justifica as escolhas de arquitetura (30 min)
- Playtest coletivo entre grupos e fechamento da Unidade II (15 min)

<!--
Reservar tempo real de rotação entre grupos durante o Playtest coletivo.
Entrega da semana: gameplay funcional consolidado do Módulo 2, avaliado por Code Review e Playtest coletivo.
-->

---

<!-- _class: question -->

# Cada sistema do módulo funciona sozinho — mas o jogador consegue percorrer o nível do início ao fim, sem que nenhum precise ser retrabalhado?

Pense em portas, alavancas, baús e o `Checkpoint` construídos em semanas separadas.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que um Vertical Slice não é a soma isolada de sistemas testados cada um em seu canto — é a integração deles em um fluxo único.
Se o contrato Interactable e os Signals foram bem desenhados desde a Semana 5, a resposta deve ser sim, sem exigir alteração estrutural agora.
-->

---

## Integração: Um Único Fluxo Jogável

- Vertical Slice não é a soma isolada de sistemas — é a integração deles em uma experiência única
- Verifica se o desacoplamento ensinado desde a Semana 5 (contrato `Interactable`, Signals) permitiu montar tudo sem lógica duplicada
- Portas, alavancas, baús e `Checkpoint` conectados em um caminho único, do início ao fim

<!--
Erro comum: descobrir que um sistema anterior foi implementado de forma isolada e precisa de retrabalho — tratar como sinal de que o contrato Interactable não foi seguido à risca.
Erro comum: preferir criar novos objetos interativos a conectar os existentes — o objetivo é integração, não expansão de escopo.
-->

---

## Arquitetura — O Fluxo Integrado do Módulo 2

- `GameManager`/`SaveManager` (Autoload) sustentam o estado global do fluxo
- Contrato `Interactable` + Signals conectam Player, portas, alavancas, baús e `Checkpoint` sem lógica duplicada
- `ItemData`/Enum definem os dados coletáveis; `SaveData`/`SaveComponent` persistem o progresso real
- Nenhum sistema exige alteração estrutural para se conectar aos demais

<!--
Diagrama sugerido: Player → InteractionComponent → (Door | Lever | Chest | Checkpoint) via contrato Interactable → Signals → GameManager/SaveManager → SaveComponent → SaveData (user://).
Reforçar: se algum sistema exige retrabalho para integrar, é sinal de desacoplamento malfeito, não de imprevisto normal.
-->

---

> **Imagem sugerida**
>
> Objetivo: ilustrar o fluxo jogável integrado que o grupo deve alcançar.
> Enquadramento: mapa simplificado do nível de teste do grupo, visto de cima.
> Elementos presentes: ícones de porta, alavanca, baú e checkpoint distribuídos no espaço, conectados por uma linha pontilhada representando o caminho jogável do início ao objetivo.
> Destaque visual: a linha de fluxo contínua, mostrando que os sistemas não são ilhas isoladas.
> Legenda sugerida: "Fluxo jogável integrado: cada sistema do Módulo 2 conectado ao caminho único do jogador."

<!--
Usar esta imagem na introdução do laboratório de integração.
-->

---

<!-- _class: comparison -->

## Síntese Comparativa do Módulo 2 — Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Autoload, contrato via duck typing/Orchestrator, Signals, Resource + Enum, `SaveData`/FileAccess

</div>
<div class="col negative">

### Unity

- Sem Autoload formal, Interfaces em C#, UnityEvent/C# Actions, `ScriptableObject`/`enum`, `PlayerPrefs`/JSON

</div>
</div>

<!--
Nenhuma comparação nova é introduzida aqui — é o momento de consolidar as comparações já feitas nas Semanas 4 a 7.
Pedir a cada grupo que articule essas comparações com as próprias palavras durante o Code Review.
-->

---

## Laboratório — Integração do Fluxo Completo

Cada grupo:

1. Posiciona/reposiciona `Door`, `Lever`, `Chest` e `Checkpoint`, formando um caminho único
2. Confirma que a alavanca controla a porta via Signal já conectado (Semana 5)
3. Confirma que o baú concede um item refletido no `GameManager`/`SaveManager`
4. Posiciona o `Checkpoint` em ponto lógico do caminho
5. Percorre o fluxo do início ao fim; fecha e reabre o jogo para confirmar persistência

<!--
Erro comum: deixar o Checkpoint gravando o estado completo do GameManager em vez de apenas os dados definidos em SaveData.
-->

---

## Preparando a Justificativa de Arquitetura

- Para cada sistema do módulo, o grupo escreve uma frase: "por que fizemos dessa forma, e não de outra possível?"
- Distribuir a explicação entre integrantes — evitar que apenas uma pessoa saiba justificar as decisões técnicas
- Ensaiar mostrando o jogo sendo jogado do início ao fim, pausando em cada sistema

<!--
A partir deste Code Review, a disciplina cobra não só que o sistema funcione, mas por quê — habilidade exigida de forma crescente até a Semana 17.
Erro comum: preparar apresentação que descreve cada sistema isoladamente em vez do fluxo integrado.
-->

---

## Boas Práticas — Code Review e Playtest

- Ensaiar com o jogo rodando de verdade, nunca descrevendo o código em abstrato
- Deixar o colega jogar livremente no Playtest, sem instruções verbais prévias
- Registrar objetivamente os pontos observados, mesmo sem tempo de corrigir agora
- Tratar feedback com o mesmo profissionalismo esperado em uma equipe real

<!--
Code Review avalia arquitetura (Rubrica 4); Playtest avalia a experiência de quem joga sem conhecer a implementação. São ângulos complementares do mesmo entregável.
-->

---

<!-- _class: exercise -->

# Laboratório — Code Review e Playtest Coletivo

Apresente o fluxo jogável integrado ao professor, justificando as escolhas de arquitetura adotadas pelo grupo.

<div class="objectives">

**Entrega:** gameplay funcional consolidado do Módulo 2, avaliado por Code Review (Rubrica 4) e Playtest coletivo entre grupos.

</div>

<!--
Sem instrumento de desafio livre — a entrega da semana é a própria apresentação da integração completa.
Este entregável fecha a Unidade II e compõe, junto ao Checkpoint da Semana 6, a base de avaliação processual do Módulo 2.
-->

---

## Fechamento — Encontro 2

- Fluxo jogável único e coerente, sem sistemas isolados
- Progresso real persistido entre sessões, confirmado via `Checkpoint`
- Code Review (Rubrica 4) e Playtest coletivo realizados
- Unidade II — Construir Sistemas — encerrada

<!--
Dificuldade esperada: apresentar cada sistema isoladamente em vez do fluxo integrado — reforçar que o objetivo é a integração, não a soma de partes.
-->

---

## Resultado Esperado da Semana

- Vertical Slice com `GameManager`/`SaveManager`, contrato `Interactable`, Signals, `ItemData`/Enum e `SaveData`/`Checkpoint` integrados em um único fluxo
- Progresso real persistido entre sessões, não apenas entre cenas
- Turma relaciona `SaveData`/FileAccess ao equivalente da Unity (`PlayerPrefs`/JSON)
- Code Review e Playtest coletivo de encerramento do Módulo 2 concluídos

<!--
Este resultado corresponde ao "Produto do Módulo 2" do roadmap (PROJECT_ARCHITECTURE.md, seção 6): gameplay funcional com portas, baús, alavancas, checkpoints e progresso persistente integrados.
-->

---

## Checklist da Semana

- [ ] Classe `SaveData` (Resource) com `itens_coletados` e `ultimo_checkpoint`
- [ ] `SaveComponent` gravando e lendo corretamente em `user://`
- [ ] Progresso confirmado como persistente entre execuções (fechar e reabrir o jogo)
- [ ] `Checkpoint` implementando o contrato `Interactable`, sem lógica duplicada
- [ ] Portas, alavancas, baús e `Checkpoint` conectados em um único fluxo, do início ao fim
- [ ] Code Review (Rubrica 4) e Playtest coletivo realizados

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 8.
-->

---

## Próximos Passos — Semana 8

O gameplay funcional consolidado nesta semana é a base direta da Semana 8, que inicia a Unidade III (Resolver Problemas) com o `HealthComponent` — reutilizando o mesmo padrão de Component já estabelecido pelo `SaveComponent` — e a fundamentação de AnimationTree/BlendSpace. A metodologia muda de Studio Based Learning para Challenge Based Learning: o professor apresenta problemas e os grupos propõem soluções com autonomia crescente.

Leitura recomendada: Godot Docs — Saving Games, Resources, File System; Unity Manual (consulta comparativa) — PlayerPrefs.

<!--
Referências completas: ver Tutorial Semana 7 (Encontros 1 e 2) e Plano de Aula Semana 7.
-->
