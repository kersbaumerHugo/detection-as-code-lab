# False Positive Analysis

## Objetivo

Documentar possíveis falsos positivos das regras Sigma deste laboratório e sugerir formas de triagem para reduzir ruído operacional.

Uma boa regra de detecção não deve apenas identificar comportamento suspeito. Ela também precisa ser compreensível, revisável e útil para um analista durante uma investigação.

---

## Regra: Linux Failed SSH Login Attempt

### Comportamento detectado

A regra identifica mensagens relacionadas a falhas de autenticação SSH, como:

- `Failed password`
- `Invalid user`

Esse comportamento pode indicar brute force, password spraying, enumeração de usuários ou tentativa manual de acesso indevido.

### Possíveis falsos positivos

- Usuário legítimo digitando senha incorreta.
- Administrador testando acesso remoto.
- Script interno com credenciais desatualizadas.
- Scanner autorizado em ambiente de laboratório.
- Ferramenta de inventário ou automação tentando acessar hosts via SSH.

### Como reduzir ruído

- Criar limiar mínimo de tentativas por IP.
- Agrupar eventos por usuário e IP de origem.
- Considerar uma janela de tempo.
- Criar allowlist para IPs internos conhecidos.
- Correlacionar falhas com login bem-sucedido posterior.
- Diferenciar tentativa única de comportamento repetitivo.

### Perguntas de triagem

- O IP de origem é interno ou externo?
- Quantas tentativas ocorreram?
- As tentativas foram contra um único usuário ou vários?
- Houve login bem-sucedido depois das falhas?
- O usuário tentado existe no ambiente?
- Esse comportamento já ocorreu antes?

---

## Regra: Suspicious PowerShell Remote Download

### Comportamento detectado

A regra identifica execução de PowerShell com comandos associados a download remoto, como:

- `Invoke-WebRequest`
- `iwr`
- `DownloadString`
- `Net.WebClient`
- `curl`
- `wget`

Esse comportamento pode indicar download de payload, script remoto ou ferramenta usada em pós-exploração.

### Possíveis falsos positivos

- Scripts legítimos de administração.
- Automação de instalação de software.
- Troubleshooting feito por time de infraestrutura.
- Ferramentas internas de suporte.
- Pipelines ou scripts corporativos executando downloads controlados.
- Ambientes de laboratório.

### Como reduzir ruído

- Verificar se o domínio de destino é confiável.
- Criar allowlist para scripts internos conhecidos.
- Avaliar o processo pai.
- Avaliar o usuário que executou o comando.
- Verificar se o arquivo baixado foi executado.
- Correlacionar com EDR, proxy, DNS e firewall.
- Diferenciar download interno de download externo.

### Perguntas de triagem

- Quem executou o comando?
- O processo pai faz sentido?
- O destino do download é conhecido?
- O arquivo foi salvo em diretório suspeito?
- O comando usou flags como `-EncodedCommand`, `-NoProfile` ou `-ExecutionPolicy Bypass`?
- Houve execução do arquivo depois do download?

---

## Regra: Suspicious Long DNS Query

### Comportamento detectado

A regra identifica consultas DNS com subdomínios anormalmente longos, o que pode indicar DNS tunneling, beaconing ou transporte de dados codificados via DNS.

### Possíveis falsos positivos

- CDNs.
- Serviços cloud.
- Ferramentas de telemetria.
- Plataformas de analytics.
- Ferramentas de segurança.
- Aplicações legítimas usando identificadores longos.
- Testes internos de segurança.

### Como reduzir ruído

- Avaliar frequência das consultas.
- Agrupar eventos por host de origem.
- Verificar reputação do domínio.
- Criar allowlist para fornecedores conhecidos.
- Correlacionar com volume de DNS por endpoint.
- Avaliar tipos de query, como `A`, `AAAA`, `TXT` ou `NULL`.
- Verificar se o domínio base é novo ou desconhecido.

### Perguntas de triagem

- Qual host gerou a consulta?
- As consultas ocorrem em alta frequência?
- O domínio é conhecido pelo ambiente?
- Existe comunicação posterior com o domínio resolvido?
- O padrão parece codificado ou aleatório?
- Outros hosts consultaram o mesmo domínio?
- Há eventos relacionados no EDR, firewall ou proxy?

---

## Conclusão

Falsos positivos são parte natural do ciclo de vida de uma regra de detecção.

O objetivo deste laboratório é mostrar que uma detecção deve ser tratada como código e também como produto operacional: precisa ser validada, documentada, revisada e melhorada continuamente.