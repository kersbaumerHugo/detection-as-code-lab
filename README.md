# Detection-as-Code Lab

Projeto prático de Detection Engineering usando regras Sigma versionadas em Git e validação automatizada com CI/CD.

## Objetivo

O objetivo deste laboratório é aplicar práticas de DevOps ao ciclo de vida de regras de detecção em segurança, criando um fluxo simples de Detection-as-Code.

## O que é Detection-as-Code?

Detection-as-Code é a prática de tratar regras de detecção como código: elas são versionadas, revisadas, testadas e validadas automaticamente antes de serem usadas em um ambiente de segurança.

## Tecnologias usadas

- Sigma
- GitHub Actions
- Python
- sigma-cli
- yamllint
- Git/GitHub

## Estrutura

```text
detections/
|  sigma/
|  |    linux_failed_ssh_login.yml
|  |    windows_powershell_remote_download.yml
|  |    suspicious_dns_long_query.yml
|.github/
|   |   workflows/
|   |   |   detection-ci.yml
```
## Regras implementadas
|Regra|Fonte de log|Objetivo|Severidade|
|-|-|-|-|
|Linux Failed SSH Login Attempt	|Linux/SSHD|	Detectar falhas de login SSH|	Medium
Suspicious PowerShell Remote Download|Windows/Process Creation|	Detectar PowerShell baixando conteúdo remoto|High
|Suspicious Long DNS Query|	DNS	|Detectar consultas DNS anormalmente longas|Medium

## Pipeline CI/CD

A pipeline executa validações automáticas nas regras:

 - Validação de sintaxe YAML com yamllint.
 - Validação das regras Sigma com sigma check.

### Como rodar localmente

```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

yamllint detections/sigma
sigma check detections/sigma
```

## Aprendizados

Este projeto conecta práticas de DevOps e Blue Team, demonstrando como regras de detecção podem ser mantidas com versionamento, revisão e automação.

## Current maturity level

Este projeto concluiu o Nível 1:

- Regras Sigma iniciais
- Validação local
- Pipeline CI/CD
- README inicial

Agora está evoluindo para o Nível 2:

- Logs de exemplo
- Documentação por regra
- Análise de falso positivo
- Plano de teste
- Checklist de revisão

## Detection Engineering Workflow

1. Criar ou alterar regra Sigma.
2. Validar sintaxe localmente.
3. Validar regra com sigma-cli.
4. Adicionar log de exemplo.
5. Documentar falsos positivos.
6. Abrir Pull Request.
7. Aguardar pipeline CI/CD.
8. Fazer merge após validação.