# Plano de Ensino

## Identificação da disciplina

**Disciplina:** Tendências de Motores de Jogos
**Código da Unidade Curricular:** IN46A
**Curso:** Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** Instituto Federal de Mato Grosso do Sul (IFMS) — Campus Dourados
**Período letivo:** Último semestre do curso
**Carga Horária Semanal:** 6 h/a (4h30)
**Carga Horária Semestral:** 102 h/a (76h)
**Organização didática:** 17 semanas, 2 encontros semanais de 2h15
**Motor de referência:** Unreal Engine 5.6
**Pré-requisitos:** Programação, Game Design, Unity, Inteligência Artificial, Computação Gráfica e Projeto Integrador

## Ementa

- Análise e comparação dos diversos motores de jogos presentes na indústria de jogos digitais;
- Desenvolvimento de jogos utilizando um motor;
- Comparando recursos em diferentes motores de jogos e transição entre motores de jogo.

## Objetivo Geral

Desenvolver no estudante a capacidade de compreender a arquitetura de motores de jogos modernos e de transferir esse conhecimento para a aprendizagem autônoma de novos motores, utilizando a Unreal Engine 5.6 como estudo de caso privilegiado e não como fim em si mesma.

## Objetivos Específicos

- Compreender os conceitos universais que estruturam motores de jogos modernos (arquitetura de editor, gameplay framework, sistemas de animação, inteligência artificial, interface e otimização).
- Identificar como esses conceitos universais se manifestam concretamente na Unreal Engine 5.6.
- Estabelecer comparações sistemáticas entre a Unreal Engine e a Unity, e, quando pertinente, com Godot, O3DE, Stride e CryEngine.
- Desenvolver um Vertical Slice de forma incremental ao longo do semestre, integrando progressivamente novos sistemas sem descartar o que já foi construído.
- Justificar tecnicamente decisões arquiteturais de projeto a partir de critérios de boas práticas da indústria.
- Analisar projetos profissionais de referência (Lyra, Stack O Bot, Action RPG, Content Examples) como forma de engenharia reversa e consolidação de autonomia.
- Consultar de forma crítica e autônoma a documentação oficial de diferentes motores.

## Competências Desenvolvidas

- Leitura e compreensão de arquitetura de motores de jogos.
- Autonomia para aprendizagem de novos motores e ferramentas.
- Pensamento comparativo e transferência de conceitos entre plataformas distintas.
- Capacidade de propor e justificar soluções técnicas diante de problemas de desenvolvimento.
- Organização técnica de projeto e disciplina de versionamento e documentação.
- Comunicação técnica por meio de apresentações, code review e playtests.
- Postura profissional equivalente à de um pequeno estúdio de desenvolvimento.

## Metodologias de Ensino

A disciplina é predominantemente prática, com teoria reduzida ao mínimo necessário para embasar a construção. A progressão metodológica acompanha o aumento gradual de autonomia do estudante ao longo do semestre:

- **Scaffolded Learning** (Módulo 1): o professor demonstra e o estudante replica, em um projeto totalmente guiado.
- **Studio Based Learning** (Módulos 2 e 4): o professor demonstra conceitos e propõe pequenos desafios (Módulo 2) ou atua como diretor técnico conduzindo feedback contínuo, code review e playtests (Módulo 4).
- **Challenge Based Learning** (Módulo 3): o professor apresenta problemas e os estudantes propõem soluções com maior autonomia.
- **Reverse Engineering** (Módulo 5): os estudantes analisam projetos profissionais e discutem arquitetura de forma comparativa entre motores, com autonomia plena.

Cada encontro segue o ciclo conceito → demonstração → construção → desafio → revisão, sem inversão dessa ordem. Toda aula busca responder quatro perguntas: qual conceito universal está sendo ensinado, como ele é implementado na Unreal, como seria implementado na Unity e como esse conhecimento pode ser transferido para outro motor.

## Organização da Disciplina

A disciplina é organizada em cinco módulos, articulados em torno do desenvolvimento contínuo de um único Vertical Slice. Nenhum conteúdo é descartado de um módulo para o outro; cada módulo amplia o projeto anterior.

### Módulo 1 — Aprender a Ferramenta

**Objetivo pedagógico:** apresentar a arquitetura da Unreal Engine e familiarizar o estudante com o editor, compreendendo os conceitos universais de motor por trás da ferramenta.

**Competências desenvolvidas:** leitura do editor, compreensão da relação entre Actors, Components e Blueprints, e reconhecimento de conceitos de renderização moderna.

**Principais sistemas explorados:** Editor, Viewport, Content Browser, Actors, Components, Character e Character Movement, Enhanced Input, Blueprint, Materiais, Landscape, Lumen e Nanite.

**Produto esperado:** primeiro protótipo executável (build) explorável.

**Metodologia predominante:** Scaffolded Learning, com autonomia muito baixa.

### Módulo 2 — Construir Sistemas

**Objetivo pedagógico:** introduzir o gameplay framework da Unreal e consolidar a construção de sistemas fundamentais de jogabilidade.

**Competências desenvolvidas:** compreensão do fluxo de controle de um jogo (GameMode, GameState, PlayerController, GameInstance) e uso de comunicação entre sistemas via interfaces e eventos.

**Principais sistemas explorados:** GameMode, GameState, PlayerController, GameInstance, Blueprint Interfaces, Event Dispatchers, Actor Components, Data Assets, Data Tables, Structs, Enums e SaveGame.

**Produto esperado:** gameplay funcional, com desafios aplicados de portas, baús, alavancas, NPCs e checkpoints integrados ao projeto único.

**Metodologia predominante:** Studio Based Learning, com autonomia baixa.

### Módulo 3 — Resolver Problemas

**Objetivo pedagógico:** desenvolver a capacidade de propor soluções técnicas diante de problemas de jogabilidade, ampliando a autonomia do estudante.

**Competências desenvolvidas:** integração de sistemas de animação, interface e inteligência artificial na resolução de problemas de design.

**Principais sistemas explorados:** Animation Blueprint, Blend Spaces, Montages, UMG, HUD, Inventory, Interaction, Navigation, Behavior Trees e Blackboards.

**Produto esperado:** Vertical Slice jogável, com sistemas de animação, interface e IA integrados.

**Metodologia predominante:** Challenge Based Learning, com autonomia média.

### Módulo 4 — Produzir como um Pequeno Estúdio

**Objetivo pedagógico:** consolidar práticas de produção, otimização e finalização de projeto sob a perspectiva de um pequeno estúdio de desenvolvimento.

**Competências desenvolvidas:** polimento técnico e visual, otimização de desempenho, empacotamento e organização de projeto conforme boas práticas de produção.

**Principais sistemas explorados:** Materials, Material Instances, Foliage, Áudio, Optimization, Profiling e Packaging.

**Produto esperado:** Vertical Slice final, otimizado e empacotado como build distribuível.

**Metodologia predominante:** Studio Based Learning, com o professor atuando como diretor técnico, autonomia alta, feedback contínuo, code review e playtests.

### Módulo 5 — Comparar Arquiteturas e Aprender Novos Motores

**Objetivo pedagógico:** consolidar a autonomia do estudante por meio da análise de projetos profissionais e da comparação explícita entre arquiteturas de diferentes motores.

**Competências desenvolvidas:** leitura crítica de projetos de referência, argumentação técnica comparativa e transferência de conhecimento entre motores.

**Principais sistemas explorados:** estudo de casos profissionais (Lyra, Stack O Bot, Action RPG Sample, Content Examples) e comparação arquitetural com Unity, Godot, O3DE, Stride e CryEngine.

**Produto esperado:** apresentação técnica final do projeto, incluindo justificativa de decisões arquiteturais e comparação entre motores.

**Metodologia predominante:** Reverse Engineering, com autonomia muito alta.

## Estratégias de Ensino-Aprendizagem

- Cada encontro é estruturado no ciclo introdução, demonstração, desenvolvimento e feedback, nunca de forma exclusivamente expositiva.
- Todo novo conteúdo reutiliza sistemas desenvolvidos em módulos anteriores, evitando exercícios isolados: todo exercício pertence ao Vertical Slice único da disciplina.
- Todo conceito é apresentado antes de sua implementação, primeiro em sua forma universal e, em seguida, discutido em sua realização na Unreal Engine, com comparação sistemática à Unity e, quando pertinente, a Godot, O3DE, Stride ou CryEngine.
- A quantidade de orientação docente diminui progressivamente ao longo do semestre, acompanhando a evolução de Scaffolded Learning para Reverse Engineering.
- Estimula-se constantemente a consulta autônoma à documentação oficial, sem reprodução de trechos extensos, priorizando resumo e reinterpretação didática do conteúdo.
- Ao final de cada módulo, é produzido um artefato funcional e jogável, consolidando o aprendizado do período.

## Recursos Didáticos

- Unreal Engine 5.6 (editor, projetos de exemplo e samples oficiais).
- Projetos de referência oficiais: Lyra Starter Game, Stack O Bot, Content Examples e Action RPG Sample.
- Kenney Assets (kenney.nl): biblioteca de assets 2D e 3D sob licença CC0, utilizada para prototipagem rápida e composição do Vertical Slice sem dependência de ativos pagos.
- Documentação oficial da Epic Games, Unreal Engine Learning Library e Unreal Community Wiki.
- Documentação oficial da Unity (Unity Manual e Unity Learn), para fins comparativos.
- Ambiente de laboratório de desenvolvimento com estações equipadas para produção em Unreal Engine.
- Ferramentas de versionamento e organização de projeto para acompanhamento do desenvolvimento incremental do Vertical Slice.
- Ferramentas de apresentação e registro para code review, playtests e apresentações técnicas.

## Avaliação da Aprendizagem

A disciplina não utiliza prova tradicional. A avaliação é processual e coerente com as metodologias ativas adotadas, privilegiando:

- o desenvolvimento incremental do Vertical Slice ao longo do semestre;
- a resolução de desafios propostos em cada módulo;
- a participação ativa em laboratório;
- o funcionamento efetivo do projeto em cada entrega;
- a organização técnica do projeto (estrutura, nomenclatura, versionamento);
- a aplicação correta e justificada dos recursos da Unreal Engine explorados em cada módulo;
- a capacidade de justificar decisões arquiteturais tomadas durante o desenvolvimento;
- apresentações técnicas, com destaque para a apresentação final do Módulo 5;
- sessões de code review, avaliando qualidade e clareza da implementação;
- playtests, avaliando jogabilidade e experiência do usuário.

A ponderação entre esses critérios deve refletir a progressão de autonomia da disciplina, atribuindo peso crescente à capacidade de justificativa técnica e de comparação arquitetural nos módulos finais.

## Bibliografia Básica

Bibliografia oficial conforme o Projeto Pedagógico do Curso Superior de Tecnologia em Jogos Digitais (IFMS, Campus Dourados):

- CONCI, Aura; VASCONCELOS, Cristina Nader; AZEVEDO, Eduardo. **Computação gráfica: teoria e prática: geração de imagens**. 2. ed. Rio de Janeiro: Elsevier, 2018. 335 p. ISBN 9788535287790.
- AKENINE-MÖLLER, Tomas et al. **Real-time rendering**. 4. ed. Boca Raton, FL: CRC Press, 2016. xiv, 1178 p. ISBN 9781138627000.
- CONCI, Aura; AZEVEDO, Eduardo; LETA, Fabiana R. **Computação gráfica: volume 2**. Rio de Janeiro: Elsevier, 2008. 407 p. ISBN 9788535223293.

## Bibliografia Complementar

- ROGERS, Scott; LUZ, Alan Richard da. **Level up: um guia para o design de grandes jogos**. São Paulo: Blucher, 2012. 494 p. ISBN 9788521207009.
- SALEN, Katie; ZIMMERMAN, Eric. **Regras do jogo: fundamentos do design de jogos: principais conceitos: volume 1**. São Paulo: Blucher, 2012. 167 p. ISBN 9788521206262.
- SALEN, Katie; ZIMMERMAN, Eric. **Regras do jogo: fundamentos do design de jogos: regras: volume 2**. São Paulo: Blucher, 2012. 229 p. ISBN 9788521206279.
- SALEN, Katie; ZIMMERMAN, Eric. **Regras do jogo: fundamentos do design de jogos: interação lúdica: volume 3**. São Paulo: Blucher, 2012. 258 p. ISBN 9788521206286.
- SALEN, Katie; ZIMMERMAN, Eric. **Regras do jogo: fundamentos do design de jogos: cultura: volume 4**. São Paulo: Blucher, 2012. 153 p. ISBN 9788521206293.

## Referências Técnicas Complementares (Unreal Engine e Unity)

As obras acima constituem a bibliografia oficial do PPC. Para fins de apoio prático ao desenvolvimento em Unreal Engine 5.6 e à comparação entre motores, a disciplina utiliza ainda as seguintes fontes de consulta técnica, não substitutas da bibliografia oficial:

- EPIC GAMES. **Unreal Engine 5 Documentation**. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library**. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- EPIC GAMES. **Samples and Tutorials**. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/samples-and-tutorials.
- UNITY TECHNOLOGIES. **Unity Manual**. Disponível em: https://docs.unity3d.com/Manual/.
- UNITY TECHNOLOGIES. **Unity Learn**. Disponível em: https://learn.unity.com/.
- GODOT ENGINE. **Godot Documentation**. Disponível em: https://docs.godotengine.org/.
- Unreal Community Wiki. Disponível em: https://unrealcommunity.wiki/.
- LOOMAN, Tom. Disponível em: https://www.tomlooman.com/.
- BenUI. Disponível em: https://benui.ca/.
- GDC Vault. Disponível em: https://gdcvault.com/.
