# Java Bootstrap - Infrastructure (GitOps) ☸️

Repositório de configuração e deployment para o ecossistema `java-bootstrap`. 
Este repositório utiliza o padrão de **Shared Helm Charts** consumindo o template de [k8s-helm-templates](https://github.com/rg-hermann/k8s-helm-templates).

## 🏗️ Estrutura
- `Chart.yaml`: Declara a dependência do template base.
- `values-dev.yaml`: Overrides para ambiente de desenvolvimento/local.
- `values-prod.yaml`: Overrides para ambiente de produção.

## 🚀 Como fazer o Deploy (Local)

### 1. Atualizar dependências
Como o template base vive em outro repo, você precisa baixá-lo localmente para testar:
```bash
helm dependency update
```
2. Validar o Render (Dry-run)
Para ver se o YAML final está correto:
```bash
helm install --debug --dry-run java-app . -f values-dev.yaml
```
🔄 Fluxo GitOps (ArgoCD)
Este repositório é monitorado pelo ArgoCD.

Novos commits no java-bootstrap geram imagens no GHCR.

O pipeline de CI atualiza a tag nos arquivos values-*.yaml deste repo.

O ArgoCD detecta a mudança e aplica no cluster automaticamente.