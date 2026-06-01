# 📖 Conceitos Fundamentais — Git

## 1. O que é Controle de Versão?

Controle de versão é um sistema que registra mudanças em arquivos ao longo do tempo, permitindo:

- Voltar a versões anteriores
- Comparar mudanças entre versões
- Trabalhar em paralelo sem conflitos
- Rastrear quem fez o quê e quando

### Tipos de controle de versão

| Tipo | Exemplo | Característica |
|------|---------|---------------|
| Local | RCS | Apenas na máquina |
| Centralizado | SVN, CVS | Servidor central único |
| **Distribuído** | **Git**, Mercurial | Cada clone é um repositório completo |

---

## 2. Git vs GitHub

| Aspecto | Git | GitHub |
|---------|-----|--------|
| O que é | Ferramenta de versionamento | Plataforma de hospedagem |
| Onde roda | Local (sua máquina) | Nuvem (servidor) |
| Função | Controlar versões | Colaboração, PRs, Issues |
| Alternativas | — | GitLab, Bitbucket, Azure DevOps |
| Precisa de internet? | ❌ Não | ✅ Sim |

### Analogia

> **Git** = o motor do carro (faz o trabalho)
> **GitHub** = a estrada (onde você compartilha e colabora)

---

## 3. Repositório

### O que é?

Um repositório (repo) é uma pasta que o Git monitora. Contém todos os arquivos do projeto + o histórico completo de mudanças (na pasta `.git/`).

```
meu-projeto/
├── .git/              ← Histórico completo (NÃO mexer aqui)
│   ├── objects/       ← Todos os commits, blobs, trees
│   ├── refs/          ← Branches e tags
│   ├── HEAD           ← Branch atual
│   └── config         ← Configurações do repo
├── src/               ← Seus arquivos
├── README.md
└── .gitignore
```

### Local vs Remoto

```
┌──────────────────┐              ┌──────────────────┐
│  Repositório     │    push      │  Repositório     │
│  LOCAL           │ ───────────► │  REMOTO          │
│  (sua máquina)   │              │  (GitHub)        │
│                  │ ◄─────────── │                  │
│                  │    pull      │                  │
└──────────────────┘              └──────────────────┘
```

---

## 4. As 3 Áreas do Git

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  Working         │     │   Staging Area   │     │   Repository     │
│  Directory       │────►│   (Index)        │────►│   (.git)         │
│                  │ add │                  │commit│                  │
│  Onde você edita │     │  "Área de        │     │  Histórico       │
│  os arquivos     │     │   preparação"    │     │  permanente      │
└──────────────────┘     └──────────────────┘     └──────────────────┘
```

| Área | O que contém | Comando para mover |
|------|-------------|-------------------|
| Working Directory | Arquivos que você está editando | — |
| Staging Area | Mudanças prontas para commit | `git add` |
| Repository | Commits salvos permanentemente | `git commit` |

### Por que existe o Staging?

Permite **selecionar** quais mudanças entram no commit. Você pode ter 10 arquivos modificados mas commitar apenas 3 que fazem sentido juntos.

---

## 5. Commits

### O que é?

Um commit é um **snapshot** do projeto em um momento específico. Cada commit tem:

| Propriedade | Descrição |
|-------------|-----------|
| Hash (SHA-1) | Identificador único (ex: `a1b2c3d`) |
| Autor | Quem fez o commit |
| Data | Quando foi feito |
| Mensagem | Descrição da mudança |
| Parent | Commit anterior (forma a cadeia) |

### Histórico como cadeia

```
commit 1 ← commit 2 ← commit 3 ← commit 4 (HEAD)
   │          │          │          │
   └──────────┴──────────┴──────────┘
              Histórico linear
```

---

## 6. Branches

### O que é?

Uma branch é um **ponteiro** para um commit. Permite trabalhar em funcionalidades isoladas sem afetar o código principal.

```
          feature/login
              │
              ▼
    C1 ← C2 ← C3 ← C4
              │
              ▼
             main
```

### Branch principal

| Nome | Convenção |
|------|-----------|
| `main` | Padrão atual (GitHub) |
| `master` | Padrão antigo |

### HEAD

`HEAD` é um ponteiro que indica **onde você está agora** (qual branch/commit).

```
HEAD → main → commit C4
```

---

## 7. Merge vs Rebase

### Merge

Cria um **commit de merge** que une duas branches:

```
        C3 ← C4 (feature)
       /         \
C1 ← C2 ← ← ← ← C5 (merge commit) ← main
```

### Rebase

**Reaplica** commits de uma branch sobre outra (histórico linear):

```
Antes:  C1 ← C2 ← C3 (main)
              └── C4 ← C5 (feature)

Depois: C1 ← C2 ← C3 ← C4' ← C5' (feature rebased)
                    │
                   main
```

### Quando usar cada um?

| Situação | Usar |
|----------|------|
| Merge de feature para main | `merge` |
| Atualizar feature com main | `rebase` |
| Branch compartilhada | `merge` (nunca rebase em branch pública) |
| Histórico limpo | `rebase` |

---

## 8. Conflitos

### Quando acontecem?

Quando duas branches modificam a **mesma linha** do **mesmo arquivo**.

### Como resolver

```
<<<<<<< HEAD
código da sua branch
=======
código da outra branch
>>>>>>> feature/login
```

1. Edite o arquivo escolhendo o código correto
2. Remova os marcadores (`<<<<`, `====`, `>>>>`)
3. `git add arquivo.txt`
4. `git commit`

---

## 9. .gitignore

### O que é?

Arquivo que diz ao Git quais arquivos/pastas **ignorar** (não versionar).

### Exemplo

```gitignore
# Dependências
node_modules/
vendor/

# Ambiente
.env
.env.local

# Build
dist/
build/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Logs
*.log
```

---

## Resumo Visual

```
┌─────────────────────────────────────────────────────────────┐
│                      GIT - CONCEITOS                          │
│                                                              │
│  ÁREAS              OBJETOS           OPERAÇÕES              │
│  ─────              ───────           ─────────              │
│  • Working Dir      • Commit          • Add (stage)          │
│  • Staging          • Tree            • Commit (save)        │
│  • Repository       • Blob            • Push (share)         │
│                     • Tag             • Pull (update)        │
│                                       • Merge (combine)      │
│  PONTEIROS          REMOTES           • Rebase (replay)      │
│  ────────           ───────                                  │
│  • HEAD             • origin                                 │
│  • branch           • upstream                               │
│  • tag                                                       │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
