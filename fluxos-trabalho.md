# 🔄 Fluxos de Trabalho — Git Workflows

## 1. Por que ter um fluxo definido?

Sem um fluxo de trabalho, equipes enfrentam:
- Conflitos constantes
- Código quebrado na branch principal
- Dificuldade para fazer releases
- Sem saber o que está em produção

---

## 2. Git Flow

### Visão geral

Fluxo mais estruturado, ideal para projetos com releases planejadas.

```
main ─────────────────────────────────────────────────────── (produção)
  │                                          │
  └── release/1.0 ──────────────────────────►┘
        │                                    
  develop ────────────────────────────────────── (integração)
    │         │         │
    └── feature/login   └── feature/dashboard
```

### Branches

| Branch | Propósito | Vida |
|--------|-----------|------|
| `main` | Código em produção | Permanente |
| `develop` | Integração de features | Permanente |
| `feature/*` | Nova funcionalidade | Temporária |
| `release/*` | Preparação para release | Temporária |
| `hotfix/*` | Correção urgente em produção | Temporária |

### Quando usar

- Projetos com ciclos de release definidos
- Equipes grandes (5+ devs)
- Software com múltiplas versões em produção

---

## 3. GitHub Flow

### Visão geral

Fluxo simplificado, ideal para deploy contínuo.

```
main ──────────────────────────────────────── (sempre deployável)
  │              │              │
  └── feature/A  └── feature/B  └── fix/bug-123
       │              │              │
       └── PR ────────┘── PR ────────┘── PR → merge → deploy
```

### Regras

1. `main` está **sempre** deployável
2. Crie branch a partir de `main` para qualquer mudança
3. Faça commits na branch
4. Abra um **Pull Request**
5. Após review e aprovação, merge para `main`
6. Deploy automático após merge

### Quando usar

- Deploy contínuo (várias vezes ao dia)
- Equipes pequenas/médias
- Projetos web com uma versão em produção

---

## 4. Trunk-Based Development

### Visão geral

Todos commitam direto na `main` (ou em branches muito curtas).

```
main ──C1──C2──C3──C4──C5──C6──C7──C8── (commits frequentes)
              │         │
              └─ feat ──┘ (branch vive < 1 dia)
```

### Regras

1. Branches vivem no **máximo 1-2 dias**
2. Commits pequenos e frequentes
3. Feature flags para código incompleto
4. CI/CD obrigatório (testes a cada commit)

### Quando usar

- Equipes com alta maturidade
- CI/CD robusto
- Deploy múltiplas vezes ao dia
- Google, Facebook, Netflix usam este modelo

---

## 5. Comparação

| Aspecto | Git Flow | GitHub Flow | Trunk-Based |
|---------|----------|-------------|-------------|
| Complexidade | Alta | Baixa | Média |
| Branches | Muitas | Poucas | Mínimas |
| Deploy | Por release | Contínuo | Contínuo |
| Equipe ideal | Grande | Pequena/Média | Madura |
| Risco de conflito | Baixo | Médio | Alto (mitigado por CI) |

---

## 6. Pull Requests (PRs)

### O que é?

Um Pull Request é um **pedido para mesclar** sua branch na branch principal. Permite:
- Code review antes do merge
- Discussão sobre a implementação
- CI/CD automático (testes rodam no PR)
- Histórico de decisões

### Anatomia de um bom PR

```markdown
## Descrição
Adiciona autenticação JWT ao endpoint /login

## O que foi feito
- Implementado middleware de autenticação
- Adicionados testes unitários
- Atualizada documentação da API

## Como testar
1. Rodar `npm test`
2. Fazer POST para /login com credenciais válidas
3. Verificar token no response

## Screenshots (se aplicável)
[imagem do resultado]
```

### Boas práticas de PR

| Prática | Por quê |
|---------|---------|
| PRs pequenos (< 400 linhas) | Mais fácil de revisar |
| Um PR = uma funcionalidade | Facilita rollback |
| Descrição clara | Reviewer entende o contexto |
| Testes passando | Não quebra a main |
| Self-review antes de pedir review | Pega erros óbvios |

---

## 7. Conventional Commits

### Formato

```
<tipo>(<escopo>): <descrição>

[corpo opcional]

[rodapé opcional]
```

### Tipos

| Tipo | Quando usar | Exemplo |
|------|-------------|---------|
| `feat` | Nova funcionalidade | `feat: adicionar login com Google` |
| `fix` | Correção de bug | `fix: corrigir cálculo de frete` |
| `docs` | Documentação | `docs: atualizar README` |
| `style` | Formatação (sem mudar lógica) | `style: aplicar prettier` |
| `refactor` | Refatoração | `refactor: extrair função de validação` |
| `test` | Testes | `test: adicionar testes do carrinho` |
| `chore` | Manutenção | `chore: atualizar dependências` |

---

## Resumo

```
┌─────────────────────────────────────────────────────────────┐
│              ESCOLHA SEU FLUXO                                │
│                                                              │
│  Projeto pessoal / pequeno?     → GitHub Flow                │
│  Equipe grande + releases?      → Git Flow                   │
│  Deploy contínuo + CI forte?    → Trunk-Based                │
│  Não sabe?                      → GitHub Flow (mais simples) │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
