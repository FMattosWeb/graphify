---
name: graphify
description: Graphify CLI para análise visual e grafos de repositórios de código.
---

# Graphify

A skill Graphify opera a análise visual e geração de grafos de código do repositório.

## Boas Práticas de Commit e `.gitignore` para `graphify-out/`

A execução do Graphify gera a pasta `graphify-out/` contendo grafos (`graph.json`), visualizadores interativos (`*.html`), caches de AST (`cache/`) e relatórios.

### 1. Padrão Recomendado (Docs-First / Git Friendly)
Para evitar inchar o histórico do Git com arquivos JSON de mais de 8MB e dezenas de fragmentos de cache a cada commit, comite **apenas** o relatório em Markdown e ignore o restante:

```gitignore
# Graphify - Versionar apenas relatório executivo; ignorar JSONs pesados, HTMLs e caches
graphify-out/*
!graphify-out/GRAPH_REPORT.md
```

### 2. Desrastreamento de Arquivos Antigos (Untrack)
Se `graphify-out/` já tiver sido commitado no passado, o `.gitignore` não terá efeito até que o cache do Git seja limpo:
```bash
git rm -r --cached graphify-out/
git add graphify-out/GRAPH_REPORT.md
```

### 3. Recuperação Local do Grafo Completo
Qualquer desenvolvedor ou agente pode regenerar os visualizadores HTML e o grafo JSON localmente a qualquer momento executando:
```bash
graphify update .
# ou
graphify extract .
```

