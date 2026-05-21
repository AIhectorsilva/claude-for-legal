# Lexia · CHANGELOG

> Registro de cambios por sesión de desarrollo.
> Formato: [YYYY-MM-DD] · Descripción · Responsable

---

## [2026-05-19] · Área LOPD/Privacidad completa · Héctor Silva

### Engine (claude-for-legal)
- Fork del repo `anthropics/claude-for-legal` a `AIhectorsilva/claude-for-legal`
- Estructura `privacy-legal-es` duplicada del plugin `privacy-legal` original
- `CLAUDE.md` español del plugin redactado — perfil de práctica template
  con marco RGPD + LOPDGDD + AEPD, plazos críticos, posiciones en contratos
  de encargado, sistema de citaciones y umbrales de triaje
- 9 skills completos y validados con casos reales:
  - `cold-start-interview-es` — onboarding 6 bloques, genera CLAUDE.md personalizado
  - `respondedor-arsulipo-es` — respuesta ARSULIPO Art. 15-21 RGPD
  - `notificador-brecha-aepd` — análisis y notificación brechas 72h Art. 33-34 RGPD
  - `triador-privacidad-es` — triaje EIPD obligatoria / recomendada / STOP
  - `generador-pias-aepd` — EIPDs completas metodología AEPD Art. 35-36 RGPD
  - `revisor-dpa-encargado` — revisión contratos encargado Art. 28 RGPD + CCT 2021
  - `generador-clausulas-rgpd` — cláusulas informativas, consentimiento, cookies AEPD 2023
  - `analizador-gap-regulatorio` — gap analysis normativa vs. política, escala sancionadora
  - `monitor-politica-privacidad` — detección deriva política vs. práctica real
- Sistema de citaciones implementado como capa central:
  `[FUENTE: BOE]` · `[FUENTE: AEPD]` · `[FUENTE: RGPD]` · `[FUENTE: CENDOJ]` · `[VERIFICAR]`
- Decisión de arquitectura CENDOJ documentada: modo asistente manual permanente
- Perfil de Demalia Consulting generado y activo via cold-start
- `PROYECTO.md` — documentación maestra del proyecto (15 secciones)
- `TODO.md` — roadmap Sprint 2 completo
- `CHANGELOG.md` — este archivo

### Instalación en Claude Code
- Plugin registrado en `marketplace.json`
- Plugin instalado y validado: `/plugin install privacy-legal-es@claude-for-legal`
- Todos los skills disponibles via `/privacy-legal-es:[skill]`

### Decisiones técnicas registradas
- CENDOJ: NO conectar vía MCP — licencia comercial + CAPTCHA anti-IA
- MCP conectores BOE + AEPD + BORME + TC: reservados para Sprint 2
- `author` en `plugin.json` debe ser objeto, no string (Claude Code lo rechaza)
- Sistema `[FUENTE: X]` / `[VERIFICAR]` es capa central desde Sprint 1

---

*Próxima sesión: panel web Next.js (lexia-app) + Sprint 2 MCPs*
