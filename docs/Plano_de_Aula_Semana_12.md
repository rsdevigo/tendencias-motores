# Semana 12 🔵

## Introdução da Semana

A Semana 12 abre a Unidade IV — Produzir como um Pequeno Estúdio, encerrando o eixo de resolução de problemas da Unidade III (Semanas 8–11) e iniciando uma metodologia nova: Studio Based Learning com autonomia alta, na qual o professor atua como diretor técnico em vez de propor desafios fechados. O eixo conceitual da semana é a padronização e a otimização da produção visual em escala de estúdio, resolvido na Unreal por dois recursos complementares — Material Instance (parametrização de materiais sem recompilar shaders) e Foliage Tool (composição de cena em massa com controle de performance). O Encontro 1 fundamenta Material Instance versus Material base e refatora os materiais já existentes no projeto (criados na Semana 1, cena de graybox) em instâncias parametrizadas; o Encontro 2 fundamenta a Foliage Tool e a utiliza para compor vegetação/elementos de cena no nível do Vertical Slice consolidado na Semana 11. A semana encerra com Code Review formal (Rubrica 4), com ênfase renovada em boas práticas de nomenclatura e organização de pastas, consistente com a virada de ênfase avaliativa do Sistema de Avaliação para os Módulos 4 e 5 (arquitetura, consistência e capacidade de explicar decisões). Nenhum sistema anterior é descartado: `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD` e `BP_Enemy` com Behavior Tree/Blackboard permanecem intactos — a semana refina a camada visual do mesmo Vertical Slice.

## Objetivos Gerais

- Compreender Material Instance como estratégia universal de parametrização e otimização de materiais em produção de jogos.
- Compreender a Foliage Tool como ferramenta de composição de cena em massa, com controle de densidade e performance.
- Refatorar os materiais existentes do projeto em Material Instances parametrizadas, sem alterar nenhum sistema de gameplay.
- Compor vegetação/elementos de cena no nível do Vertical Slice, elevando sua qualidade visual sem comprometer a jogabilidade construída até a Semana 11.

## Resultados Esperados

Ao final da semana, cada grupo terá seus materiais principais refatorados em Material Instances organizadas segundo o PROJECT_ARCHITECTURE.md (`Materials/Base/` e `Materials/Instances/`, prefixos `M_` e `MI_`), e um nível com composição de vegetação/elementos de cena via Foliage Tool, evidenciando ganho visual perceptível sobre o graybox original. O Code Review de encerramento (Rubrica 4) terá avaliado formalmente materiais e composição de cena.

---

# Encontro 1

## Objetivos de Aprendizagem

- Diferenciar Material base de Material Instance e explicar por que a parametrização evita recompilação de shader.
- Comparar Material Instance na Unreal com Material Property Blocks na Unity.
- Refatorar os materiais existentes do projeto em Material Instances parametrizadas.

## Conteúdos

- Material base como grafo de shader compilado, versus Material Instance como conjunto de valores paramétricos sobre esse grafo.
- Parâmetros de material (cor, textura, rugosidade, valores escalares) expostos para instanciação.
- Refatoração guiada de um material existente do projeto em Material base parametrizado + Material Instance.

## Conceitos Fundamentais

O conceito universal desta aula é a separação entre a estrutura de um material (o grafo de nós que define como a superfície reage à luz) e os valores que essa estrutura recebe (a cor, a textura, a rugosidade específicas de uma superfície). Compilar um shader é uma operação custosa; se cada variação visual de uma mesma superfície — pedra limpa, pedra com musgo, pedra molhada — exigir um grafo próprio, o projeto multiplica o custo de compilação e a dificuldade de manutenção sem necessidade. A Unreal resolve isso com o `Material Instance`, que herda o grafo compilado do Material base e expõe apenas os parâmetros marcados como editáveis, permitindo dezenas de variações visuais a partir de uma única estrutura compilada uma única vez. Este é o primeiro momento do semestre em que o foco recai sobre a camada de produção visual em si — até aqui, os materiais existiam apenas como parte do graybox exploratório do Módulo 1 (Semana 1) — e antecipa o mesmo princípio de parametrização que a Foliage Tool aplicará à composição de cena no Encontro 2.

## Recursos da Unreal

Material, Material Instance, Material Editor, parâmetros (Scalar Parameter, Vector Parameter, Texture Parameter).

## Comparação com Unity

A Unity resolve um problema equivalente com Material Property Blocks e com a própria estrutura de Materials herdando de um Shader: o Shader define a estrutura compilada e cada Material (ou Material Property Block, para variações em runtime sem duplicar o asset) define os valores aplicados sobre essa estrutura. O princípio é o mesmo nas duas engines — separar a estrutura compilada da parametrização de instância —, mas a Unreal tributa essa separação de forma mais explícita e hierárquica no próprio Content Browser (Material pai visível, Material Instances como filhos diretos), enquanto na Unity a relação Shader → Material é mais direta e a variação via Property Block é tipicamente resolvida em código, não no editor. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com o nível do Vertical Slice (Módulo 3, Semana 11) e os materiais originais da Semana 1 ainda como Materials simples, sem instâncias.
- Um Material base de exemplo pré-configurado (fora da visão da turma) com parâmetros expostos (cor base, rugosidade, textura), e duas Material Instances derivadas dele demonstrando variação visual.
- Slides com o diagrama Material base (grafo compilado) → parâmetros expostos → Material Instance A / Material Instance B, reforçando reuso sem recompilação.
- REFERENCES.md e documentação de Unreal Engine Materials disponíveis para consulta durante o laboratório.
- Estrutura de pastas `Materials/Base/` e `Materials/Instances/` (PROJECT_ARCHITECTURE.md, seção 8) revisada previamente em cada projeto de grupo, para orientar a reorganização durante o laboratório.
- **Nota de contingência:** este encontro não depende de nenhum sistema de gameplay e pode ser comprimido reduzindo o número de materiais refatorados por grupo, sem prejuízo conceitual, caso falte tempo — priorizar a refatoração de pelo menos um material com resultado visível sobre a cobertura de todos os materiais do nível.

## Cronograma do Encontro

- 15 min — Revisão do estado atual do Vertical Slice (Módulo 3) e do estado visual do nível desde a Semana 1.
- 20 min — Fundamentação: Material base versus Material Instance, parâmetros expostos e o custo de recompilação de shader.
- 35 min — Demonstração: criação guiada de um Material base parametrizado e duas Material Instances derivadas, com variação visual sem recompilação.
- 50 min — Laboratório: cada grupo refatora seus materiais existentes em Material base + Material Instances, organizando as pastas conforme o PROJECT_ARCHITECTURE.md.
- 15 min — Feedback: verificação da estrutura de pastas, nomenclatura (`M_`, `MI_`) e variação visual obtida em cada grupo.

## Desenvolvimento

O encontro parte da constatação de que os materiais do nível existem desde a Semana 1 como Materials simples, sem parametrização, um ponto de atenção natural agora que o Vertical Slice está jogável e o foco muda para produção. O professor demonstra a criação de um Material base com parâmetros expostos (cor, rugosidade, textura) e a derivação de duas Material Instances a partir dele, mostrando a mesma estrutura compilada gerando duas variações visuais distintas. Cada grupo replica o processo sobre seus próprios materiais, migrando ao menos as superfícies mais recorrentes do nível (paredes, piso do Dungeon Kit) para a estrutura Material base + Material Instances, organizando as pastas conforme o PROJECT_ARCHITECTURE.md.

## Desafio

Não há desafio de liberdade de solução neste encontro — a refatoração de materiais existentes é demonstração e adaptação guiada, preparando a autonomia maior da Foliage Tool no Encontro 2 e do desafio de otimização da Semana 13.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir ao menos um Material base parametrizado e duas Material Instances derivadas dele aplicadas ao nível, organizadas em `Materials/Base/` e `Materials/Instances/` com nomenclatura `M_` e `MI_`, sem alterar nenhum sistema de gameplay.

## Evidências para Avaliação

Organização de pastas e nomenclatura dos materiais conforme boas práticas da Unreal 5.6 e do PROJECT_ARCHITECTURE.md (seções 8 e 9) — insumo direto para o Code Review do Encontro 2 (Rubrica 4, critério "Boas práticas gerais").

## Dificuldades Esperadas

Grupos podem expor parâmetros em excesso, sem propósito visual claro, confundindo parametrização com simples exposição de todos os valores do grafo. Intervenção: perguntar "esse parâmetro realmente precisa variar entre instâncias, ou pertence à estrutura fixa do material?" e reforçar que parametrizar tudo indistintamente reproduz na Material Instance o mesmo problema de falta de estrutura que a técnica deveria resolver. Grupos com dificuldade para visualizar o ganho de performance da instância sobre a duplicação de Materials devem ser direcionados à documentação oficial antes de receber a resposta direta.

---

# Encontro 2

## Objetivos de Aprendizagem

- Explicar a Foliage Tool como ferramenta de composição de cena em massa, com controle de densidade e performance.
- Reconhecer o compromisso entre densidade visual e custo de renderização em composição de vegetação/elementos de cena.
- Compor vegetação/elementos de cena no nível do Vertical Slice, reutilizando as Material Instances criadas no Encontro 1.

## Conteúdos

- Foliage Tool como sistema de instanciamento em massa (instanced static meshes) para elementos repetidos de cena.
- Parâmetros de densidade, escala e distribuição na pintura de foliage.
- Composição guiada de vegetação/elementos de cena sobre o nível do Vertical Slice já existente.
- Code Review de encerramento: materiais e composição de cena (Rubrica 4).

## Conceitos Fundamentais

O conceito universal desta aula é a instanciação em massa como resposta ao problema de compor uma cena com milhares de elementos repetidos (grama, pedras, detritos) sem que cada um exija um Actor individual no nível, o que inviabilizaria a performance. A Foliage Tool "pinta" instâncias de uma mesma malha estática sobre a superfície do nível, agrupando-as internamente em um único componente otimizado (`Instanced Static Mesh Component`) em vez de criar um Actor por elemento — o mesmo princípio de parametrização e reuso de estrutura ensinado com Material Instance no Encontro 1, agora aplicado à geometria em vez de à superfície. A densidade de pintura é uma decisão de produção, não apenas estética: mais instâncias aumentam o custo de renderização, antecipando diretamente o tema de Optimization e Profiling da Semana 13. Este encontro também retoma o `HealthComponent`, o `InteractionComponent`, o `InventoryComponent` e o `BP_Enemy` construídos até a Semana 11 apenas como pano de fundo inalterado — nenhum deles é tocado; a composição de foliage é estritamente uma camada visual sobre o nível já jogável.

## Recursos da Unreal

Foliage Tool, Instanced Static Mesh, Material Instance (reutilizada do Encontro 1).

## Comparação com Unity

A Unity resolve um problema equivalente com o Terrain Tools' Tree and Detail Painting (para vegetação sobre Terrain) ou com GPU Instancing/`Graphics.DrawMeshInstanced` para instanciamento em massa fora do contexto de Terrain, agrupando elementos repetidos em chamadas de renderização otimizadas de forma análoga ao `Instanced Static Mesh Component` da Unreal. O princípio de evitar um Actor/GameObject por elemento repetido é o mesmo nas duas engines; a diferença está no acoplamento da ferramenta — na Unreal a Foliage Tool funciona sobre qualquer superfície estática do nível, enquanto na Unity a pintura de vegetação nativa está historicamente mais associada ao sistema de Terrain, exigindo abordagens adicionais para composição fora dele. Não aprofundar mais que isso; a comparação mais ampla é retomada na Unidade V.

## Preparação do Professor

- Projeto de cada grupo com Material Instances organizadas do Encontro 1 e o nível do Vertical Slice (Módulo 3) intacto.
- Um conjunto de meshes de vegetação/elementos de cena de prototipagem (Kenney Assets ou Nature Kit equivalente, CC0) disponibilizado previamente a todos os grupos.
- Uma composição de foliage de exemplo pré-configurada (fora da visão da turma), demonstrando densidade adequada versus densidade excessiva sobre a mesma área.
- Modelo de Avaliação — Code Review (Rubrica 4) impresso ou digital, pronto para uso ao final do encontro.
- REFERENCES.md e documentação de Unreal Engine Materials (seção de Foliage) disponíveis para consulta durante o laboratório.
- **Nota de contingência:** o Code Review de encerramento é o núcleo avaliativo do encontro e não deve ser comprimido; se necessário, reduzir a área do nível coberta por foliage por grupo, mantendo intacto o tempo reservado ao Code Review.

## Cronograma do Encontro

- 15 min — Revisão das Material Instances criadas no Encontro 1 e do estado visual atual do nível.
- 20 min — Fundamentação: Foliage Tool como instanciamento em massa, densidade e custo de renderização.
- 30 min — Demonstração: pintura guiada de vegetação/elementos de cena sobre uma área do nível, comparando densidade adequada e excessiva.
- 40 min — Laboratório: cada grupo compõe vegetação/elementos de cena em seu próprio nível, reutilizando as Material Instances do Encontro 1.
- 30 min — Code Review formal (Rubrica 4): avaliação de materiais e composição de cena de cada grupo.

## Desenvolvimento

O professor demonstra a pintura de vegetação/elementos de cena com a Foliage Tool sobre uma área de teste, ajustando densidade e escala, e evidenciando visualmente a diferença entre uma composição equilibrada e uma composição excessivamente densa (antecipando o tema de otimização da Semana 13 sem aprofundar profiling nesta aula). Cada grupo aplica a Foliage Tool ao seu próprio nível do Vertical Slice, compondo vegetação ou elementos de cena que reforcem a identidade visual do projeto, reutilizando as Material Instances organizadas no Encontro 1. Encerrado o laboratório, o professor conduz o Code Review formal de materiais e composição de cena, conforme Rubrica 4 do Sistema de Avaliação.

## Desafio

Não há desafio de liberdade de solução neste encontro — a composição de foliage é adaptação guiada sobre um nível já existente; a autonomia alta característica do Módulo 4 se expressa na escolha de quais áreas e elementos compor, sem restrição de solução técnica única.

## Critérios de Sucesso

Ao final do encontro, cada grupo deve possuir vegetação/elementos de cena compostos via Foliage Tool no nível do Vertical Slice, com densidade visualmente equilibrada, reutilizando as Material Instances do Encontro 1, e ter passado pelo Code Review formal de materiais e composição de cena.

## Evidências para Avaliação

Code Review formal (Rubrica 4) de materiais e composição de cena, com ênfase em nomenclatura (`M_`, `MI_`), organização de pastas (`Materials/Base/`, `Materials/Instances/`) e ausência de duplicação de materiais equivalentes, conforme Sistema de Avaliação (Semana 12) e a progressão avaliativa dos Módulos 4 e 5, que passa a priorizar arquitetura e consistência.

## Dificuldades Esperadas

Grupos podem pintar foliage com densidade excessiva por priorizar impacto visual imediato sobre custo de performance. Intervenção: perguntar "essa densidade seria sustentável se o nível fosse dez vezes maior?" e reforçar que a decisão de densidade é uma decisão de produção, retomada com dados concretos na Semana 13 (Profiling). Grupos que criarem novos Materials duplicados em vez de derivar Material Instances do Encontro 1 devem ser direcionados de volta à estrutura Material base + Instance durante o próprio Code Review, sem necessidade de refazer o encontro.

---

# Resultado Esperado da Semana

Ao final da Semana 12, cada grupo terá seus materiais principais organizados como Material base parametrizado com Material Instances derivadas (`Materials/Base/`, `Materials/Instances/`, prefixos `M_`/`MI_`), e um nível com vegetação/elementos de cena compostos via Foliage Tool, reutilizando essas mesmas instâncias. Conceitualmente, a turma deve dominar a separação entre estrutura compilada e parametrização de instância, tanto em materiais quanto em instanciamento de geometria em massa. Nenhum sistema de gameplay dos Módulos 1 a 3 — `HealthComponent`, `InteractionComponent`, `InventoryComponent`, `BPI_Interactable`, `WBP_HUD`, `BP_Enemy` com Behavior Tree/Blackboard — foi alterado; a semana refina exclusivamente a camada visual do Vertical Slice, avaliada formalmente por Code Review (Rubrica 4).

# Preparação para a Próxima Semana

A Semana 13 mantém a metodologia de Studio Based Learning da Unidade IV, avançando para áudio integrado a eventos de gameplay já existentes (interação, passos, ambiente) e para Optimization e Profiling como etapa obrigatória de produção — retomando diretamente a discussão de custo de densidade de foliage iniciada nesta semana, agora com ferramentas de profiling concretas e um desafio de otimização com solução própria por grupo.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Unreal Engine Materials. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Material Instances e Foliage Tool. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Material Property Blocks e Terrain Tools (Tree and Detail Painting), para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeos sugeridos (apenas como apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, com vídeos introdutórios de Materials e Foliage; **PrismaticaDev**, para exemplos aplicados de composição de cena e materiais; **Ryan Laley**, para exemplos práticos de Material Instances em produção.
