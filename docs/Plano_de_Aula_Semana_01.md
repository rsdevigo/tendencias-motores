# Semana 1

## Introdução da Semana

Esta é a primeira semana da disciplina e o ponto de partida da Unidade I — Aprender a Ferramenta. Antes de qualquer botão do Unreal Editor, a semana estabelece a pergunta que orienta todo o semestre: o que é uma game engine e como ela organiza um mundo jogável? A partir dessa fundamentação, a turma inicia a estrutura do projeto único da disciplina (Vertical Slice, nome de trabalho *O Templo Esquecido*) e aprende o primeiro conceito universal de composição de motores: Actor e Component.

A metodologia da semana é Scaffolded Learning — o professor demonstra e o estudante replica, com autonomia muito baixa, condizente com o Módulo 1 e com o fato de ser a primeira semana de contato com a Unreal Engine 5.6.

## Objetivos Gerais

- Compreender o que é uma game engine e por que ela existe, antes de qualquer manipulação de interface.
- Reconhecer a organização do Unreal Editor (Viewport, Content Browser, estrutura de projeto) como instância concreta de conceitos presentes em qualquer engine.
- Compreender Actor e Component como unidade universal de composição de motores, em contraste com herança.
- Iniciar a estrutura de pastas e organização do projeto do Vertical Slice, que será reutilizada em todas as semanas seguintes.

## Resultados Esperados

Ao final da semana, cada grupo terá o projeto do Vertical Slice criado e organizado no Unreal Editor, além de um primeiro Actor customizado com Components, incluindo uma variação própria implementada como desafio. Nenhum sistema de gameplay ainda é esperado — o resultado é puramente estrutural e conceitual, servindo de base para a Semana 2.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o papel de uma game engine na organização de um mundo jogável, distinguindo engine, editor e jogo.
- Identificar as áreas principais do Unreal Editor (Viewport, Content Browser, Outliner, Details) e sua função.
- Criar e organizar a estrutura inicial de pastas do projeto do Vertical Slice.

## Conteúdos

- O que é uma game engine e por que ela existe.
- Tour guiado pelo Unreal Editor: Viewport, Content Browser, estrutura de projeto.
- Criação e organização inicial do projeto do Vertical Slice.

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre **engine** (o software que fornece as ferramentas e o runtime) e **jogo** (o conteúdo e a lógica construídos sobre ela). Toda engine moderna — Unreal, Unity, Godot, O3DE — resolve o mesmo conjunto de problemas: renderização, física, gerenciamento de assets, organização de cena e execução de lógica de gameplay. O editor é apenas a interface que expõe esses sistemas ao desenvolvedor. Compreender essa separação evita que o estudante confunda "aprender Unreal" com "aprender a fazer jogos", reforçando o objetivo da disciplina de ensinar conceitos transferíveis entre motores.

## Recursos da Unreal

Unreal Editor, Viewport, Content Browser, estrutura de pastas de projeto.

## Comparação com Unity

A organização do Unreal Editor (Viewport, Content Browser, Outliner, Details) corresponde diretamente à Scene View, Project Window, Hierarchy e Inspector da Unity. A diferença arquitetural mais relevante nesta etapa é que a Unreal já nasce com um Gameplay Framework robusto embutido (que será explorado no Módulo 2), enquanto a Unity oferece uma base mais minimalista, deixando essa camada mais a cargo do desenvolvedor. Não aprofundar — este ponto será retomado na Semana 4.

## Preparação do Professor

- Projeto Unreal Engine 5.6 em branco, template Third Person, pronto para demonstração ao vivo.
- Estrutura de pastas de referência já organizada (Content > Project, Blueprints, Assets, Maps) para servir de modelo.
- Kenney Prototype Kit importado, para uso a partir da Semana 3 (não obrigatório nesta aula, mas útil ter disponível).
- Slides com a definição de engine, a distinção engine/editor/jogo e um panorama visual das áreas do editor.
- PROJECT_ARCHITECTURE.md impresso ou projetado, para apresentar aos estudantes o escopo do Vertical Slice que será construído ao longo do semestre.

## Cronograma do Encontro

- 15 min — Apresentação da disciplina, do Vertical Slice e da lógica de avaliação processual (sem prova).
- 25 min — Fundamentação: o que é uma engine, por que existe, distinção engine/editor/jogo.
- 30 min — Demonstração guiada: tour pelo Unreal Editor (Viewport, Content Browser, Outliner, Details).
- 45 min — Laboratório: cada estudante/grupo cria seu projeto Third Person e organiza a estrutura inicial de pastas replicando o modelo demonstrado.
- 20 min — Feedback: verificação da estrutura de pastas de cada grupo e dúvidas sobre navegação no editor.

## Desenvolvimento

A aula abre sem tocar no editor: primeiro se discute o conceito de engine e por que ela existe, situando a Unreal como um caso concreto entre várias engines possíveis. Em seguida, o professor projeta o editor e faz um tour guiado pelas áreas principais, explicando a função de cada uma antes de qualquer ação prática. Só então os estudantes replicam a criação de um novo projeto Third Person e organizam a estrutura de pastas seguindo o padrão demonstrado, que será reutilizado em todas as semanas seguintes do Vertical Slice.

## Desafio

Não há desafio neste encontro — o Encontro 1 da Semana 1 é integralmente demonstração e replicação guiada, coerente com a autonomia muito baixa do início do Módulo 1.

## Critérios de Sucesso

Ao final do encontro, cada estudante/grupo deve ter um projeto Unreal Engine 5.6 criado, com estrutura de pastas organizada e navegável, correspondendo ao padrão demonstrado em aula.

## Evidências para Avaliação

Organização técnica do projeto (estrutura, nomenclatura) desde o primeiro encontro, conforme previsto no Sistema de Avaliação — critério que será revisitado ao longo de todo o semestre, não apenas nos checkpoints formais.

## Dificuldades Esperadas

Estudantes vindos de Unity podem tentar mapear diretamente conceitos (ex.: procurar um "Assets folder" idêntico) sem perceber diferenças de convenção. Intervenção: reforçar verbalmente que a equivalência é funcional, não literal, e retomar a comparação de forma breve sempre que surgir confusão.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Actor e Component como unidade universal de composição em motores de jogos, contrastando composição com herança.
- Criar um Actor Blueprint com Components via Unreal Editor.
- Implementar uma variação própria de Component, produzindo um comportamento visual diferente do demonstrado.

## Conteúdos

- Actor e Component como unidade universal de composição (composição versus herança).
- Comparação breve com GameObject/Component da Unity.
- Criação guiada de um Actor com Components via Blueprint.

## Conceitos Fundamentais

O conceito universal é **composição sobre herança** como padrão arquitetural dominante em motores de jogos modernos. Um Actor é um contêiner que ganha comportamento e forma anexando Components (malha, colisão, luz, áudio, lógica), em vez de depender de uma árvore rígida de herança de classes. Esse padrão resolve o problema de reutilização de comportamento sem acoplamento excessivo — um mesmo Component pode ser anexado a Actors completamente diferentes. É o mesmo problema que toda engine moderna precisa resolver, e a forma como cada uma resolve (Actor/Component na Unreal, GameObject/Component na Unity, Node na Godot) é uma decisão arquitetural específica sobre um conceito universal comum.

## Recursos da Unreal

Actors, Components, Blueprint.

## Comparação com Unity

O par Actor/Component da Unreal corresponde diretamente ao par GameObject/Component da Unity — em ambos os casos, o comportamento é montado por composição, não por herança de classes de gameplay. A diferença mais relevante é que, na Unreal, o Actor já é uma classe C++/Blueprint com ciclo de vida e replicação embutidos, enquanto na Unity o GameObject é um contêiner mais genérico, com o comportamento definido quase inteiramente pelos Components (MonoBehaviours) anexados. Não aprofundar mais que isso — o objetivo é reconhecer a equivalência conceitual, não decorar diferenças de implementação.

## Preparação do Professor

- Projeto criado no Encontro 1 aberto e pronto para continuar.
- Um Actor Blueprint de exemplo pré-configurado (fora da visão da turma) com dois ou três Components (Static Mesh, Point Light, Box Collision), para demonstração passo a passo.
- Assets simples do Kenney Prototype Kit disponíveis para variação visual (formas geométricas básicas).
- Slides com o diagrama composição versus herança e a correspondência Actor/Component ↔ GameObject/Component.

## Cronograma do Encontro

- 5 min — Revisão rápida do Encontro 1 (estrutura de projeto e navegação no editor).
- 15 min — Fundamentação: composição versus herança, Actor e Component como unidade universal.
- 35 min — Demonstração: criação guiada de um Actor Blueprint com Components (malha, colisão, luz).
- 45 min — Laboratório: cada estudante/grupo replica o Actor demonstrado no próprio projeto.
- 20 min — Desafio: adicionar um Component adicional, produzindo um comportamento visual diferente do demonstrado.
- 15 min — Feedback: showcase rápido das variações de cada grupo e fechamento da semana.

## Desenvolvimento

O encontro retoma o projeto criado no Encontro 1 e introduz o primeiro elemento de composição do Vertical Slice: um Actor Blueprint com múltiplos Components. O professor demonstra a criação passo a passo, explicando a função de cada Component anexado antes de adicioná-lo. Em seguida, cada grupo replica o mesmo Actor dentro do próprio projeto, consolidando a estrutura de pastas organizada no encontro anterior. Por fim, o desafio pede que cada grupo acrescente um Component diferente do demonstrado, produzindo uma variação visual própria — primeiro pequeno exercício de autonomia da disciplina, ainda dentro de um escopo estreito e seguro.

## Desafio

Adicionar um Component adicional ao Actor demonstrado, produzindo um comportamento visual diferente do apresentado em aula (por exemplo, uma luz de cor distinta, uma malha adicional ou um efeito de rotação simples). Deve permitir diferentes soluções, sem gabarito único.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve ter um Actor Blueprint funcional no projeto do Vertical Slice, com ao menos os Components demonstrados em aula mais uma variação própria resultante do desafio.

## Evidências para Avaliação

Funcionamento do Actor com Components (Rubrica de qualidade técnica/funcionamento) e capacidade de propor uma variação própria diante de um desafio de liberdade restrita — primeira manifestação, ainda mínima, do eixo de Desafios Técnicos do Sistema de Avaliação.

## Dificuldades Esperadas

Estudantes podem tentar resolver a variação do desafio criando uma nova classe de Actor em vez de anexar um Component adicional, replicando o padrão de herança da programação tradicional. Intervenção: relembrar verbalmente o princípio de composição sobre herança antes de auxiliar tecnicamente, redirecionando para a solução via Component.

---

# Resultado Esperado da Semana

Ao final da Semana 1, cada estudante/grupo deve possuir: um projeto Unreal Engine 5.6 criado e organizado segundo a estrutura de pastas do Vertical Slice; um Actor Blueprint funcional composto por múltiplos Components, incluindo uma variação própria criada no desafio. Conceitualmente, a turma deve dominar a distinção entre engine e jogo, a navegação básica pelo Unreal Editor e o princípio de composição sobre herança como base de qualquer motor de jogos moderno.

# Preparação para a Próxima Semana

A Semana 2 depende diretamente do Actor criado nesta semana: o BP_Player será configurado a partir de um Character (subclasse de Actor com Components de movimentação), reutilizando a estrutura de pastas e a familiaridade com o editor e com Components já construída. A distinção Actor/Component também será retomada ao explicar por que Character é uma especialização de Actor com Components adicionais (Character Movement Component), e não uma classe isolada.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Visão geral do Editor. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Actors e Components (Gameplay Framework). Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — GameObjects e Components, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de tour pelo editor.
