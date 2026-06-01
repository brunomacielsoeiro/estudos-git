# 🛠️ Comandos Git — Referência Completa

## Configuração Inicial

```bash
# Configurar nome e email (obrigatório antes do primeiro commit)
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"

# Verificar configurações
git config --list

# Configurar editor padrão
git config --global core.editor "code --wait"
```

---

## Comandos Básicos

### Criar e clonar repositórios

| Comando | Descrição |
|---------|-----------|
| `git init` | Inicializa um repositório Git na pasta atual |
| `git clone <url>` | Clona um repositório remoto para a máquina local |

```bash
# Criar novo repositório
mkdir meu-projeto && cd meu-projeto
git init

# Clonar repositório existente
git clone https://github.com/usuario/repo.git
```

### Verificar estado

| Comando | Descrição |
|---------|-----------|
| `git status` | Mostra arquivos modificados, staged e untracked |
| `git log` | Mostra histórico de commits |
| `git log --oneline` | Histórico resumido (1 linha por commit) |
| `git diff` | Mostra diferenças não staged |
| `git diff --staged` | Mostra diferenças staged (prontas para commit) |

```bash
# Ver status
git status

# Histórico bonito
git log --oneline --graph --all

# Ver mudanças em um arquivo
git diff arquivo.txt
```

---

## Staging e Commits

### Adicionar ao staging

| Comando | Descrição |
|---------|-----------|
| `git add <arquivo>` | Adiciona arquivo específico ao staging |
| `git add .` | Adiciona todos os arquivos modificados |
| `git add -p` | Adiciona interativamente (escolhe hunks) |
| `git reset <arquivo>` | Remove arquivo do staging (sem perder mudanças) |

```bash
# Adicionar arquivo específico
git add README.md

# Adicionar tudo
git add .

# Remover do staging (desfaz o add)
git reset HEAD arquivo.txt
```

### Fazer commits

| Comando | Descrição |
|---------|-----------|
| `git commit -m "msg"` | Cria commit com mensagem |
| `git commit -am "msg"` | Add + commit (apenas tracked files) |
| `git commit --amend` | Edita o último commit (mensagem ou conteúdo) |

```bash
# Commit simples
git commit -m "feat: adicionar página de login"

# Corrigir último commit (antes de push)
git commit --amend -m "feat: adicionar página de login com validação"
```

---

## Branches

### Gerenciar branches

| Comando | Descrição |
|---------|-----------|
| `git branch` | Lista branches locais |
| `git branch <nome>` | Cria nova branch |
| `git checkout <branch>` | Muda para outra branch |
| `git checkout -b <nome>` | Cria e muda para nova branch |
| `git branch -d <nome>` | Deleta branch (se já foi merged) |
| `git branch -D <nome>` | Força deleção da branch |

```bash
# Criar e mudar para nova branch
git checkout -b feature/login

# Voltar para main
git checkout main

# Deletar branch após merge
git branch -d feature/login
```

### Merge e Rebase

| Comando | Descrição |
|---------|-----------|
| `git merge <branch>` | Mescla branch na atual |
| `git rebase <branch>` | Reaplica commits sobre outra branch |
| `git merge --abort` | Cancela merge com conflito |

```bash
# Merge: trazer feature para main
git checkout main
git merge feature/login

# Rebase: atualizar feature com main
git checkout feature/login
git rebase main
```

---

## Repositório Remoto

### Gerenciar remotes

| Comando | Descrição |
|---------|-----------|
| `git remote -v` | Lista repositórios remotos |
| `git remote add origin <url>` | Adiciona remote |
| `git push -u origin main` | Push + configura tracking |
| `git push` | Envia commits para o remote |
| `git pull` | Baixa e mescla mudanças do remote |
| `git fetch` | Baixa mudanças sem mesclar |

```bash
# Configurar remote
git remote add origin https://github.com/usuario/repo.git

# Primeiro push
git push -u origin main

# Pushes seguintes
git push

# Atualizar local com remote
git pull origin main
```

---

## Desfazer Mudanças

| Comando | O que desfaz | Perigoso? |
|---------|-------------|-----------|
| `git checkout -- <arquivo>` | Mudanças não staged | ⚠️ Perde mudanças |
| `git reset HEAD <arquivo>` | Remove do staging | ✅ Seguro |
| `git reset --soft HEAD~1` | Desfaz commit (mantém staging) | ✅ Seguro |
| `git reset --mixed HEAD~1` | Desfaz commit (mantém working dir) | ✅ Seguro |
| `git reset --hard HEAD~1` | Desfaz commit (perde tudo) | 🔴 Perigoso |
| `git revert <hash>` | Cria commit que desfaz outro | ✅ Seguro |

```bash
# Descartar mudanças em arquivo (CUIDADO: perde as mudanças)
git checkout -- arquivo.txt

# Desfazer último commit mantendo as mudanças
git reset --soft HEAD~1

# Reverter commit de forma segura (cria novo commit)
git revert abc1234
```

---

## Stash (Guardar temporariamente)

| Comando | Descrição |
|---------|-----------|
| `git stash` | Guarda mudanças temporariamente |
| `git stash list` | Lista stashes salvos |
| `git stash pop` | Restaura último stash e remove da lista |
| `git stash apply` | Restaura último stash (mantém na lista) |
| `git stash drop` | Remove stash da lista |

```bash
# Guardar mudanças para trocar de branch
git stash

# Voltar e restaurar
git stash pop
```

---

## Tags

| Comando | Descrição |
|---------|-----------|
| `git tag v1.0.0` | Cria tag leve |
| `git tag -a v1.0.0 -m "msg"` | Cria tag anotada |
| `git push origin v1.0.0` | Envia tag para remote |
| `git push origin --tags` | Envia todas as tags |

```bash
# Criar release tag
git tag -a v1.0.0 -m "Primeira versão estável"
git push origin v1.0.0
```

---

## Comandos Úteis do Dia a Dia

```bash
# Ver quem alterou cada linha de um arquivo
git blame arquivo.txt

# Buscar commit que introduziu um bug
git bisect start
git bisect bad          # commit atual tem bug
git bisect good abc123  # commit antigo sem bug

# Limpar arquivos untracked
git clean -fd

# Ver diferença entre branches
git diff main..feature/login

# Cherry-pick (trazer commit específico)
git cherry-pick abc1234
```

---

## Resumo Visual

```
┌─────────────────────────────────────────────────────────────┐
│                    COMANDOS MAIS USADOS                       │
│                                                              │
│  INÍCIO          TRABALHO         COMPARTILHAR               │
│  ────────        ────────         ────────────               │
│  git init        git add .        git push                   │
│  git clone       git commit       git pull                   │
│                  git status       git fetch                  │
│                  git diff                                    │
│                                                              │
│  BRANCHES        DESFAZER         HISTÓRICO                  │
│  ────────        ────────         ─────────                  │
│  git branch      git reset        git log                    │
│  git checkout    git revert       git blame                  │
│  git merge       git stash        git diff                   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
