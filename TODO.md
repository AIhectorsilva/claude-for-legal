# Lexia · TODO Sprint 2

> Archivo de tareas pendientes tras completar Sprint 1 (área LOPD/Privacidad).
> Actualizar tras cada sesión de desarrollo.
> Última actualización: 19/05/2026

---

## 🔴 PRIORIDAD CRÍTICA

### Contratos de encargado — Demalia Consulting (detectado en cold-start)
El perfil de Demalia tiene 0 contratos Art. 28 firmados con ningún proveedor.
Exposición real e inmediata.
- [ ] HubSpot DPA — revisar con `/privacy-legal-es:revisor-dpa-encargado`
- [ ] Google Workspace / Meet / Drive DPA — ídem
- [ ] Slack DPA — ídem (datos bajo secreto profesional)
- [ ] Brevo DPA — ídem
- [ ] Holded DPA — ídem

### Registro de Actividades de Tratamiento (RAT) — Art. 30 RGPD
Demalia no tiene RAT. Obligatorio para cualquier responsable del tratamiento.
- [ ] Crear RAT inicial para Demalia Consulting
- [ ] Incorporar skill `generador-rat-es` al área LOPD en Sprint 2

### Política de privacidad de Demalia
No existe. Necesaria antes de cualquier actividad comercial web.
- [ ] Generar con `/privacy-legal-es:generador-clausulas-rgpd`
- [ ] Revisión letrada (Leo)
- [ ] Publicar en web cuando esté lista

---

## 🟠 PRIORIDAD ALTA

### Setup Enterprise Anthropic
- [ ] Solicitar acceso Enterprise a Anthropic
- [ ] Firmar DPA (Data Processing Agreement) con Anthropic
      → Necesario para cumplir RGPD al tratar datos de clientes con la API
- [ ] Activar Zero Data Retention (ZDR) en la cuenta
      → Sin ZDR, los inputs/outputs pueden usarse para entrenamiento
      → Crítico cuando los despachos suban documentos de clientes
- [ ] Revisar los límites de rate y tokens en el plan Enterprise
- [ ] Actualizar stack técnico en PROYECTO.md con el plan definitivo

### MCP conectores Sprint 2 — verificación normativa en tiempo real

**Conectar (en este orden):**
- [ ] BOE API (`boe.es/datosabiertos`)
      → Objetivo: promover `[FUENTE: BOE]` de conocimiento del modelo
        a cita verificada en tiempo real
      → Actualizar `.mcp.json` de todos los plugins `*-legal-es`
- [ ] Sede electrónica AEPD (`sedeagpd.gob.es`)
      → Objetivo: resoluciones sancionadoras recientes, guías actualizadas,
        estado de notificaciones de brecha enviadas
- [ ] BORME (`boe.es/borme`)
      → Objetivo: verificación datos registrales de responsables/encargados
- [ ] Tribunal Constitucional (`tribunalconstitucional.es`)
      → Objetivo: jurisprudencia constitucional en materia de privacidad
- [ ] Diarios autonómicos relevantes
      → DOGC (Cataluña), BOJA (Andalucía), BOCM (Madrid), BOPV (País Vasco)
      → Objetivo: normativa autonómica (sanidad, educación, función pública)

**NO conectar:**
- ❌ CENDOJ — licencia comercial + CAPTCHA anti-IA. Modo asistente manual permanente.

**Tras conectar los MCPs:**
- [ ] Actualizar `.mcp.json` de `privacy-legal-es` con los conectores
- [ ] Revisar los 9 SKILL.md de `privacy-legal-es`
      → Promover `[VERIFICAR]` → `[FUENTE: X]` donde el MCP ya resuelva
      → Los `[VERIFICAR]` restantes son señal para el letrado, no errores

---

## 🟡 PRIORIDAD MEDIA

### Panel web Next.js (lexia-app)
- [ ] Crear repo `github.com/AIhectorsilva/lexia-app`
- [ ] Setup inicial Next.js 14 + TypeScript + Tailwind + shadcn/ui
- [ ] Conectar Supabase (auth + DB + RLS multi-tenant)
- [ ] Ruta `/onboarding` — cold-start como formulario web paso a paso
      → Equivalente al `cold-start-interview-es` pero en UI web
      → Guardar perfil en Supabase (tabla `despachos`)
- [ ] Ruta `/dashboard` — 8 skills como cards accionables
- [ ] Ruta `/skill/[nombre]` — interfaz de cada skill
      → Input del usuario → llamada a API con SKILL.md como system prompt
      → Output formateado + opciones de exportar/guardar
- [ ] Ruta `/perfil` — ver/editar el perfil de práctica
- [ ] Ruta `/historial` — outputs generados anteriores
- [ ] Conectar SKILL.md con Anthropic API
      → `system` = contenido del SKILL.md
      → `user` = perfil del despacho (desde Supabase) + input del usuario
- [ ] Implementar RLS en todas las tablas de Supabase
- [ ] Diseño UX del onboarding — 6 pasos como en el cold-start

### Mejoras detectadas en skills LOPD durante la sesión

- [ ] **`respondedor-arsulipo-es`**: añadir flujo específico para
      denegaciones parciales con plantilla de carta de denegación motivada
      (actualmente redirige a escalación sin plantilla)
- [ ] **`notificador-brecha-aepd`**: añadir integración con formulario
      real de la sede AEPD (campos exactos del formulario electrónico)
      cuando Sprint 2 conecte el MCP de sede AEPD
- [ ] **`generador-pias-aepd`**: añadir skill companion
      `generador-rat-es` para generar el Registro de Actividades
      de Tratamiento (Art. 30 RGPD) directamente desde la EIPD
- [ ] **`cold-start-interview-es`**: añadir bloque 7 opcional para
      despachos que asesoran a clientes con tratamientos de categorías
      especiales (sector sanitario, RRHH, etc.)
- [ ] **Todos los skills**: cuando Sprint 2 conecte BOE y AEPD,
      revisar todas las citas `[VERIFICAR]` y promover las que
      los MCP puedan resolver

### Área Laboral (employment-legal-es) — próxima área a construir
- [ ] Analizar skills del plugin `employment-legal` original
- [ ] Mapear equivalencias con derecho laboral español
      → ET (Real Decreto Legislativo 2/2015)
      → LISOS (Real Decreto Legislativo 5/2000)
      → LRJS (Ley 36/2011)
      → Convenios colectivos sectoriales
- [ ] Scaffold del plugin `employment-legal-es`
- [ ] Skills previstos (9):
      - `cold-start-interview-laboral-es`
      - `revisor-contrato-trabajo-es`
      - `clasificador-riesgo-despido-es`
      - `generador-carta-despido-es`
      - `analizador-convenio-colectivo-es`
      - `triador-clasificacion-trabajador-es`
      - `generador-politica-teletrabajo-es`
      - `monitor-compliance-laboral-es`
      - `calculador-indemnizacion-es`

---

## 🔵 PRIORIDAD BAJA / BACKLOG

### Áreas legales futuras
- [ ] `commercial-legal-es` — Mercantil y contratos
- [ ] `corporate-legal-es` — Societario y M&A
- [ ] `litigation-legal-es` — Litigios y procedimiento
- [ ] `ip-legal-es` — Propiedad intelectual
- [ ] `regulatory-legal-es` — Regulatorio sectorial

### Infraestructura
- [ ] CI/CD — GitHub Actions para validar SKILL.md en cada PR
      → `scripts/validate.py` del repo original como base
- [ ] Tests de regresión para los 9 skills de `privacy-legal-es`
      → Casos de prueba documentados con inputs y outputs esperados
- [ ] Dominio `lexia.demalia.es` — DNS y SSL
- [ ] Monitoring de la API — alertas de errores y latencia

### Producto
- [ ] Pricing y planes de Lexia (definir con Izan)
- [ ] Onboarding deck para primeros clientes (con Dani)
- [ ] Demo grabada de los 8 skills LOPD para prospección (con Izan)
- [ ] Landing page de Lexia (cuando haya panel web)

### Mejoras de UX para el panel web
- [ ] Exportar outputs como PDF / Word
- [ ] Historial de conversaciones por cliente/asunto
- [ ] Notificaciones de plazos (próximo vencimiento ARSULIPO, etc.)
- [ ] Integración con firma digital (Signaturit / DocuSign)

---

## ✅ Completado en Sprint 1

- [x] Fork y setup de `claude-for-legal`
- [x] Scaffold de `privacy-legal-es`
- [x] `CLAUDE.md` — perfil de práctica template español
- [x] `cold-start-interview-es` — onboarding del despacho
- [x] `respondedor-arsulipo-es`
- [x] `notificador-brecha-aepd`
- [x] `triador-privacidad-es`
- [x] `generador-pias-aepd`
- [x] `revisor-dpa-encargado`
- [x] `generador-clausulas-rgpd`
- [x] `analizador-gap-regulatorio`
- [x] `monitor-politica-privacidad`
- [x] Perfil de Demalia Consulting generado y activo en disco
- [x] `PROYECTO.md` — documentación maestra del proyecto
- [x] `TODO.md` — este archivo

---

*Demalia Consulting · hector@demaliaconsulting.com*
*Sprint 1 completado: 19/05/2026*
*Sprint 2 objetivo: panel web + MCPs + Enterprise Anthropic*
