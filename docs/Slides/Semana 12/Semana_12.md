---
marp: true
theme: academic-course
paginate: true
header: 'Semana 12 — Materials, Material Overrides e Foliage (MultiMeshInstance3D)'
footer: 'IFMS · Tecnologia em Jogos Digitais · Tendências de Motores de Jogos'
---

<!-- _class: cover -->

![logo](https://dummyimage.com/280x90/ffffff/1f4e79&text=IFMS)

# Semana 12

## Materials, Material Overrides e Foliage (MultiMeshInstance3D)

<div class="meta">

**Disciplina:** Tendências de Motores de Jogos (IN46A)
**Curso:** Tecnologia em Jogos Digitais — IFMS Campus Dourados
**Unidade IV — Produzir como um Pequeno Estúdio** (Semanas 12–14)
**Projeto:** Vertical Slice *O Templo Esquecido*
**Code Review 🔵** — Rubrica 4 (não encerra a Unidade IV)

</div>

<!--
A Semana 11 encerrou a Unidade III com o Vertical Slice jogável completo: animação, HUD, inventário, interação, IA (Navigation + Behavior Tree/Blackboard) e combate simples, avaliados em Playtest e Showcase.
A partir de agora a disciplina muda de pergunta: não "que sistema falta?", mas "como transformar um protótipo funcional em um produto entregável?". Nenhum sistema novo de gameplay é introduzido no Módulo 4.
Metodologia: Studio Based Learning — professor como diretor técnico. Autonomia alta.
-->

---

## Objetivos da Semana

- Compreender Material Override/Unique Material como estratégia universal de parametrização, distinta de criar um material base novo por objeto
- Compreender MultiMeshInstance3D como ferramenta de composição de cena em escala
- Refatorar os materiais já existentes no projeto para uma estrutura base + Overrides, sem duplicar recursos
- Compor a densidade visual da zona externa com MultiMeshInstance3D, sem comprometer a performance
- Passar pelo Code Review de materiais e composição de cena (Rubrica 4)

<!--
Encontro 1 resolve a parametrização de um material por instância. Encontro 2 resolve a composição de cena em escala com elementos repetidos.
Referência: Godot Docs — Standard Material 3D; Unity Manual — Materials.
-->

---

<!-- _class: chapter -->

## Encontro 1

# Material Base e Material Override

<span class="chapter-number">01</span>

<!--
Encontro guiado. Retoma o Vertical Slice já jogável desde a Semana 11, sem alterar nenhuma mecânica — a única mudança desta semana é na camada de apresentação visual.
-->

---

## Agenda do Encontro 1

- Revisão do Encontro 2 da Semana 11 (Vertical Slice completo, encerramento da Unidade III) (15 min)
- Introdução: o problema da duplicação de materiais em um projeto de produção (20 min)
- Demonstração: material base + Material Override aplicado a um conjunto de objetos (30 min)
- Laboratório: cada grupo audita os próprios materiais e refatora ao menos um conjunto de objetos (50 min)
- Feedback e fechamento (20 min)

<!--
Ciclo pedagógico: Conceito → Demonstração → Construção → Desafio → Revisão. Nunca inverter.
Não há desafio de solução livre neste encontro — a refatoração parte diretamente do material já existente em cada projeto, criado desde a Semana 3.
-->

---

<!-- _class: question -->

# Por que criar um material novo para cada variação de cor de um mesmo objeto não escala?

Pense no custo de manutenção quando o material base precisa mudar globalmente.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que duplicar materiais multiplica o custo de manutenção e memória sem necessidade.
Erro comum: assumir que cada variação visual exige um recurso de material inteiro novo.
-->

---

## O Problema: Duplicação de Materiais

- Múltiplas instâncias de um mesmo tipo de objeto precisam de pequenas variações visuais (cor, brilho, textura)
- Recriar um material completo para cada variação multiplica custo de manutenção e memória
- Mesmo princípio já ensinado com Resources customizados na Semana 6 — agora aplicado ao domínio visual

<!--
Conceito universal: separar dado compartilhado (material base) de dado específico de instância (Override) — mesma lógica da separação Resource/instância da Semana 6.
Referência: Godot Docs — Standard Material 3D.
-->

---

## Material Base × Material Override / Unique Material

- **Material base** — definição compartilhada entre instâncias
- **Material Override / Unique Material** — cópia parametrizada aplicada a uma instância específica, sem duplicar a definição inteira
- Aplicado diretamente no `MeshInstance3D`, pelo menu de contexto do editor

<!--
Erro comum: confundir Override com criar um material novo do zero, duplicando a definição em vez de parametrizar uma cópia da instância.
Referência: Godot Docs — Standard Material 3D (seção Material Overrides).
-->

---

<!-- _class: comparison -->

## Parametrização de Material no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `StandardMaterial3D` como material base compartilhado
- Material Override / Unique Material — aplicado direto no `MeshInstance3D` pelo editor

</div>
<div class="col negative">

### Unity

- Material (asset) como base compartilhada entre `Renderer`s
- `MaterialPropertyBlock` via código, ou duplicar o asset — sem Override nativo do editor tão direto

</div>
</div>

<!--
Princípio universal idêntico: separar definição compartilhada de parametrização por instância evita duplicação em disco/memória e perda de sincronização.
A diferença está no fluxo de configuração, não em qualquer diferença conceitual relevante.
-->

---

## Demonstração — Material Base + Override Guiados

O que será construído:

- Um conjunto de objetos com materiais duplicados desnecessariamente (problema isolado, fora do projeto real)
- Refatoração para um material base único + Override parametrizado por instância

Por quê: fixar o padrão antes de tocar no projeto real de cada grupo.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Demonstrar primeiro o problema isolado, depois conduzir a auditoria guiada do projeto real de cada grupo.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a diferença entre múltiplos materiais duplicados e um material base único com Overrides por instância.
> Enquadramento: lado a lado — à esquerda vários objetos cada um com seu próprio material completo; à direita os mesmos objetos com um material base compartilhado e pequenos indicadores de Override.
> Elementos presentes: objetos de teste (cubos ou esferas simples), ícone de material duplicado (à esquerda) versus ícone de material base + Override (à direita).
> Destaque visual: contraste de cor entre a versão "antes" (vermelho, ineficiente) e "depois" (verde, parametrizada).
> Legenda sugerida: "Material base compartilhado + Override parametrizado evita duplicar a definição inteira do material."

<!--
Usar esta imagem na introdução do problema, antes da demonstração no editor.
-->

---

## Laboratório — Auditoria e Refatoração de Materiais

Cada grupo, no próprio projeto:

1. Audita os materiais já existentes desde a Semana 3, identificando duplicações evitáveis
2. Refatora ao menos um conjunto de objetos para material base + Override parametrizado por instância
3. Confere visualmente que a aparência dos objetos não mudou em relação ao Playtest anterior

<!--
Critério de sucesso: ao menos um conjunto de objetos reorganizado em material base + Override, sem duplicação, sem alteração perceptível no gameplay.
Dificuldade esperada: refatorar materiais que já funcionavam corretamente sem necessidade real, gastando tempo em otimização de baixo impacto — reforçar que a auditoria deve priorizar duplicação real.
Dificuldade esperada: alterar acidentalmente a aparência de objetos já validados em Playtests anteriores — reforçar checagem visual antes/depois.
-->

---

## Fechamento — Encontro 1

- Materiais existentes auditados e ao menos um conjunto refatorado para base + Override
- Nenhuma duplicação de materiais equivalentes
- Nenhuma alteração perceptível no gameplay ou nas mecânicas já funcionais
- Próximo passo: composição de cena com MultiMeshInstance3D, no Encontro 2

<!--
A refatoração conduzida aqui é parte do Code Review de encerramento da semana (Encontro 2).
-->

---

<!-- _class: chapter -->

## Encontro 2

# MultiMeshInstance3D e Code Review

<span class="chapter-number">02</span>

<!--
Retoma os materiais refatorados no Encontro 1, soma a composição de cena em escala com MultiMeshInstance3D e fecha com o Code Review (Rubrica 4).
-->

---

## Agenda do Encontro 2

- Revisão do Encontro 1 (materiais refatorados em base + Overrides) (15 min)
- Demonstração: MultiMeshInstance3D configurado sobre um terreno de teste (25 min)
- Laboratório: cada grupo compõe vegetação/elementos de cena na zona externa do próprio projeto (55 min)
- Code Review de materiais e composição de cena (Rubrica 4) (40 min)

<!--
Reservar tempo real para o Code Review — instrumento de avaliação formal deste encontro, não deve ser comprimido.
-->

---

<!-- _class: question -->

# Como compor centenas de plantas na zona externa sem instanciar centenas de Scenes?

Pense no custo de desenho de cada elemento individual em escala.

<!--
Discussão rápida, 2–3 minutos. Objetivo: levar a turma a perceber que instanciar Scenes individuais não escala para grandes quantidades de elementos repetidos.
Erro comum: assumir que mais elementos visuais sempre exigem mais Scenes instanciadas.
-->

---

## O Problema: Composição de Cena em Escala

- Uma cena de produção precisa de grandes quantidades de elementos visuais repetidos (vegetação, rochas, detalhes)
- Instanciar uma Scene por elemento é custoso em desempenho, em qualquer engine
- É preciso agrupar instâncias repetidas de uma mesma malha em uma única chamada de desenho

<!--
Conceito universal: trocar flexibilidade individual por escala e performance — mesma lógica por trás de qualquer Foliage Tool de qualquer engine.
Referência: Godot Docs — MultiMeshInstance3D (não copiar trechos, apenas resumir).
-->

---

## `MultiMeshInstance3D`

- Agrupa múltiplas instâncias de uma mesma malha em uma única chamada de desenho
- Elementos compostos não possuem lógica própria — apenas presença visual
- Ferramenta de composição de cena, não um sistema de gameplay

<!--
Erro comum: tratar os elementos compostos como se pudessem ter lógica individual (colisão específica, interação) — reforçar que MultiMeshInstance3D não substitui Scenes com lógica própria.
-->

---

<!-- _class: comparison -->

## Composição em Escala no Godot × Unity

<div class="columns">
<div class="col positive">

### Godot

- `MultiMeshInstance3D` — ferramenta de propósito geral, aplicável a qualquer composição repetida
- Uma única chamada de desenho para múltiplas instâncias

</div>
<div class="col negative">

### Unity

- Foliage Tool (Terrain Tools) — pensada especificamente para pintura de vegetação sobre terreno
- GPU Instancing — sobre `Renderer`s compartilhando o mesmo material

</div>
</div>

<!--
Princípio universal idêntico: agrupar instâncias repetidas em chamadas de desenho reduzidas, em vez de tratar cada elemento como objeto individual completo.
A diferença está no escopo da ferramenta, não no princípio.
-->

---

## Demonstração — MultiMeshInstance3D sobre Terreno de Teste

O que será construído:

- Um `MultiMeshInstance3D` configurado sobre um terreno de teste, com elementos do Kenney Nature Kit
- Ajuste de densidade e distribuição de instâncias

Por quê: fixar o padrão guiado antes de cada grupo compor a própria zona externa.

<!--
Não detalhar passo a passo aqui — sem Tutorial correspondente nesta semana (produção de tutoriais encerrada no Módulo 2, PEDAGOGICAL_RULES.txt).
Assets do Kenney Nature Kit já disponíveis no projeto desde a Semana 3.
-->

---

> **Imagem sugerida**
>
> Objetivo: mostrar a diferença de escala entre instanciar Scenes individuais e usar MultiMeshInstance3D para o mesmo conjunto de vegetação.
> Enquadramento: comparação lado a lado da mesma área externa do nível, antes (Scenes individuais, esparsa) e depois (MultiMeshInstance3D, densa).
> Elementos presentes: elementos de vegetação do Kenney Nature Kit (grama, arbustos, pedras) distribuídos sobre a zona externa do Vertical Slice.
> Destaque visual: indicador de número de chamadas de desenho (draw calls) menor na versão com MultiMeshInstance3D.
> Legenda sugerida: "MultiMeshInstance3D agrupa múltiplas instâncias da mesma malha em uma única chamada de desenho."

<!--
Usar esta imagem durante a demonstração, antes do laboratório.
-->

---

## Laboratório — Composição da Zona Externa

Cada grupo, na zona externa do próprio projeto:

1. Configura um `MultiMeshInstance3D` com elementos do Kenney Nature Kit
2. Ajusta densidade e distribuição, com liberdade de escolha entre os elementos já disponíveis
3. Observa o impacto no desempenho ao aumentar a densidade

<!--
Critério de sucesso: zona externa composta com MultiMeshInstance3D, mantendo desempenho estável, sem alteração de mecânica.
Dificuldade esperada: densidade excessiva sem observar impacto no desempenho — reforçar que densidade visual e performance são parte da mesma decisão.
Como diretor técnico, o professor orienta densidade e distribuição sem impor uma composição única para todos os grupos.
-->

---

## Arquitetura — Materiais e Composição de Cena

- Auditoria de materiais (Encontro 1) → material base + Override parametrizado por instância
- Composição de cena (Encontro 2) → `MultiMeshInstance3D` sobre a zona externa, elementos sem lógica própria
- Nenhum dos dois sistemas altera geometria, mecânica ou sistemas de gameplay já funcionais

<!--
Diagrama sugerido: Materiais existentes (Semana 3+) → Auditoria → Material base + Override. Em paralelo: Kenney Nature Kit → MultiMeshInstance3D → Zona externa composta.
Erro comum: confundir a camada de apresentação visual (materiais, composição) com sistemas de gameplay — nenhuma lógica é adicionada nesta semana.
-->

---

<!-- _class: exercise -->

# Code Review — Materiais e Composição de Cena

Apresente a refatoração de materiais do Encontro 1 e a composição de vegetação do Encontro 2, justificando as decisões de parametrização e otimização adotadas.

<div class="objectives">

**Entrega:** Code Review (Rubrica 4) — organização, nomenclatura, modularidade, reutilização e boas práticas.

</div>

<!--
Mesmo instrumento já aplicado nas Semanas 7 e 10, com ênfase deslocada para arquitetura e consistência, conforme progressão do Sistema de Avaliação para os Módulos 4 e 5.
Dificuldade esperada: dificuldade em justificar por que um material foi parametrizado com Override em vez de duplicado — reforçar a pergunta "por que este caminho e não outro?".
-->

---

## Boas Práticas — Materiais e Composição

- Priorizar material base + Override sobre duplicar a definição inteira do material
- Tratar densidade visual e desempenho como parte da mesma decisão, nunca etapas separadas
- Nunca atribuir lógica de gameplay a elementos compostos via MultiMeshInstance3D
- Checar visualmente antes/depois de cada refatoração de material compartilhado

<!--
Estes são exatamente os pontos observados no Code Review de encerramento da semana.
-->

---

## Fechamento — Encontro 2

- `MultiMeshInstance3D` configurado sobre a zona externa de cada grupo, com desempenho estável
- Materiais refatorados no Encontro 1 e composição de cena deste encontro apresentados no Code Review
- Nenhuma alteração de mecânica ou sistema de gameplay em toda a semana
- Próximo passo: áudio integrado a eventos de gameplay e Profiling/Optimization, na Semana 13

<!--
Dificuldade esperada: tratar o Code Review como avaliação apenas do resultado visual, sem justificar as decisões técnicas — reforçar que a justificativa faz parte do critério.
-->

---

## Resultado Esperado da Semana

- Materiais do Vertical Slice organizados em material base + Overrides parametrizados, sem duplicação
- Zona externa composta com elementos de vegetação/cena via `MultiMeshInstance3D`, com desempenho estável
- Nenhuma alteração de mecânica, sistema de gameplay ou geometria do Vertical Slice
- Code Review de materiais e composição de cena (Rubrica 4) concluído

<!--
Este resultado corresponde à linha Material Overrides/MultiMeshInstance3D do roadmap (PROJECT_ARCHITECTURE.md) e abre a Unidade IV.
-->

---

## Checklist da Semana

- [ ] Materiais existentes auditados, com ao menos um conjunto refatorado para base + Override
- [ ] Nenhuma duplicação de materiais equivalentes
- [ ] Zona externa composta via `MultiMeshInstance3D`, com desempenho estável
- [ ] Nenhuma alteração perceptível no gameplay ou nas mecânicas já validadas
- [ ] Code Review de materiais e composição de cena (Rubrica 4) concluído

<!--
Usar este checklist como roteiro de verificação rápida no início da Semana 13.
-->

---

## Próximos Passos — Semana 13

A Semana 13 dá continuidade ao polimento técnico do Módulo 4, integrando áudio a eventos de gameplay já existentes (interação, passos, ambiente) via `AudioStreamPlayer`, e introduzindo Profiling e Optimization como etapa obrigatória de produção antes da exportação final da Semana 14 — os materiais e a composição de cena refinados nesta semana serão parte direta do que o Profiler avaliará como possíveis gargalos técnicos.

Leitura recomendada: Godot Docs — Standard Material 3D; Unity Manual (consulta comparativa) — Materials; Kenney Assets (kenney.nl).

<!--
Referências completas: ver Plano de Aula Semana 12. Sem Tutorial correspondente — produção de tutoriais encerrada no Módulo 2 (PEDAGOGICAL_RULES.txt).
-->
