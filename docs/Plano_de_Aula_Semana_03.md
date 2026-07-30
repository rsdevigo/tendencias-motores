# Semana 3

## Introdução da Semana

A Semana 3 encerra a Unidade I — Aprender a Ferramenta. Se as Semanas 1 e 2 estabeleceram a unidade universal de composição (Actor/Component) e o desacoplamento entre input e ação (Enhanced Input), esta semana responde à pergunta que fecha o módulo: como uma engine renderiza e empacota um mundo jogável? A turma aplica um material simples e um terreno básico ao mesmo nível de teste em que o BP_Player já se move, ativa os pilares de renderização moderna da Unreal (Nanite e Lumen) e gera o primeiro build executável do Vertical Slice.

A metodologia permanece Scaffolded Learning, coerente com a autonomia ainda muito baixa do Módulo 1 — o professor demonstra, o aluno replica. Não há desafio de liberdade de solução nesta semana: o Encontro 2 concentra o instrumento avaliativo de encerramento de módulo (Checkpoint + Showcase), e a prioridade pedagógica é garantir que todo grupo chegue a um build funcional, não introduzir uma nova decisão técnica autônoma.

## Objetivos Gerais

- Compreender o Material Graph como conceito universal de shader nodal, antes de qualquer detalhe de nó específico da Unreal.
- Modelar um terreno básico via Landscape para o nível de teste do Vertical Slice.
- Compreender Nanite (geometria virtualizada) e Lumen (iluminação global dinâmica) como soluções específicas da Unreal para dois problemas universais de renderização moderna: complexidade geométrica e iluminação indireta.
- Compreender o pipeline de Packaging como a etapa que transforma um projeto editável em um produto executável e distribuível.
- Gerar o primeiro build empacotado do Vertical Slice, com o BP_Player funcional dentro dele.

## Resultados Esperados

Ao final da semana, cada grupo terá um nível de teste com material e terreno básicos, Lumen e Nanite ativos e ajustados, e um primeiro build executável do Vertical Slice — o BP_Player controlável por Enhanced Input, já construído nas Semanas 1 e 2, rodando dentro desse build. Este é o Checkpoint de encerramento do Módulo 1: o resultado ainda é estrutural (sem sistemas de gameplay além de locomoção e câmera), mas passa a existir fora do Editor, encerrando a Unidade I com um artefato jogável concreto.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o Material Graph como conceito universal de shader nodal, independente da sintaxe específica de qualquer engine.
- Criar um material simples usando texturas básicas e parâmetros de superfície.
- Modelar um terreno básico via Landscape para o nível de teste do Vertical Slice.

## Conteúdos

- Material Graph: conceito de shader nodal.
- Criação guiada de um material simples.
- Landscape como ferramenta de terreno.
- Modelagem básica do terreno do nível de teste.

## Conceitos Fundamentais

O conceito universal desta aula é o shader nodal: qualquer engine moderna resolve a aparência de uma superfície através de um grafo de nós que combina texturas, valores escalares e operações matemáticas para produzir as propriedades físicas de um material (cor base, rugosidade, metalicidade, normal), em vez de exigir que o desenvolvedor escreva código de shader diretamente. O Material Graph da Unreal é uma implementação específica desse conceito, com nós próprios (Texture Sample, Scalar Parameter, Vector Parameter) e material domains (Surface, Deferred Decal etc.). Landscape, por sua vez, resolve um problema à parte — o de terreno em larga escala, esculpido por heightmap e pintado por camadas de material — que não deve ser confundido com um Static Mesh comum. Compreender essa separação (aparência de superfície versus geometria de terreno) prepara a turma para reconhecer, no Encontro 2, que Nanite e Lumen resolvem problemas de geometria e de iluminação de forma igualmente distinta.

## Recursos da Unreal

Material Graph, Texture Sample, Scalar Parameter, Vector Parameter, Landscape, nível de teste do Vertical Slice.

## Comparação com Unity

O Material Graph da Unreal corresponde ao Shader Graph da Unity: ambos abstraem a criação de shaders em um grafo nodal, evitando código de shader escrito à mão para a maioria dos casos. A diferença arquitetural mais relevante é que a Unreal integra o Material Graph nativamente ao pipeline de renderização desde a primeira versão, com material domains e blend modes configuráveis diretamente no grafo, enquanto a Unity, historicamente dividida entre Built-in Render Pipeline e pipelines mais recentes (URP/HDRP), só oferece Shader Graph de forma plena nesses pipelines modernos. Landscape corresponde ao Terrain da Unity, com papel equivalente (heightmap + camadas de material); não aprofundar mais que isso — o ponto será retomado, se necessário, na Unidade V.

## Preparação do Professor

- Projeto de cada grupo (Semanas 1 e 2) aberto, com BP_Player funcional e controlável no nível de teste.
- Texturas simples do Kenney Prototype Kit/Nature Kit organizadas na pasta `Textures/` para uso imediato.
- Um material de exemplo pré-configurado (fora da visão da turma), como referência de Texture Sample + Scalar Parameter, para demonstração passo a passo.
- Landscape de exemplo esculpido previamente (fora da visão da turma), para demonstração de sculpt e paint.
- Slides com o diagrama Textura/Parâmetro → Material Graph → Superfície, e a distinção entre Material (aparência) e Landscape (geometria de terreno).
- PROJECT_ARCHITECTURE.md disponível para reforçar as convenções `M_` (Material) e a subpasta `Materials/Base/`.

## Cronograma do Encontro

- 15 min — Revisão do BP_Player e do nível de teste consolidados na Semana 2.
- 20 min — Fundamentação: Material Graph como shader nodal universal, e Landscape como ferramenta de terreno.
- 35 min — Demonstração: criação guiada de um material simples e escultura básica de um terreno com Landscape.
- 50 min — Laboratório: cada grupo cria seu próprio material e modela o terreno do nível de teste.
- 15 min — Feedback: verificação do material e do terreno de cada grupo, dúvidas sobre parâmetros.

## Desenvolvimento

O encontro parte do nível de teste já existente, ainda em graybox, e mostra por que um mundo jogável exige tanto uma solução de aparência de superfície (Material) quanto uma solução de geometria de terreno (Landscape) — dois problemas distintos, resolvidos por ferramentas distintas. O professor demonstra a criação de um material simples a partir de uma textura do Kenney, ajustando parâmetros básicos (cor, rugosidade), e em seguida esculpe um terreno mínimo com Landscape, aplicando esse material a ele. Cada grupo replica os dois processos no próprio nível de teste, produzindo uma primeira versão visualmente reconhecível do ambiente em que o BP_Player já se move.

## Desafio

Não há desafio neste encontro — a criação do material e do terreno é demonstração e replicação guiada, coerente com a autonomia muito baixa do Módulo 1 e com a proximidade do Checkpoint de encerramento no Encontro 2.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve ter um material simples aplicado a um terreno básico via Landscape, compondo o nível de teste em que o BP_Player já se move, com nomenclatura de material conforme a convenção `M_` do PROJECT_ARCHITECTURE.md.

## Evidências para Avaliação

Organização e nomenclatura do material e do terreno conforme as convenções do PROJECT_ARCHITECTURE.md (Rubrica 1 — Desenvolvimento Semanal, critério Execução).

## Dificuldades Esperadas

Estudantes podem tentar aplicar um Static Mesh comum como terreno em vez de usar Landscape, ou confundir parâmetros de material com propriedades de iluminação da cena. Intervenção: reforçar verbalmente que Landscape resolve um problema de geometria em larga escala que um Static Mesh não resolve com a mesma eficiência, e redirecionar ajustes de iluminação para o Encontro 2, quando Lumen for introduzido.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar Nanite (geometria virtualizada) e Lumen (iluminação global dinâmica) como soluções da Unreal para dois problemas universais de renderização moderna.
- Explicar o pipeline de Packaging como transformação de um projeto editável em um build executável.
- Ativar e ajustar Nanite/Lumen no nível de teste e gerar o primeiro build empacotado do Vertical Slice.

## Conteúdos

- Nanite: geometria virtualizada.
- Lumen: iluminação global dinâmica.
- Comparação com as soluções equivalentes da Unity.
- Pipeline de Packaging e geração de build.

## Conceitos Fundamentais

O conceito universal desta aula tem duas partes. A primeira é o problema da complexidade geométrica: toda engine precisa decidir quanto detalhe poligonal exibir em tela sem comprometer performance, tradicionalmente resolvido por LODs manuais; Nanite resolve esse problema virtualizando a geometria, exibindo o detalhe necessário a cada pixel sem exigir LODs criados à mão. A segunda é o problema da iluminação indireta: toda engine precisa simular como a luz rebate entre superfícies, tradicionalmente resolvido por lightmaps pré-calculados (bake) ou soluções de tempo real limitadas; Lumen resolve esse problema com iluminação global totalmente dinâmica, sem necessidade de bake prévio, reagindo a mudanças de geometria e luz em tempo real. Packaging, por sua vez, é o conceito universal de transformar um projeto que só roda dentro do Editor em um executável autocontido, capaz de rodar fora dele — todo o trabalho de renderização (materiais, Landscape, Nanite, Lumen) só se torna um produto jogável real através dessa etapa.

## Recursos da Unreal

Nanite, Lumen, Packaging, nível de teste do Vertical Slice.

## Comparação com Unity

Nanite não possui equivalente direto na Unity: o caminho tradicional (e ainda majoritário na Unity) é a criação manual de LODs e o uso cuidadoso de contagem de polígonos por cena, embora a Unity venha explorando soluções próprias de geometria em alta densidade em pipelines mais recentes. Lumen corresponde, em intenção, ao Enlighten/GI dinâmico da Unity (URP/HDRP) ou a soluções de terceiros, mas a Unreal entrega Lumen ativado por padrão em novos projetos, enquanto a Unity historicamente depende mais de bake de lightmaps (Progressive Lightmapper) para iluminação indireta de alta qualidade. Packaging corresponde ao Build da Unity (File > Build Settings): ambos resolvem o mesmo problema de gerar um executável a partir do projeto, com pipelines de configuração de plataforma-alvo equivalentes em intenção. Não aprofundar mais que isso — o objetivo é reconhecer a equivalência conceitual, não decorar diferenças de configuração; a comparação arquitetural mais profunda entre motores é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com material e Landscape do Encontro 1 prontos.
- Nanite e Lumen já suportados pelo template/projeto (verificar configuração de projeto antes da aula, evitando perda de tempo com troubleshooting de configuração em aula).
- Slides com o diagrama Geometria bruta → Nanite → Detalhe por pixel, e Luz emitida → Lumen → Iluminação indireta em tempo real.
- Passo a passo de Packaging testado previamente pelo professor na mesma versão de engine usada pela turma, para evitar surpresas durante a demonstração.
- Modelo de Avaliação de Checkpoint (Rubrica 3 do Sistema de Avaliação) impresso ou digital, pronto para preenchimento durante o Showcase.
- Tempo estimado de build reservado no cronograma do encontro (builds podem levar alguns minutos; considerar iniciar o packaging de cada grupo o quanto antes no laboratório).

## Cronograma do Encontro

- 10 min — Revisão rápida do material e do terreno do Encontro 1.
- 20 min — Fundamentação: Nanite (geometria virtualizada), Lumen (iluminação global dinâmica) e o pipeline de Packaging.
- 30 min — Demonstração: ativação e ajuste de Nanite/Lumen no nível de teste, e passo a passo guiado de Packaging.
- 45 min — Laboratório: cada grupo ativa Nanite/Lumen no próprio nível e inicia o packaging do seu build.
- 30 min — Checkpoint + Showcase: cada grupo executa seu build empacotado e demonstra o BP_Player controlável dentro dele; preenchimento do Modelo de Avaliação de Checkpoint (Rubrica 3).

## Desenvolvimento

O encontro retoma o nível de teste já materializado (material + Landscape) e o eleva a um padrão de renderização moderno, ativando Lumen para iluminação global dinâmica e verificando o comportamento de Nanite sobre a geometria do nível. O professor demonstra o processo completo de Packaging — da configuração de plataforma-alvo até a geração do executável — usando o próprio projeto de demonstração como exemplo, para que a turma veja o pipeline inteiro antes de replicá-lo. Cada grupo então ativa Nanite/Lumen no próprio nível e conduz o packaging do seu projeto, encerrando o encontro (e a Unidade I) com a execução do build fora do Editor: o BP_Player, construído na Semana 1 e conectado a Enhanced Input na Semana 2, deve se mover dentro desse executável.

## Desafio

Não há desafio de liberdade de solução neste encontro. O instrumento avaliativo do encontro é o Checkpoint de encerramento do Módulo 1, não um desafio técnico de solução aberta — a prioridade é a existência de um build funcional, não uma decisão técnica autônoma.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir um build executável do Vertical Slice, gerado fora do Editor, com Nanite e Lumen ativos no nível de teste e o BP_Player controlável dentro do executável por meio do esquema de Enhanced Input configurado na Semana 2.

## Evidências para Avaliação

Execução bem-sucedida do build de cada grupo durante o Showcase, avaliada pelo Modelo de Avaliação de Checkpoint (Rubrica 3 — Checkpoints), com registro de eventuais bloqueios técnicos identificados; organização geral do nível conforme PROJECT_ARCHITECTURE.md (Rubrica 1 — Desenvolvimento Semanal, critério Execução).

## Dificuldades Esperadas

Erros de packaging (referências quebradas, plataforma-alvo mal configurada, tempo de build maior que o previsto) são o risco mais provável do encontro. Intervenção: professor deve ter testado o próprio passo a passo de Packaging na mesma versão de engine antes da aula; iniciar o packaging de cada grupo o mais cedo possível no laboratório, para que builds mais lentos não comprometam o tempo do Checkpoint; grupos que não concluírem o build a tempo devem apresentar o estado do Editor (nível com Nanite/Lumen ativos) no Showcase, com o build finalizado como pendência registrada no Modelo de Avaliação de Checkpoint, sem que isso implique reabertura do módulo seguinte.

---

# Resultado Esperado da Semana

Ao final da Semana 3, cada estudante/grupo deve possuir: um primeiro build executável do Vertical Slice, gerado via Packaging, contendo o nível de teste com material simples, terreno via Landscape, Nanite e Lumen ativos, e o BP_Player funcional (Character + Enhanced Input) dentro desse executável. Conceitualmente, a turma deve dominar o Material Graph como shader nodal universal, a distinção entre Material e Landscape, os problemas universais de complexidade geométrica e iluminação indireta resolvidos por Nanite e Lumen, e o papel do Packaging como etapa que transforma projeto em produto. Esta é a entrega de encerramento do Módulo 1 e da Unidade I — Aprender a Ferramenta.

# Preparação para a Próxima Semana

A Semana 4 abre a Unidade II — Construir Sistemas — e depende do nível de teste e do build consolidados nesta semana como base estável sobre a qual o framework de jogo será construído: GameMode (regras da partida), GameState (estado compartilhado), PlayerController (ponte entre jogador e Pawn) e GameInstance (persistência entre níveis) passam a organizar, por trás do que já é visível, um jogo que até aqui era apenas um protótipo navegável. A distinção entre conceito universal e implementação específica, já exercitada com Enhanced Input e agora com Nanite/Lumen, será retomada ao comparar GameMode/GameState com a ausência de um equivalente direto na Unity (padrão de Managers/Singletons).

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Unreal Engine Materials. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Nanite Virtualized Geometry. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Lumen Global Illumination and Reflections. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Packaging Your Project. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Materiais, Landscape, Nanite e Lumen. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Shader Graph, Terrain e Build Settings, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Nanite, Lumen e Packaging; **PrismaticaDev**, para material e Landscape.
