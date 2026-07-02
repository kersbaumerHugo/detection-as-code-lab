# Detection Test Plan

## Objetivo

Definir como as regras Sigma deste laboratório serão revisadas, validadas e testadas.

## Escopo atual

O projeto valida:

- Sintaxe YAML
- Estrutura das regras Sigma
- Presença de exemplos de logs
- Documentação de triagem

## Testes automatizados atuais

A pipeline executa:

```bash
yamllint detections/sigma
sigma check detections/sigma
```

Testes manuais

Para cada regra:

Ler a descrição.
Conferir a fonte de log esperada.
Comparar com log de exemplo.
Revisar falsos positivos.
Revisar plano de triagem.
Executar validação local.
Abrir Pull Request.
Confirmar sucesso da pipeline.
Critério de aceite

Uma regra só deve ser considerada pronta quando:

Passar na pipeline;
tiver documentação;
tiver pelo menos um log de exemplo;
tiver falsos positivos descritos;
tiver orientação básica de investigação SOC.