# False Positive Analysis

## Objetivo

Documentar possíveis falsos positivos das regras Sigma deste laboratório e formas de triagem.

## Por que falsos positivos importam?

Uma regra de detecção útil não deve apenas encontrar comportamento suspeito. Ela também precisa ser analisável por um time de SOC, evitando alertas excessivos e ruído operacional.

## Regra: Linux Failed SSH Login Attempt

### Possíveis falsos positivos

- Usuário legítimo errando senha
- Admin testando conexão
- Automação interna com credencial incorreta

### Como reduzir ruído

- Criar limiar mínimo de tentativas
- Agrupar eventos por IP
- Ignorar IPs internos conhecidos
- Correlacionar com login bem-sucedido

## Regra: Suspicious PowerShell Remote Download

### Possíveis falsos positivos

- Scripts administrativos
- Instalação de software
- Ferramentas de troubleshooting
- Automação de TI

### Como reduzir ruído

- Criar allowlist de scripts internos
- Verificar parent process
- Verificar usuário executor
- Verificar destino do download

## Regra: Suspicious Long DNS Query

### Possíveis falsos positivos

- CDN
- Telemetria de ferramentas cloud
- Soluções de segurança
- Tracking de aplicações legítimas

### Como reduzir ruído

- Correlacionar volume e frequência
- Verificar reputação do domínio
- Agrupar por host de origem
- Ignorar domínios internos ou fornecedores conhecidos