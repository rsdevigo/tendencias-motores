# Semana 12 — Materials, Material Overrides e Foliage (MultiMeshInstance3D)

**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** IFMS — Campus Dourados
**Unidade IV — Produzir como um Pequeno Estúdio** (Semanas 12–14) | **Metodologia:** Studio Based Learning — professor atua como diretor técnico. Muito laboratório, feedback contínuo, playtests, code reviews. Autonomia alta.
**Code Review (🔵)** — esta semana aplica a Rubrica 4 (Code Review) sobre materiais e composição de cena, mas não fecha a Unidade IV (encerramento apenas na Semana 14).

## Introdução da Semana

A Semana 11 encerrou a Unidade III com o Vertical Slice jogável completo: animação, HUD, inventário, interação ampliada, IA (Navigation + Behavior Tree/Blackboard via LimboAI) e combate simples integrados em um único fluxo, avaliado em Playtest coletivo e Showcase. A partir da Semana 12, a disciplina muda de pergunta: não "que sistema falta?", mas "como transformar um protótipo funcional em um produto entregável?". Nenhum sistema novo de gameplay é introduzido no Módulo 4 — o professor passa a atuar como diretor técnico, e o foco é polimento técnico e produção em escala de estúdio. A Semana 12 abre esse módulo com o nível visual do projeto: refatorar os materiais já existentes (aplicados desde a Semana 3) em Material Overrides parametrizados, e compor a densidade visual da zona externa com MultiMeshInstance3D (Foliage). Nenhuma geometria, mecânica ou sistema de gameplay é alterado nesta semana — apenas a camada de apresentação visual do mesmo Vertical Slice que já roda de ponta a ponta desde a Semana 11.

## Objetivos Gerais

- Compreender Material Override/Unique Material como estratégia universal de parametrização e otimização visual, distinta de criar um material base novo para cada objeto.
- Compreender MultiMeshInstance3D como ferramenta de composição de cena em escala — densidade, performance e composição visual de elementos repetidos.
- Refatorar os materiais já existentes no projeto para uma estrutura parametrizada e reutilizável, sem duplicar materiais base.
- Compor a densidade visual da zona externa do Vertical Slice com MultiMeshInstance3D, sem comprometer a performance do projeto.
- Passar pelo Code Review de materiais e composição de cena (Rubrica 4), justificando as decisões de parametrização e otimização adotadas.

## Resultados Esperados

Ao final da semana, cada grupo possui os materiais do próprio Vertical Slice reorganizados em uma estrutura de material base + Material Overrides parametrizados (sem duplicação de recursos de material), e a zona externa do projeto com elementos de vegetação/cena compostos via MultiMeshInstance3D, mantendo desempenho estável — o conjunto avaliado em Code Review de materiais e composição de cena.

---

# Encontro 1

## Objetivos de Aprendizagem

- Explicar a diferença entre material base e Material Override/Unique Material como estratégia de parametrização.
- Identificar, no próprio projeto, quais materiais existentes deveriam ser um único material base parametrizado em vez de múltiplos materiais duplicados.
- Refatorar ao menos um conjunto de objetos do projeto para usar um material base com Overrides parametrizados por instância.

## Conteúdos

- O problema da duplicação de materiais: por que criar um `StandardMaterial3D` novo para cada variação de cor/textura de um mesmo tipo de objeto é uma prática que não escala em um projeto de estúdio.
- Material base como definição compartilhada e Material Override/Unique Material como parametrização por instância, sem duplicar o recurso de material inteiro.
- Auditoria guiada dos materiais já existentes no Vertical Slice (criados desde a Semana 3) para identificar candidatos a refatoração.
- Refatoração guiada de um conjunto de objetos do projeto (ex.: variações de cor de um mesmo tipo de Pickup ou elemento de cenário) para material base + Overrides.

## Conceitos Fundamentais

Todo projeto de produção em escala enfrenta o mesmo problema estrutural: múltiplas instâncias de um mesmo tipo de objeto precisam de pequenas variações visuais (cor, brilho, textura), mas recriar um material completo para cada variação multiplica o custo de manutenção e de memória sem necessidade. O Godot resolve isso com a distinção entre material base (compartilhado entre instâncias) e Material Override/Unique Material (uma cópia parametrizada aplicada a uma instância específica, sem duplicar a definição inteira do material). Esse é o mesmo princípio de separação entre dado compartilhado e dado específico de instância já ensinado com Resources customizados na Semana 6 — agora aplicado ao domínio visual em vez de ao domínio de gameplay. Como o Módulo 4 tem autonomia alta e o professor atua como diretor técnico, a auditoria dos materiais existentes é conduzida como revisão crítica do próprio trabalho acumulado desde a Semana 3, não como um novo tutorial de materiais do zero.

## Recursos do Godot

`StandardMaterial3D`, Material Override, Unique Material (menu de contexto do MeshInstance3D no editor).

## Comparação com Unity

A Unity resolve o mesmo problema com Material Property Blocks e Material Instances: um material base compartilhado entre múltiplos `Renderer`s, com valores específicos de instância aplicados via `MaterialPropertyBlock` sem duplicar o asset de material inteiro. O princípio universal é idêntico nas duas engines: separar a definição compartilhada da parametrização por instância evita tanto a duplicação de recursos em disco/memória quanto a perda de sincronização quando o material base precisa ser ajustado globalmente. A diferença está no fluxo de configuração — no Godot o Override é aplicado diretamente no `MeshInstance3D` pelo editor; na Unity, historicamente, o desenvolvedor decide entre duplicar o asset de Material ou usar `MaterialPropertyBlock` via código — não há equivalente de "Override" nativo do editor tão direto quanto o do Godot.

## Preparação do Professor

- Projeto do Vertical Slice retomado da Semana 11, com Vertical Slice jogável completo e estável.
- Levantamento prévio (feito pelo próprio professor) de quais materiais do projeto de referência são bons candidatos a Material Override, para orientar a auditoria em aula sem entregá-la pronta.
- Slides com o comparativo Material Override/Unique Material (Godot) × Material Instances/Material Property Blocks (Unity).
- Ficha de Code Review (Rubrica 4) do Sistema de Avaliação, para apresentar aos grupos ao final do Encontro 2 — não aplicada neste encontro.

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 2 da Semana 11 (Vertical Slice jogável completo, encerramento da Unidade III) |
| 20 min | Introdução: o problema da duplicação de materiais em um projeto de produção |
| 30 min | Demonstração: material base + Material Override/Unique Material aplicado a um conjunto de objetos |
| 50 min | Laboratório: cada grupo audita os próprios materiais e refatora ao menos um conjunto de objetos para material base + Overrides |
| 20 min | Feedback e fechamento |

## Desenvolvimento

O encontro parte do Vertical Slice já jogável desde a Semana 11, sem alterar nenhuma mecânica ou sistema de gameplay — a única mudança desta semana é na camada de apresentação visual. O professor demonstra primeiro o problema isoladamente (um conjunto de objetos com materiais duplicados desnecessariamente), antes de tocar no projeto real de cada grupo. Em seguida, demonstra a refatoração guiada de um material base com Override parametrizado por instância. Cada grupo audita os próprios materiais, acumulados desde a Semana 3, identifica onde há duplicação evitável e refatora ao menos um conjunto de objetos — como o módulo tem autonomia alta, o professor circula como diretor técnico, orientando decisões em vez de demonstrar cada caso individualmente.

## Desafio

Não há desafio de solução livre neste encontro: a refatoração de materiais é guiada e parte diretamente do material já existente em cada projeto, servindo de base à composição de cena do Encontro 2.

## Critérios de Sucesso

Cada grupo possui, ao final do encontro, ao menos um conjunto de objetos do próprio Vertical Slice reorganizado em material base + Material Override, sem duplicação de materiais equivalentes, e sem qualquer alteração perceptível no gameplay ou nas mecânicas já funcionais.

## Evidências para Avaliação

Sem instrumento formal isolado neste encontro (Rubrica 1 — Desenvolvimento Semanal, aplicada de forma contínua). A refatoração conduzida aqui é parte do Code Review de encerramento da semana (Encontro 2).

## Dificuldades Esperadas

- Confundir Material Override com a criação de um material completamente novo, duplicando a definição em vez de parametrizar uma cópia da instância — reforçar a diferença entre "novo material" e "override de instância".
- Refatorar materiais que já funcionavam corretamente sem necessidade real de parametrização, gastando tempo de laboratório em uma otimização de baixo impacto — reforçar que a auditoria deve priorizar os casos de duplicação real, não qualquer material do projeto.
- Alterar acidentalmente a aparência de objetos já validados em Playtests anteriores ao refatorar o material base compartilhado — reforçar a checagem visual comparativa antes/depois de cada refatoração.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar MultiMeshInstance3D como ferramenta de composição de cena em escala, distinta de instanciar múltiplas Scenes individuais.
- Compor elementos de vegetação/cena na zona externa do Vertical Slice usando MultiMeshInstance3D.
- Participar do Code Review de materiais e composição de cena, justificando as decisões de parametrização e otimização adotadas.

## Conteúdos

- MultiMeshInstance3D como solução de desempenho para grandes quantidades de instâncias de uma mesma malha (vegetação, rochas, elementos repetidos de cenário), equivalente à Foliage Tool.
- Diferença entre instanciar uma Scene por elemento (custo alto em escala) e usar MultiMeshInstance3D (uma única chamada de desenho para múltiplas instâncias).
- Composição guiada de vegetação/elementos de cena na zona externa do Vertical Slice (Kenney Nature Kit) usando MultiMeshInstance3D, com atenção à densidade e à performance.
- Code Review (Rubrica 4) sobre os materiais refatorados no Encontro 1 e a composição de cena deste encontro — organização, nomenclatura, modularidade e reutilização.

## Conceitos Fundamentais

O Encontro 1 resolveu a parametrização de um material por instância. O Encontro 2 resolve um problema adjacente, mas distinto: como compor uma cena com uma grande quantidade de elementos visuais repetidos (vegetação, rochas, detalhes de ambiente) sem que cada elemento seja uma Scene instanciada individualmente, o que rapidamente se torna custoso em desempenho. O `MultiMeshInstance3D` resolve isso agrupando múltiplas instâncias de uma mesma malha em uma única chamada de desenho, trocando flexibilidade individual por escala e performance — a mesma lógica por trás de qualquer Foliage Tool de qualquer engine. É importante que o grupo perceba que essa é uma ferramenta de composição de cena, não um sistema de gameplay: os elementos compostos com MultiMeshInstance3D não possuem lógica própria, apenas presença visual. O Code Review de encerramento da semana aplica a mesma Rubrica 4 já usada nas Semanas 7 e 10, mas com ênfase deslocada para arquitetura, consistência e boas práticas consolidadas, como já previsto na progressão de ênfase avaliativa do Sistema de Avaliação para os Módulos 4 e 5.

## Recursos do Godot

`MultiMeshInstance3D`, Kenney Nature Kit (assets de vegetação já disponíveis no projeto, conforme direção de arte definida em PROJECT_ARCHITECTURE.md).

## Comparação com Unity

A Unity resolve o mesmo problema de composição em escala com a Foliage Tool (parte do Terrain Tools) ou, de forma mais geral, com GPU Instancing sobre `Renderer`s compartilhando o mesmo material — o princípio universal é idêntico: agrupar instâncias repetidas de uma mesma malha em chamadas de desenho reduzidas, em vez de tratar cada elemento como um objeto individual completo. A diferença está no escopo da ferramenta — a Foliage Tool da Unity é pensada especificamente para pintura de vegetação sobre terreno, enquanto o `MultiMeshInstance3D` do Godot é uma ferramenta de propósito mais geral, aplicável a qualquer composição de instâncias repetidas, não apenas vegetação.

## Preparação do Professor

- Projetos de cada grupo com materiais refatorados do Encontro 1.
- Cena de exemplo com MultiMeshInstance3D configurado sobre um terreno de teste, preparada para demonstração, sem distribuir antes da aula.
- Assets do Kenney Nature Kit já disponíveis nos projetos (direção de arte definida em PROJECT_ARCHITECTURE.md), conferidos previamente quanto à compatibilidade com MultiMesh.
- Ficha de Code Review (Rubrica 4) do Sistema de Avaliação, impressa ou digital.
- Slides com o comparativo MultiMeshInstance3D (Godot) × Foliage Tool/GPU Instancing (Unity).

## Cronograma do Encontro (2h15)

| Duração | Atividade |
|---|---|
| 15 min | Revisão do Encontro 1 (materiais refatorados em base + Overrides) |
| 25 min | Demonstração: MultiMeshInstance3D configurado sobre um terreno de teste |
| 55 min | Laboratório: cada grupo compõe vegetação/elementos de cena na zona externa do próprio projeto usando MultiMeshInstance3D |
| 40 min | Code Review de materiais e composição de cena (Rubrica 4) |

## Desenvolvimento

O encontro abre com a demonstração guiada de um `MultiMeshInstance3D` configurado sobre um terreno de teste, cobrindo a diferença entre instanciar Scenes individuais e agrupar instâncias em uma única chamada de desenho. Cada grupo aplica essa ferramenta à própria zona externa do Vertical Slice, compondo vegetação e elementos de cena do Kenney Nature Kit já disponíveis no projeto, com atenção à densidade visual e ao impacto de performance — como diretor técnico, o professor orienta decisões de densidade e distribuição sem impor uma composição única para todos os grupos. O encontro fecha com o Code Review de materiais e composição de cena, em que cada grupo apresenta a refatoração de materiais do Encontro 1 e a composição de vegetação deste encontro, justificando as decisões de parametrização e otimização adotadas diante do professor.

## Desafio

Não há desafio de solução livre com liberdade ampla neste encontro: a composição de cena com MultiMeshInstance3D é guiada quanto à ferramenta, mas cada grupo decide livremente a distribuição, densidade e escolha de elementos de vegetação/cena para a própria zona externa, dentro do que já existe no Kenney Nature Kit do projeto. **Entrega: Code Review de materiais e composição de cena.**

## Critérios de Sucesso

Cada grupo possui, ao final da semana, os materiais do próprio Vertical Slice organizados em material base + Overrides parametrizados sem duplicação, a zona externa composta com elementos de vegetação/cena via MultiMeshInstance3D mantendo desempenho estável, e passou pelo Code Review justificando as decisões técnicas tomadas em ambos os encontros.

## Evidências para Avaliação

**Code Review** (Rubrica 4 do Sistema de Avaliação) — organização, nomenclatura, modularidade, reutilização, comunicação entre sistemas e boas práticas gerais aplicadas à refatoração de materiais e à composição de cena desta semana, mesmo instrumento já aplicado nas Semanas 7 e 10 e reaplicado na Semana 14.

## Dificuldades Esperadas

- Compor densidade de vegetação excessiva via MultiMeshInstance3D sem observar o impacto no desempenho, comprometendo a estabilidade já validada em Playtests anteriores — reforçar que densidade visual e performance são parte da mesma decisão, não etapas separadas.
- Tratar os elementos compostos com MultiMeshInstance3D como se pudessem ter lógica individual (colisão específica por instância, interação), confundindo uma ferramenta de composição visual com um sistema de gameplay — reforçar que MultiMeshInstance3D não substitui Scenes com lógica própria.
- Dificuldade em justificar tecnicamente, no Code Review, por que um material foi parametrizado com Override em vez de duplicado — reforçar a prática de perguntar "por que este caminho e não outro?", já consolidada desde os Desafios Técnicos de módulos anteriores.

---

# Resultado Esperado da Semana

Ao final da Semana 12, cada grupo possui o mesmo Vertical Slice jogável já validado na Semana 11 — sem qualquer alteração de mecânica ou sistema de gameplay —, agora com os materiais reorganizados em uma estrutura de material base + Material Overrides parametrizados, sem duplicação de recursos, e com a zona externa composta com elementos de vegetação/cena via MultiMeshInstance3D, mantendo desempenho estável. O grupo passou pelo Code Review de materiais e composição de cena, justificando tecnicamente as decisões de parametrização e otimização adotadas — consolidando a postura de diretor técnico do professor e de autonomia alta característica do Módulo 4.

# Preparação para a Próxima Semana

A Semana 13 dá continuidade ao polimento técnico do Módulo 4, integrando áudio a eventos de gameplay já existentes (interação, passos, ambiente) via AudioStreamPlayer, e introduzindo Profiling e Optimization como etapa obrigatória de produção antes da exportação final da Semana 14 — os materiais e a composição de cena refinados nesta semana serão parte direta do que o Profiler avaliará como possíveis gargalos técnicos.

# Referências

- Godot Documentation — Standard Material 3D: https://docs.godotengine.org/en/stable/tutorials/3d/standard_material_3d.html
- Orchestrator — Documentação oficial: https://orchestrator.cratercrash.space/
- Unity Manual (consulta comparativa) — Materials: https://docs.unity3d.com/Manual/Materials.html
- Kenney Assets (CC0): https://kenney.nl/
- Canais recomendados para consulta complementar (não substituem a documentação oficial): GDQuest (https://www.youtube.com/@GDQuest), Clear Code (https://www.youtube.com/@ClearCode)
