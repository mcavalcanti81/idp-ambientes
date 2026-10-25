# idp-ambientes

Repositório de ambientes do plat-idplabs: guarda **qual versão de cada componente está em cada ambiente**, e nada mais. Os manifestos ficam no repositório de cada app (`deploy/<componente>/overlays/<ambiente>`).

Modelo descrito na ADR-0006 do plat-idplabs.

## Estrutura

```
argocd/applicationset.yaml     # cria uma Application do Argo CD por arquivo em envs/
envs/<ambiente>/<componente>.yaml
```

Um arquivo de ambiente:

```yaml
repo: github.com/mcavalcanti81/idp-exemplo-api
component: exemplo-api
tag: v0.1.0
cluster: in-cluster
namespace: exemplo-dev
```

`cluster` e `namespace` vêm de `delivery.environments` no `platform.yaml` do app.

## Promover e reverter

- **Promover:** PR trocando `tag`. Mudanças em `envs/prod/` exigem aprovação (CODEOWNERS).
- **Reverter:** reverter o PR. A tag anterior continua existindo.
- **Auditoria:** `git log envs/prod/` mostra o que esteve em produção e quem aprovou.

Hoje a troca de tag é manual. O comando `promote` do engine vai abrir esses PRs automaticamente.
