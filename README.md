# 📚 Estudos de Git e GitHub

> Projeto de estudos sobre controle de versão com Git e GitHub, abordando desde conceitos fundamentais até fluxos de trabalho colaborativos e boas práticas de versionamento. Atividade acadêmica para cumprimento de horas complementares.

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [O que você vai aprender](#o-que-você-vai-aprender)
- [Estrutura do Repositório](#estrutura-do-repositório)
- [Fluxo de Trabalho Git](#fluxo-de-trabalho-git)
- [Conexão com outros projetos](#conexão-com-outros-projetos)
- [Referências](#referências)

---

## Sobre o Projeto

Git é o sistema de controle de versão mais utilizado no mundo. Este repositório documenta os fundamentos necessários para trabalhar com Git e GitHub de forma profissional — desde o primeiro commit até estratégias de branching em equipe.

### Por que Git é essencial?

- Todo projeto de software usa controle de versão
- É pré-requisito para CI/CD, DevOps e colaboração em equipe
- Permite rastrear mudanças, reverter erros e trabalhar em paralelo
- GitHub é a principal plataforma de portfólio para desenvolvedores

---

## O que você vai aprender

| Tema | Arquivo | Descrição |
|------|---------|-----------|
| Comandos Git | [comandos-git.md](./comandos-git.md) | Referência completa de comandos com exemplos |
| Conceitos | [conceitos-git.md](./conceitos-git.md) | Repositórios, staging, commits, branches |
| Fluxos de Trabalho | [fluxos-trabalho.md](./fluxos-trabalho.md) | Git Flow, GitHub Flow, trunk-based |
| Boas Práticas | [boas-praticas.md](./boas-praticas.md) | Commits, branches, PRs, .gitignore |

---

## Estrutura do Repositório

```
estudos-git/
├── README.md              ← Este arquivo (visão geral)
├── comandos-git.md        ← Referência de comandos com exemplos
├── conceitos-git.md       ← Fundamentos teóricos
├── fluxos-trabalho.md     ← Estratégias de branching
└── boas-praticas.md       ← Padrões profissionais
```

---

## Fluxo de Trabalho Git

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  Working     │     │   Staging    │     │    Local     │     │   Remote     │
│  Directory   │────►│    Area      │────►│  Repository  │────►│  Repository  │
│              │ add │   (Index)    │commit│   (.git)     │push │  (GitHub)    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
       ▲                                                              │
       └──────────────────────────────────────────────────────────────┘
                                    pull / clone
```

### Ciclo de vida dos arquivos

```
Untracked → Staged → Committed → Modified → Staged → Committed → ...
    │          │          │           │
    └── git add ┘    git commit      edit
```

---

## Conexão com outros projetos

Git é a base de tudo:

- **DevOps** — CI/CD depende de Git (push triggers pipeline)
- **Terraform** — Versionamento de infraestrutura
- **CloudFormation** — Templates versionados em repositórios
- **Docker** — Dockerfile versionado, builds automatizados
- **Kubernetes** — GitOps (ArgoCD, Flux)

---

## Referências

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [Pro Git Book (gratuito)](https://git-scm.com/book/pt-br/v2)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

---

## 📄 Licença

MIT License
