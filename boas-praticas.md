# ✅ Boas Práticas — Git e GitHub

## 1. Commits

### Mensagens de commit

| Prática | Exemplo bom | Exemplo ruim |
|---------|-------------|-------------|
| Verbo no imperativo | `adicionar validação de email` | `adicionei validação` |
| Específico | `corrigir cálculo de desconto acima de 50%` | `fix bug` |
| Curto (< 72 chars) | `feat: adicionar filtro por data` | `feat: adicionar filtro por data no relatório de vendas que estava faltando desde a sprint passada` |
| Sem ponto final | `docs: atualizar README` | `docs: atualizar README.` |

### Frequência de commits

```
✅ CORRETO: Commits pequenos e frequentes
   commit 1: "feat: criar modelo User"
   commit 2: "feat: adicionar validação de email"
   commit 3: "test: testes do modelo User"

❌ ERRADO: Um commit gigante
   commit 1: "adicionar tudo do módulo de usuários"
```

### Regra de ouro

> Cada commit deve representar **uma mudança lógica** que pode ser revertida independentemente.

---

## 2. Branches

### Nomenclatura

| Padrão | Exemplo | Uso |
|--------|---------|-----|
| `feature/<desc>` | `feature/login-google` | Nova funcionalidade |
| `fix/<desc>` | `fix/calculo-frete` | Correção de bug |
| `hotfix/<desc>` | `hotfix/crash-checkout` | Correção urgente em prod |
| `docs/<desc>` | `docs/atualizar-api` | Documentação |
| `refactor/<desc>` | `refactor/extrair-service` | Refatoração |

### Regras

| Prática | Por quê |
|---------|---------|
| Nunca commite direto na `main` | Protege código de produção |
| Branches curtas (< 1 semana) | Evita conflitos grandes |
| Delete branch após merge | Mantém repo limpo |
| Uma branch = uma tarefa | Facilita review e rollback |

---

## 3. .gitignore

### Sempre ignore

```gitignore
# Dependências (reinstalável)
node_modules/
vendor/
.venv/

# Variáveis de ambiente (SEGREDOS!)
.env
.env.local
.env.production

# Build (regenerável)
dist/
build/
*.o
*.class

# IDE (pessoal de cada dev)
.vscode/settings.json
.idea/
*.swp

# Sistema operacional
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*

# Credenciais (NUNCA versionar)
*.pem
*.key
credentials.json
```

### Regra

> Se é **regenerável**, **pessoal** ou **secreto**, vai no `.gitignore`.

---

## 4. README

### Todo repositório deve ter

| Seção | Conteúdo |
|-------|----------|
| Título + descrição | O que o projeto faz |
| Como instalar | Pré-requisitos e setup |
| Como usar | Comandos ou exemplos |
| Estrutura | Organização das pastas |
| Contribuição | Como contribuir |
| Licença | Tipo de licença |

---

## 5. Segurança

### Nunca versione

| Tipo | Exemplo | Alternativa |
|------|---------|-------------|
| Senhas | `password = "123"` | Variáveis de ambiente |
| API Keys | `AKIAIOSFODNN7EXAMPLE` | AWS Secrets Manager |
| Tokens | `ghp_xxxxxxxxxxxx` | `.env` + `.gitignore` |
| Certificados | `server.key` | Vault, KMS |

### Se vazou acidentalmente

```bash
# 1. Rotacione a credencial IMEDIATAMENTE
# 2. Remova do histórico (BFG Repo-Cleaner)
bfg --delete-files credentials.json
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# 3. Force push (CUIDADO)
git push --force
```

> ⚠️ Mesmo após remover do histórico, considere a credencial **comprometida** e rotacione.

---

## 6. Colaboração

### Code Review

| Prática | Benefício |
|---------|-----------|
| Revisar antes de aprovar | Pega bugs e melhora qualidade |
| Comentários construtivos | Ensina e não ofende |
| Aprovar apenas se entendeu | Responsabilidade compartilhada |
| Não bloquear por estilo | Use linter automático |

### Issues e Projects

| Ferramenta | Uso |
|-----------|-----|
| Issues | Reportar bugs, pedir features |
| Labels | Categorizar (bug, enhancement, docs) |
| Milestones | Agrupar por release |
| Projects | Kanban board (To Do, In Progress, Done) |

---

## 7. Checklist do Repositório Profissional

- [ ] README.md completo e atualizado
- [ ] .gitignore adequado ao projeto
- [ ] Licença definida (LICENSE)
- [ ] Sem credenciais no código
- [ ] Commits com mensagens claras
- [ ] Branch principal protegida
- [ ] CI/CD configurado (se aplicável)
- [ ] Contributing guide (se open source)

---

## Resumo

```
┌─────────────────────────────────────────────────────────────┐
│              BOAS PRÁTICAS GIT                                │
│                                                              │
│  COMMITS           BRANCHES          SEGURANÇA               │
│  ───────           ────────          ─────────               │
│  • Pequenos        • Nomes claros    • .gitignore            │
│  • Frequentes      • Curtas          • Sem secrets           │
│  • Descritivos     • Delete após     • Rotacionar se         │
│  • Imperativo        merge             vazar                 │
│                                                              │
│  COLABORAÇÃO       ORGANIZAÇÃO                               │
│  ───────────       ───────────                               │
│  • Pull Requests   • README                                  │
│  • Code Review     • Estrutura clara                         │
│  • Issues          • Licença                                 │
│  • Conventional    • .gitignore                              │
│    Commits                                                   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
