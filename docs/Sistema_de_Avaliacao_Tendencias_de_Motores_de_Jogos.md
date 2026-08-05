# Sistema de Avaliação
**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** Instituto Federal de Mato Grosso do Sul (IFMS) — Campus Dourados

## Filosofia de Avaliação

A disciplina não utiliza prova tradicional. A avaliação é processual, contínua e diretamente amarrada ao desenvolvimento incremental do Vertical Slice único do semestre. Ela acompanha a progressão metodológica descrita no Plano de Ensino e no Cronograma: Scaffolded Learning no Módulo 1, Studio Based Learning nos Módulos 2 e 4, Challenge Based Learning no Módulo 3 e Reverse Engineering no Módulo 5.

Avaliar, nesta disciplina, significa medir evolução, domínio conceitual, capacidade de aplicação prática e capacidade de justificar decisões técnicas — nunca apenas o resultado estético final. Um Vertical Slice visualmente simples, mas bem arquitetado e defendido tecnicamente, deve ser avaliado melhor do que um projeto visualmente elaborado sem organização, sem compreensão conceitual ou sem justificativa técnica.

Todos os instrumentos avaliativos derivam diretamente dos marcos já definidos no Cronograma (checkpoints, code reviews, playtests, feedbacks formais e apresentações das semanas 3, 5, 6, 7, 9, 10, 11, 12, 13, 14, 15, 16 e 17) e do Quadro de Avaliação Contínua nele estabelecido. Nenhum instrumento avaliativo é criado fora dessa estrutura.

A quantidade de orientação docente diminui ao longo do semestre e, em paralelo, o peso relativo da justificativa técnica e da capacidade de comparação arquitetural aumenta nos módulos finais, conforme já determinado no Plano de Ensino.

---

# Distribuição das notas

| Componente | Peso | Instrumentos no Cronograma |
|---|---|---|
| Desenvolvimento Semanal | 20% | Todas as semanas — participação, execução e autonomia em laboratório |
| Desafios Técnicos | 15% | Desafios propostos nas Semanas 1, 2, 4, 5, 6, 8, 9, 10, 11, 13 e 16 |
| Checkpoints | 10% | Semanas 3, 6 e 16 |
| Code Review | 15% | Semanas 7, 10, 12 e 14 |
| Playtest | 10% | Semanas 7, 11 e 14 |
| Apresentações | 10% | Showcases das Semanas 3 e 11; Apresentação Técnica Final da Semana 17 |
| Vertical Slice Final (Projeto) | 20% | Entrega consolidada da Semana 14 (build otimizado) e defesa arquitetural da Semana 17 |
| **Total** | **100%** | |

> **Nota sobre a Semana 7 e a Semana 15 na Rubrica 2:** os desafios de integração final da Semana 7 e de análise arquitetural da Semana 15 existem e são avaliados, mas deliberadamente **não** entram na lista de "Desafios Técnicos" (Rubrica 2) acima. A Semana 7 já é avaliada pela Rubrica 4 — Code Review (a integração de todos os desafios do Módulo 2 é exatamente o que o Code Review dessa semana verifica); a Semana 15 já é avaliada pelo instrumento de Feedback Formal (a proposta de decisão arquitetural revisitada é o próprio objeto desse feedback). Avaliar essas duas semanas também pela Rubrica 2 duplicaria a pontuação sobre o mesmo entregável.

### Justificativa de cada componente

**Desenvolvimento Semanal (20%).** É o componente de maior peso individual porque a disciplina é predominantemente prática e cada encontro segue o ciclo conceito → demonstração → construção → desafio → revisão. Medir apenas entregas pontuais ignoraria a consistência exigida por um projeto incremental único, no qual cada semana constrói sobre a anterior.

**Desafios Técnicos (15%).** Os desafios são o mecanismo pelo qual a autonomia é exercitada de forma crescente (do Módulo 1 ao Módulo 5). Avaliá-los separadamente do desenvolvimento semanal permite reconhecer especificamente a capacidade de resolver problemas com liberdade de solução, que é o núcleo do Challenge Based Learning do Módulo 3 e da autonomia alta do Módulo 4.

**Checkpoints (10%).** Os checkpoints (Semanas 3, 6 e 16) verificam se o progresso esperado para aquele ponto do semestre foi de fato atingido, funcionando como pontos de controle de risco para o projeto incremental. Peso moderado porque seu papel é diagnóstico, não somativo isolado.

**Code Review (15%).** Reflete a exigência de boas práticas do Godot (nomenclatura, modularidade, organização de Scenes/Scripts/Orchestrations) que a disciplina prioriza desde o CLAUDE.md do projeto. Peso alto porque a disciplina forma para postura profissional de estúdio, na qual a qualidade da implementação é tão relevante quanto o resultado visível.

**Playtest (10%).** Mede a experiência efetiva de jogo — funcionamento, usabilidade e clareza para o jogador — complementando o Code Review, que é uma avaliação de "caixa aberta". Peso menor que Code Review porque a disciplina não avalia qualidade artística nem quantidade de assets.

**Apresentações (10%).** Concentra-se nos showcases de encerramento de módulo e na apresentação técnica final, medindo comunicação técnica e domínio do projeto. Peso crescente de fato ao longo do semestre (ver seção de Coerência), culminando na Semana 17.

**Vertical Slice Final — Projeto (20%).** É o segundo maior componente porque sintetiza toda a disciplina: arquitetura, gameplay, qualidade técnica, uso correto dos recursos do Godot e capacidade de justificar decisões, tal como avaliado na Rubrica 7.

---

# Rubrica 1
## Desenvolvimento Semanal

**Aplicação:** todas as semanas de aula, com foco especial no encontro de "Desenvolvimento" do ciclo conceito → demonstração → construção → desafio → revisão.

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Participação** | Envolve-se ativamente em todas as etapas do encontro, contribui com perguntas e observações que avançam a discussão do grupo. | Participa de todas as etapas do encontro, com contribuições pontuais quando solicitado. | Participa das etapas principais, mas permanece passivo na maior parte do tempo. | Ausente ou desengajado na maior parte do encontro; não interage com o conteúdo ou com o grupo. |
| **Preparação** | Chega ao encontro com o projeto do Vertical Slice já organizado e revisado desde a aula anterior, pronto para construir sobre o que já existe. | Chega preparado, com pequenos ajustes pendentes que não comprometem o início da construção. | Precisa de tempo do início do encontro para organizar o que ficou pendente da aula anterior. | Não retoma o trabalho da aula anterior; o projeto está no mesmo estado ou em estado pior do que ao final do último encontro. |
| **Execução** | Implementa corretamente o conceito demonstrado, sem erros de configuração, replicando com precisão o padrão do Godot apresentado em aula. | Implementa corretamente o conceito, com pequenos erros que corrige de forma autônoma durante o encontro. | Implementa o conceito de forma parcial ou com erros que exigem intervenção direta do professor para correção. | Não consegue implementar o conceito demonstrado, mesmo com apoio do professor. |
| **Autonomia** | Resolve dúvidas de execução consultando a documentação oficial antes de solicitar ajuda, de forma coerente com o nível de autonomia esperado no módulo. | Tenta resolver de forma independente antes de pedir ajuda, mesmo sem sucesso completo. | Recorre à ajuda do professor ou dos colegas antes de tentar soluções próprias. | Depende integralmente da intervenção do professor para qualquer avanço, mesmo em tarefas já demonstradas. |
| **Evolução** | O trabalho da semana demonstra evolução clara sobre o estado do Vertical Slice na semana anterior, sem retrabalho de sistemas já concluídos. | O trabalho da semana avança o projeto, com necessidade pontual de retrabalho em sistemas anteriores. | O avanço da semana é mínimo ou depende fortemente de retrabalho do que já havia sido construído. | Não há avanço perceptível no projeto em relação à semana anterior, ou houve regressão funcional. |

### Guia para o Professor — Desenvolvimento Semanal

**Evidências a observar:** estado do projeto no início e no fim de cada encontro; histórico de versionamento (commits, backups) coerente com o cronograma de construção; capacidade de retomar o próprio trabalho sem reexplicação completa do professor.

**Erros comuns:** estudantes que recriam do zero elementos já prontos em vez de reutilizá-los (violação direta da regra "todo exercício pertence ao Vertical Slice"); dependência de anotações externas em vez de consulta à documentação oficial do Godot; confundir "estar presente" com "estar participando".

**Sugestões de feedback:** ao identificar baixa autonomia, direcionar o estudante à seção específica da documentação oficial antes de responder diretamente; elogiar explicitamente quando o estudante reutiliza um sistema anterior em vez de duplicar lógica; ao final de cada módulo, comunicar ao estudante em que ponto da progressão de autonomia (guiado → mentor → revisor) ele se encontra.

### Modelo de Avaliação — Desenvolvimento Semanal

**Turma:** _______________ **Módulo:** _____ **Semana:** _____ **Data:** ___ / ___ / ______
**Aluno(s)/Grupo avaliado:** ___________________________________________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Participação | ☐ | ☐ | ☐ | ☐ | |
| Preparação | ☐ | ☐ | ☐ | ☐ | |
| Execução | ☐ | ☐ | ☐ | ☐ | |
| Autonomia | ☐ | ☐ | ☐ | ☐ | |
| Evolução | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 20 → **Nota do componente (0–10) = (Soma ÷ 20) × 10 =** _____

**Observações / feedback ao estudante:**
_________________________________________________________________________
_________________________________________________________________________

---

# Rubrica 2
## Desafios Técnicos

**Aplicação:** desafios das Semanas 1, 2, 4, 5, 6, 8, 9, 10, 11, 13 e 16.

> **Nota:** os desafios da Semana 7 (integração final do Módulo 2) e da Semana 15 (análise arquitetural comparada) não são avaliados por esta rubrica, para evitar dupla pontuação sobre o mesmo entregável — a Semana 7 é avaliada pela Rubrica 4 (Code Review) e a Semana 15 pelo instrumento de Feedback Formal da própria semana (ver "Distribuição das notas").

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Solução proposta** | A solução vai além do mínimo exigido pelo desafio, demonstrando compreensão do conceito universal por trás dele, não apenas da execução no Godot. | A solução atende integralmente ao desafio proposto, com compreensão clara do conceito envolvido. | A solução atende parcialmente ao desafio, com lacunas conceituais que comprometem partes do resultado. | A solução não atende ao desafio proposto ou demonstra desconhecimento do conceito envolvido. |
| **Uso correto do Godot** | Utiliza os recursos do Godot indicados no módulo (ver GODOT_REFERENCE.md) de forma tecnicamente correta e apropriada ao problema. | Utiliza os recursos indicados corretamente, com pequenos desvios que não comprometem o funcionamento. | Utiliza os recursos de forma incorreta ou inadequada em pontos específicos, mas o resultado ainda funciona. | Utiliza os recursos de forma incorreta a ponto de comprometer o funcionamento ou contrariar boas práticas básicas da engine. |
| **Criatividade** | Propõe uma solução própria e diferenciada da demonstrada em aula, dentro da liberdade explicitamente oferecida pelo desafio. | Propõe variações pontuais sobre a solução demonstrada em aula. | Reproduz de forma quase idêntica a solução demonstrada em aula, com adaptações mínimas. | Não há tentativa de solução própria; o desafio é resolvido apenas copiando a demonstração sem adaptação ao contexto pedido. |
| **Organização** | Nomenclatura, estrutura de pastas e organização de Scenes/Scripts/Orchestrations seguem boas práticas do Godot 4.7 de forma consistente. | Organização adequada, com pequenas inconsistências de nomenclatura ou estrutura. | Organização confusa em partes da solução, dificultando a leitura por terceiros. | Ausência de organização; nomes padrão da engine não alterados, estrutura de pastas desorganizada. |
| **Funcionamento** | A solução funciona integralmente, sem bugs perceptíveis, em qualquer ordem de teste. | A solução funciona, com bugs menores que não comprometem a experiência central. | A solução funciona parcialmente ou apenas em condições específicas de teste. | A solução não funciona ou quebra o funcionamento de sistemas já existentes no Vertical Slice. |

### Guia para o Professor — Desafios Técnicos

**Evidências a observar:** se a solução do desafio foi de fato integrada ao Vertical Slice único (nunca um mini game isolado); se o estudante consegue explicar, mesmo brevemente, por que escolheu determinada abordagem entre as possíveis.

**Erros comuns:** implementar o desafio como sistema desconectado do projeto principal; copiar a solução demonstrada sem qualquer adaptação, mesmo quando o desafio pede explicitamente uma variação própria; ignorar boas práticas de nomenclatura por pressa em fazer "funcionar".

**Sugestões de feedback:** perguntar sempre "por que você escolheu esse caminho e não outro possível?" antes de validar o desafio; quando a solução for tecnicamente correta mas pouco original, reconhecer o acerto técnico e explicitamente convidar a uma segunda iteração mais autoral; usar os desafios de maior autonomia (Módulos 3 e 4) para calibrar o quanto o estudante já consegue caminhar sem demonstração prévia.

### Modelo de Avaliação — Desafios Técnicos

**Turma:** _______________ **Semana/Desafio:** _____________________ **Data:** ___ / ___ / ______
**Grupo avaliado:** _____________________ **Integrantes:** ___________________________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Solução proposta | ☐ | ☐ | ☐ | ☐ | |
| Uso correto do Godot | ☐ | ☐ | ☐ | ☐ | |
| Criatividade | ☐ | ☐ | ☐ | ☐ | |
| Organização | ☐ | ☐ | ☐ | ☐ | |
| Funcionamento | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 20 → **Nota do componente (0–10) = (Soma ÷ 20) × 10 =** _____

**Solução escolhida pelo grupo (breve descrição):**
_________________________________________________________________________

**Observações / feedback ao grupo:**
_________________________________________________________________________

---

# Rubrica 3
## Checkpoints

**Aplicação:** Semana 3 (1º build executável), Semana 6 (progresso do Módulo 2) e Semana 16 (preparação da apresentação final).

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Progresso esperado** | O progresso supera o esperado para o ponto do cronograma, incorporando elementos além do mínimo definido no módulo. | O progresso corresponde integralmente ao esperado para aquele ponto do cronograma. | O progresso está abaixo do esperado, mas ainda em ritmo recuperável dentro do módulo atual. | O progresso está muito abaixo do esperado, comprometendo a entrega de encerramento do módulo. |
| **Funcionalidades implementadas** | Todas as funcionalidades previstas até o checkpoint estão implementadas e integradas ao Vertical Slice único. | A maioria das funcionalidades previstas está implementada, com uma ou duas pendências claramente identificadas. | Parte relevante das funcionalidades previstas está ausente ou implementada apenas parcialmente. | A maior parte das funcionalidades previstas até o checkpoint está ausente. |
| **Qualidade técnica** | A implementação segue boas práticas do Godot 4.7 sem necessidade de retrabalho estrutural nos módulos seguintes. | A implementação é tecnicamente sólida, com ajustes pontuais recomendados para os próximos módulos. | A implementação apresenta problemas técnicos que exigirão retrabalho relevante nos próximos módulos. | A implementação apresenta problemas técnicos estruturais que comprometem a continuidade do projeto. |
| **Estabilidade** | O build/projeto roda sem falhas, travamentos ou erros visíveis durante toda a demonstração do checkpoint. | O build/projeto roda com falhas raras e não críticas. | O build/projeto apresenta falhas frequentes, mas ainda permite demonstração do progresso. | O build/projeto não roda ou trava de forma a impedir a demonstração do checkpoint. |

### Guia para o Professor — Checkpoints

**Evidências a observar:** comparação direta entre o que está descrito como "produto esperado" do módulo no Plano de Ensino/Cronograma e o que de fato está funcional no checkpoint; se o build da Semana 3 realmente exporta (Export), e não apenas roda no editor.

**Erros comuns:** apresentar funcionalidades "quase prontas" como se estivessem completas; não testar o build fora do ambiente do editor antes do checkpoint; ignorar pendências técnicas que se acumulam e só aparecem como problema estrutural em módulos futuros.

**Sugestões de feedback:** tratar o checkpoint como ponto de diagnóstico e correção de rota, não apenas de nota — comunicar claramente ao grupo o que precisa ser resolvido antes do próximo marco avaliativo (Semana 7, 11 ou 17, conforme o caso); reforçar que estabilidade tem peso equivalente a funcionalidade, pois um build instável invalida qualquer avaliação de conteúdo.

### Modelo de Avaliação — Checkpoints

**Turma:** _______________ **Checkpoint (Semana 3 / 6 / 16):** _____ **Data:** ___ / ___ / ______
**Grupo avaliado:** _____________________________________________________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Progresso esperado | ☐ | ☐ | ☐ | ☐ | |
| Funcionalidades implementadas | ☐ | ☐ | ☐ | ☐ | |
| Qualidade técnica | ☐ | ☐ | ☐ | ☐ | |
| Estabilidade | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 16 → **Nota do componente (0–10) = (Soma ÷ 16) × 10 =** _____

**Pendências a resolver antes do próximo marco avaliativo:**
_________________________________________________________________________

**Observações / feedback ao grupo:**
_________________________________________________________________________

---

# Rubrica 4
## Code Review

**Aplicação:** Semanas 7 (Módulo 2), 10 (inventário/interação), 12 (materiais/cena) e 14 (encerramento do build final).

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Organização dos Scripts/Orchestrations** | Grafos e scripts organizados, com comentários e agrupamento lógico (funções nomeadas, grafos de Orchestrator organizados) que tornam a leitura imediata. | Organizados na maior parte do projeto, com pontos isolados sem comentário ou agrupamento. | Funcionais, mas com organização inconsistente entre diferentes partes do projeto. | Desorganizados, sem comentários ou agrupamento, exigindo esforço significativo para compreensão. |
| **Nomenclatura** | Variáveis, funções, Scenes e assets seguem convenção de nomenclatura consistente e descritiva em todo o projeto. | Nomenclatura consistente na maior parte do projeto, com exceções pontuais. | Nomenclatura inconsistente ou pouco descritiva em partes relevantes do projeto. | Nomes padrão da engine mantidos (ex.: "Node2D", "Control1") ou nomenclatura sem qualquer padrão identificável. |
| **Modularidade** | Lógica dividida em funções/Components reutilizáveis, evitando duplicação de lógica entre Scenes. | Modularidade presente na maior parte do projeto, com duplicações pontuais e justificáveis. | Modularidade limitada, com duplicação relevante de lógica entre diferentes Scenes. | Ausência de modularidade; lógica duplicada extensivamente ou concentrada em uma única Scene monolítica. |
| **Reutilização** | Sistemas construídos em módulos anteriores são reutilizados de forma explícita e correta nos módulos seguintes. | Reutilização presente na maior parte do projeto, com alguma recriação evitável. | Reutilização parcial; partes do projeto recriam funcionalidades já existentes em outros sistemas. | Sistemas anteriores são ignorados e recriados do zero, contrariando a regra de reutilização entre módulos. |
| **Comunicação entre sistemas** | Sistemas se comunicam por padrões desacoplados (contrato Interactable, Signals) apropriados ao caso de uso. | Comunicação majoritariamente desacoplada, com referências diretas pontuais e justificáveis. | Comunicação com dependências diretas relevantes entre sistemas que poderiam ser desacopladas. | Comunicação por referências diretas e acopladas em toda a extensão do projeto, sem uso de contrato Interactable/Signals onde caberia. |
| **Boas práticas gerais** | Segue boas práticas atuais do Godot 4.7 de forma consistente (estrutura de pastas, Nodes apropriados, uso correto de Signals). | Segue boas práticas na maior parte do projeto, com desvios pontuais e não críticos. | Segue boas práticas de forma inconsistente, com desvios que afetam a manutenibilidade do projeto. | Não segue boas práticas básicas da engine, comprometendo a manutenibilidade do projeto. |

### Guia para o Professor — Code Review

**Evidências a observar:** abrir os scripts/Orchestrations ao vivo com o grupo e pedir que expliquem sua própria lógica; verificar se sistemas de módulos anteriores (contrato Interactable da Semana 5, Resource customizado da Semana 6) ainda existem e são usados, ou se foram silenciosamente substituídos por soluções redundantes.

**Erros comuns:** lógica de gameplay inteira dentro do script do Player, sem qualquer Component ou função auxiliar; uso de referências diretas (`get_node`/caminhos fixos) em cascata em vez do contrato Interactable já ensinado na Semana 5; nomenclatura copiada de tutoriais externos que não reflete o vocabulário do projeto do grupo.

**Sugestões de feedback:** conduzir o code review como diálogo técnico, pedindo que o próprio grupo identifique o que reorganizaria; priorizar feedback sobre acoplamento e duplicação, que são os problemas que mais se agravam ao longo de um projeto incremental de um único semestre; documentar decisões técnicas discutidas no code review para conferência no code review seguinte.

### Modelo de Avaliação — Code Review

**Turma:** _______________ **Semana (7 / 10 / 12 / 14):** _____ **Data:** ___ / ___ / ______
**Grupo avaliado:** _____________________________________________________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Organização dos Scripts/Orchestrations | ☐ | ☐ | ☐ | ☐ | |
| Nomenclatura | ☐ | ☐ | ☐ | ☐ | |
| Modularidade | ☐ | ☐ | ☐ | ☐ | |
| Reutilização | ☐ | ☐ | ☐ | ☐ | |
| Comunicação entre sistemas | ☐ | ☐ | ☐ | ☐ | |
| Boas práticas gerais | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 24 → **Nota do componente (0–10) = (Soma ÷ 24) × 10 =** _____

**Pontos a reorganizar até o próximo code review:**
_________________________________________________________________________

**Observações / feedback ao grupo:**
_________________________________________________________________________

---

# Rubrica 5
## Playtest

**Aplicação:** Semanas 7, 11 e 14.

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Funcionamento** | Todas as mecânicas jogáveis funcionam corretamente durante toda a sessão de playtest, sem necessidade de intervenção da equipe. | Mecânicas funcionam corretamente, com intervenção pontual da equipe em situações específicas e não recorrentes. | Mecânicas funcionam de forma inconsistente, exigindo intervenção frequente da equipe durante o playtest. | Mecânicas centrais não funcionam ou impedem a continuidade do playtest. |
| **Usabilidade** | O jogador consegue compreender e executar as ações principais sem explicação prévia da equipe. | O jogador compreende as ações principais com uma breve explicação inicial. | O jogador precisa de orientação contínua da equipe para progredir no playtest. | O jogador não consegue progredir mesmo com orientação contínua da equipe. |
| **Bugs** | Nenhum bug crítico observado; eventuais bugs visuais não afetam a jogabilidade. | Bugs presentes, mas contornáveis, sem impedir a conclusão do playtest. | Bugs relevantes que interrompem o fluxo de jogo em mais de uma ocasião. | Bugs críticos que impedem a conclusão do playtest ou quebram a experiência de forma irreversível. |
| **Feedback visual** | O jogo comunica claramente ao jogador o resultado de suas ações (dano, coleta, interação) por meio de retorno visual e/ou sonoro apropriado. | A maior parte das ações relevantes possui retorno visual/sonoro claro, com exceções pontuais. | Parte relevante das ações não possui retorno perceptível, gerando confusão ocasional no jogador. | Ausência praticamente total de retorno visual/sonoro às ações do jogador. |
| **Clareza da interface** | HUD e demais elementos de UI comunicam o estado do jogo de forma imediata e sem ambiguidade. | HUD comunica o estado do jogo com pequenas ambiguidades pontuais. | HUD presente, mas com informações confusas ou incompletas em relação ao estado real do jogo. | HUD ausente ou com informações que não correspondem ao estado real do jogo. |
| **Experiência do jogador** | O jogador relata compreensão clara do objetivo e da progressão, mesmo sem conhecer o projeto previamente. | O jogador compreende o objetivo geral, com dúvidas pontuais sobre progressão. | O jogador tem dificuldade para identificar o objetivo ou a progressão do jogo. | O jogador não consegue identificar o objetivo do jogo mesmo após a sessão completa. |

### Guia para o Professor — Playtest

**Evidências a observar:** reações do jogador que não é membro do grupo (idealmente colegas de outro grupo), não apenas o relato da própria equipe; frequência de intervenção manual da equipe durante a sessão.

**Erros comuns:** a própria equipe jogar o playtest em vez de observar um jogador externo; confundir "o jogo funciona para quem o desenvolveu" com "o jogo funciona para um jogador novo"; ignorar problemas de clareza de interface por já conhecerem o funcionamento internamente.

**Sugestões de feedback:** sempre que possível, cruzar grupos para que um teste o projeto do outro (como já previsto no playtest cruzado da Semana 14); registrar os bugs e pontos de confusão observados durante o playtest e cobrar sua correção no code review seguinte; lembrar a turma que qualidade artística e quantidade de assets não são critério — a avaliação é sobre funcionamento e clareza da experiência.

### Modelo de Avaliação — Playtest

**Turma:** _______________ **Semana (7 / 11 / 14):** _____ **Data:** ___ / ___ / ______
**Grupo avaliado:** _____________________ **Jogador(es) externo(s):** _______________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Funcionamento | ☐ | ☐ | ☐ | ☐ | |
| Usabilidade | ☐ | ☐ | ☐ | ☐ | |
| Bugs | ☐ | ☐ | ☐ | ☐ | |
| Feedback visual | ☐ | ☐ | ☐ | ☐ | |
| Clareza da interface | ☐ | ☐ | ☐ | ☐ | |
| Experiência do jogador | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 24 → **Nota do componente (0–10) = (Soma ÷ 24) × 10 =** _____

**Bugs/pontos de confusão observados (a corrigir até o próximo code review):**
_________________________________________________________________________

**Observações / feedback ao grupo:**
_________________________________________________________________________

---

# Rubrica 6
## Apresentações

**Aplicação:** Showcases das Semanas 3 e 11; Apresentação Técnica Final da Semana 17.

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Comunicação** | Apresentação clara, objetiva e adequada ao tempo disponível, sem leitura de slides ou anotações. | Apresentação clara, com apoio pontual em anotações, dentro do tempo disponível. | Apresentação com dificuldades de clareza ou ultrapassa significativamente o tempo disponível. | Apresentação confusa, desorganizada ou incompreensível para quem não conhece o projeto previamente. |
| **Demonstração** | O Vertical Slice é demonstrado ao vivo, sem falhas, cobrindo os sistemas relevantes daquele ponto do semestre. | O Vertical Slice é demonstrado ao vivo, com falhas menores contornadas pela equipe. | A demonstração ao vivo apresenta falhas relevantes ou é parcialmente substituída por vídeo/imagens estáticas. | Não há demonstração funcional ao vivo do projeto. |
| **Justificativas técnicas** | O grupo justifica tecnicamente cada decisão arquitetural relevante, relacionando-a aos conceitos universais estudados. | O grupo justifica a maioria das decisões técnicas, com alguma dificuldade em conectá-las aos conceitos universais. | O grupo descreve as decisões técnicas, mas sem justificá-las adequadamente. | O grupo não consegue justificar as decisões técnicas tomadas no projeto. |
| **Domínio do projeto** | Qualquer integrante do grupo consegue explicar qualquer parte do projeto, incluindo partes implementadas por colegas. | A maioria dos integrantes consegue explicar a maior parte do projeto. | Apenas parte do grupo consegue explicar o projeto; alguns integrantes desconhecem partes relevantes. | Apenas um integrante domina o projeto; os demais não conseguem responder sobre partes básicas. |
| **Capacidade de responder perguntas** | Responde a perguntas técnicas com segurança e profundidade, incluindo perguntas sobre alternativas não escolhidas. | Responde à maioria das perguntas técnicas com segurança. | Responde apenas a perguntas superficiais; tem dificuldade com perguntas técnicas mais específicas. | Não consegue responder às perguntas técnicas feitas sobre o próprio projeto. |

### Guia para o Professor — Apresentações

**Evidências a observar:** se a apresentação é conduzida por todo o grupo de forma equilibrada; se as justificativas mencionam explicitamente os conceitos universais e a comparação com Unity (e outros motores, quando pertinente), como exigido pela filosofia da disciplina.

**Erros comuns:** apresentação concentrada em um único integrante, mascarando desconhecimento dos demais; justificativas de decisões técnicas limitadas a "porque funcionou", sem relação com o conceito estudado; uso de vídeo pré-gravado no lugar de demonstração ao vivo sem justificativa técnica válida (ex.: build instável já identificado em checkpoint anterior).

**Sugestões de feedback:** distribuir perguntas entre diferentes integrantes do grupo durante a sessão de perguntas; na Semana 17, cobrar explicitamente a comparação arquitetural com Unity e o motor adicional escolhido pelo grupo na Semana 16; valorizar respostas que reconheçam limitações do próprio projeto tanto quanto respostas que defendam acertos.

### Modelo de Avaliação — Apresentações

**Turma:** _______________ **Apresentação (Semana 3 / 11 / 17):** _____ **Data:** ___ / ___ / ______
**Grupo avaliado:** _____________________ **Integrantes:** ___________________________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Comunicação | ☐ | ☐ | ☐ | ☐ | |
| Demonstração | ☐ | ☐ | ☐ | ☐ | |
| Justificativas técnicas | ☐ | ☐ | ☐ | ☐ | |
| Domínio do projeto | ☐ | ☐ | ☐ | ☐ | |
| Capacidade de responder perguntas | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 20 → **Nota do componente (0–10) = (Soma ÷ 20) × 10 =** _____

**Perguntas feitas ao grupo e qualidade das respostas:**
_________________________________________________________________________

**Observações / feedback ao grupo:**
_________________________________________________________________________

---

# Rubrica 7
## Vertical Slice Final

**Aplicação:** entrega consolidada da Semana 14 (build otimizado) e avaliação final integrada na Semana 17.

> Não avaliar qualidade artística. Não avaliar quantidade de assets.

| Critério | Excelente | Bom | Satisfatório | Insuficiente |
|---|---|---|---|---|
| **Arquitetura** | Arquitetura clara, com separação de responsabilidades coerente entre GameManager, SaveManager e demais sistemas construídos no semestre. | Arquitetura coerente na maior parte do projeto, com sobreposição pontual de responsabilidades entre sistemas. | Arquitetura funcional, mas com sobreposição relevante de responsabilidades entre sistemas que deveriam estar separados. | Arquitetura confusa ou inexistente; lógica concentrada sem separação de responsabilidades. |
| **Gameplay** | Todos os sistemas de gameplay construídos ao longo do semestre (interação, inventário, animação, IA, UI) estão integrados e funcionais em conjunto. | A maioria dos sistemas está integrada e funcional, com uma ou duas integrações incompletas. | Parte relevante dos sistemas funciona isoladamente, mas não está plenamente integrada ao fluxo de jogo. | Sistemas de gameplay não funcionam em conjunto ou apresentam falhas que impedem a experiência completa. |
| **Organização** | Estrutura de pastas, nomenclatura e organização de assets seguem um padrão consistente em todo o projeto. | Organização consistente na maior parte do projeto, com exceções pontuais. | Organização inconsistente em partes relevantes do projeto. | Ausência de organização perceptível na estrutura do projeto. |
| **Qualidade técnica** | Implementação segue boas práticas do Godot 4.7 de forma consistente, sem gargalos técnicos identificados no profiling da Semana 13. | Implementação tecnicamente sólida, com gargalos pontuais já identificados e parcialmente tratados. | Implementação com problemas técnicos relevantes, alguns não tratados após o profiling. | Implementação com problemas técnicos estruturais que comprometem a estabilidade do projeto. |
| **Polimento** | Ajustes finais (áudio integrado a eventos, feedback visual, transições) elevam a experiência de jogo de forma perceptível, sem depender de qualidade artística dos assets. | Ajustes finais presentes na maior parte da experiência, com lacunas pontuais. | Ajustes finais limitados a poucos pontos da experiência. | Ausência de ajustes finais; experiência idêntica a versões preliminares do projeto. |
| **Uso correto dos recursos do Godot** | Os recursos explorados no semestre (Input Map, contrato Interactable, Resource customizado, AnimationTree, Control nodes, Behavior Trees/LimboAI, Materials, etc.) são utilizados conforme suas finalidades documentadas. | Recursos utilizados corretamente na maior parte do projeto, com desvios pontuais de finalidade. | Recursos utilizados de forma parcialmente inadequada em relação à sua finalidade documentada. | Recursos utilizados de forma incorreta ou substituídos por soluções improvisadas que contrariam boas práticas básicas. |
| **Consistência** | O projeto mantém coerência visual, técnica e de gameplay entre os sistemas adicionados em diferentes módulos, sem partes que pareçam "descoladas" do restante. | O projeto é majoritariamente coerente, com uma ou duas partes que destoam do restante. | O projeto apresenta partes claramente desconectadas entre si, evidenciando falta de integração entre módulos. | O projeto parece uma colagem de sistemas desconectados, sem coerência entre os módulos. |
| **Documentação** | O projeto possui documentação técnica clara (decisões de arquitetura, sistemas implementados) suficiente para que outra pessoa compreenda o projeto sem o grupo presente. | Documentação presente e compreensível, com lacunas pontuais. | Documentação superficial, insuficiente para compreender decisões relevantes do projeto. | Documentação ausente ou inexistente. |
| **Exportação** | Build final exportado roda de forma estável fora do editor, em condições equivalentes às testadas na Semana 14. | Build exportado roda com falhas raras e não críticas fora do editor. | Build exportado roda com falhas frequentes fora do editor. | Build não exporta corretamente ou não roda fora do editor. |
| **Capacidade de explicar decisões** | O grupo explica e justifica qualquer decisão arquitetural do projeto, incluindo alternativas descartadas e comparação com Unity/outros motores. | O grupo explica a maioria das decisões arquiteturais, com justificativa técnica adequada. | O grupo descreve as decisões arquiteturais, mas com dificuldade de justificá-las tecnicamente. | O grupo não consegue explicar as decisões arquiteturais do próprio projeto. |

### Guia para o Professor — Vertical Slice Final

**Evidências a observar:** se o build da Semana 14 realmente corresponde ao que é apresentado na Semana 17, ou se houve mudanças não documentadas nesse intervalo; se a documentação técnica do grupo permite reconstruir o raciocínio de decisões tomadas em módulos anteriores (ex.: por que optaram por Interface em vez de herança na Semana 5).

**Erros comuns:** avaliar o Vertical Slice pela qualidade visual dos assets (contrariando explicitamente a regra desta rubrica); penalizar projetos simples que são, no entanto, tecnicamente sólidos e bem justificados; não verificar o empacotamento de fato, avaliando apenas a versão rodando no editor.

**Sugestões de feedback:** usar esta rubrica em conjunto com a Rubrica 6 (Apresentações) na Semana 17, já que arquitetura e capacidade de justificar decisões se demonstram principalmente na defesa oral; ao identificar falhas de arquitetura, relacioná-las a conceitos estudados em módulos específicos, ajudando o estudante a localizar exatamente onde a decisão poderia ter sido diferente; reforçar publicamente exemplos de justificativa técnica bem construída, pois isso eleva o padrão da turma para a apresentação final.

### Modelo de Avaliação — Vertical Slice Final

**Turma:** _______________ **Etapa (Semana 14 / Semana 17):** _____ **Data:** ___ / ___ / ______
**Grupo avaliado:** _____________________ **Integrantes:** ___________________________________

| Critério | Excelente (4) | Bom (3) | Satisfatório (2) | Insuficiente (1) | Nota |
|---|:---:|:---:|:---:|:---:|:---:|
| Arquitetura | ☐ | ☐ | ☐ | ☐ | |
| Gameplay | ☐ | ☐ | ☐ | ☐ | |
| Organização | ☐ | ☐ | ☐ | ☐ | |
| Qualidade técnica | ☐ | ☐ | ☐ | ☐ | |
| Polimento | ☐ | ☐ | ☐ | ☐ | |
| Uso correto dos recursos do Godot | ☐ | ☐ | ☐ | ☐ | |
| Consistência | ☐ | ☐ | ☐ | ☐ | |
| Documentação | ☐ | ☐ | ☐ | ☐ | |
| Exportação | ☐ | ☐ | ☐ | ☐ | |
| Capacidade de explicar decisões | ☐ | ☐ | ☐ | ☐ | |

**Soma:** _____ / 40 → **Nota do componente (0–10) = (Soma ÷ 40) × 10 =** _____

> Lembrete: não pontuar qualidade artística nem quantidade de assets em nenhum critério acima.

**Observações / feedback ao grupo:**
_________________________________________________________________________
_________________________________________________________________________

---

# Coerência com a Progressão Metodológica

A aplicação das rubricas acima não é estática: o peso relativo dos critérios dentro de cada rubrica deve acompanhar a evolução de autonomia da disciplina, definida no Plano de Ensino e no PEDAGOGICAL_RULES.txt.

| Momento do semestre | Módulos | Ênfase avaliativa dominante | Critérios que recebem mais atenção |
|---|---|---|---|
| Início | Módulo 1 (Semanas 1–3) | Reprodução e compreensão | Execução correta (Rubrica 1), uso correto do Godot (Rubrica 2), funcionamento e estabilidade (Rubrica 3) |
| Meio | Módulos 2 e 3 (Semanas 4–11) | Adaptação e resolução de problemas | Autonomia e evolução (Rubrica 1), solução proposta e criatividade (Rubrica 2), comunicação entre sistemas (Rubrica 4), funcionamento no playtest (Rubrica 5) |
| Final | Módulos 4 e 5 (Semanas 12–17) | Autonomia, arquitetura e tomada de decisão | Arquitetura, consistência e capacidade de explicar decisões (Rubrica 7), justificativas técnicas (Rubrica 6), boas práticas consolidadas (Rubrica 4) |

Esta progressão não altera os pesos percentuais definidos na seção "Distribuição das notas" — ela orienta *onde* o professor deve concentrar a atenção qualitativa dentro de cada critério das rubricas, em cada momento do semestre, mantendo a avaliação coerente com o aumento contínuo de autonomia previsto para a disciplina.
