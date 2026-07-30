# Manual do Professor
**Disciplina:** Tendências de Motores de Jogos (IN46A) — Curso Superior de Tecnologia em Jogos Digitais
**Instituição:** Instituto Federal de Mato Grosso do Sul (IFMS) — Campus Dourados

Este manual é o guia operacional de quem vai ministrar a disciplina. Ele não repete o conteúdo do Plano de Ensino, do Cronograma, dos Planos de Aula, dos Tutoriais ou das Rubricas — todos esses documentos já existem e são normativos. O que este manual faz é explicar **como usar** esses documentos no dia a dia da disciplina, e como pensar as decisões que eles não cobrem explicitamente.

Ele foi escrito para servir qualquer professor que assuma a disciplina, em qualquer momento: alguém que nunca a ministrou, alguém com pouca experiência em Unreal Engine, alguém vindo de Unity, ou alguém assumindo a turma no meio do semestre.

---

## 1. Filosofia da Disciplina

### 1.1 Por que Unreal Engine

A disciplina não ensina Unreal Engine. Ela usa a Unreal Engine 5.6 como **estudo de caso** para ensinar conceitos que existem em qualquer motor de jogos moderno: composição de entidades, gameplay framework, comunicação desacoplada entre sistemas, dados de design separados de lógica, animação por máquina de estados, IA baseada em árvores de decisão, interface em tempo real, otimização e empacotamento. A Unreal foi escolhida porque expõe esses conceitos de forma explícita e nomeada (Actor/Component, GameMode/GameState, Blueprint Interfaces, Behavior Tree), o que facilita apontar para o conceito universal por trás do botão.

Se em algum momento uma aula vira "como usar tal recurso da Unreal" sem nunca responder "que problema universal isso resolve, e como outro motor resolveria o mesmo problema", a aula perdeu o eixo da disciplina. Esse é o teste mais simples para saber se uma aula está no caminho certo.

### 1.2 Por que um único Vertical Slice

A disciplina desenvolve um único projeto incremental (nome de trabalho *O Templo Esquecido*, ver PROJECT_ARCHITECTURE.md) em vez de minigames isolados por tema. Isso existe porque a disciplina não quer ensinar recursos da engine em vitrine — quer ensinar como um projeto real integra sistemas construídos em momentos diferentes, sem descartar nada. Cada nova semana pousa sobre o que já existe: o inventário da Semana 10 reutiliza os itens modelados na Semana 6, o combate da Semana 11 reutiliza o HealthComponent construído na Semana 8. Um professor que introduz um exercício desconectado do Vertical Slice está, na prática, contradizendo o projeto pedagógico da disciplina.

### 1.3 Por que a disciplina é totalmente prática

A carga teórica é mínima e nunca expositiva pura: PEDAGOGICAL_RULES.txt proíbe aulas exclusivamente expositivas e exige que todo encontro siga o ciclo conceito → demonstração → construção → desafio → revisão. A justificativa é dupla: os estudantes já chegam com base de Programação, Game Design, Unity, IA e Computação Gráfica (não é uma disciplina introdutória), e o objetivo final — autonomia para aprender qualquer motor — só se desenvolve fazendo, não ouvindo.

### 1.4 Por que o foco está em conceitos universais

Toda aula deveria, mesmo que implicitamente, responder quatro perguntas: qual conceito universal está sendo ensinado, como ele é implementado na Unreal, como seria implementado na Unity, e como esse conhecimento se transfere para outro motor. Esse é o critério mais importante para julgar se um material (slide, tutorial, desafio) está alinhado com a disciplina — não a qualidade da explicação da Unreal isoladamente, mas se ela está ancorada num conceito que sobrevive fora da Unreal.

### 1.5 Como a Unreal é utilizada como estudo de caso

Isso não é uma abstração vaga: PROJECT_ARCHITECTURE.md já define exatamente que sistema da Unreal ensina que conceito, e o Cronograma já embute a comparação com Unity (e, quando pertinente, Godot, O3DE, Stride ou CryEngine) em cada semana. O papel do professor não é decidir se compara — a comparação já está prevista — e sim conduzir essa comparação com profundidade adequada ao momento do semestre, sem deixá-la virar um comentário de rodapé nem um desvio de meia aula.

---

## 2. Organização da Disciplina

A disciplina tem cinco módulos, cada um com metodologia e nível de autonomia próprios. Os detalhes completos (objetivos, sistemas, produto esperado) estão no Plano de Ensino e no Cronograma — aqui apenas a lógica de progressão que amarra os cinco módulos entre si.

| Módulo | Semanas | Metodologia dominante | Autonomia | Produto |
|---|---|---|---|---|
| 1 — Aprender a Ferramenta | 1–3 | Scaffolded Learning | Muito baixa | Primeiro build executável |
| 2 — Construir Sistemas | 4–7 | Studio Based Learning | Baixa | Gameplay funcional |
| 3 — Resolver Problemas | 8–11 | Challenge Based Learning | Média | Vertical Slice jogável |
| 4 — Produzir como Pequeno Estúdio | 12–14 | Studio Based Learning (diretor técnico) | Alta | Vertical Slice final empacotado |
| 5 — Comparar Arquiteturas | 15–17 | Reverse Engineering | Muito alta | Apresentação técnica final |

A variável que muda de módulo para módulo não é o conteúdo técnico isolado — é **quanto o professor resolve pelo estudante**. No Módulo 1, o professor demonstra e o estudante replica passo a passo (por isso existem Tutoriais para os Módulos 1 e 2 — ver seção 5.2). No Módulo 3, o professor apresenta um problema e cada grupo propõe sua própria solução; não existe mais um caminho único demonstrado a ser replicado. No Módulo 5, o professor deixa de ensinar sistemas novos e passa a atuar como interlocutor de uma análise que o próprio estudante conduz.

Um erro comum de professor novo na disciplina é manter o mesmo nível de condução do Módulo 1 até o Módulo 3 ou 4, "porque funciona". Isso contradiz diretamente a progressão pedagógica da disciplina e priva o estudante do desenvolvimento de autonomia que é o objetivo central do curso.

---

## 3. Como Utilizar os Materiais

Os documentos do projeto não são peças soltas — formam uma cadeia, e cada um depende do anterior:

```
Plano de Ensino
   ↓ (define módulos, metodologia, avaliação geral)
Cronograma
   ↓ (distribui o Plano de Ensino em 17 semanas concretas)
Plano de Aula (por semana)
   ↓ (detalha os dois encontros daquela semana do Cronograma)
Tutorial (apenas Módulos 1 e 2)
   ↓ (passo a passo de apoio para o estudante executar o que o Plano de Aula descreve)
Slides (todas as semanas)
   ↓ (material de apresentação em aula, alinhado ao Plano de Aula)
Rubricas (Sistema de Avaliação)
   (avaliam o que foi de fato produzido, nos marcos já definidos no Cronograma)
```

- **Plano de Ensino**: a constituição da disciplina. Define objetivos, metodologias por módulo, critérios gerais de avaliação e bibliografia oficial. Não muda de semestre para semestre a menos que o PPC do curso mude.
- **Cronograma**: a tradução do Plano de Ensino em 17 semanas concretas, com pergunta norteadora, documentação de referência, conteúdo de cada encontro e marcos avaliativos. É o documento que o professor deveria ter aberto o tempo todo durante o semestre.
- **Plano de Aula (semanal)**: expande cada linha do Cronograma em objetivos de aprendizagem, conceitos fundamentais, comparação com Unity, preparação necessária, cronograma minuto a minuto e dificuldades esperadas. É o documento de referência principal para preparar cada encontro.
- **Tutorial**: só existe para os Módulos 1 e 2 (ver seção 5.2 sobre o motivo). É material de apoio ao estudante, não ao professor — mas o professor deve conhecê-lo, porque o laboratório assume que o estudante o está seguindo.
- **Slides**: material de apresentação, alinhado ao conteúdo do Plano de Aula da mesma semana. Não substituem a preparação do professor — são apoio visual, não roteiro de fala.
- **Rubricas (Sistema de Avaliação)**: aplicadas apenas nos marcos já definidos no Cronograma e no Quadro de Avaliação Contínua. O professor não cria novos instrumentos avaliativos fora dessa estrutura.

Além desses, três documentos de contexto ficam por trás de toda decisão de conteúdo, mesmo sem aparecer explicitamente em cada material: COURSE_CONTEXT.txt (perfil dos estudantes e filosofia geral), PEDAGOGICAL_RULES.txt (regras de condução pedagógica) e PROJECT_ARCHITECTURE.md (referência técnica única do Vertical Slice — todo Blueprint, Component e convenção de nomenclatura mencionados em qualquer Plano de Aula vêm de lá). Se um Plano de Aula parecer contradizer PROJECT_ARCHITECTURE.md em algum detalhe técnico, o documento de arquitetura prevalece; o problema deve ser sinalizado para correção do material, nunca resolvido ad hoc improvisando uma arquitetura paralela em aula.

---

## 4. Fluxo de Cada Semana

### Antes da aula

- Ler o Plano de Aula da semana (não apenas revisar de memória — os detalhes de cronograma minuto a minuto e dificuldades esperadas mudam de semana para semana).
- Se a semana pertence ao Módulo 1 ou 2, executar o Tutorial correspondente você mesmo, do início ao fim, no seu próprio projeto de referência — não apenas ler. Isso expõe travas que só aparecem na prática (versão de plugin, nome de asset renomeado, passo que pressupõe algo não dito).
- Revisar os Slides da semana e ajustá-los mentalmente ao ritmo real da turma (uma turma mais lenta ou mais rápida que a média muda quanto tempo cada slide "aguenta" em aula).
- Conferir o estado do projeto de referência: se você mantém um projeto de demonstração próprio (recomendado), garanta que ele está no estado esperado ao final da semana anterior, pronto para a demonstração desta semana.

### Durante a aula

- Apresentar o conceito antes de qualquer implementação — nunca inverter essa ordem (regra explícita do PEDAGOGICAL_RULES.txt).
- Demonstrar ao vivo, não apenas narrar. Mesmo no Módulo 4/5, onde a autonomia é alta, alguma demonstração pontual costuma ser necessária quando um problema técnico específico aparece.
- Acompanhar o laboratório circulando entre grupos, não permanecendo à frente da sala. É no laboratório que aparecem os erros de execução que a Rubrica 1 avalia.
- Fechar com feedback — mesmo que informal, mesmo que não seja um instrumento avaliativo formal daquela semana. O ciclo conceito → demonstração → construção → desafio → revisão exige revisão em todo encontro, não só nas semanas com instrumento formal.

### Após a aula

- Registrar dificuldades observadas (mesmo que informalmente) — elas alimentam o "Guia para o Professor" da rubrica aplicável e ajudam a calibrar a próxima intervenção com aquele grupo específico.
- Se a semana teve instrumento avaliativo formal (checkpoint, code review, playtest, feedback formal ou apresentação), preencher o modelo de avaliação da rubrica correspondente enquanto a memória do encontro ainda está fresca — não adiar para o fim de semana.
- Preparar a próxima semana com base na seção "Preparação para a Próxima Semana" do Plano de Aula atual, que já aponta a dependência direta entre uma semana e a seguinte.

---

## 5. Condução das Aulas

### 5.1 Equilíbrio entre demonstração, laboratório, desafio e feedback

O tempo de cada encontro (2h15) é limitado e o cronograma minuto a minuto de cada Plano de Aula já propõe uma divisão. A lógica por trás dessa divisão é constante ao longo do semestre: a fundamentação conceitual deve ser breve e afiada (raramente mais de 20–25 minutos), a demonstração deve ser suficiente para que o laboratório funcione sem o professor precisar refazer a explicação a cada grupo, e o laboratório deve ocupar a maior fatia do tempo — é onde a Rubrica 1 (Desenvolvimento Semanal) é de fato observável.

Quando ajudar e quando permitir que o estudante resolva sozinho: a régua é a autonomia esperada para o módulo em curso (seção 2). No Módulo 1, um estudante travado numa configuração básica deve receber ajuda direta e rápida — insistir em "descubra sozinho" nesse ponto não ensina autonomia, apenas frustra sem propósito pedagógico. No Módulo 3 em diante, a primeira resposta a uma dúvida de execução deveria ser uma pergunta de volta ("o que a documentação oficial diz sobre isso?", "o que você já tentou?"), reservando a solução direta para quando o estudante já tentou e não avançou.

### 5.2 Por que tutoriais só existem até o Módulo 2

Esta é uma regra estrutural do projeto, não uma preferência estilística: tutoriais passo a passo só são produzidos como material complementar para os Módulos 1 e 2. Nesses módulos a metodologia é Scaffolded/Studio Based Learning com autonomia baixa — o tutorial libera o tempo do encontro para discutir conceito e comparação com Unity em vez de narrar clique a clique, e dá suporte ao estudante fora de aula. A partir do Módulo 3 (Challenge Based Learning), um roteiro fechado entregaria a solução e esvaziaria o desafio — a ausência de tutorial não é uma lacuna a preencher, é a própria condição da metodologia. Um professor que sinta falta de um "tutorial da Semana 9" e cogite escrever um por conta própria deve primeiro reler esta seção: produzir esse material contradiz diretamente a arquitetura pedagógica da disciplina.

---

## 6. Laboratório

Boas práticas para o momento de laboratório, que é onde a maior parte do tempo de aula é investida:

- Estimular experimentação: um estudante que tenta uma variação não demonstrada e erra aprendeu mais sobre o sistema do que um que só replicou com precisão. Isso é coerente com o critério "Criatividade" da Rubrica 2.
- Evitar resolver tudo para os estudantes. Uma boa métrica pessoal: se você está resolvendo o mesmo tipo de problema em três grupos diferentes na mesma aula, pare e faça uma intervenção coletiva rápida em vez de repetir a solução individualmente três vezes.
- Incentivar consulta à documentação oficial antes de perguntar ao professor — é um critério explícito da Rubrica 1 (Autonomia) e uma regra geral do PEDAGOGICAL_RULES.txt.
- Incentivar depuração: quando um Blueprint não funciona, a primeira pergunta ao estudante deveria ser "o que você já verificou?", não a solução.
- Promover colaboração entre grupos, especialmente porque o Vertical Slice de cada grupo evolui em paralelo — soluções diferentes para o mesmo desafio (ver seção 7) são material de discussão coletiva valioso.

---

## 7. Desafios

Todo desafio proposto no Cronograma já existe com um grau de liberdade definido (ver a coluna de desafios em cada semana do Plano de Aula). O papel do professor é:

- **Apresentar o desafio depois da demonstração**, nunca antes — o ciclo da disciplina não se inverte.
- **Adaptar a dificuldade** apenas dentro do espaço já previsto: um grupo mais avançado pode ser estimulado a ir além do mínimo do desafio (o que já é reconhecido pelo critério "Excelente" da Rubrica 2), mas o desafio em si não deve ser trocado por outro fora do Cronograma.
- **Oferecer pistas por aproximação**, não por solução: a primeira pista deveria apontar para o conceito ("qual sistema já construído resolve um problema parecido?"), a segunda para a documentação oficial, e só a terceira para um caminho técnico mais específico — nunca a solução completa.
- **Evitar entregar a solução**: se um grupo trava completamente e o tempo de aula está acabando, prefira reduzir o escopo do desafio para aquele grupo específico (uma variação mais simples da mesma ideia) a entregar a implementação pronta. Entregar a solução invalida o critério "Criatividade" da Rubrica 2 e frustra o objetivo do desafio.

---

## 8. Playtests

- **Quando realizar**: nos marcos já definidos no Cronograma — Semanas 7, 11 e 14. Não é recomendável improvisar playtests fora desses pontos como substituto de avaliação formal, mas nada impede sessões informais de teste entre grupos em qualquer semana como prática de laboratório.
- **Como organizar**: sempre que possível, cruzar grupos — um grupo joga o projeto do outro. A Rubrica 5 é explícita: a própria equipe jogar o próprio playtest é um erro comum que compromete a avaliação de usabilidade.
- **O que observar**: não apenas se o jogo funciona, mas se um jogador que nunca viu o projeto entende o que fazer sem explicação prévia da equipe. Registre bugs e pontos de confusão reais, não o que a equipe alega que "só acontece às vezes".
- **Como conduzir o feedback**: separar claramente o que é bug (a corrigir até o próximo Code Review) do que é falta de clareza de interface ou de progressão (a discutir como problema de design, não de implementação).

---

## 9. Code Reviews

- **Frequência**: Semanas 7 (Módulo 2), 10 (inventário/interação), 12 (materiais/cena) e 14 (encerramento do build final) — já fixadas no Cronograma e na Rubrica 4.
- **Critérios**: organização dos Blueprints, nomenclatura, modularidade, reutilização de sistemas anteriores e comunicação desacoplada entre sistemas (Interfaces, Event Dispatchers) — nessa ordem de atenção, não apenas "funciona ou não funciona".
- **Foco da revisão**: priorizar organização, modularidade, legibilidade e boas práticas de Blueprint sobre o simples funcionamento. Um Blueprint que funciona mas está inteiro dentro do Event Graph do Character, sem componentes nem funções nomeadas, deve receber nota mais baixa do que um Blueprint modular com uma pequena falha funcional pontual — é exatamente o que a Rubrica 4 pede.
- **Boas práticas de condução**: abrir os Blueprints ao vivo com o grupo e pedir que expliquem sua própria lógica, em vez de o professor navegar sozinho pelo projeto. Verificar explicitamente se sistemas de módulos anteriores (Interfaces da Semana 5, Data Tables da Semana 6) ainda existem e são reutilizados, ou se foram silenciosamente substituídos — esse é o erro mais comum e mais grave em um projeto incremental de um único semestre.

---

## 10. Avaliação

### Como utilizar as rubricas

Cada uma das sete rubricas do Sistema de Avaliação está amarrada a marcos específicos do Cronograma — nenhuma rubrica deve ser aplicada fora desses marcos, e nenhum instrumento avaliativo novo deve ser criado fora da estrutura já definida (ver "Distribuição das notas" no Sistema de Avaliação).

### Quando aplicar

Use o Quadro de Avaliação Contínua do Cronograma como referência rápida de qual instrumento cai em qual semana. Antes de cada marco, releia o "Guia para o Professor" da rubrica correspondente — ele lista evidências a observar e erros comuns específicos daquele instrumento, que mudam bastante entre, por exemplo, um Checkpoint (foco em progresso e estabilidade) e uma Apresentação (foco em comunicação e domínio do projeto).

### Como registrar evidências

Os "Modelos de Avaliação" ao final de cada rubrica já são o formulário de registro — preencha-os no próprio momento do encontro sempre que possível, não de memória depois. Para a Rubrica 1 (Desenvolvimento Semanal), que se aplica todo encontro, não é necessário preencher o modelo completo toda semana para cada grupo; uma nota qualitativa breve por grupo já sustenta a avaliação processual, reservando o formulário completo para os momentos em que a nota for questionada ou para uma amostra periódica.

### Como fornecer feedback

Trate cada instrumento como diagnóstico antes de nota: a seção "Sugestões de feedback" de cada rubrica orienta isso especificamente (por exemplo, na Rubrica 3 — Checkpoints —, comunicar claramente o que precisa ser resolvido antes do próximo marco, não apenas atribuir uma nota).

### Como acompanhar a evolução do estudante

A ênfase avaliativa muda ao longo do semestre mesmo sem mudar os pesos percentuais (ver "Coerência com a Progressão Metodológica" no Sistema de Avaliação): no início, o que mais importa é reprodução correta e funcionamento; no meio, autonomia e resolução de problemas; no final, arquitetura e capacidade de justificar decisões. Comunicar ao estudante, ao final de cada módulo, em que ponto da progressão de autonomia (guiado → mentor → revisor) ele se encontra é uma prática recomendada explicitamente pela Rubrica 1.

---

## 11. Dificuldades Comuns por Módulo

### Módulo 1 (Semanas 1–3)

- **Técnicas**: estudantes vindos de Unity tentam mapear literalmente conceitos de um motor para o outro (procurar uma "Assets folder" idêntica, esperar um Inspector idêntico). Intervenção: reforçar que a equivalência é funcional, não literal.
- **Conceituais**: confundir "aprender Unreal" com o objetivo real da disciplina (aprender conceitos transferíveis). Intervenção: retomar explicitamente a pergunta "isso existiria em qualquer motor?" sempre que a aula correr risco de virar tutorial de botões.
- **Pedagógicas**: professor tentado a acelerar demais por já perceber estudantes com boa base de Unity. Intervenção: lembrar que a autonomia muito baixa do Módulo 1 é proposital — mesmo estudantes experientes precisam da fundamentação conceitual antes da prática, porque é ela que sustenta a comparação entre motores mais adiante.

### Módulo 2 (Semanas 4–7)

- **Técnicas**: uso de referências diretas (Cast to) em cascata em vez das Interfaces recém-ensinadas (Semana 5). Intervenção: redirecionar para o padrão de Interface antes de aceitar a solução acoplada.
- **Conceituais**: dificuldade em enxergar por que GameMode/GameState/PlayerController/GameInstance precisam ser papéis separados, já que a Unity não tem equivalente direto e formal. Intervenção: usar exemplos concretos do próprio Vertical Slice para cada papel, evitando explicação puramente abstrata.
- **Pedagógicas**: grupos recriando do zero elementos já prontos em vez de reutilizá-los, violando a regra "todo exercício pertence ao Vertical Slice". Intervenção: no Code Review da Semana 7, verificar explicitamente a reutilização de sistemas de semanas anteriores.

### Módulo 3 (Semanas 8–11)

- **Técnicas**: lógica de animação, HUD ou IA implementada de forma monolítica, sem componentes reutilizáveis (ex.: HealthComponent duplicado entre BP_Player e BP_Enemy em vez de compartilhado). Intervenção: Code Review da Semana 10 e Playtest da Semana 11 são os pontos formais para capturar isso, mas vale sinalizar informalmente antes.
- **Conceituais**: dificuldade em decompor um problema aberto (metodologia Challenge Based Learning) depois de dois módulos guiados. Intervenção: pistas por aproximação (seção 7), nunca solução direta — é o momento em que a autonomia precisa começar a aparecer de fato.
- **Pedagógicas**: professor tentado a demonstrar a solução completa de um desafio "para adiantar", contradizendo a metodologia do módulo. Intervenção: lembrar que a autonomia média do Módulo 3 é o próprio objeto de avaliação da Rubrica 2 nesse momento do semestre.

### Módulo 4 (Semanas 12–14)

- **Técnicas**: problemas de performance não identificados antes do Profiling da Semana 13, aparecendo tarde demais para correção confortável. Intervenção: sugerir profiling informal já na Semana 12.
- **Conceituais**: confundir polimento técnico com qualidade artística — a disciplina explicitamente não avalia isso (Rubrica 7). Intervenção: reforçar que o critério é "eleva a experiência sem depender de qualidade artística dos assets", nunca "está bonito".
- **Pedagógicas**: grupos atrasados chegando ao empacotamento da Semana 14 sem terem testado o build fora do editor antes. Intervenção: cobrar explicitamente um teste de build empacotado como pré-requisito do Playtest cruzado.

### Módulo 5 (Semanas 15–17)

- **Técnicas**: nenhuma — nenhum sistema novo é implementado neste módulo (ver PROJECT_ARCHITECTURE.md, seção 6).
- **Conceituais**: dificuldade em ir além de descrever decisões técnicas e efetivamente justificá-las em termos de conceitos universais. Intervenção: nas Semanas 15 e 16, exigir explicitamente a pergunta "por que essa decisão e não outra possível?" antes de aceitar a análise como completa.
- **Pedagógicas**: apresentação final concentrada em um único integrante do grupo, mascarando desconhecimento dos demais (erro comum já listado na Rubrica 6). Intervenção: distribuir perguntas entre integrantes durante a sessão de perguntas da Semana 17.

---

## 12. Gerenciamento do Projeto

**Como manter o Vertical Slice consistente**: PROJECT_ARCHITECTURE.md é a referência única de nomenclatura, estrutura de pastas e arquitetura — qualquer dúvida sobre "como isso deveria se chamar" ou "onde isso deveria morar" se resolve consultando esse documento, não decidindo caso a caso em aula.

**Como evitar retrabalho**: a causa mais comum de retrabalho é um grupo ignorar um sistema já construído e recriar uma versão paralela (ex.: um segundo sistema de vida em vez de reutilizar o HealthComponent). O Code Review é o ponto de controle formal para isso, mas revisões informais durante o laboratório evitam que o problema só apareça semanas depois.

**Quando refatorar**: dentro do semestre, refatoração só se justifica quando o sistema atual impede a construção do próximo módulo (ex.: um GameMode mal estruturado que trava a integração da Semana 5). Refatoração por preferência estética, sem impacto funcional, não deve consumir tempo de laboratório às custas do conteúdo da semana.

**Como lidar com estudantes atrasados**: identificar o quanto antes se o atraso é de execução (technical debt recuperável no próprio módulo) ou de compreensão conceitual (que se propaga e se agrava a cada módulo seguinte, já que a disciplina é cumulativa). Atrasos de compreensão merecem intervenção individual fora do ritmo do laboratório coletivo, o quanto antes.

**Como recuperar estudantes que perderam aulas**: por causa da natureza cumulativa do Vertical Slice, a recuperação nunca deve ser "pular para o conteúdo de hoje" — o estudante precisa fechar a lacuna estrutural da semana perdida antes, ainda que de forma condensada (o Tutorial da semana perdida, quando existir, é o material mais direto para isso). Priorizar sempre a reconstrução dos sistemas de que as semanas seguintes dependem diretamente, verificando as dependências listadas no roadmap do PROJECT_ARCHITECTURE.md.

---

## 13. Comparações entre Motores

A comparação com Unity já está embutida em praticamente todo Plano de Aula do semestre; com Godot, O3DE, Stride ou CryEngine ela aparece quando pertinente, mais concentrada no Módulo 5. Ao conduzir qualquer comparação:

- Ancorar sempre no conceito universal primeiro, e só então mostrar a implementação específica de cada motor — nunca o inverso.
- Evitar transformar a comparação em inventário de diferenças de interface ("aqui o botão fica à esquerda, lá fica à direita"). O que importa é a decisão arquitetural por trás (ex.: Unreal formaliza GameMode como classe nativa; Unity depende de convenção própria do time — ver PROJECT_ARCHITECTURE.md, seção 12).
- Não aprofundar além do que o Plano de Aula da semana já prevê. Algumas comparações são deliberadamente breves ("não aprofundar — será retomado na Semana X") porque serão revisitadas com mais profundidade adiante; respeitar esse ritmo evita gastar tempo de laboratório em uma discussão que ainda não tem base suficiente.
- No Módulo 5, a comparação deixa de ser pontual e passa a ser o próprio objeto de estudo — aí sim cabe aprofundamento maior, incluindo motores além de Unity conforme a escolha de cada grupo na Semana 16.

---

## 14. Recursos Recomendados

Consulte REFERENCES.md para a lista completa; a organização abaixo é apenas um resumo de uso rápido, seguindo a mesma ordem de prioridade já definida naquele documento (documentação oficial da Epic em primeiro lugar, depois Learning Library, Samples, Unreal Community Wiki, livros, documentação da Unity e comunidade).

- **Documentação**: Unreal Engine Documentation (dev.epicgames.com) como primeira fonte sempre; Unity Manual/Unity Learn e Godot Documentation para comparação.
- **Samples**: Lyra Starter Game, Stack O Bot, Content Examples e Action RPG Sample — usados principalmente no Módulo 5, mas úteis como referência de boas práticas em qualquer módulo.
- **Vídeos**: canais oficiais e da comunidade (Unreal Engine, Mathew Wadstein, PrismaticaDev, Ryan Laley, LeafBranchGames, Smart Poly) — sempre como apoio complementar, nunca substituindo a documentação oficial.
- **Livros**: a bibliografia oficial do PPC (Computação Gráfica, Real-Time Rendering, Level Up!, Regras do Jogo) deve ser citada integralmente no Plano de Ensino; livros técnicos complementares (Game Engine Architecture, Game Programming Patterns, Design Patterns) são apoio de leitura para o professor, não bibliografia do estudante.
- **Comunidade**: Tom Looman, BenUI e Unreal Community Wiki para dúvidas técnicas específicas de Blueprint e boas práticas.
- **Ferramentas**: Kenney Assets (CC0) como única fonte de arte do projeto — nunca produção artística própria dos estudantes, conforme PROJECT_ARCHITECTURE.md.

---

## 15. Checklists

### Antes do semestre

- [ ] Ler o Plano de Ensino, o Cronograma completo e o PROJECT_ARCHITECTURE.md do início ao fim.
- [ ] Preencher a tabela de "Ancoragem no Calendário Acadêmico" do Cronograma com o calendário letivo vigente do IFMS, identificando feriados e eventos que colidem com encontros.
- [ ] Confirmar Unreal Engine 5.6 instalada e testada no laboratório (não apenas na máquina do professor).
- [ ] Preparar um projeto de referência próprio, seguindo a estrutura de pastas de PROJECT_ARCHITECTURE.md, para demonstrações.
- [ ] Revisar o "Plano de contingência" do Cronograma e identificar, no seu calendário real, quais encontros compressíveis e quais não-compressíveis coincidem com datas de risco (feriados, eventos).

### Antes de cada módulo

- [ ] Reler a seção do módulo no Plano de Ensino e no roadmap de PROJECT_ARCHITECTURE.md.
- [ ] Confirmar que o produto esperado do módulo anterior está de fato consolidado antes de avançar.
- [ ] Revisar a rubrica que será aplicada no encerramento do módulo.

### Antes de cada semana

- [ ] Ler o Plano de Aula da semana (os dois encontros).
- [ ] Se Módulo 1 ou 2, executar o Tutorial da semana pessoalmente antes de levá-lo à turma.
- [ ] Revisar os Slides da semana.
- [ ] Preparar os assets/arquivos indicados na seção "Preparação do Professor" do Plano de Aula.

### Antes de cada encontro

- [ ] Confirmar o estado do projeto de demonstração (deve refletir o final do encontro anterior).
- [ ] Revisar o cronograma minuto a minuto do encontro e ajustar mentalmente ao ritmo real da turma.
- [ ] Ter a documentação oficial relevante (link de REFERENCES.md) aberta e pronta para consulta em aula.

### Após cada encontro

- [ ] Registrar dificuldades observadas, mesmo informalmente.
- [ ] Se houve instrumento avaliativo formal, preencher o modelo de avaliação correspondente.
- [ ] Verificar a seção "Preparação para a Próxima Semana" do Plano de Aula atual.

### Final do módulo

- [ ] Aplicar a rubrica de encerramento (Checkpoint, Code Review, Playtest ou Apresentação, conforme a semana).
- [ ] Comunicar a cada grupo em que ponto da progressão de autonomia ele se encontra.
- [ ] Confirmar que nenhum sistema do módulo ficou pendente antes de iniciar o módulo seguinte.

### Final do semestre

- [ ] Conferir que o build final empacotado (Semana 14) corresponde ao apresentado na Semana 17, sem mudanças não documentadas.
- [ ] Aplicar a Rubrica 7 (Vertical Slice Final) em conjunto com a Rubrica 6 (Apresentações) na Semana 17.
- [ ] Consolidar as notas de todos os componentes conforme os pesos da seção "Distribuição das notas" do Sistema de Avaliação.
- [ ] Registrar, para uso em semestres futuros, quais adaptações de ritmo ou conteúdo funcionaram ou não com esta turma.

---

## 16. FAQ

**E se um estudante/grupo terminar antes do previsto?**
Direcione para os elementos "além do mínimo" já previstos nos critérios "Excelente" das rubricas relevantes (Rubrica 2, por exemplo, já prevê uma solução que vai além do exigido). Não introduza conteúdo de semanas futuras fora de ordem — isso quebra a progressão de dependências do roadmap.

**E se vários estudantes ficarem atrasados?**
Trate como sinal de que o ritmo da semana precisa ser recalibrado, não apenas como problema individual. Consulte o "Plano de contingência" do Cronograma para saber quais partes daquela semana são compressíveis, e considere redistribuir conteúdo dentro do próprio módulo antes de considerar adiar uma entrega.

**Quando devo mostrar a solução de um desafio?**
Só depois que o grupo já tentou de forma genuína e o tempo de aula está se esgotando — e mesmo assim, prefira reduzir o escopo do desafio para aquele grupo a entregar a implementação pronta (ver seção 7).

**Posso adaptar os desafios?**
Sim, dentro do grau de liberdade já previsto em cada desafio do Cronograma — por exemplo, ajustar a dificuldade para cima para um grupo mais avançado. Não é recomendável substituir um desafio inteiro por outro fora do Cronograma, porque cada desafio tem correspondência direta com o roadmap de PROJECT_ARCHITECTURE.md.

**E se a Unreal apresentar problemas técnicos durante a aula (crash, erro de compilação, plugin quebrado)?**
Tenha sempre um projeto de referência próprio pronto para demonstração, independente do estado dos projetos dos estudantes. Se o problema afetar a turma inteira (ex.: erro de uma versão específica do Editor), documente o contorno encontrado — ele provavelmente se repetirá em semestres futuros com a mesma versão da engine.

**O que fazer caso um conteúdo não caiba no tempo previsto?**
Consulte primeiro o "Plano de contingência" do Cronograma: alguns encontros são identificados como compressíveis, outros explicitamente não devem ser comprimidos (os que concentram instrumentos avaliativos de encerramento de módulo). Comprimir um encontro compressível é preferível a atropelar um encontro de encerramento.

**Um estudante pode propor ampliar o escopo do Vertical Slice (nova mecânica, sistema mais complexo)?**
Não. O escopo é fixo desde o Módulo 1 (PROJECT_ARCHITECTURE.md, seção 4) e a lista de itens "Fora do Escopo" (multiplayer, GAS, Mass AI, C++ avançado, entre outros) nunca deve ser incorporada, independentemente do interesse de um grupo específico — extensões de escopo comprometem a viabilidade do projeto dentro do semestre.

**Por que não existe tutorial para as semanas do Módulo 3 em diante?**
Ver seção 5.2 — é uma decisão estrutural, não uma lacuna. Produzir um tutorial passo a passo para essas semanas contradiz a metodologia de Challenge Based Learning que rege o módulo.

---

## 17. Adaptações

**Turmas menores** (poucos grupos): há mais tempo de acompanhamento individual por grupo em cada laboratório; aproveite para aprofundar o feedback qualitativo (Rubrica 1) em vez de apenas cobrir mais conteúdo no mesmo tempo.

**Turmas maiores** (muitos grupos): priorize intervenções coletivas quando o mesmo erro aparecer em múltiplos grupos (ver seção 6), e considere estender ligeiramente o tempo de laboratório às custas da fundamentação teórica nas semanas em que o conceito já for familiar à maioria.

**Laboratórios com computadores mais lentos**: a Semana 3 (Nanite/Lumen) e o Módulo 4 (otimização) são os pontos mais sensíveis a hardware limitado. Considere, nessas semanas, demonstrar em uma máquina de referência mais potente (se disponível) e ajustar as expectativas de qualidade visual do Vertical Slice de cada grupo — sem nunca usar isso como critério de avaliação, já que a Rubrica 7 explicitamente não avalia qualidade artística.

**Estudantes com diferentes níveis de experiência prévia** (ex.: alguns com mais prática em Unity do que outros): use a comparação Unreal-Unity já prevista em cada semana como ponte para os estudantes mais experientes em Unity, mas nunca assuma esse nível como piso da turma — a fundamentação conceitual de cada semana deve continuar partindo do zero em Unreal, coerente com o público-alvo descrito em COURSE_CONTEXT.txt.

Nenhuma dessas adaptações deve alterar os objetivos da disciplina, o escopo do Vertical Slice ou os marcos avaliativos já fixados no Cronograma — apenas o ritmo e a ênfase de condução.

---

*Manual do Professor — Disciplina Tendências de Motores de Jogos, IFMS Campus Dourados. Deve ser lido em conjunto com o Plano de Ensino, o Cronograma, PROJECT_ARCHITECTURE.md e o Sistema de Avaliação, que permanecem os documentos normativos da disciplina.*
