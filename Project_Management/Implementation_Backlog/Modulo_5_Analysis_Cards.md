# Cards de Análise — Milestone MS-5 (Semanas 15–17)

**Nenhum destes cards é um Implementation Card no sentido de código.** O Cronograma é explícito: "Nenhum sistema novo é adicionado ao Vertical Slice" (Semana 15) e "nenhuma alteração de código é esperada nesta semana" (regra reforçada em Semana 15, item "Dificuldades Esperadas"). Por isso, o template abaixo substitui "Arquivos Esperados"/"Implementação" por "Entregável"/"Método", mantendo Objetivo, Documentos, Testes (aqui, "Verificação"), Critérios de Aceite e Definition of Done.

---

## IC-VS15-01 — Engenharia Reversa: TPS Demo e Platformer 2D Demo

**Objetivo:** ler a arquitetura de dois projetos oficiais do Godot e traçar paralelos explícitos com o Vertical Slice construído nos Milestones 1–4.

**Contexto:** abre a Unidade V — muda de "produzir" para "analisar".

**Documentos de Referência:** Godot Demo Projects (github.com/godotengine/godot-demo-projects); `PROJECT_ARCHITECTURE.md` §12 (base de comparação, a expandir).

**Entregável:** documento/apresentação curta listando, para cada padrão relevante do TPS Demo e do Platformer 2D Demo (Signals, Autoload, Resource customizado, Components, State Machine/Behavior Tree), se o próprio projeto resolveu de forma igual, similar ou diferente — e por quê.

**Método:**
1. Ler a estrutura de cenas e scripts do TPS Demo (gameplay framework: player, câmera, armas, inimigos).
2. Traçar paralelo direto com decisões do próprio Vertical Slice desde o Módulo 1.
3. Repetir para o Platformer 2D Demo.
4. Identificar ao menos uma decisão arquitetural própria que poderia ser refeita à luz da análise.

**Restrições:** nenhuma alteração de código do Vertical Slice nesta semana — apenas registro escrito da análise.

**Verificação:** o documento cobre pelo menos um paralelo por sistema principal do projeto (Signals, Autoload, contrato Interactable, Resource, Component, Behavior Tree).

**Critérios de Aceite:**
- [ ] Paralelos traçados para os dois Demo Projects.
- [ ] Ao menos uma decisão arquitetural própria marcada como "refazível", com justificativa.

**Definition of Done:** Feedback formal (Semana 15) recebido.

**Dependências:** Blocked By: IC-VS14-01 (o projeto precisa estar consolidado para servir de base de comparação — não depende de DC-02/DC-05 estarem resolvidos, pois a análise é sobre o que existe, não sobre o que falta). Blocks: IC-VS16-01.

**Story Points:** 3

---

## IC-VS16-01 — Quadro Comparativo Godot × Unity × Motor Adicional

**Objetivo:** consolidar, em um único quadro, a comparação sistemática feita ao longo do semestre.

**Contexto:** primeira etapa da Semana 16.

**Documentos de Referência:** `PROJECT_ARCHITECTURE.md` §12 (tabela-base, a expandir, nunca substituir).

**Entregável:** quadro comparativo cobrindo gameplay framework, animação, IA, UI e pipeline de produção, com base nos sistemas realmente construídos (não em teoria genérica).

**Método:**
1. Revisar `PROJECT_ARCHITECTURE.md` §12 como ponto de partida.
2. Para cada sistema construído nos Milestones 1–4, confirmar/expandir a linha correspondente com o que foi de fato implementado no próprio projeto (não apenas o conceito genérico).
3. Escolher um motor adicional (Unreal Engine, O3DE ou Stride) e ampliar a comparação para ele, com justificativa da escolha.

**Restrições:** expandir a tabela existente, nunca reescrevê-la do zero ou contradizer o que já está registrado.

**Verificação:** cada linha da tabela expandida cita um sistema real do projeto, não uma generalização.

**Critérios de Aceite:**
- [ ] Quadro comparativo Godot × Unity completo.
- [ ] Motor adicional escolhido e comparação ampliada, com justificativa.

**Definition of Done:** insumo pronto para IC-VS16-02.

**Dependências:** Blocked By: IC-VS15-01. Blocks: IC-VS16-02.

**Story Points:** 3

---

## IC-VS16-02 — Checkpoint de Preparação da Apresentação Final 🔴

**Objetivo:** preparar o roteiro da apresentação técnica final.

**Contexto:** segunda etapa da Semana 16 — encerra a Unidade V antes da apresentação.

**Documentos de Referência:** todos os anteriores, de forma sintética.

**Entregável:** roteiro com recorte do Vertical Slice a apresentar, decisões arquiteturais centrais a justificar, e a comparação entre motores (IC-VS16-01) como fio condutor.

**Método:**
1. Definir o recorte do Vertical Slice mais relevante para demonstrar em tempo limitado.
2. Listar as decisões arquiteturais centrais a justificar (mínimo 3).
3. Integrar o quadro comparativo (IC-VS16-01) como fio condutor da narrativa da apresentação.

**Restrições:** o roteiro deve ser sobre o projeto real, não uma descrição genérica de "o que é Godot".

**Verificação:** o roteiro permite a qualquer pessoa do projeto conduzir a apresentação sem decorar um texto.

**Critérios de Aceite:**
- [ ] Roteiro de apresentação com recorte, decisões e comparação definidos.

**Definition of Done:** Checkpoint de preparação (Semana 16 🔴) entregue.

**Dependências:** Blocked By: IC-VS16-01. Blocks: IC-VS17-01.

**Story Points:** 2

---

## IC-VS17-01 — Apresentação Técnica Final 🔴

**Objetivo:** apresentar e defender tecnicamente o Vertical Slice completo. **Encerra o projeto.**

**Contexto:** última semana — sem conteúdo novo, apenas demonstração e defesa.

**Documentos de Referência:** síntese de toda a documentação consultada no semestre.

**Entregável:** apresentação ao vivo (ou vídeo/build) do Vertical Slice, cobrindo conceito universal → implementação Godot → comparação com outro motor, para cada decisão central listada em IC-VS16-02.

**Método:**
1. Demonstrar o Vertical Slice ao vivo, seguindo o roteiro de IC-VS16-02.
2. Justificar cada decisão arquitetural central, relacionando-a ao conceito universal por trás dela.
3. Responder perguntas técnicas com base no projeto real, incluindo alternativas não escolhidas.

**Restrições:** nenhum recurso novo do Godot é aberto no editor durante a apresentação — o projeto é evidência, não objeto de nova exploração.

**Verificação:** capacidade de responder, sem roteiro decorado, por que cada decisão central foi tomada.

**Critérios de Aceite:**
- [ ] Vertical Slice demonstrado do início ao fim.
- [ ] Decisões arquiteturais justificadas com o vocabulário conceito → implementação → transferência.

**Definition of Done:** apresentação técnica final realizada. Fim do plano de produção.

**Dependências:** Blocked By: IC-VS16-02. Blocks: nenhuma (última carta do plano).

**Story Points:** 3
