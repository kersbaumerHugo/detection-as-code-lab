# Rule Review Checklist

Use este checklist antes de aceitar uma nova regra de detecção no repositório.

O objetivo é garantir que cada regra seja clara, revisável, testável e útil para um fluxo básico de investigação SOC.

---

## 1. Metadata

- [ ] A regra possui título claro?
- [ ] A regra possui ID único?
- [ ] O status está definido?
- [ ] A descrição explica o comportamento detectado?
- [ ] O autor está definido?
- [ ] A data está preenchida?
- [ ] A severidade está definida?
- [ ] Existem tags MITRE ATT&CK quando aplicável?

---

## 2. Log source

- [ ] A fonte de log está clara?
- [ ] O produto, serviço ou categoria fazem sentido?
- [ ] A regra depende de campos específicos?
- [ ] Os campos usados na detecção existem na fonte de log esperada?
- [ ] A documentação explica qual log alimentaria a regra?

---

## 3. Detection logic

- [ ] A lógica da detecção está clara?
- [ ] O operador usado faz sentido?
- [ ] A regra é específica o suficiente?
- [ ] A regra evita padrões genéricos demais?
- [ ] A condição final está correta?
- [ ] A regra evita alertar por comportamento benigno óbvio?
- [ ] A detecção pode ser explicada em linguagem simples?

---

## 4. False positives

- [ ] Existem falsos positivos documentados?
- [ ] Os falsos positivos fazem sentido para o ambiente?
- [ ] Existe sugestão de redução de ruído?
- [ ] Existe recomendação de allowlist quando aplicável?
- [ ] A regra considera comportamento administrativo legítimo?

---

## 5. SOC investigation

- [ ] Existe orientação básica de triagem?
- [ ] A documentação responde “o que investigar depois”?
- [ ] Existem perguntas de investigação?
- [ ] Existem possíveis ações de resposta?
- [ ] A severidade está coerente com o impacto esperado?

---

## 6. Testing

- [ ] Existe pelo menos um log de exemplo?
- [ ] A regra passou no `yamllint`?
- [ ] A regra passou no `sigma check`?
- [ ] A alteração passou na pipeline CI/CD?
- [ ] A documentação foi atualizada junto com a regra?
- [ ] O Pull Request descreve o que mudou?

---

## 7. Pull Request

- [ ] O PR possui resumo claro?
- [ ] O PR lista arquivos alterados?
- [ ] O PR explica a motivação da regra?
- [ ] O PR informa como a regra foi validada?
- [ ] O PR inclui evidência da pipeline passando?

---

## Critério de aceite

Uma regra só deve ser considerada pronta quando:

- passar na validação automática;
- possuir documentação mínima;
- possuir exemplo de log;
- listar falsos positivos;
- explicar como investigar;
- ter severidade coerente;
- estar versionada em Git.