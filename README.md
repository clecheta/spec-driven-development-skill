# SDD — Spec Driven Development

Agent skill that turns a product conversation into tracker items and the documents a team needs before code. You talk in your own language; the agent answers in that language. Headings inside the Tech Spec and the Product Spec stay in Portuguese.

This page is the human guide. `SKILL.md` is what the agent follows. English first, português do Brasil abaixo.

## English

### Install

Put this repository where the agent loads skills, with `SKILL.md` at the skill root:

| Scope | Path |
|-------|------|
| Every project on this machine | `~/.cursor/skills/sdd/` |
| One repository | `<project>/.cursor/skills/sdd/` |

Open a new chat afterward.

### What the project must have

Every mode except `create-adr` stops until the project contains `.cursor/rules/issue-tracker.mdc`. That file is the only source of project facts. State these, in prose or frontmatter:

| Fact | What to write |
|------|----------------|
| `tracker` | `gitlab` today. The bridge is `references/trackers/gitlab.md`. |
| Project path or id | The id the bridge sends (GitLab full path, e.g. `group/project`). |
| Area labels | How cards are classified (repo, module, or the equivalent). |
| Queue signals | The real label names for **Backlog**, **Tech Spec**, **Product Spec**, and **architecture**. |
| Assignee policy | Who is assigned on every write. Usual choice: the authenticated user. |

Optional: a base URL for human links, paths to product docs used when drafting, notes about MCP limits, `adr_dir`, and `adr_format` (`md` or `mdc`). When `adr_dir` or `adr_format` is set, it wins over folder discovery.

A GitLab MCP must already be connected. The skill calls the tools named in the bridge. It does not scan the tool catalog and it does not call the GitLab REST API.

Design depth for mode `architecture` follows the companion skill `feature-architecture` when that skill is installed. This skill still owns the comment on the item and the `architecture` label.

### What to say

Card, issue, work item, ticket, story, bug, task, epic, and incident are the same object (and so are the Portuguese names). Name the mode or describe the job.

| You want | Example | What happens |
|----------|---------|--------------|
| Capture an idea or bug | “Create a card: …” | Searches open items. On a likely duplicate, asks whether to complement that card or create a new one. Shows a draft and waits. Creates with **Backlog** plus area labels, or edits the existing description. A complement does not re-apply Backlog. |
| Tech Spec | “Refine #42” | Asks until the goal is clear, fills **POR QUE / O QUE / COMO**, waits, posts a comment, adds **Tech Spec**. Title and description stay as they are. |
| Product Spec | “Write the product spec for #42” | Asks until problem, bet (metric from X to Y by a date), success criteria, how to measure, and minimum scope are clear. About one page. Waits, then comments and adds **Product Spec**. |
| Architecture | “Architecture for #42” or “arch #42” | Phase 1 ends only when you approve the restated understanding. Phase 2 ends only when you approve the design. Then it comments and adds **architecture**. Suggests an ADR only when the decision should outlive the card. |
| ADR | “Create an ADR: we will …” | Finds this repo’s ADR folder and style. Refuses trivia, churn, and implementation detail. Draft, your approval, then one file. If a card id is in play, comments the relative path. No queue label. |
| Read | “Read #42” or paste the URL | Loads title, state, labels, description, and comments verbatim. Writes nothing. |
| Comment | “Comment on #42: …” | Posts one comment as soon as the item and the text are clear. |
| Still needed? | “Check #42 against the code” | Reads the card, searches local repos, posts a table (**Corrigido**, **Parcial**, **Aberto**, **Inconclusivo**) and a verdict. May recommend closing. Leaves the card open. |

Give an id (`42`, `#42`) or a tracker URL when the item already exists. Free text, `@files`, folders, and links are valid input on create, refine, spec, architecture, and ADR.

### Order

```text
create → (spec?) → (refine?) → architecture
         ↘ refine ↗
```

`spec` and `refine` are optional, in either order, and either may be skipped. When both `refine` and `architecture` run, refine comes first. `read`, `comment`, and `check` work at any time. `create-adr` sits outside this sequence.

A new card can go straight to architecture. The agent does not chain the next mode unless you ask.

### What it leaves alone

It does not implement code, close cards, or move columns past the four queue labels. It never applies `interação::humano`, `dev::ok`, or `ready4Dev`. On the current GitLab bridge, milestone, start date, and item-to-item links are skipped; the confirmation says so. Related cards are cited by id in the description.

### Map of this repo

| Path | Role |
|------|------|
| `SKILL.md` | Procedure the agent follows |
| `references/modes/` | One file per mode. `arch` uses `architecture.md` |
| `references/trackers/gitlab.md` | Exact MCP calls. A new tracker is another file here with the same operation names |
| `references/rule-contract.md` | Fields of `issue-tracker.mdc` |
| `assets/` | Templates for Tech Spec, Product Spec, and ADR |

ADR files land in the project that owns the decision. The agent reuses an existing set (`adr-*.mdc`, `adr-*.md`, `ADR-*.md`, `NNNN-*.md`) under `.cursor/rules/architecture/`, `docs/adr/`, `docs/decisions/`, `docs/architecture/decisions/`, or `adr/`. With no set, it asks once and defaults to `docs/adr/NNNN-slug.md`. One decision per file. Date comes from the file timestamp.

License: proprietary, internal use only.

---

## Português

### Instalar

Coloque este repositório onde o agente carrega skills, com `SKILL.md` na raiz da skill:

| Alcance | Caminho |
|---------|---------|
| Todos os projetos desta máquina | `~/.cursor/skills/sdd/` |
| Um repositório | `<projeto>/.cursor/skills/sdd/` |

Abra um chat novo em seguida.

### O que o projeto precisa ter

Todo modo, exceto `create-adr`, para até o projeto ter `.cursor/rules/issue-tracker.mdc`. Esse arquivo é a única fonte de fatos do projeto. Declare o seguinte, em prosa ou frontmatter:

| Fato | O que escrever |
|------|----------------|
| `tracker` | `gitlab` hoje. A ponte é `references/trackers/gitlab.md`. |
| Caminho ou id do projeto | O id que a ponte envia (caminho completo no GitLab, ex.: `group/project`). |
| Rótulos de área | Como os cards são classificados (repo, módulo ou equivalente). |
| Sinais de fila | Os nomes reais dos rótulos **Backlog**, **Tech Spec**, **Product Spec** e **architecture**. |
| Política de responsável | Quem é atribuído em toda escrita. O usual: o usuário autenticado. |

Opcional: URL base para links humanos, caminhos da documentação de produto usada na redação, notas sobre limites do MCP, `adr_dir` e `adr_format` (`md` ou `mdc`). Se `adr_dir` ou `adr_format` estiver definido, vale mais que a descoberta de pasta.

Um MCP de GitLab já precisa estar conectado. A skill chama as ferramentas nomeadas na ponte. Ela não varre o catálogo de ferramentas e não chama a API REST do GitLab.

A profundidade de desenho do modo `architecture` segue a skill companheira `feature-architecture`, quando ela está instalada. Esta skill continua dona do comentário no item e do rótulo `architecture`.

### O que dizer

Card, issue, item de trabalho, ticket, história, bug, tarefa, épico e incidente são o mesmo objeto. Nomeie o modo ou descreva o trabalho.

| Você quer | Exemplo | O que acontece |
|-----------|---------|----------------|
| Capturar ideia ou bug | “Cria um card: …” | Busca itens abertos. Se houver duplicata provável, pergunta se complementa aquele card ou cria outro. Mostra o rascunho e espera. Cria com **Backlog** e rótulos de área, ou edita a descrição existente. Complementar não reaplica Backlog. |
| Tech Spec | “Refina o #42” | Pergunta até o objetivo ficar claro, preenche **POR QUE / O QUE / COMO**, espera, publica um comentário e adiciona **Tech Spec**. Título e descrição permanecem. |
| Product Spec | “Escreve a spec de produto do #42” | Pergunta até ficarem claros o problema, a aposta (métrica de X para Y num prazo), os critérios de sucesso, como medir e o escopo mínimo. Cerca de uma página. Espera, comenta e adiciona **Product Spec**. |
| Arquitetura | “Arquitetura do #42” ou “arch #42” | A fase 1 só termina quando você aprova o entendimento reescrito. A fase 2 só termina quando você aprova o desenho. Aí comenta e adiciona **architecture**. Sugere um ADR só quando a decisão deve durar além do card. |
| ADR | “Cria um ADR: vamos …” | Acha a pasta e o estilo de ADR deste repo. Recusa trivialidade, detalhe que muda sempre e detalhe de implementação. Rascunho, sua aprovação, um arquivo. Se houver id de card, comenta o caminho relativo. Sem rótulo de fila. |
| Ler | “Lê o #42” ou cole a URL | Traz título, estado, rótulos, descrição e comentários como estão. Não escreve nada. |
| Comentar | “Comenta no #42: …” | Publica um comentário assim que o item e o texto estão claros. |
| Ainda é necessário? | “Confere o #42 contra o código” | Lê o card, busca nos repositórios locais e publica uma tabela (**Corrigido**, **Parcial**, **Aberto**, **Inconclusivo**) com um veredito. Pode recomendar fechar. Deixa o card aberto. |

Informe um id (`42`, `#42`) ou a URL do tracker quando o item já existe. Texto livre, `@files`, pastas e links servem de entrada em criar, refine, spec, arquitetura e ADR.

### Ordem

```text
create → (spec?) → (refine?) → architecture
         ↘ refine ↗
```

`spec` e `refine` são opcionais, em qualquer ordem, e qualquer um pode ser pulado. Quando `refine` e `architecture` rodam juntos, refine vem antes. `read`, `comment` e `check` funcionam a qualquer momento. `create-adr` fica fora dessa sequência.

Um card novo pode ir direto para arquitetura. O agente não encadeia o modo seguinte sem você pedir.

### O que fica de fora

Não implementa código, não fecha cards e não move colunas além dos quatro rótulos de fila. Nunca aplica `interação::humano`, `dev::ok` ou `ready4Dev`. Na ponte atual de GitLab, milestone, data de início e vínculo entre itens são ignorados; a confirmação diz isso. Cards relacionados são citados por id na descrição.

### Mapa deste repositório

| Caminho | Papel |
|---------|--------|
| `SKILL.md` | Procedimento que o agente segue |
| `references/modes/` | Um arquivo por modo. `arch` usa `architecture.md` |
| `references/trackers/gitlab.md` | Chamadas exatas ao MCP. Um tracker novo é outro arquivo aqui, com os mesmos nomes de operação |
| `references/rule-contract.md` | Campos de `issue-tracker.mdc` |
| `assets/` | Modelos de Tech Spec, Product Spec e ADR |

Os ADR vão para o projeto dono da decisão. O agente reaproveita um conjunto existente (`adr-*.mdc`, `adr-*.md`, `ADR-*.md`, `NNNN-*.md`) em `.cursor/rules/architecture/`, `docs/adr/`, `docs/decisions/`, `docs/architecture/decisions/` ou `adr/`. Sem conjunto, pergunta uma vez e o padrão é `docs/adr/NNNN-slug.md`. Uma decisão por arquivo. A data vem do timestamp do arquivo.

Licença: proprietária, uso interno.
