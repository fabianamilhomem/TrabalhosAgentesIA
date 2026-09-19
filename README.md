# TrabalhosAgentesIA

Índice dos exercícios práticos 1.1 a 1.4 (Git, GitHub CLI e agente de IA) da disciplina de **Agentes de IA** (Mestrado IDP), realizados em 19/09/2026.

**Autoria:** Fabiana Milhomem (`fabianamilhomem`)
**Ferramentas:** Git 2.51.0, GitHub CLI (`gh`) 2.101.0, Claude Code (agente de IA) e CLI `autograde` 0.9.0

Cada exercício foi feito em um repositório próprio, seguindo o passo a passo do tutorial do professor. Todos foram validados e submetidos com `autograde validar ia-1.x`.

## Resumo

| Exercício | Tema | Repositório | Evidência |
|-----------|------|-------------|-----------|
| ia-1.1 | Primeiro repositório: add, commit e push | [meu-primeiro-repo](https://github.com/fabianamilhomem/meu-primeiro-repo) | 2 commits |
| ia-1.2 | GitHub CLI: branch, PR e merge | [exercicio-12](https://github.com/fabianamilhomem/exercicio-12) | [PR #1](https://github.com/fabianamilhomem/exercicio-12/pull/1) |
| ia-1.3 | Agente de IA cria repositório e clona | [meu-segundo-repo](https://github.com/fabianamilhomem/meu-segundo-repo) | 1 commit |
| ia-1.4 | Agente de IA cria arquivo, abre PR e faz merge | [meu-terceiro-repo](https://github.com/fabianamilhomem/meu-terceiro-repo) | [PR #1](https://github.com/fabianamilhomem/meu-terceiro-repo/pull/1) |

## ia-1.1 Meu primeiro repositório

Objetivo: exercitar `add`, `commit` e `push`.

Repositório público criado vazio (via `gh repo create meu-primeiro-repo --public`), clonado numa pasta vazia, com o `README.md` criado por `echo`, dois commits e push:

```bash
git clone https://github.com/fabianamilhomem/meu-primeiro-repo.git
cd meu-primeiro-repo
echo "# Meu Primeiro Repositorio" > README.md
echo "" >> README.md
echo "Repo do exercicio ia-1.1 da disciplina Agentes de IA." >> README.md
git add README.md
git commit -m "feat: README inicial"
echo "" >> README.md
echo "## Sobre" >> README.md
echo "Estudante da IA-2026-01." >> README.md
git commit -am "docs: secao Sobre"
git push origin main
```

## ia-1.2 GitHub CLI: branch, PR e merge

Objetivo: usar o `gh` para criar o repositório, uma branch, um Pull Request e o merge.

```bash
gh repo create exercicio-12 --public --clone
cd exercicio-12
echo "# Exercicio ia-1.2" > README.md
git add README.md
git commit -m "feat: README inicial"
git push origin main
git checkout -b feat/algo
echo "linha nova" >> README.md
git commit -am "feat: adiciona linha"
git push -u origin feat/algo
gh pr create --title "feat: adiciona uma linha ao README" --body "Trabalho do exercicio ia-1.2"
gh pr merge --squash --delete-branch
```

Observação: neste computador o Git criava a branch local como `master`, então o primeiro `git push origin main` falhou. A branch foi renomeada para `main` (`git branch -m master main`), e o Git passou a usar `init.defaultBranch main`. O restante seguiu o tutorial.

## ia-1.3 Agente cria repositório e clona

Objetivo: instruir um agente de codificação (Claude Code) a criar um repositório com o `gh` e cloná-lo. O agente foi aberto numa pasta vazia.

Prompt dado ao agente:

> Crie um repositório público no meu usuário GitHub chamado `meu-segundo-repo` usando `gh`, faça o clone local dentro desta pasta atual e adicione um README.

Comandos executados pelo agente:

```bash
gh repo create meu-segundo-repo --public --clone
cd meu-segundo-repo
echo "# Meu Segundo Repositorio" > README.md
git add README.md
git commit -m "feat: README inicial"
git push -u origin main
gh repo view --json name,visibility
```

## ia-1.4 Agente cria arquivo, abre PR e faz merge

Objetivo: pedir ao agente o ciclo completo de uma contribuição, em duas etapas.

Prompt da etapa 1:

> Crie um repositório público no GitHub chamado `meu-terceiro-repo`, clone-o, faça um commit inicial com README.md.

Prompt da etapa 2:

> Altere o diretorio de trabalho para o diretorio onde voce clonou o repositorio `meu-terceiro-repo` e crie uma branch nova, adicione um arquivo `CONTRIBUINDO.md` com um texto curto, abra um Pull Request com título descritivo e faça o merge na main.

Comandos executados pelo agente:

```bash
# etapa 1
gh repo create meu-terceiro-repo --public --clone
cd meu-terceiro-repo
echo "# Meu Terceiro Repositorio" > README.md
git add README.md && git commit -m "feat: README inicial"
git push -u origin main

# etapa 2
git checkout -b feat/contribuindo
echo "# Como contribuir" > CONTRIBUINDO.md
echo "Abra issues e PRs descritivos." >> CONTRIBUINDO.md
git add CONTRIBUINDO.md && git commit -m "docs: guia de contribuicao"
git push -u origin feat/contribuindo
gh pr create --title "docs: adiciona guia de contribuicao" --body "Texto inicial sobre como contribuir."
gh pr merge --squash --delete-branch
gh pr list --state all
```

Resultado: PR `docs: adiciona guia de contribuicao` mergeado, com a `main` contendo 2 commits.

## Este repositório

Este repositório (`TrabalhosAgentesIA`) e os repositórios `AgentesIA` e `AgentesIA-ex1-3` vieram de uma primeira tentativa dos exercícios, feita antes de seguir o tutorial à risca. Os exercícios avaliados são os quatro repositórios listados acima.
