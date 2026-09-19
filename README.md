# TrabalhosAgentesIA

Repositório dos trabalhos da disciplina de **Agentes de IA** (Mestrado IDP).
Este README documenta os exercícios práticos 1.1 a 1.4 (Git, GitHub CLI e agente de IA), realizados em 19/09/2026.

**Autoria:** Fabiana Milhomem (`fabianamilhomem`)
**Ferramentas:** Git 2.51.0, GitHub CLI (`gh`) 2.101.0 e Claude Code (agente de IA)

## Resumo

| Exercício | Tema | Onde foi feito | Evidência |
|-----------|------|----------------|-----------|
| 1.1 | Primeiro repositório: add, commit e push | `git` (linha de comando) | commit `72f7f1a` |
| 1.2 | Repositório com `gh`: branch, PR e merge | `gh` | [PR #1](https://github.com/fabianamilhomem/TrabalhosAgentesIA/pull/1) |
| 1.3 | Agente de IA cria um repositório | Claude Code | [AgentesIA-ex1-3](https://github.com/fabianamilhomem/AgentesIA-ex1-3) |
| 1.4 | PR e merge com assistente de IA | Claude Code | [PR #2](https://github.com/fabianamilhomem/TrabalhosAgentesIA/pull/2) |

## 1.1 Primeiro repositório Git (add, commit e push)

Objetivo: exercitar `add`, `commit` e `push` enviando um projeto ao GitHub.

O exercício foi feito no repositório inicial `AgentesIA` (https://github.com/fabianamilhomem/AgentesIA), que já estava criado e vazio. Os comandos foram executados como se o repositório estivesse sendo criado agora:

```bash
git init -b main
git add README.md
git commit -m "Primeiro commit: adiciona README"
git remote add origin https://github.com/fabianamilhomem/AgentesIA.git
git push -u origin main
```

O primeiro commit (`72f7f1a`) é o mesmo que aparece no histórico deste repositório. Só o `README.md` foi adicionado (`git add` explícito), e o restante da pasta ficou sem rastreamento.

## 1.2 Repositório com o GitHub CLI (`gh`): branch, PR e merge

Objetivo: usar o `gh` para criar o repositório e exercitar branch, Pull Request e merge.

1. Instalação do `gh` (`winget install --id GitHub.cli`) e login com `gh auth login --web`.
2. Criação deste repositório, já enviando a branch `main`:

   ```bash
   gh repo create TrabalhosAgentesIA --public --source=. --remote=origin --push
   ```

3. Branch, commit e PR:

   ```bash
   git switch -c feature/atualiza-readme
   git add README.md
   git commit -m "Adiciona lista de exercícios ao README"
   git push -u origin feature/atualiza-readme
   gh pr create --base main --head feature/atualiza-readme --title "Adiciona lista de exercícios ao README"
   ```

4. Merge e limpeza:

   ```bash
   gh pr merge 1 --merge --delete-branch
   git switch main && git pull
   ```

Resultado: [PR #1](https://github.com/fabianamilhomem/TrabalhosAgentesIA/pull/1) mergeado, com a branch removida.

## 1.3 Agente de IA cria um repositório

Objetivo: interagir com um agente de IA para criar um repositório.

Pedi ao Claude Code que criasse o repositório `AgentesIA-ex1-3`. O agente executou:

```bash
gh repo create AgentesIA-ex1-3 --public --add-readme \
  --description "Exercício 1.3: repositório criado por agente de IA (Claude Code)"
git clone https://github.com/fabianamilhomem/AgentesIA-ex1-3.git
```

Resultado: [AgentesIA-ex1-3](https://github.com/fabianamilhomem/AgentesIA-ex1-3), público, com README inicial e clonado localmente.

## 1.4 PR e merge com assistente de IA

Objetivo: interagir com um agente de IA para conduzir um PR e o merge.

Pedi ao Claude Code que fizesse o fluxo completo neste repositório. O agente criou a branch `feature/adiciona-gitignore`, adicionou um `.gitignore`, abriu o PR e fez o merge:

```bash
git switch -c feature/adiciona-gitignore
git add .gitignore
git commit -m "Adiciona .gitignore"
git push -u origin feature/adiciona-gitignore
gh pr create --base main --head feature/adiciona-gitignore --title "Adiciona .gitignore"
gh pr merge 2 --merge --delete-branch
```

Resultado: [PR #2](https://github.com/fabianamilhomem/TrabalhosAgentesIA/pull/2) mergeado. Os commits feitos pelo agente trazem o trailer `Co-Authored-By`.

## Histórico

```
*   Merge pull request #2 (feature/adiciona-gitignore)
*   Merge pull request #1 (feature/atualiza-readme)
*   72f7f1a Primeiro commit: adiciona README
```
