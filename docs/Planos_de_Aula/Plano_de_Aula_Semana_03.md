# Semana 3 — Materiais, Terrain3D, SDFGI/VoxelGI e Exportação

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade I — Aprender a Ferramenta** (Semanas 1–3) | **Metodologia:** Scaffolded Learning — professor demonstra, aluno replica. Autonomia muito baixa.

## Introdução da Semana

Nas Semanas 1 e 2 a turma construiu a Scene do nível de teste do Vertical Slice (*O Templo Esquecido*) e um Player (CharacterBody3D) controlável através de um Input Map próprio. Esta semana fecha o Módulo 1 respondendo a uma última pergunta antes do primeiro build executável: como uma engine renderiza um mundo jogável e como esse mundo é empacotado para rodar fora do editor? Essa pergunta se resolve em três frentes que nenhuma engine moderna escapa — materiais, iluminação global e exportação — e que, juntas, transformam a Scene explorável em algo que pode ser jogado como um executável independente.

Nada do que foi construído nas Semanas 1 e 2 é refeito: o Player e a Scene existentes recebem terreno, material e iluminação, e o mesmo projeto é exportado ao final da semana.

## Objetivos Gerais

- Compreender o papel dos materiais e do addon Terrain3D na composição visual de um nível.
- Compreender iluminação global dinâmica (SDFGI/VoxelGI) como conceito universal de renderização moderna.
- Gerar o primeiro build exportado do Vertical Slice.

## Resultados Esperados

Ao final da semana, cada estudante possui um nível de teste com terreno e material básicos, iluminação global ativa, e um build exportado e executável fora do editor — encerrando o Módulo 1 com o Checkpoint de primeiro build jogável.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar o Material Graph como implementação nodal de um shader.
- Explicar o papel do addon Terrain3D como ferramenta de terreno sem equivalente nativo no Godot.
- Criar um material simples e modelar um terreno básico para o nível do Vertical Slice.

## Conteúdos

- Materiais no Godot (StandardMaterial3D) e o conceito de Material Graph.
- Terrain3D como addon de terreno.
- Aplicação guiada de material e terreno ao nível de teste já existente.

## Conceitos Fundamentais

Toda engine 3D precisa resolver dois problemas de composição visual do mundo: como definir a aparência de uma superfície (material) e como modelar grandes extensões de terreno sem esculpir manualmente cada polígono. O primeiro problema é resolvido por um grafo de material — uma representação nodal de um shader que combina texturas, cores e parâmetros sem exigir código de shader direto. O segundo é resolvido por ferramentas dedicadas de escultura de terreno, que não fazem parte do núcleo de toda engine: o Godot não possui uma solução nativa equivalente, o que motiva o uso do addon Terrain3D nesta disciplina.

## Recursos do Godot

StandardMaterial3D, Material Graph, Terrain3D (addon), Orchestrator.

## Comparação com Unity

Na Unity, o material é resolvido pelo Shader Graph (para materiais customizados) ou pelos materiais padrão do Standard Shader/URP, com filosofia nodal semelhante ao Material Graph do Godot. Para terreno, porém, a Unity possui um sistema de Terrain nativo integrado ao editor, enquanto o Godot depende de um addon de terceiros (Terrain3D) para o mesmo papel — uma diferença arquitetural relevante que deve ficar explícita para a turma, e não apenas mencionada de passagem.

## Preparação do Professor

- Projeto do Vertical Slice (retomado da Semana 2) com o Player e o nível de teste configurados.
- Addon Terrain3D já instalado no projeto de demonstração.
- Um material de referência já configurado (StandardMaterial3D com textura simples) para demonstração do Material Graph.
- Slides com o comparativo Material Graph/Terrain3D × Shader Graph/Terrain nativo da Unity.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 2 (Player controlável com Input Map) |
| 20 min | Introdução: como uma engine resolve aparência de superfície e modelagem de terreno |
| 35 min | Demonstração: criação de um StandardMaterial3D e escultura básica de terreno com Terrain3D |
| 45 min | Laboratório: cada estudante aplica material e modela um terreno próprio no nível de teste |
| 15 min | Desafio: variar ao menos um parâmetro do material (rugosidade, cor, textura) além do demonstrado |
| 5 min | Feedback e fechamento |

## Desenvolvimento

O encontro retoma o nível de teste das Semanas 1 e 2 e adiciona duas camadas de composição visual: um material aplicado às superfícies existentes e um terreno esculpido com o addon Terrain3D. O professor demonstra a criação de um StandardMaterial3D simples e a escultura de uma área de terreno com Terrain3D, explicando por que o segundo depende de um addon e não de um recurso nativo. A turma replica ambas as etapas no próprio projeto, preparando o nível para receber iluminação global no Encontro 2.

## Desafio

Cada estudante ajusta ao menos um parâmetro do material aplicado (cor, rugosidade/roughness ou textura) de forma diferente da demonstração, justificando brevemente a escolha em relação à identidade visual do próprio nível.

## Critérios de Sucesso

Cada estudante possui, ao final do encontro, um nível de teste com terreno modelado via Terrain3D e ao menos um material aplicado, sem substituir o Player ou a Scene já existentes.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro. O material e o terreno construídos aqui compõem o Checkpoint de encerramento do Módulo 1, avaliado no Encontro 2 desta mesma semana (Rubrica 3 — Checkpoints).

## Dificuldades Esperadas

- Confundir a escultura de terreno do Terrain3D com a movimentação normal de Nodes na Scene — reforçar que o Terrain3D opera com ferramentas de pincel próprias, diferentes da manipulação padrão do editor.
- Aplicar material apenas a parte das superfícies do nível, deixando elementos sem material — orientar verificação visual completa antes de encerrar a etapa.
- Parâmetros de material extremos (rugosidade ou brilho fora de faixas realistas) que prejudicam a leitura visual do terreno na iluminação padrão do editor — orientar comparação com a referência demonstrada antes de fechar a etapa.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar iluminação global dinâmica (SDFGI/VoxelGI) como conceito universal de renderização moderna.
- Discutir a ausência de geometria virtualizada no Godot como ponto de comparação arquitetural.
- Explicar o pipeline de exportação e gerar o primeiro build executável do Vertical Slice.

## Conteúdos

- SDFGI e VoxelGI como soluções de iluminação global em tempo real.
- Geometria virtualizada (Nanite, na Unreal) como conceito ausente no Godot — discussão comparativa, sem implementação.
- Pipeline de exportação de projetos no Godot (Export Templates).

## Conceitos Fundamentais

Depois que um nível possui material e terreno, falta resolver como a luz se propaga entre as superfícies de forma crível e em tempo real — problema que toda engine moderna precisa endereçar de alguma forma, sob pena de produzir cenas com sombras e reflexos artificiais. O Godot resolve isso com SDFGI (iluminação global baseada em campos de distância com sinal) ou VoxelGI (iluminação global baseada em voxels), duas abordagens alternativas ao mesmo problema. Paralelamente, a etapa final de qualquer projeto de engine é seu empacotamento: transformar um projeto editável em um executável distribuível, processo chamado de exportação.

## Recursos do Godot

SDFGI, VoxelGI, Exportação de projeto (Export Templates), Terrain3D, StandardMaterial3D.

## Comparação com Unity

A Unity resolve iluminação global com o Global Illumination do pipeline URP/HDRP (incluindo soluções em tempo real e pré-calculadas via Lightmapping), com filosofia equivalente à do SDFGI/VoxelGI do Godot — ambas as engines oferecem alternativas para equilibrar qualidade e desempenho. Já para geometria virtualizada — a renderização de malhas extremamente detalhadas sem custo proporcional de desempenho, como o Nanite da Unreal Engine — nem Godot nem Unity possuem equivalente nativo direto; essa ausência compartilhada deve ser discutida como um limite comum das duas engines, não uma desvantagem exclusiva do Godot. Quanto à exportação, ambas as engines dependem de um processo de build baseado em templates/plataformas de destino, com fluxo conceitualmente semelhante.

## Preparação do Professor

- Projeto de demonstração com material e terreno do Encontro 1 já configurados.
- SDFGI ou VoxelGI ativado em uma Scene de referência para demonstração comparativa.
- Export Templates da versão do Godot em uso já instalados na máquina de demonstração e nas máquinas do laboratório.
- Slides com o comparativo SDFGI/VoxelGI × Global Illumination da Unity, e a discussão sobre ausência de geometria virtualizada (Nanite) em ambas.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 10 min | Revisão do Encontro 1 (nível com terreno e material) |
| 20 min | Introdução: iluminação global em tempo real e o problema da geometria virtualizada |
| 25 min | Demonstração: ativação de SDFGI/VoxelGI no nível e ajuste de parâmetros básicos |
| 20 min | Demonstração: pipeline de exportação e geração de um build de referência |
| 40 min | Laboratório: cada estudante ativa iluminação global no próprio nível e exporta seu primeiro build |
| 30 min | Checkpoint de encerramento do Módulo 1: showcase dos builds exportados |
| 10 min | Feedback e fechamento |

## Desenvolvimento

O encontro completa o nível de teste com iluminação global (SDFGI ou VoxelGI) e conduz a turma pelo pipeline de exportação do Godot, produzindo o primeiro build executável do Vertical Slice. O professor demonstra a ativação e o ajuste básico da iluminação global no nível já construído, discute a ausência de geometria virtualizada como limite compartilhado entre Godot e Unity, e em seguida demonstra o processo de exportação de ponta a ponta. A turma replica ambas as etapas, encerrando o encontro com um build próprio, testado fora do editor, que é apresentado no Showcase de fechamento do Módulo 1.

## Desafio

Não há desafio de implementação livre neste encontro — o próprio Checkpoint (build exportado e funcional) é o entregável de encerramento do módulo, já sem grau adicional de liberdade além do necessário para rodar fora do editor.

## Critérios de Sucesso

Cada estudante possui, ao final da semana, um nível de teste com terreno, material e iluminação global ativa, exportado como build executável que roda fora do editor sem falhas críticas, contendo o Player controlável construído nas Semanas 1 e 2.

## Evidências para Avaliação

**Checkpoint de encerramento do Módulo 1** (Rubrica 3 — Checkpoints): avalia progresso esperado, funcionalidades implementadas, qualidade técnica e estabilidade do build exportado. **Showcase** (Rubrica 6 — Apresentações): avalia comunicação e demonstração ao vivo do build por cada estudante/grupo.

## Dificuldades Esperadas

- Export Templates não instalados ou desatualizados na máquina do estudante, impedindo a exportação — verificar a instalação no início do laboratório, antes de iniciar a demonstração.
- SDFGI/VoxelGI ativado sem ajuste, produzindo iluminação visualmente incorreta (excesso de brilho ou escuridão) — reforçar que os parâmetros padrão raramente são o ajuste final.
- Build que roda no editor mas falha ao ser exportado (erros de dependência de assets ou configuração de exportação incompleta) — reservar tempo do laboratório para testar o executável fora do editor antes do Showcase, não apenas a versão do editor.

---

# Resultado Esperado da Semana

Ao final da Semana 3, cada estudante possui um nível de teste completo — Player controlável (Semanas 1–2), terreno e material (Encontro 1) e iluminação global ativa (Encontro 2) — exportado como o primeiro build executável do Vertical Slice, rodando de forma estável fora do editor. A turma domina a distinção entre composição visual estática (material, terreno) e renderização dinâmica (iluminação global), relaciona ambas aos equivalentes na Unity (Shader Graph/Terrain nativo e Global Illumination de URP/HDRP), reconhece a ausência de geometria virtualizada como limite compartilhado entre as duas engines, e compreende o pipeline de exportação como etapa final e obrigatória de qualquer projeto de engine. Este encontro encerra a Unidade I — Aprender a Ferramenta.

# Preparação para a Próxima Semana

O nível de teste e o Player exportados nesta semana são a base direta da Semana 4, que abre o Módulo 2 (Construir Sistemas) com a criação do `GameManager` e do `SaveManager` via Autoload/Singleton — os primeiros sistemas de gameplay propriamente ditos do Vertical Slice, construídos sobre o mesmo projeto, sem refazer nada do Módulo 1.

# Referências

- Godot Documentation — Standard Material 3D: https://docs.godotengine.org/en/stable/tutorials/3d/standard_material_3d.html
- Godot Documentation — Global Illumination (SDFGI/VoxelGI): https://docs.godotengine.org/en/stable/tutorials/3d/global_illumination/index.html
- Godot Documentation — Exporting Projects: https://docs.godotengine.org/en/stable/tutorials/export/index.html
- Terrain3D (addon) — Repositório oficial: https://github.com/TokisanGames/Terrain3D
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — Terrain: https://docs.unity3d.com/Manual/script-Terrain.html
- Unity Manual (consulta comparativa) — Global Illumination: https://docs.unity3d.com/Manual/realtime-gi-using-enlighten.html
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
