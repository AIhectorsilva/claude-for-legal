---
name: analizador-gap-regulatorio
description: >
  Compara una nueva norma, resolución, guía o criterio de la AEPD contra el
  estado actual de las políticas y procedimientos del despacho o del cliente,
  e identifica las brechas (gaps) existentes. Genera un plan de remediación
  con propietario, plazo propuesto y prioridad según el riesgo sancionador.
  Úsalo cuando el usuario diga "ha salido una nueva norma de protección de
  datos", "la AEPD ha publicado una guía nueva", "me afecta el nuevo
  reglamento X", "necesito saber qué tengo que cambiar", "quiero hacer un
  gap analysis de privacidad", o "¿cómo nos afecta esta resolución?".
argument-hint: "[pega o describe la nueva norma/guía/resolución + describe tu situación actual]"
---

# /analizador-gap-regulatorio

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: rol del despacho, sectores, política de privacidad vigente,
   procedimientos actuales, contacto de escalación.
2. Identifica la fuente normativa (BOE, DOUE, AEPD, CEPD) y su naturaleza
   (norma vinculante / guía interpretativa / resolución sancionadora /
   criterio de la AEPD).
3. Extrae los requisitos concretos que impone la nueva normativa.
4. Compara contra el estado actual del despacho/cliente.
5. Genera la tabla de gaps con prioridad y plan de remediación.
6. Todos los outputs son borradores para revisión letrada.
/privacy-legal-es:analizador-gap-regulatorio
[pega la nueva norma o descríbela + describe tu situación actual]

---

# Análisis de Brechas Regulatorias — Privacidad y Protección de Datos

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`.
Si no existe el perfil, aplica análisis genérico y etiqueta como
`[PERFIL NO CONFIGURADO]`.

**Fuentes normativas aplicables — España:**
- BOE: legislación española [FUENTE: BOE]
- DOUE: legislación y directrices de la UE [FUENTE: RGPD]
- AEPD: guías, resoluciones, criterios interpretativos [FUENTE: AEPD]
- CEPD: directrices del Comité Europeo de Protección de Datos [VERIFICAR]
- CENDOJ: jurisprudencia de tribunales españoles [señal manual — ver TODO.md]

**NO son fuentes aplicables:** FTC, state attorneys general, CCPA, HIPAA,
ni ninguna normativa estadounidense o de terceros países salvo que
expresamente sean normas de países adecuados reconocidos por la Comisión
Europea.

---

## PASO 1 — Identificación y clasificación de la fuente normativa

**Determina:**

| Campo | Valor |
|---|---|
| Nombre de la norma/guía/resolución | [extraer] |
| Tipo | Reglamento / Directiva / Ley / Guía AEPD / Resolución sancionadora / Criterio CEPD |
| Naturaleza | Vinculante / Interpretativa / Orientativa |
| Fecha de publicación | DD/MM/AAAA |
| Fecha de aplicación / entrada en vigor | DD/MM/AAAA |
| Referencia oficial | [BOE-X / DOUE L-X / Expediente AEPD X] |
| Ámbito de aplicación | ¿A quién aplica? ¿Qué sectores? ¿Qué tipos de tratamiento? |
| Tiempo hasta cumplimiento obligatorio | [días/meses desde hoy] |

**Distinción crítica:**
- **Norma vinculante** (Reglamento UE, Ley, RD): cumplimiento obligatorio
  en la fecha de aplicación. Incumplimiento → sanción directa.
- **Guía AEPD**: interpretación de la autoridad de control. No es norma,
  pero marca el estándar que la AEPD aplicará en sus inspecciones y
  resoluciones. Ignorarla es un riesgo regulatorio real. [FUENTE: AEPD]
- **Resolución sancionadora**: precedente. Indica qué conductas ya ha
  sancionado la AEPD y con qué criterio. No crea obligación directa pero
  sí jurisprudencia administrativa.

---

## PASO 2 — Extracción de requisitos

Extrae los requisitos concretos que impone la norma. Para cada requisito:

| # | Requisito | Artículo/Sección | Tipo | Plazo |
|---|---|---|---|---|
| R1 | [descripción concreta del requisito] | [referencia] | Obligatorio/Recomendado | [plazo] |
| R2 | | | | |

**Categorías de requisitos a buscar:**
- Nuevas obligaciones de información a interesados
- Nuevos consentimientos o cambios en la base jurídica
- Nuevos registros o documentación obligatoria
- Cambios en plazos (conservación, respuesta, notificación)
- Nuevas medidas de seguridad técnicas u organizativas
- Nuevas EIPDs obligatorias o ampliación de los supuestos
- Obligaciones de designar DPD o ampliar sus funciones
- Restricciones o prohibiciones de nuevos tratamientos
- Obligaciones de notificación a la AEPD
- Cambios en el régimen de encargados o subencargados
- Nuevos derechos de los interesados

---

## PASO 3 — Estado actual del despacho/cliente

Recopila el estado actual contra el que comparar. Extrae del CLAUDE.md
o pregunta al usuario:

| Área | Estado actual | Fuente |
|---|---|---|
| Política de privacidad | [URL / fecha última actualización] | CLAUDE.md / usuario |
| Registro de actividades | [Existe / No existe / Desactualizado] | usuario |
| Procedimiento ARSULIPO | [Existe / No / Parcial] | usuario |
| Contratos de encargado | [Todos firmados / Algunos / Ninguno] | usuario |
| Medidas de seguridad | [Descripción] | usuario |
| EIPD realizadas | [Cuáles / Ninguna] | usuario |
| DPD designado | [Sí / No / No obligatorio] | usuario |
| Formación del personal | [Cuándo / Nunca] | usuario |

---

## PASO 4 — Tabla de gaps

Para cada requisito de la norma, compara con el estado actual y
determina si existe brecha:
ANÁLISIS DE BRECHAS — [NOMBRE DE LA NORMA]
Responsable/Cliente: [COMPLETAR]
Fecha del análisis:  DD/MM/AAAA
[PERFIL NO CONFIGURADO si aplica]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

| # | Requisito | Estado actual | Gap | Prioridad | Riesgo sancionador |
|---|---|---|---|---|---|
| R1 | [requisito] | [estado] | ✅ Cumplido / ⚠️ Parcial / ❌ Incumplido | Alta/Media/Baja | Art. 83.X RGPD — hasta [X]M€ / N/A |
| R2 | | | | | |

**Criterios de prioridad:**

| Prioridad | Criterio |
|---|---|
| **CRÍTICA** | Incumplimiento ya sancionable + plazo vencido o inminente (<30 días) |
| **ALTA** | Incumplimiento sancionable con plazo 30-90 días / categorías especiales afectadas |
| **MEDIA** | Incumplimiento sancionable con plazo >90 días / sin categorías especiales |
| **BAJA** | Recomendación / buena práctica / guía no vinculante |

**Escala sancionadora RGPD para contextualizar:** [FUENTE: RGPD]
- Infracciones graves (Art. 83.5): hasta 20.000.000€ o 4% facturación
  global anual (la mayor)
- Infracciones menos graves (Art. 83.4): hasta 10.000.000€ o 2%
  facturación global anual (la mayor)
- Infracciones LOPDGDD (Arts. 72-74): muy graves / graves / leves
  [FUENTE: BOE]

---

## PASO 5 — Plan de remediación

Para cada gap identificado, genera la ficha de remediación:
GAP [N] — [Título]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Requisito:        [descripción]
Referencia legal: [Art. X norma Y]
Estado actual:    [descripción del gap]
Prioridad:        [CRÍTICA / ALTA / MEDIA / BAJA]
Riesgo:           [Art. 83.X RGPD — hasta X€ / orientativo]
Acción requerida: [descripción concreta de qué hay que hacer]
Propietario:      [rol — DPD / Letrado responsable / IT / RRHH]
Plazo propuesto:  DD/MM/AAAA
Dependencias:     [otras acciones que deben completarse antes]
Estado:           [ ] Pendiente  [ ] En curso  [ ] Completado
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

## PASO 6 — Resumen ejecutivo

Genera el resumen para presentar a la dirección o al cliente:
RESUMEN EJECUTIVO — GAP ANALYSIS
[NOMBRE DE LA NORMA]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Fecha del análisis:        DD/MM/AAAA
Fecha límite cumplimiento: DD/MM/AAAA
Tiempo disponible:         [X días/meses]
GAPS IDENTIFICADOS:        [N] total
Prioridad CRÍTICA:       [N]
Prioridad ALTA:          [N]
Prioridad MEDIA:         [N]
Prioridad BAJA:          [N]
ÁREAS MÁS AFECTADAS:

[área]
[área]
[área]

ACCIONES INMEDIATAS (antes de [fecha]):

[acción] — Propietario: [rol]
[acción] — Propietario: [rol]

EXPOSICIÓN REGULATORIA SIN REMEDIACIÓN:
[descripción del riesgo sancionador concreto]
COSTE ESTIMADO DE REMEDIACIÓN:
[Alto / Medio / Bajo — descripción cualitativa]
[Si el despacho tiene CLAUDE.md configurado con presupuesto: cifra]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  Borrador para revisión letrada antes de presentar
o compartir con el cliente.

---

## Guardrails obligatorios

- **Distinguir siempre entre norma vinculante y guía interpretativa** —
  el nivel de urgencia y el riesgo sancionador son diferentes.
- **Nunca minimizar el riesgo sancionador** — si hay incumplimiento
  de norma vinculante, indicar el artículo sancionador y el rango
  de la multa, aunque sea orientativo. [FUENTE: RGPD]
- **En caso de brecha CRÍTICA con plazo vencido: ESCALA** — revisión
  letrada urgente antes de cualquier otro paso.
- **Citar siempre la fuente** con [FUENTE: BOE], [FUENTE: AEPD],
  [FUENTE: RGPD], [VERIFICAR] cuando no hay fuente verificable.
- **CENDOJ:** las resoluciones de tribunales españoles son señal
  para búsqueda manual por el letrado — no citar jurisprudencia
  sin verificación. [VERIFICAR — búsqueda manual CENDOJ]
- Todos los outputs son borradores para revisión letrada.
- No usar normativa estadounidense como referencia bajo ningún
  concepto.