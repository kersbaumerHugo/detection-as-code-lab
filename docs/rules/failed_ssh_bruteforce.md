# Linux Failed SSH Login Attempt

## Objetivo

Detectar tentativas falhas de autenticação SSH em sistemas Linux.

## Contexto

Falhas de login SSH podem indicar erro legítimo de usuário, tentativa de brute force, password spraying ou enumeração de usuários.

## Fonte de log esperada

- Sistema: Linux
- Serviço: sshd
- Exemplo de arquivo: `/var/log/auth.log`

## Lógica da detecção

A regra procura mensagens contendo:

- `Failed password`
- `Invalid user`

## Exemplo de log

```log
Jun 30 10:15:23 ubuntu-server sshd[1842]: Failed password for invalid user admin from 192.168.56.20 port 53422 ssh2
```