# Lexia · TODO / Roadmap

## Sprint 1 — Skills LOPD/Privacidad (EN CURSO)
- [x] Scaffold privacy-legal-es
- [x] CLAUDE.md perfil de práctica español
- [x] respondedor-arsulipo-es
- [x] notificador-brecha-aepd
- [ ] triador-privacidad-es
- [ ] generador-pias-aepd
- [ ] revisor-dpa-encargado
- [ ] generador-clausulas-rgpd
- [ ] analizador-gap-regulatorio
- [ ] monitor-politica-privacidad
- [ ] cold-start-interview-es
- [ ] Panel web básico (Next.js) integrado con los skills

## Sprint 2 — Verificación normativa en tiempo real
- [ ] Conectar MCP → API BOE (boe.es/datosabiertos)
      Objetivo: citas [FUENTE: BOE] verificadas en tiempo real
- [ ] Conectar MCP → Sede electrónica AEPD (sedeagpd.gob.es)
      Objetivo: resoluciones sancionadoras, guías actualizadas,
      estado notificaciones de brecha enviadas
- [ ] Conectar MCP → BORME (boe.es/borme)
      Objetivo: verificación datos registrales de responsables/encargados
- [ ] Conectar MCP → Tribunal Constitucional
      Objetivo: jurisprudencia constitucional en materia de privacidad
- [ ] Conectar MCP → Diarios autonómicos relevantes
      Objetivo: normativa autonómica (sanidad, educación, función pública)
- [ ] Actualizar .mcp.json de privacy-legal-es con los conectores anteriores
- [ ] Revisar todos los SKILL.md — promover [VERIFICAR] → [FUENTE: X]
      donde el MCP ya pueda resolver la cita

## CENDOJ — Decisión de arquitectura
CENDOJ tiene régimen de licencia comercial + CAPTCHA anti-IA.
NO se conecta vía MCP.
Modo de integración: "asistente de búsqueda manual"
- El abogado localiza y descarga la sentencia desde cendoj.poderjudicial.es
- La arrastra/sube a Lexia
- Lexia la analiza, extrae ratio decidendi, aplica al caso
Las citas [FUENTE: CENDOJ] en los SKILL.md se mantienen como señal
para el letrado de que debe buscar jurisprudencia manualmente.

## Notas de arquitectura
- Sistema [FUENTE: X] y [VERIFICAR] es capa central desde Sprint 1.
  Todos los SKILL.md lo implementan desde el inicio.
  Convención:
    [FUENTE: BOE]    → norma publicada en BOE
    [FUENTE: AEPD]   → guía, resolución o criterio AEPD
    [FUENTE: CENDOJ] → señal para búsqueda manual por el letrado
    [FUENTE: RGPD]   → artículo del Reglamento (UE) 2016/679
    [VERIFICAR]      → sin fuente oficial verificable — revisar antes de usar
  En Sprint 2, los MCP sustituirán [VERIFICAR] → citas reales donde posible.
  [FUENTE: CENDOJ] permanece como señal manual por diseño, no por limitación.
