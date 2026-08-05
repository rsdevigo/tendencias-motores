---
marp: true
theme: academic-course
paginate: true
header: 'Semana 4 — GameManager e SaveManager (Autoload/Singleton)'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 4

## GameManager e SaveManager (Autoload/Singleton)

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade II — Construir Sistemas** (Semanas 4–7)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
Retomar o projeto da Semana 3 já aberto, com nível de teste, Player, material, terreno, iluminação global e build exportado.
Esta semana abre o Módulo 2 (Construir Sistemas). Nada do nível, do Player ou do build da Semana 3 é refeito — apenas ampliado.
Metodologia: Studio Based Learning, autonomia baixa — professor demonstra, aluno adapta.
-->

---

## Objetivos da Semana

- Compreender Autoload/Singleton como mecanismo nativo do Godot para estado global compartilhado entre cenas
- Construir um `GameManager` que centraliza regras de partida e estado compartilhado
- Construir um `SaveManager` que centraliza persistência de dados entre cenas

<!--
Encontro 1 cobre Autoload/Singleton e o GameManager. Encontro 2 cobre input centralizado no Player e o SaveManager, com teste real de persistência entre cenas.
Resultado esperado ao final: dois Autoloads funcionais, com estado próprio persistindo corretamente.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Autoload/Singleton e o GameManager

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o projeto da Semana 3 sem alterar nada do que já existe — nível, Player e build permanecem intactos.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 3 (build exportado, encerramento do Módulo 1) (15 min)
- Introdução: onde vive o estado que não pertence a nenhuma cena específica (20 min)
- Demonstração: criação do script `GameManager` e registro como Autoload (35 min)
- Laboratório: cada estudante cria e registra seu próprio `GameManager` (45 min)
- Desafio: adicionar uma variável de estado de partida própria (15 min)
- Feedback e fechamento (5 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
-->

---

<!-- _class: question -->

# Onde vive um dado que várias cenas precisam compartilhar, mas que não pertence a nenhuma delas?

Pense em pontuação, condição de vitória ou referência ao jogador ativo.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que uma Scene comum é descarregada ao trocar de cena, e que o dado dentro dela desaparece junto.
Erro comum: sugerir "guardar em uma variável global do script" sem perceber que isso ainda depende de uma Scene viva.
-->

---

## O Problema Universal do Estado Global

Toda engine que trabalha com múltiplas cenas precisa resolver o mesmo problema.

- Um dado guardado dentro de uma Scene comum desaparece quando ela é trocada
- Pontuação, condição de vitória e referência ao jogador ativo não pertencem a nenhuma cena específica
- Toda engine moderna oferece um mecanismo dedicado para esse tipo de estado

<!--
Conceito universal, não específico do Godot. Reforçar o hábito da disciplina: sempre perguntar "que problema universal isso resolve?" antes de "como se usa no Godot?".
Referência: Godot Docs — Singletons (Autoload).
-->

---

## Autoload/Singleton no Godot

- **Autoload** — script registrado em Project Settings, instanciado automaticamente na raiz da árvore de cenas
- Acessível globalmente por nome, de qualquer script do projeto
- Sobrevive a qualquer troca de cena
- O Godot formaliza como recurso de primeira classe do editor

<!--
Diferenciar Autoload de um Node comum adicionado a uma Scene: o Autoload vive fora da árvore de cenas do nível.
Documentação: Godot Docs — Singletons (Autoload).
-->

---

## GameManager — Papel no Projeto

- Reúne regras de partida e estado compartilhado em um único ponto
- Criado como script `Node`, registrado como Autoload
- Convenção: `class_name` em PascalCase, arquivo em snake_case
- Local no projeto: `scripts/autoload/game_manager.gd`

<!--
Reforçar a convenção de nomenclatura do PROJECT_ARCHITECTURE.md (seção 10): class_name PascalCase, arquivo snake_case.
-->

---

<!-- _class: comparison -->

## Estado Global no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Autoload/Singleton, registrado em Project Settings
- Instância única garantida pelo editor
- `GameManager` reúne GameMode + GameState

</div>
<div class="col negative">

### Unity

- Sem mecanismo formal equivalente
- Resolvido por convenção: `DontDestroyOnLoad` ou singleton manual em C#
- Depende da disciplina da equipe

</div>
</div>

<!--
A Unreal separa formalmente GameMode (regras) e GameState (estado compartilhado); o Godot não precisa dessa separação para resolver o mesmo problema.
Não ensinar Unity em profundidade — apenas contrastar arquitetura.
-->

---

## Demonstração — Criando o GameManager

O que será construído:

- Script `scripts/autoload/game_manager.gd`, com `class_name GameManager`
- Registro em **Project Settings > Autoload**
- Teste de acesso a partir do script do Player, com `print(GameManager)`

Por quê: primeiro Autoload do projeto, base de todo o Módulo 2.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 4, Encontro 1). O slide só estrutura a demonstração ao vivo.
Reforçar: remover o print() de teste antes de encerrar a demonstração.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a aba Autoload de Project Settings com o `GameManager` recém-registrado.
> Enquadramento: captura de tela da janela Project Settings, aba Autoload.
> Elementos presentes: campo Path apontando para `res://scripts/autoload/game_manager.gd`, campo Node Name como `GameManager`, caixa Enable marcada.
> Destaque visual: a linha do `GameManager` na lista de Autoloads.
> Legenda sugerida: "GameManager registrado e habilitado como Autoload em Project Settings."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — GameManager

Cada estudante replica, no próprio projeto:

1. Pasta `scripts/autoload/` criada, conforme PROJECT_ARCHITECTURE.md
2. Script `game_manager.gd`, com `class_name GameManager`
3. Registro em **Project Settings > Autoload**
4. Teste de acesso ao `GameManager` a partir do script do Player
5. Remoção do `print()` de teste ao final

<!--
Erro comum: registrar o Autoload com Node Name em minúsculo ou diferente de GameManager — sempre ajustar manualmente para PascalCase.
Erro comum: testar o acesso antes de salvar o registro em Project Settings.
-->

---

## Boas Práticas — Autoload

- Manter todo Autoload dentro de `scripts/autoload/`, nunca solto na raiz de `res://`
- Escrever, desde o primeiro script, um comentário curto explicando sua responsabilidade
- Testar o acesso ao Autoload a partir de uma cena diferente da que está sendo editada
- Nunca duplicar em uma Scene um dado que já pertence ao `GameManager`

<!--
Esse hábito evita que o GameManager acumule, nas semanas seguintes, responsabilidades que deveriam pertencer ao SaveManager ou a um Component.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 1

Adicione ao `GameManager` uma variável de estado de partida própria, não demonstrada em aula — um contador de tentativas, um estado de progresso ou uma flag de evento.

<div class="objectives">

Justifique em um comentário no script por que essa variável pertence ao `GameManager` e não a uma Scene específica.

</div>

<!--
Circular pela sala pedindo justificativas curtas em voz alta. Sem instrumento formal de avaliação neste encontro.
-->

---

## Fechamento — Encontro 1

- `GameManager` criado e registrado como Autoload, com acesso validado a partir do Player
- Variável de estado própria do desafio adicionada, com justificativa comentada
- Nível, Player e build da Semana 3 permanecem intactos
- Próximo passo: input centralizado no Player e SaveManager, no Encontro 2

<!--
Dificuldade esperada: confundir Autoload com Node comum de Scene — reforçar que ele vive fora da árvore de cenas do nível.
Este resultado corresponde ao início do item "GameManager (Autoload)" do roadmap (PROJECT_ARCHITECTURE.md, seção 6).
-->

---

<!-- _class: chapter -->

## Encontro 2

# Input no Player e o SaveManager

<span class="chapter-number">02</span>

<!--
Encontro depende diretamente do GameManager do Encontro 1. Confirmar que todos têm o Autoload registrado e testado antes de prosseguir.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (`GameManager` registrado como Autoload) (10 min)
- Introdução: input centralizado no Player e o problema da persistência (20 min)
- Demonstração: criação do `SaveManager` e variável persistente (35 min)
- Laboratório: cada estudante cria seu `SaveManager` e testa persistência (45 min)
- Desafio: dado próprio persistindo entre cenas (20 min)
- Feedback e fechamento (5 min)

<!--
Reservar tempo real para o teste de troca de cena no laboratório — é o momento em que o conceito de Autoload se torna concreto para a turma.
-->

---

<!-- _class: question -->

# Por que o Godot não separa "quem controla" de "o que é controlado", como a Unreal faz?

Pense em como o Player já lê input desde a Semana 2.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a reconhecer essa ausência como escolha arquitetural, não limitação.
Esta parte é conceitual — sem alteração no projeto.
-->

---

## Input de Alto Nível no Player

- Unreal separa formalmente PlayerController (lê input) de Pawn/Character (é controlado)
- Godot concentra a leitura de input de alto nível no próprio Node do Player
- Não é uma limitação — é uma escolha arquitetural válida
- Reduz camadas de indireção para ações simples de gameplay

<!--
Reforçar: essa centralização é a base para o Player acionar interações na Semana 5 e abrir o menu de pausa na Semana 9.
-->

---

<!-- _class: comparison -->

## Input Centralizado no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Sem separação nativa Pawn/Controller
- Input concentrado no próprio Player

</div>
<div class="col negative">

### Unity

- Também sem separação formal
- Input tipicamente no script do personagem ou Input System conectado a ele

</div>
</div>

<!--
Godot e Unity resolvem esse problema de forma semelhante — diferente da Unreal, que formaliza a separação Pawn/Controller.
-->

---

## O Problema Universal da Persistência

Toda engine multi-cena precisa de um lugar para guardar dados que sobrevivem à troca de cena — antes mesmo de qualquer gravação em disco.

- `GameManager` guarda regras e estado da partida atual
- `SaveManager` guarda dados que precisam sobreviver à troca de cena
- Separação evita que um único Autoload acumule responsabilidades demais

<!--
Preparar o terreno para a serialização em disco, construída na Semana 7 (SaveComponent/SaveData).
-->

---

## SaveManager — Segundo Autoload do Projeto

- Script `Node` independente, com `class_name SaveManager`
- Registrado separadamente em **Project Settings > Autoload**
- Local no projeto: `scripts/autoload/save_manager.gd`
- Guarda dados que sobrevivem à troca de cena, em memória

<!--
Reforçar: SaveManager e GameManager nunca herdam um do outro nem dependem de detalhes internos um do outro.
-->

---

<!-- _class: comparison -->

## Persistência entre Cenas no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- Segundo Autoload dedicado (`SaveManager`)
- Sobrevivência garantida pelo registro em Project Settings

</div>
<div class="col negative">

### Unity

- Singleton manual, muitas vezes o mesmo objeto do "game manager"
- Sobrevivência via `DontDestroyOnLoad`

</div>
</div>

<!--
O Godot separa formalmente os dois papéis em Autoloads independentes; na Unity essa separação depende da disciplina da equipe.
-->

---

## Demonstração — SaveManager e Persistência

O que será construído:

- Script `save_manager.gd`, com uma variável persistente (ex.: `itens_coletados`)
- Scene de teste `level_teste_persistencia.tscn`
- Troca de cena real, validando que o valor não é perdido

Por quê: um Autoload só demonstra sua utilidade quando testado sob o cenário que ele resolve.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 4, Encontro 2).
Reforçar: reverter a Main Scene para level_exploration.tscn ao final do teste.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a aba Autoload de Project Settings com dois registros — `GameManager` e `SaveManager` — lado a lado.
> Enquadramento: captura de tela da janela Project Settings, aba Autoload.
> Elementos presentes: lista com os dois Autoloads, coluna Path e coluna Node Name.
> Destaque visual: as duas linhas, reforçando que são Autoloads independentes.
> Legenda sugerida: "GameManager e SaveManager registrados como Autoloads independentes ao final da Semana 4."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — SaveManager

Cada estudante replica, no próprio projeto:

1. Script `save_manager.gd`, com `class_name SaveManager`
2. Registro em **Project Settings > Autoload**
3. Variável persistente e função simples para alterá-la
4. Scene de teste com troca real de cena, validando a persistência
5. Reversão da Main Scene para `level_exploration.tscn`

<!--
Erro comum: declarar a variável de teste dentro da Scene em vez do SaveManager — o valor seria perdido ao trocar de cena.
Erro comum: esquecer de reverter a Main Scene após o teste.
-->

---

## Boas Práticas — SaveManager

- Manter `GameManager` e `SaveManager` como scripts totalmente independentes
- Comentar, no topo de cada Autoload, qual tipo de dado ele guarda
- Sempre testar persistência com uma troca de cena real, nunca apenas revisando o código
- Nomear variáveis de forma que já sugiram o que representam no Vertical Slice final

<!--
Reforçar: nenhum arquivo é salvo em disco nesta semana — a serialização só chega na Semana 7.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 2

Defina e implemente, no `SaveManager`, um dado próprio que deve persistir entre cenas — pontuação, item coletado ou estado de progresso, diferente do demonstrado.

<div class="objectives">

Valide a persistência com uma troca de cena real dentro do projeto.

</div>

<!--
Cada grupo escolhe seu próprio dado. Sem instrumento formal isolado — compõe a base avaliada no Checkpoint da Semana 6.
-->

---

## Checkpoint — Base do Módulo 2

Ao final da semana, cada estudante possui:

- `GameManager` (Autoload), com variável de estado de partida própria
- `SaveManager` (Autoload), independente, com dado persistindo entre cenas
- Nível, Player e build da Semana 3, sem nenhuma alteração

<!--
Rubrica 3 — Checkpoints (progresso, funcionalidades, qualidade técnica). Sem instrumento formal isolado neste encontro; pré-requisito direto do Checkpoint da Semana 6.
-->

---

## Fechamento — Encontro 2

- Discussão sobre input centralizado no Player concluída
- `SaveManager` criado, registrado e testado com troca real de cena
- Desafio do grupo (dado próprio persistente) implementado
- Módulo 2 avança com dois Autoloads funcionais

<!--
Dificuldade esperada: sobrepor responsabilidades entre GameManager e SaveManager — reforçar a separação de papéis.
-->

---

## Resultado Esperado da Semana

- `GameManager` (Autoload), com regras e estado de partida compartilhado
- `SaveManager` (Autoload), independente, com dado de progresso persistindo entre cenas
- Turma relaciona Autoload/Singleton à ausência de equivalente formal na Unity
- Turma compreende input centralizado no Player como escolha arquitetural válida

<!--
Esses dois sistemas abrem a Unidade II e sustentam toda a arquitetura de gameplay das semanas seguintes.
-->

---

## Checklist da Semana

- [ ] Script `game_manager.gd` criado, com `class_name GameManager`, registrado como Autoload
- [ ] Variável de estado própria do desafio adicionada ao `GameManager`
- [ ] Script `save_manager.gd` criado, com `class_name SaveManager`, registrado como Autoload
- [ ] Variável persistente implementada e validada com troca real de cena
- [ ] Main Scene revertida para `level_exploration.tscn` após o teste
- [ ] Dado próprio do desafio do `SaveManager` implementado e validado

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 5.
-->

---

## Próximos Passos — Semana 5

Os dois Autoloads construídos nesta semana são a base direta da Semana 5:

- Contrato `Interactable` e Signals para comunicação desacoplada entre sistemas
- Primeiro objeto interativo do Vertical Slice (porta ou equivalente)

Leitura recomendada: Godot Docs — Singletons (Autoload), GDScript; Unity Manual (consulta comparativa) — DontDestroyOnLoad.

<!--
Nada desta semana será refeito — apenas ampliado. Reforçar isso à turma para reduzir ansiedade sobre "ter feito certo".
Referências completas: ver Tutorial Semana 4 (Encontros 1 e 2) e Plano de Aula Semana 4.
-->
