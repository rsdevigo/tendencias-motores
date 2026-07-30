# Tutorial - Semana 3 - Encontro 1

## Introdução

Nas Semanas 1 e 2 você construiu o `BP_Player` — um Character completo, com locomoção própria e um esquema inteiro de Enhanced Input. Mas até agora ele só existe sobre um graybox: formas geométricas sem material definido, sem chão modelado, apenas um espaço de teste. Este encontro responde a uma pergunta diferente das anteriores: como uma engine resolve a aparência de uma superfície e a geometria de um terreno em larga escala? São dois problemas distintos — aparência e geometria — e a Unreal os resolve com duas ferramentas separadas: o Material Graph e o Landscape.

Este tutorial não substitui a explicação do professor em sala. Ele existe para que você possa acompanhar a implementação passo a passo durante o laboratório e revisitar os passos depois da aula, sem depender da documentação oficial da Epic.

## Objetivos da Semana

- Explicar o Material Graph como conceito universal de shader nodal, independente da sintaxe específica de qualquer engine.
- Criar um material simples usando texturas básicas e parâmetros de superfície.
- Modelar um terreno básico via Landscape para o nível de teste do Vertical Slice.

## Resultado Esperado ao Final da Semana

Um material simples (`M_`) aplicado a um terreno básico modelado via Landscape, compondo visualmente o `Map_Exploration` em que o `BP_Player` já se move. Este é o resultado esperado ao final deste Encontro 1 especificamente — o Encontro 2 eleva esse nível a um padrão de renderização moderno (Nanite e Lumen) e gera o primeiro build executável.

## Pré-requisitos

- Ter concluído a Semana 2: `BP_Player` funcional como Character, controlável por Enhanced Input (movimentação, câmera e salto), com uma Input Action adicional do desafio.
- Compreender a diferença entre Pawn e Character e o papel do Character Movement Component.

---

# Antes de começar

## O que você deverá possuir antes desta semana

- O projeto da Semana 2, aberto no Unreal Editor 5.6, com o `BP_Player` funcional e controlável exclusivamente por Enhanced Input no `Map_Exploration`.

## Arquivos necessários

- Nenhum arquivo externo é necessário além dos pacotes de assets já indicados abaixo.

## Assets utilizados

- Texturas simples do Kenney Prototype Kit ou Kenney Nature Kit, organizadas na pasta `Textures/` do projeto (PROJECT_ARCHITECTURE.md, seção 8). Esta é a primeira semana em que assets externos ao template entram no projeto.

## Projeto esperado

O mesmo projeto da Semana 2, com as pastas `Materials/Base/` e `Textures/` prontas para receber o novo material, e o `Map_Exploration` disponível para receber o terreno via Landscape.

---

# Parte 1 — Material Graph: shader nodal universal

## Objetivo

Compreender o Material Graph como a solução da Unreal para o problema universal de definir a aparência de uma superfície, e criar um material simples a partir de uma textura.

## Conceito

Toda engine moderna precisa resolver o mesmo problema: como transformar uma textura, um valor numérico e algumas operações matemáticas na cor, rugosidade, metalicidade e relevo de uma superfície, sem exigir que o desenvolvedor escreva código de shader à mão para cada caso. A solução universal para isso é o **shader nodal**: um grafo visual em que cada nó representa uma operação (amostrar uma textura, multiplicar um valor, combinar dois vetores) e as conexões entre os nós definem o caminho até as propriedades finais do material.

O **Material Graph** é a implementação específica da Unreal para esse conceito. Nele, um nó **Texture Sample** lê os pixels de uma textura, um **Scalar Parameter** expõe um valor numérico ajustável (como rugosidade), e um **Vector Parameter** expõe uma cor ou vetor ajustável. Esses nós se conectam aos pinos finais do material — Base Color, Roughness, Metallic, Normal — que juntos definem como a superfície reage à luz. Todo material também define um **Material Domain** (o mais comum sendo "Surface", para superfícies sólidas comuns).

Compreender essa separação entre a intenção (o que a superfície deve parecer) e a implementação nodal (como os nós chegam a esse resultado) prepara você para reconhecer, mais adiante neste mesmo encontro, que o Landscape resolve um problema completamente diferente: não a aparência de uma superfície, mas a geometria de um terreno em larga escala.

## Passo a passo

1. No Content Browser, abrir a pasta `Materials/Base`.
2. Clicar com o botão direito, selecionar "Material" e nomear como `M_Ground`, seguindo a convenção `M_` do projeto (PROJECT_ARCHITECTURE.md, seção 9).
3. Abrir o `M_Ground` com um duplo clique para acessar o Material Editor.
4. No painel Details do material (com nenhum nó selecionado), confirmar que o "Material Domain" está definido como "Surface".
5. Arrastar uma textura simples da pasta `Textures/` para dentro do grafo — isso cria automaticamente um nó "Texture Sample".
6. Conectar a saída RGB do nó "Texture Sample" ao pino "Base Color" do nó principal do material.
7. Clicar com o botão direito no grafo vazio, buscar por "Scalar Parameter" e adicionar um nó; nomeá-lo como `Roughness_Amount` no painel Details.
8. Conectar a saída do `Roughness_Amount` ao pino "Roughness" do nó principal.
9. Clicar em "Apply" e depois em "Save" no Material Editor.

## Resultado esperado

Um material `M_Ground` funcional, com uma textura conectada ao Base Color e um parâmetro escalar ajustável conectado ao Roughness, pronto para ser aplicado a uma superfície.

## Verificando

Na pré-visualização do Material Editor (esfera ou plano de exemplo), confirme que a textura aparece corretamente projetada e que alterar o valor de `Roughness_Amount` no painel Details muda visivelmente o brilho da superfície de pré-visualização.

## Problemas comuns

- **Textura aparece preta ou distorcida na pré-visualização:** confirme que a textura foi arrastada corretamente para o grafo e que a saída RGB (não Alpha) foi conectada ao Base Color.
- **Esquecer de clicar em "Apply":** alterações no Material Graph não afetam superfícies no nível até que o material seja aplicado e salvo.
- **Confundir Scalar Parameter com Constant:** um Scalar Parameter pode ser exposto e ajustado fora do grafo (inclusive em Material Instances futuras, a partir do Módulo 4); uma Constant não pode.

## Boas práticas

Nomeie parâmetros pela propriedade que representam (`Roughness_Amount`), nunca por nomes genéricos como `Param1` — esse hábito facilita a criação de Material Instances no Módulo 4, quando os mesmos parâmetros serão reaproveitados para variações do material sem duplicar o grafo inteiro.

## Comparação com Unity

O Material Graph da Unreal corresponde ao Shader Graph da Unity: ambos abstraem a criação de shaders em um grafo nodal, evitando código de shader escrito à mão para a maioria dos casos. A diferença arquitetural mais relevante é que a Unreal integra o Material Graph nativamente ao pipeline de renderização desde a primeira versão, com Material Domains e blend modes configuráveis diretamente no grafo, enquanto a Unity, historicamente dividida entre o Built-in Render Pipeline e pipelines mais recentes (URP/HDRP), só oferece o Shader Graph de forma plena nesses pipelines modernos.

---

# Parte 2 — Landscape: geometria de terreno em larga escala

## Objetivo

Compreender o Landscape como ferramenta distinta do material, dedicada exclusivamente à geometria de terreno, e modelar um terreno básico para o nível de teste.

## Conceito

O material resolve a aparência de uma superfície, mas não resolve um segundo problema universal: como representar um terreno grande, irregular e esculpível, sem modelar manualmente cada elevação como um Static Mesh comum. Um Static Mesh é adequado para objetos com geometria fixa e relativamente pequena (uma caixa, uma parede, um baú); ele não escala bem para um terreno de centenas de metros com variações de altura suaves.

O **Landscape** resolve esse problema com uma abordagem própria: um heightmap (mapa de alturas) define a elevação do terreno ponto a ponto, e o terreno pode ser esculpido em tempo real dentro do editor com ferramentas de sculpt (elevar, abaixar, suavizar) e pintado com camadas de material (paint layers), sem exigir remodelagem manual de geometria a cada ajuste.

É essencial não confundir os dois conceitos desta aula: o material (`M_Ground`) definido na Parte 1 resolve a aparência da superfície; o Landscape, agora, resolve a geometria do terreno sobre o qual esse material será aplicado. Um Static Mesh comum não deve ser usado como substituto de terreno em larga escala — essa distinção evita um dos erros mais frequentes desta etapa do curso.

## Passo a passo

1. No `Map_Exploration`, abrir a aba "Landscape" no modo de edição (Modes > Landscape, ou o atalho equivalente no menu Modes do editor).
2. Na seção "Manage", configurar os parâmetros iniciais do Landscape: número de componentes, tamanho de seção e escala geral, mantendo os valores padrão sugeridos pelo editor para um terreno de teste pequeno.
3. Clicar em "Create" para gerar o Landscape vazio (plano) na cena.
4. Selecionar a aba "Sculpt" e escolher a ferramenta "Sculpt" (elevar/abaixar terreno).
5. Ajustar o "Brush Size" e a "Tool Strength" no painel lateral para um valor moderado.
6. Esculpir manualmente pequenas variações de elevação na área em que o `BP_Player` já transita, evitando alterações bruscas que dificultem a locomoção testada nas Semanas 1 e 2.
7. Selecionar a ferramenta "Smooth" e suavizar as transições mais abruptas entre as elevações criadas.
8. Selecionar a aba "Paint" e adicionar uma camada de pintura (Paint Layer), associando o material `M_Ground` criado na Parte 1 como base do Landscape.
9. Pintar a camada sobre toda a superfície esculpida, cobrindo o terreno com o material criado.
10. Salvar o nível (`Map_Exploration`).

## Resultado esperado

Um terreno com variações de elevação suaves, coberto pelo material `M_Ground`, substituindo o piso plano genérico usado como graybox nas Semanas 1 e 2, com o `BP_Player` ainda capaz de se mover livremente sobre ele.

## Verificando

Entre em modo Play e percorra o terreno com o `BP_Player`: a locomoção configurada na Semana 2 deve continuar funcionando normalmente sobre as variações de elevação, sem que o Character fique preso ou atravesse a geometria.

## Problemas comuns

- **Esculpir elevações bruscas demais:** pode fazer o `BP_Player` ficar preso ou pular de forma não intencional ao colidir com rampas íngremes; use a ferramenta "Smooth" para suavizar após esculpir.
- **Esquecer de associar o Paint Layer a um material:** o Landscape aparece sem textura (cinza ou preto) até que uma camada de pintura com material seja criada e aplicada.
- **Confundir Landscape com Static Mesh:** tentar modelar o terreno inteiro como um Static Mesh comum é ineficiente e não escala; sempre use Landscape para geometria de terreno em larga escala.

## Boas práticas

Esculpa o terreno em pequenos incrementos, testando a locomoção do `BP_Player` a cada ajuste relevante, em vez de esculpir toda a área de uma vez e só testar ao final — o mesmo hábito de ajuste incremental já recomendado para os parâmetros de movimento na Semana 2.

## Comparação com Unity

O Landscape da Unreal corresponde ao Terrain da Unity, com papel equivalente: ambos utilizam heightmap para definir elevação e camadas de material (paint layers) para textura. A equivalência conceitual é direta; a comparação arquitetural mais profunda entre as duas soluções (desempenho, streaming de terreno em larga escala) é retomada, se necessário, na Unidade V do curso.

---

# Ao final da semana

Este Encontro 1 cobre a primeira metade da Semana 3. Ao final dele, o projeto deve conter um material simples (`M_Ground`) aplicado a um terreno modelado via Landscape no `Map_Exploration`, com o `BP_Player` (já completo desde a Semana 2) se movendo normalmente sobre essa nova geometria. Isso corresponde à linha "Cena de teste (graybox)" do roadmap do Módulo 1 no PROJECT_ARCHITECTURE.md, evoluindo o nível de teste de um graybox neutro para um ambiente visualmente reconhecível. O Encontro 2 eleva esse mesmo nível a Nanite e Lumen e gera o primeiro build executável do Vertical Slice.

# Desafio

Não há desafio neste encontro — a criação do material e do terreno é demonstração e replicação guiada, coerente com a autonomia muito baixa do Módulo 1 (PEDAGOGICAL_RULES.txt) e com a proximidade do Checkpoint de encerramento de módulo no Encontro 2.

# Checklist

☐ `M_Ground` criado na pasta `Materials/Base`, com Texture Sample conectado ao Base Color e Scalar Parameter conectado ao Roughness

☐ Landscape criado no `Map_Exploration`, com elevações esculpidas e suavizadas

☐ Paint Layer do Landscape associado ao material `M_Ground`

☐ `BP_Player` capaz de se mover normalmente sobre o novo terreno, sem ficar preso

☐ Consigo explicar de memória a diferença entre Material (aparência) e Landscape (geometria)

☐ Nível salvo sem erros

# Glossário

- **Material Graph:** grafo nodal da Unreal que define a aparência de uma superfície (cor, rugosidade, metalicidade, relevo) a partir de texturas e parâmetros.
- **Texture Sample:** nó que amostra os pixels de uma textura dentro do Material Graph.
- **Scalar/Vector Parameter:** nós que expõem valores numéricos ou vetoriais ajustáveis dentro e fora do Material Graph.
- **Material Domain:** classificação do material quanto ao seu uso (Surface, Deferred Decal, entre outros).
- **Landscape:** ferramenta da Unreal para modelagem de terreno em larga escala via heightmap e camadas de pintura (paint layers).
- **Paint Layer:** camada de material pintável sobre a superfície de um Landscape.

# Referências

- EPIC GAMES. **Unreal Engine 5 Documentation** — Unreal Engine Materials. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials.
- EPIC GAMES. **Unreal Engine 5 Documentation** — Landscape Outdoor Terrain. Disponível em: https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine.
- EPIC GAMES. **Unreal Engine Learning Library** — introdução a Materiais e Landscape. Disponível em: https://dev.epicgames.com/community/unreal-engine/learning.
- UNITY TECHNOLOGIES. **Unity Manual** — Shader Graph e Terrain, para fins comparativos. Disponível em: https://docs.unity3d.com/Manual/.
- Vídeo sugerido (apoio complementar, nunca substituindo a documentação oficial): canal oficial **Unreal Engine**, vídeos introdutórios de Materiais e Landscape; **PrismaticaDev**, para material e Landscape.
