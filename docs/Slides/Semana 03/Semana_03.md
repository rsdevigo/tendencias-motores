---
marp: true
theme: academic-course
paginate: true
header: 'Semana 3 — Materiais, Terrain3D, SDFGI/VoxelGI e Exportação'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 3

## Materiais, Terrain3D, SDFGI/VoxelGI e Exportação

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade I — Aprender a Ferramenta** (Semanas 1–3)
**Projeto:** Vertical Slice *O Templo Esquecido*

</div>

<!--
Retomar o projeto da Semana 2 já aberto, com Player controlável e Scene level_exploration.tscn, antes de começar.
Esta semana encerra o Módulo 1 e a Unidade I. Nada do Player ou da Scene existente é refeito — apenas ampliado.
Metodologia: Scaffolded Learning, autonomia muito baixa — professor demonstra, aluno replica.
-->

---

## Objetivos da Semana

- Compreender materiais e o addon Terrain3D como composição visual de um nível
- Compreender iluminação global dinâmica (SDFGI/VoxelGI) como conceito universal de renderização
- Gerar o primeiro build exportado do Vertical Slice

<!--
Encontro 1 cobre materiais e terreno. Encontro 2 cobre iluminação global e exportação, encerrando o Módulo 1 com o Checkpoint de primeiro build jogável.
Resultado esperado ao final: nível de teste completo, exportado como executável funcional fora do editor.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Materiais e Terrain3D

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma a Scene das Semanas 1 e 2 e adiciona material e terreno — nada do Player é alterado.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 2 (Player controlável) (15 min)
- Introdução: aparência de superfície e modelagem de terreno (20 min)
- Demonstração: StandardMaterial3D e escultura com Terrain3D (35 min)
- Laboratório: cada estudante aplica material e modela terreno próprio (45 min)
- Desafio: variar um parâmetro do material (15 min)
- Feedback e fechamento (5 min)

<!--
Ciclo pedagógico da disciplina: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
-->

---

<!-- _class: question -->

# Como uma superfície "sabe" como reagir à luz — e como se modela um terreno inteiro sem esculpir cada polígono à mão?

Pense em qualquer jogo 3D que vocês já jogaram.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a nomear "material"/"shader" e "ferramenta de terreno" sem depender de sintaxe de nenhuma engine específica.
Erro comum: respostas vagas ("a textura resolve") — insistir até surgir a ideia de parâmetros combinados (cor, rugosidade, textura).
-->

---

## O Problema Universal do Material

Toda superfície visível em um jogo 3D responde à mesma pergunta: como ela reage à luz?

- Cor, brilho, rugosidade e textura se combinam para produzir essa resposta
- Escrever um shader manualmente para cada superfície é inviável na maioria dos projetos
- Engines modernas oferecem uma representação nodal desse problema: o **Material Graph**

<!--
Conceito universal, não específico do Godot. Reforçar o hábito da disciplina: sempre perguntar "que problema universal isso resolve?" antes de "como se usa no Godot?".
Referência: Godot Docs — Standard Material 3D.
-->

---

## Material Graph no Godot

- **StandardMaterial3D** — material pronto, parâmetros expostos no Inspector (Albedo, Roughness, Metallic)
- Suficiente para a maior parte das superfícies do graybox desta disciplina
- **Visual Shader** — grafo nodal completo do Godot, usado quando o StandardMaterial3D não é suficiente
- Este encontro trabalha exclusivamente com StandardMaterial3D

<!--
Não confundir StandardMaterial3D (parâmetros prontos) com Visual Shader (grafo nodal completo) — o primeiro basta para o nível de teste.
Documentação: Godot Docs — Standard Material 3D.
-->

---

## O Problema Universal do Terreno

Modelar grandes extensões de terreno polígono a polígono não é viável para nenhuma equipe.

- Engines modernas oferecem ferramentas dedicadas de escultura de terreno
- Pincéis de altura, textura por camadas, otimização própria de malha
- O Godot **não** possui essa ferramenta no núcleo da engine

<!--
Essa ausência motiva o uso do addon Terrain3D nesta disciplina — é uma diferença arquitetural real, não um detalhe menor.
-->

---

## Terrain3D — Addon sem Equivalente Nativo

- **Terrain3D** — addon de terceiros que adiciona escultura e texturização de terreno ao editor
- **Terrain3D Storage** — recurso que armazena a geometria e as texturas do terreno esculpido
- Ferramentas de pincel próprias, ativadas apenas com o Node `Terrain3D` selecionado
- Sem Terrain3D, não há fluxo de terreno equivalente ao de engines com Terrain nativo

<!--
Reforçar: Terrain3D não é "mais uma feature" do Godot — é uma peça externa que resolve uma lacuna real do núcleo da engine.
Documentação: repositório oficial do Terrain3D.
-->

---

<!-- _class: comparison -->

## Materiais e Terreno no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- StandardMaterial3D com parâmetros prontos no Inspector
- Visual Shader para casos avançados
- Terreno depende do addon Terrain3D (terceiros)

</div>
<div class="col negative">

### Unity

- Standard Shader/URP com parâmetros equivalentes
- Shader Graph para materiais customizados
- Terrain **nativo**, integrado ao editor

</div>
</div>

<!--
Materiais: filosofia muito próxima entre as duas engines. Terreno: diferença arquitetural real — Unity resolve nativamente, Godot depende de addon.
Não ensinar Unity em profundidade — apenas contrastar arquitetura.
-->

---

## Demonstração — Material e Terreno

O que será construído:

- `StandardMaterial3D` aplicado ao Node `Chao`, salvo em `materials/chao_prototype.tres`
- Node `Terrain3D` como filho de `NivelTeste`, com Terrain3D Storage em `resources/terrain/`
- Elevação e depressão esculpidas, com textura do Kenney Mini Dungeon pintada

Por quê: primeira composição visual real do nível, base direta da iluminação global no Encontro 2.

<!--
Não detalhar passo a passo aqui — isso é papel do Tutorial (Semana 3, Encontro 1). O slide só estrutura a demonstração ao vivo.
Reforçar: material sempre salvo como recurso externo (.tres), nunca embutido na Scene.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar o Node `Chao` com material aplicado (textura visível no Viewport) ao lado do painel de ferramentas do Terrain3D com um pincel de escultura ativo.
> Enquadramento: captura de tela dividida — Inspector com o StandardMaterial3D à esquerda, Viewport 3D com terreno esculpido à direita.
> Elementos presentes: campo Albedo com textura atribuída, pincel de escultura do Terrain3D, relevo com elevação e depressão visíveis.
> Destaque visual: contorno colorido na área do terreno recém-esculpida.
> Legenda sugerida: "Material aplicado ao Chao e terreno esculpido com Terrain3D, lado a lado."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — Material e Terreno

Cada estudante replica, no próprio projeto:

1. `StandardMaterial3D` aplicado ao `Chao`, salvo em `materials/chao_prototype.tres`
2. Textura do Kenney Mini Dungeon no Albedo, Roughness ajustado
3. Node `Terrain3D` com Storage salva em `resources/terrain/`
4. Elevação e depressão esculpidas, com textura pintada sobre a superfície
5. Player reposicionado sobre área plana do novo terreno

<!--
Erro comum: material criado como recurso embutido, não salvo como .tres externo.
Erro comum: Player spawnando dentro do relevo esculpido — reposicionar manualmente após a escultura.
-->

---

## Boas Práticas — Materiais e Terreno

- Sempre salvar materiais como recursos externos (`.tres`), nunca embutidos na Scene
- Nomear arquivos pela função (`chao_prototype.tres`), não por aparência (`material_cinza.tres`)
- Esculpir variações suaves de relevo, evitando elevações abruptas no graybox
- Testar a movimentação do Player sobre o terreno antes de considerar a etapa concluída

<!--
Reutilização de materiais e organização de recursos externos seguem o PROJECT_ARCHITECTURE.md.
-->

---

<!-- _class: exercise -->

# Desafio — Encontro 1

Ajuste ao menos um parâmetro do material aplicado ao `Chao` — cor do Albedo, Roughness ou textura — de forma diferente da demonstração.

<div class="objectives">

Justifique brevemente a escolha em relação à identidade visual pretendida para o próprio nível. Não há solução única.

</div>

<!--
Circular pela sala pedindo justificativas curtas em voz alta. Sem instrumento formal de avaliação neste encontro.
-->

---

## Fechamento — Encontro 1

- `Chao` com StandardMaterial3D aplicado, textura e Roughness ajustados
- Terreno esculpido com Terrain3D, elevação e depressão, textura pintada
- Player posicionado sobre área plana do novo terreno
- Próximo passo: iluminação global e exportação, no Encontro 2

<!--
Dificuldade esperada: Player preso ou flutuando sobre relevo esculpido — reforçar reposicionamento manual antes de encerrar.
O material e o terreno construídos aqui compõem o Checkpoint de encerramento do Módulo 1, avaliado no Encontro 2.
-->

---

<!-- _class: chapter -->

## Encontro 2

# SDFGI/VoxelGI e Exportação

<span class="chapter-number">02</span>

<!--
Encontro depende diretamente do material e terreno do Encontro 1. Confirmar que todos abrem a Scene sem erros antes de prosseguir.
Este encontro encerra o Módulo 1 e a Unidade I — Aprender a Ferramenta.
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (terreno e material) (10 min)
- Introdução: iluminação global e geometria virtualizada (15 min)
- Demonstração: SDFGI/VoxelGI e ajuste de parâmetros (15 min)
- Demonstração: pipeline de exportação (15 min)
- Laboratório: cada estudante ativa iluminação e exporta seu build (40 min)
- Checkpoint: showcase dos builds exportados (30 min)
- Feedback e fechamento (10 min)

<!--
Retomar rapidamente o estado do nível do Encontro 1 antes de avançar — é pré-requisito direto.
Reservar tempo real para o showcase — é o Checkpoint de encerramento do Módulo 1.
-->

---

<!-- _class: question -->

# Por que um nível com apenas uma luz direta parece plano e artificial?

Pense em superfícies que ficam completamente escuras mesmo perto de uma parede iluminada.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a identificar que falta luz "saltando" entre superfícies — luz indireta.
-->

---

## Iluminação Global — Problema Universal

Superfícies fora do alcance direto da luz não deveriam ficar completamente escuras — deveriam receber luz refletida por superfícies próximas.

- Calcular isso com precisão total, a cada frame, é inviável em tempo real
- Engines modernas oferecem aproximações otimizadas desse cálculo
- Chamada de **iluminação global**

<!--
Conceito universal de renderização moderna. Reforçar antes de qualquer implementação no Godot.
Referência: Godot Docs — Global Illumination (SDFGI/VoxelGI).
-->

---

## SDFGI e VoxelGI no Godot

- **SDFGI** — aproxima a geometria por campos de distância com sinal, sem dados pré-calculados
- **VoxelGI** — discretiza a cena em voxels, maior precisão em volumes menores e delimitados
- Duas abordagens alternativas ao mesmo problema, com trade-offs de escala e precisão
- SDFGI **amplifica** a luz existente — ajustar a luz principal em conjunto, nunca isoladamente

<!--
Erro comum: SDFGI habilitado sem ajustar a luz principal, produzindo cena estourada ou escura demais.
Documentação: Godot Docs — Global Illumination.
-->

---

<!-- _class: comparison -->

## Iluminação Global no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- SDFGI/VoxelGI — inteiramente dinâmicos
- Sem bake prévio necessário
- Configurado no `WorldEnvironment`

</div>
<div class="col negative">

### Unity

- Global Illumination (URP/HDRP)
- Tempo real **ou** Lightmapping pré-calculado
- Abordagem híbrida, com opção de bake

</div>
</div>

<!--
Mesmo objetivo conceitual — luz indireta crível com custo controlado. Godot sempre dinâmico; Unity oferece opção híbrida com bake.
Não ensinar Unity em profundidade — apenas contrastar arquitetura.
-->

---

<!-- _class: diagram -->

## Diagrama Sugerido — Limite Compartilhado

> **Diagrama sugerido**
>
> Comparação lado a lado: `Unreal Engine (Nanite)` → geometria virtualizada, LOD automático em tempo real. `Godot` e `Unity` → sem equivalente nativo, dependem de LOD manual, impostors e occlusion culling.
> Objetivo: visualizar que a ausência de geometria virtualizada é um limite compartilhado, não uma desvantagem exclusiva do Godot.
> Legenda sugerida: "Nanite resolve um problema que Godot e Unity ainda tratam com técnicas tradicionais."

<!--
Discussão puramente conceitual, sem implementação. Manter breve — não consumir tempo de laboratório.
Reforçar: não é falha exclusiva do Godot, é limite compartilhado com a Unity.
-->

---

## Geometria Virtualizada — Um Limite Compartilhado

- **Nanite** (Unreal Engine) renderiza malhas extremamente detalhadas sem LOD manual
- Nem Godot nem Unity possuem solução nativa equivalente
- Ambas dependem de LOD manual, impostors e occlusion culling
- Discussão conceitual — sem implementação nesta disciplina

<!--
Erro comum: tratar isso como falha exclusiva do Godot — reforçar que a Unity compartilha a mesma limitação.
Conectar à tabela de comparações arquiteturais do PROJECT_ARCHITECTURE.md (seção 12).
-->

---

## Exportação — Do Editor ao Executável

Um projeto Godot, enquanto aberto no editor, depende do próprio editor para rodar.

- **Exportação** — empacotar o projeto em um executável autocontido
- **Export Templates** — versões pré-compiladas do runtime, específicas por plataforma
- Sem os templates corretos instalados, a exportação falha antes de começar

<!--
Verificar Export Templates é o primeiro passo prático, não um detalhe menor — reforçar isso antes de abrir a janela de Export.
Documentação: Godot Docs — Exporting Projects.
-->

---

<!-- _class: comparison -->

## Exportação no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- **Project > Export**, presets por plataforma
- Depende de Export Templates instalados

</div>
<div class="col negative">

### Unity

- **Build Settings**, targets por plataforma
- Depende de módulos de plataforma instalados

</div>
</div>

<!--
Fluxo conceitual equivalente em ambas as engines — configurar preset/target, garantir módulos corretos, gerar executável autocontido.
-->

---

## Demonstração — Iluminação e Exportação

O que será construído:

- `WorldEnvironment` com SDFGI habilitado, recurso salvo em `resources/`
- Preset de exportação criado em **Project > Export**
- Primeiro build executável, testado fora do editor

Por quê: fecha o Módulo 1 com um nível jogável e distribuível fora do Godot.

<!--
Não detalhar passo a passo aqui — o Tutorial (Semana 3, Encontro 2) cobre isso em detalhe.
Reforçar: sempre testar o executável fora do editor antes do showcase.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a janela **Project > Export**, com um preset já configurado para a plataforma de destino.
> Enquadramento: captura de tela da janela Export do Godot, lista de presets à esquerda e opções à direita.
> Elementos presentes: botão "Add...", preset nomeado ("Build Semana 3"), botão "Export Project" no rodapé.
> Destaque visual: o botão "Export Project".
> Legenda sugerida: "Janela de exportação com o preset configurado para o primeiro build do Vertical Slice."

<!--
Usar esta imagem como referência caso a demonstração ao vivo não seja possível.
-->

---

## Laboratório — Iluminação e Exportação

Cada estudante realiza, no próprio projeto:

1. `WorldEnvironment` com SDFGI habilitado, salvo em `resources/`
2. Ajuste da intensidade da `LuzPrincipal` em conjunto com o SDFGI
3. Preset de exportação criado em **Project > Export**
4. Build exportado para `builds/semana_03/`
5. Executável testado fora do editor — Player e terreno funcionando

<!--
Erro comum: build roda no editor mas falha exportado — revisar aba Resources do preset.
Reservar tempo real de laboratório para testar o executável fora do editor, não apenas a versão do editor.
-->

---

## Boas Práticas — Iluminação e Build

- Comparar visualmente a cena com SDFGI ativado e desativado antes de concluir o ajuste
- Salvar o `Environment` como recurso externo, junto com materiais e Terrain3D Storage
- Nomear presets de exportação de forma identificável (`Build Semana 3`)
- Sempre testar o executável exportado fora do editor antes do showcase

<!--
Um projeto que só funciona no editor não é um build validado — reforçar isso antes do Checkpoint.
-->

---

## Checkpoint — Encerramento do Módulo 1

Showcase: cada estudante apresenta seu build exportado, rodando fora do editor.

- Nível de teste com terreno, material e iluminação global
- Player controlável, herdado das Semanas 1 e 2
- Executável estável, sem falhas críticas

<!--
Rubrica 3 — Checkpoints (progresso, funcionalidades, qualidade técnica, estabilidade do build).
Rubrica 6 — Apresentações (comunicação e demonstração ao vivo).
-->

---

## Fechamento — Encontro 2

- SDFGI habilitado, luz indireta visível no terreno e no `Chao`
- Discussão sobre ausência de geometria virtualizada (Nanite) concluída
- Primeiro build executável exportado e testado fora do editor
- Módulo 1 e Unidade I — Aprender a Ferramenta encerrados

<!--
Dificuldade esperada: Export Templates não instalados a tempo — verificar isso no início do laboratório, não durante a demonstração.
-->

---

## Resultado Esperado da Semana

- Nível de teste com terreno (Terrain3D) e material (StandardMaterial3D)
- Iluminação global ativa via SDFGI, em `WorldEnvironment` salvo externamente
- Primeiro build executável, testado fora do editor
- Turma relaciona materiais/terreno/iluminação/exportação aos equivalentes na Unity

<!--
Checkpoint de encerramento do Módulo 1 (Rubrica 3) e Showcase (Rubrica 6) avaliados neste encontro.
-->

---

## Checklist da Semana

- [ ] `Chao` com StandardMaterial3D aplicado, salvo em `materials/chao_prototype.tres`
- [ ] Node `Terrain3D` com Storage salva em `resources/terrain/`, terreno esculpido e texturizado
- [ ] Player reposicionado sobre área plana do terreno
- [ ] `WorldEnvironment` com SDFGI habilitado, salvo em `resources/`
- [ ] Preset de exportação criado e build gerado em `builds/semana_03/`
- [ ] Executável testado fora do editor, sem falhas críticas

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 4.
-->

---

## Próximos Passos — Semana 4

O nível de teste e o Player exportados nesta semana são a base direta da Semana 4, que abre o **Módulo 2 (Construir Sistemas)**:

- `GameManager` e `SaveManager` via Autoload/Singleton
- Primeiros sistemas de gameplay propriamente ditos do Vertical Slice

Leitura recomendada: Godot Docs — Standard Material 3D, Global Illumination, Exporting Projects; Unity Manual (consulta comparativa) — Terrain, Global Illumination.

<!--
Nada desta semana será refeito — apenas ampliado. Reforçar isso à turma para reduzir ansiedade sobre "ter feito certo".
Referências completas: ver Tutorial Semana 3 (Encontros 1 e 2) e Plano de Aula Semana 3.
-->
