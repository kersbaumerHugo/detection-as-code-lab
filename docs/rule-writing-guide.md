# Rule Review Checklist

Use este checklist antes de aceitar uma nova regra de detecção no repositório.

## Metadata

- [ ] A regra possui título claro?
- [ ] A regra possui ID único?
- [ ] O status está definido?
- [ ] A descrição explica o comportamento detectado?
- [ ] O autor está definido?
- [ ] A data está preenchida?

## Log source

- [ ] A fonte de log está clara?
- [ ] O produto, serviço ou categoria fazem sentido?
- [ ] A regra depende de campos específicos?

## Detection logic

- [ ] A condição principal está clara?
- [ ] O operador usado faz sentido?
- [ ] A regra é específica o suficiente?
- [ ] A regra evita padrões genéricos demais?

## SOC analysis

- [ ] Existem falsos positivos documentados?
- [ ] Existe sugestão de triagem?
- [ ] Existe severidade definida?
- [ ] Existe referência MITRE ATT&CK?

## Testing

- [ ] Existe log de exemplo?
- [ ] A regra passou no yamllint?
- [ ] A regra passou no sigma check?
- [ ] A alteração passou na pipeline CI/CD?