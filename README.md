# Avaliação Técnica AppSec

Este repositório faz parte de um projeto para avaliação ténica.
O objetivo deste teste é desenvolver um workflow que inclua verificações de código com soluções SAST e DAST.
Também foram adicionados a este teste secret scanning e container scanning.
Também foi configurado Branch Protection para Main.

## As soluções utilzadas foram:
  - **Secret Scanning**: GitLeaks, Trofflehogg e 2ms (by Checkmarx).
  - **SAST**: Sonarcloud.
  - **DAST**: OWASP Zap.
  - **Container Scanning**: Trivy. 


## Estrutura do Workflow

A melhor prática seria ter todo workflow de segurança em outro repositório, fora do projeto principal, e ser acionado a partir de um único yml orquestrador.
Isso colabora com um melhor gerenciamento e uma manutenção mais segura apenas pelo time de AppSec.
Neste teste todos os yml estão no diretório .github/workflows

```
└── workflows
    ├── appsec-workflow.yml
    ├── docker-image.yml
    ├── gitleaks-check.yml
    ├── owaspzap-check.yml
    ├── sonarcloud-check.yml
    ├── trivy-check.yml
    ├── trufflehogg-check.yml
    └── twoms-check.yml
```

### AppsecWorkflow
Responsável por orquestrar todos os scans e checagens.

### Gitleaks
Verifica a presença de segredos expostos no código fonte, como tokens, chaves de API e credenciais.

**Inputs Requeridos**:
- `GITHUB_TOKEN`: Token de acesso ao GitHub.
- `GITLEAKS_LICENSE`: Licença para o Gitleaks (Necessário para organizations).

### OWASP ZAP
Realiza análises de código dinamico (DAST) para identificar problemas de segurança, bugs e vulnerabilidades.

**Inputs Requeridos**:
- `GITHUB_TOKEN`: Token de acesso ao github.

### SONARCLOUD
Realiza análises de código estático (SAST) para identificar problemas de segurança, bugs e vulnerabilidades.

**Inputs Requeridos**:
- `GITHUB_TOKEN`: Token de acesso ao github.
- `SONAR_TOKEN`: Token de autenticação para o SonarCloud.

### 2MS, Trivy e Trufflehogg
Realiza análises em busca de secrets no código.

