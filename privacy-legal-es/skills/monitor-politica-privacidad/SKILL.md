---
name: monitor-politica-privacidad
description: >
  Detecta la deriva entre la política de privacidad publicada por el despacho
  o el cliente y la práctica real del tratamiento de datos. Compara la política
  vigente contra el perfil de práctica del CLAUDE.md, los cambios de tratamiento
  comunicados y la normativa actual. Genera un diff marcado con los puntos de
  deriva y un borrador de política actualizada para revisión letrada.
  Úsalo cuando el usuario diga "quiero revisar mi política de privacidad",
  "han cambiado nuestros tratamientos y no hemos actualizado la política",
  "el DPD dice que la política está desactualizada", "necesito actualizar
  el aviso de privacidad", o "han pasado más de 12 meses desde la última
  revisión de la política".
  También se activa automáticamente cuando generador-pias-aepd o
  analizador-gap-regulatorio detectan que la política necesita actualización.
argument-hint: "[pega la política actual o su URL + describe los cambios en la práctica]"
---

# /monitor-politica-privacidad

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: URL de la política vigente, tratamientos actuales, encargados,
   DPD, fecha de última revisión.
2. Obtiene el texto de la política actual (del usuario o de la URL).
3. Identifica los cambios en la práctica respecto a lo declarado en la política.
4. Compara contra los requisitos del Art. 13 RGPD.
5. Genera el diff de deriva y el borrador de política actualizada.
6. Todos los outputs son borradores para revisión letrada antes de publicar.
/privacy-legal-es:monitor-politica-privacidad
[pega la política actual o su URL + describe los cambios en la práctica]

---

# Monitor de Política de Privacidad

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`.
Si no existe el perfil, solicita al usuario la política actual y los
cambios en la práctica, y etiqueta como `[PERFIL NO CONFIGURADO]`.

**Marco jurisdiccional:** España.
- Información obligatoria: Arts. 13-14 RGPD [FUENTE: RGPD]
- Principio de transparencia: Art. 5.1.a RGPD [FUENTE: RGPD]
- Lenguaje claro y sencillo: Art. 12.1 RGPD [FUENTE: RGPD]
- Guía política de privacidad AEPD [FUENTE: AEPD]

---

## PASO 1 — Recopilación de la política actual y los cambios

**Obtén:**

| Elemento | Fuente |
|---|---|
| Texto de la política actual | URL del CLAUDE.md / pegado por el usuario |
| Fecha de la última actualización | Del propio documento |
| Tratamientos actuales del despacho/cliente | CLAUDE.md sección 2 / usuario |
| Cambios en la práctica desde la última revisión | Usuario |
| Encargados actuales | CLAUDE.md sección 4 / usuario |
| DPD actual | CLAUDE.md / usuario |
| Nuevas transferencias internacionales | Usuario |
| Nuevas finalidades o bases jurídicas | Usuario |

**Alerta de antigüedad:**
Si la política tiene más de 12 meses sin revisión → advertir:
"⚠️ La política no se ha revisado en más de 12 meses. Aunque no
hayan cambiado los tratamientos, es recomendable una revisión
periódica para verificar que sigue siendo exacta y completa."
[FUENTE: AEPD]

---

## PASO 2 — Checklist Art. 13 RGPD

Verifica que la política actual contiene todos los elementos
obligatorios del Art. 13 RGPD. [FUENTE: RGPD]

| # | Elemento obligatorio | ¿Presente? | ¿Correcto? | ¿Actualizado? |
|---|---|---|---|---|
| 1 | Identidad y datos de contacto del responsable | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 2 | Datos de contacto del DPD (si existe) | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 3 | Finalidades del tratamiento | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 4 | Base jurídica de cada tratamiento | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 5 | Intereses legítimos (si es la base jurídica) | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 6 | Destinatarios o categorías de destinatarios | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 7 | Transferencias internacionales y garantías | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 8 | Plazos de conservación | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 9 | Derecho de acceso | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 10 | Derecho de rectificación | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 11 | Derecho de supresión | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 12 | Derecho de limitación | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 13 | Derecho de portabilidad | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 14 | Derecho de oposición | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 15 | Derecho a retirar el consentimiento | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 16 | Derecho a reclamar ante la AEPD | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |
| 17 | Si hay decisiones automatizadas: lógica + consecuencias | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ |

---

## PASO 3 — Detección de deriva

Compara sistemáticamente la práctica real contra lo declarado en
la política. Para cada punto de deriva, genera una ficha:
DERIVA [N] — [Título]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Tipo:             [ ] Tratamiento nuevo no declarado
[ ] Tratamiento modificado
[ ] Encargado nuevo no declarado
[ ] Transferencia internacional nueva
[ ] Base jurídica incorrecta o cambiada
[ ] Plazo de conservación incorrecto
[ ] Derecho ARSULIPO mal descrito
[ ] Dato de contacto desactualizado
[ ] Elemento Art. 13 ausente
[ ] Lenguaje confuso o no claro (Art. 12.1 RGPD)
Descripción:      [qué dice la política vs. qué ocurre en la práctica]
Riesgo:           [Alto / Medio / Bajo — descripción del riesgo]
Referencia legal: [Art. X RGPD / Guía AEPD]
Acción requerida: [actualizar política / actualizar práctica / ambas]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**Tipos de deriva más frecuentes a detectar:**

1. **Nuevos encargados no declarados** — proveedor de cloud, SaaS,
   gestoría, email marketing contratado después de publicar la política
2. **Nuevas transferencias internacionales** — encargado que usa
   infraestructura fuera del EEE sin declararlo
3. **Nuevas finalidades** — uso de datos para fines no previstos
   en la política original (function creep)
4. **Base jurídica incorrecta** — política dice "interés legítimo"
   pero en la práctica se pide consentimiento, o viceversa
5. **Plazos de conservación genéricos** — "el tiempo necesario"
   sin concretar — incumple el deber de información [FUENTE: AEPD]
6. **DPD no actualizado** — cambio de DPD no reflejado
7. **Contacto de ejercicio de derechos inoperativo** — email
   desactualizado o formulario que no funciona
8. **Lenguaje no claro** — términos técnicos sin explicación,
   párrafos de más de 5 líneas sin estructura, ausencia de capas
   de información [FUENTE: AEPD]
9. **Ausencia de mención a reclamación ante AEPD** — obligatorio
   en toda política [FUENTE: RGPD]
10. **Política no fechada o sin versión** — dificulta acreditar
    qué versión estaba vigente en cada momento

---

## PASO 4 — Log de cambios

Genera el log de cambios para control de versiones:
LOG DE CAMBIOS — POLÍTICA DE PRIVACIDAD
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Versión anterior: [N] — [DD/MM/AAAA]
Versión propuesta: [N+1] — [DD/MM/AAAA]
Elaborado por: [nombre] con asistencia Lexia/Demalia
Revisión letrada: [pendiente — nombre + fecha]
CAMBIOS PROPUESTOS:
┌─────┬──────────────────────────────┬─────────────────────────────────┬─────────┐
│  #  │        Sección afectada      │         Cambio propuesto        │ Motivo  │
├─────┼──────────────────────────────┼─────────────────────────────────┼─────────┤
│  1  │ [sección]                    │ [descripción del cambio]        │ [causa] │
│  2  │                              │                                 │         │
└─────┴──────────────────────────────┴─────────────────────────────────┴─────────┘
CAMBIOS QUE REQUIEREN NUEVA RECOGIDA DE CONSENTIMIENTO:
[ ] Sí — [describir cuáles y por qué]
[ ] No — los cambios son actualizaciones de información, no de base
jurídica ni de finalidad
COMUNICACIÓN A INTERESADOS:
[ ] Requerida — cambio material en tratamiento o base jurídica
[ ] Recomendada — cambio significativo aunque no material
[ ] No requerida — actualización menor de información
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

## PASO 5 — Borrador de política actualizada

Genera la política de privacidad actualizada completa, integrando
todos los cambios detectados. Sigue el mismo formato que el
generador-clausulas-rgpd pero aplicado a la política existente:

- Mantener la estructura y el tono de la política original
  donde sea correcto
- Sustituir o añadir solo lo que ha derivado o falta
- Marcar con `[MODIFICADO]` las secciones cambiadas
- Marcar con `[NUEVO]` las secciones añadidas
- Marcar con `[ELIMINADO — ver nota]` lo que se suprime
- Conservar `[COMPLETAR]` donde falte información del responsable
- Fecha de la nueva versión: DD/MM/AAAA (fecha de aprobación,
  no de generación del borrador)

**Criterios de lenguaje claro** (Art. 12.1 RGPD + Guía AEPD):
[FUENTE: RGPD] [FUENTE: AEPD]
- Frases cortas, párrafos de máximo 5 líneas
- Sin latinismos ni tecnicismos sin explicar
- Estructura con epígrafes numerados y títulos claros
- Información en capas: resumen en la primera capa,
  detalle en secciones expandibles o enlazadas
- Uso de "usted" en comunicaciones formales
- Verbos en activo: "tratamos sus datos" no "sus datos son tratados"

---

## PASO 6 — Resumen ejecutivo
RESUMEN MONITOR DE POLÍTICA
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Política analizada:       [nombre/URL]
Versión actual:           [N] — [DD/MM/AAAA]
Fecha del análisis:       DD/MM/AAAA
Antigüedad de la política: [X meses]
ELEMENTOS ART. 13 RGPD:
Presentes y correctos:  [N]/17
Ausentes o incorrectos: [N]
PUNTOS DE DERIVA:         [N] total
Alto riesgo:            [N]
Riesgo medio:           [N]
Riesgo bajo:            [N]
¿REQUIERE NUEVA RECOGIDA DE CONSENTIMIENTO?
[ ] Sí — [describir]
[ ] No
¿REQUIERE COMUNICACIÓN A INTERESADOS?
[ ] Sí — [describir]
[ ] No
RECOMENDACIÓN:
[ ] Actualización urgente — deriva de alto riesgo detectada
[ ] Actualización recomendada — deriva de riesgo medio
[ ] Revisión menor — sin deriva significativa
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  Borrador para revisión letrada antes de publicar.
Nunca publicar la política actualizada sin validación
letrada previa.

---

## Guardrails obligatorios

- **Nunca publicar directamente** — la política actualizada es
  siempre un borrador para revisión letrada. [FUENTE: AEPD]
- **Cambio de finalidad o base jurídica → nueva recogida de
  consentimiento** si la base original era el consentimiento.
  [FUENTE: RGPD]
- **Cambio material en el tratamiento → comunicar a interesados**
  antes de publicar la nueva política. [FUENTE: RGPD]
- **Lenguaje claro es obligatorio, no opcional** — Art. 12.1 RGPD.
  Si la política original usa lenguaje opaco, corregirlo en el
  borrador. [FUENTE: RGPD]
- **Siempre incluir la mención a la AEPD** como autoridad ante
  la que reclamar — es elemento obligatorio del Art. 13 RGPD.
  [FUENTE: RGPD]
- **Alerta si la política tiene más de 12 meses** sin revisión —
  aunque no haya cambios declarados, recomendar revisión.
  [FUENTE: AEPD]
- Citar siempre [FUENTE: RGPD], [FUENTE: AEPD], [FUENTE: BOE],
  [VERIFICAR].
- Si al analizar la política aparecen datos personales de
  terceros (clientes, empleados), manejar con la misma cautela
  que el respondedor-arsulipo-es.