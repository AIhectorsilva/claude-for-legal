# Lexia · TODO / Roadmap

## Sprint 1 — Skills LOPD/Privacidad (EN CURSO)
- [x] Scaffold privacy-legal-es
- [x] CLAUDE.md perfil de práctica español
- [x] respondedor-arsulipo-es
- [ ] notificador-brecha-aepd
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
      Objetivo: citas [FUENTE: BOE] verificadas en tiempo real, no desde
      conocimiento del modelo
- [ ] Conectar MCP → CENDOJ (jurisprudencia tribunales españoles)
      Objetivo: reemplazar [VERIFICAR] en citas jurisprudenciales por
      citas verificadas con enlace directo
- [ ] Conectar MCP → Sede electrónica AEPD
      Objetivo: resoluciones sancionadoras recientes, guías actualizadas,
      estado de notificaciones de brecha enviadas
- [ ] Actualizar .mcp.json de privacy-legal-es con los tres conectores
- [ ] Revisar todos los SKILL.md y promover [VERIFICAR] → [FUENTE: X]
      donde el MCP ya pueda resolver la cita

## Notas de arquitectura
- Sistema [FUENTE: X] y [VERIFICAR] es capa central desde Sprint 1.
  Todos los SKILL.md lo implementan desde el inicio — no es un añadido.
  Convención:
    [FUENTE: BOE]    → norma publicada en BOE, referencia verificable
    [FUENTE: AEPD]   → guía, resolución o criterio publicado por la AEPD
    [FUENTE: CENDOJ] → jurisprudencia de tribunales españoles
    [FUENTE: RGPD]   → artículo del Reglamento (UE) 2016/679
    [VERIFICAR]      → sin fuente oficial verificable en este momento —
                       revisar antes de usar en documento final
  En Sprint 2, los MCP sustituirán [VERIFICAR] por citas reales donde
  sea posible. Los [VERIFICAR] restantes son señales para el letrado
  revisor, no errores.
