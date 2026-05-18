---
name: generador-pias-aepd
description: >
  Genera Evaluaciones de Impacto en la Protección de Datos (EIPD) completas
  conforme a la metodología de la AEPD y el Art. 35 RGPD. Conduce una
  entrevista de intake sobre el tratamiento propuesto, analiza necesidad y
  proporcionalidad, identifica y evalúa riesgos, propone medidas mitigadoras
  y genera el documento EIPD en formato profesional listo para revisión letrada.
  Úsalo cuando el triador-privacidad-es haya determinado EIPD OBLIGATORIA o
  EIPD RECOMENDADA, o cuando el usuario diga "necesito hacer una EIPD",
  "tengo que hacer una evaluación de impacto", "el DPD me pide una EIPD",
  o "quiero documentar el análisis de riesgos de este tratamiento".
  No iniciar este skill si el triador ha emitido resultado STOP — una EIPD
  no subsana la falta de base jurídica.
argument-hint: "[describe el tratamiento — o di 'vengo del triador' si ya lo analizaste]"
---

# /generador-pias-aepd

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: rol del despacho, sectores, DPD si existe, EIPD de referencia
   del despacho (sección 8).
2. Si viene del triador-privacidad-es, reutiliza la información ya recopilada
   sin preguntar de nuevo.
3. Completa el intake con lo que falte (Paso 1).
4. Genera la EIPD completa siguiendo la estructura de la guía metodológica
   de la AEPD. [FUENTE: AEPD]
5. Output: documento EIPD completo — borrador para revisión letrada y DPD.
6. El tratamiento NO puede iniciarse hasta que la EIPD esté finalizada,
   revisada y aprobada. [FUENTE: RGPD]
/privacy-legal-es:generador-pias-aepd
[describe el tratamiento o di "vengo del triador"]

---

# Generador de EIPD — Evaluación de Impacto en la Protección de Datos

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`.
Si existe una EIPD de referencia del despacho (sección 8), úsala como
plantilla de formato y estilo. Si no, aplica la estructura de la guía
metodológica de la AEPD. [FUENTE: AEPD]

**Marco jurisdiccional:** España. Art. 35-36 RGPD + guía metodológica AEPD
+ directrices WP248rev.01 CEPD. [FUENTE: AEPD] [VERIFICAR — WP248rev.01]

---

## PASO 1 — Intake del tratamiento

Si vienes del triador, los campos ya recopilados no se preguntan de nuevo.
Completa solo lo que falte para la EIPD:

**Información básica (del triador o nueva):**
- Nombre del tratamiento / proyecto
- Responsable del tratamiento (nombre + NIF)
- DPD o contacto de privacidad (si existe)
- Fecha de inicio prevista
- Descripción detallada de la finalidad
- Categorías de datos personales tratados
- Categorías de interesados afectados
- Volumen aproximado de interesados
- Base jurídica (Art. 6 RGPD + Art. 9.2 si categorías especiales)

**Información adicional para la EIPD:**
- ¿Cómo se recogen los datos? (directamente del interesado / de terceros /
  generados automáticamente)
- ¿Dónde se almacenan? (sistemas internos / nube / encargados)
- ¿Quién tiene acceso? (perfiles de acceso)
- ¿Cuánto tiempo se conservan?
- ¿Se comunican a terceros? ¿Cuáles? ¿Con qué base?
- ¿Hay transferencias internacionales? ¿A qué países? ¿Con qué garantías?
- ¿Hay decisiones automatizadas o perfilado?
- ¿Qué medidas de seguridad técnicas y organizativas existen ya?
- ¿Se ha consultado al DPD? ¿Cuál es su posición?

---

## PASO 2 — Generación del documento EIPD

Genera el documento completo con la siguiente estructura:

---
EVALUACIÓN DE IMPACTO EN LA PROTECCIÓN DE DATOS (EIPD)
Conforme al Art. 35 del Reglamento (UE) 2016/679 (RGPD)
y la Guía metodológica de la AEPD
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DOCUMENTO BORRADOR — Revisión letrada y DPD obligatoria
antes de aprobar e iniciar el tratamiento
Referencia:      EIPD-[AÑO]-[NÚM]
Versión:         0.1 — Borrador inicial
Fecha:           DD/MM/AAAA
Responsable:     [nombre del responsable del tratamiento]
Elaborado por:   [nombre — generado con asistencia Lexia/Demalia]
DPD consultado:  [Sí/No/No designado]

### SECCIÓN 1 — DESCRIPCIÓN DEL TRATAMIENTO

**1.1 Identificación**

| Campo | Valor |
|---|---|
| Nombre del tratamiento | [nombre] |
| Responsable | [nombre + NIF] |
| DPD / Contacto privacidad | [nombre + email] |
| Encargados del tratamiento | [listar] |
| Fecha prevista de inicio | DD/MM/AAAA |
| Fecha de esta EIPD | DD/MM/AAAA |

**1.2 Descripción de la finalidad y del tratamiento**

[Descripción detallada en lenguaje claro de qué se hace con los datos,
para qué, cómo y sobre quién. Mínimo 3-5 párrafos cubriendo: contexto
del tratamiento, finalidad específica, flujo de datos desde la recogida
hasta la supresión, sistemas implicados y actores involucrados.]

**1.3 Categorías de datos y de interesados**

| Categoría de datos | Fuente | ¿Cat. especial Art. 9? | Volumen aprox. |
|---|---|---|---|
| [dato] | [origen] | Sí/No | [número] |

**1.4 Base jurídica**

| Finalidad | Base Art. 6 RGPD | Base Art. 9.2 (si aplica) |
|---|---|---|
| [finalidad] | Art. 6.1.[x] — [descripción] | Art. 9.2.[x] / N/A |

**1.5 Plazos de conservación**

| Categoría de datos | Plazo | Justificación |
|---|---|---|
| [dato] | [plazo] | [base legal o criterio] |

**1.6 Destinatarios y transferencias**

| Destinatario | Relación | Base de la comunicación | ¿Transferencia internacional? |
|---|---|---|---|
| [nombre] | Encargado/Responsable independiente | [base] | Sí/No — [garantías si sí] |

---

### SECCIÓN 2 — NECESIDAD Y PROPORCIONALIDAD

Evalúa si el tratamiento cumple los principios del Art. 5 RGPD:
[FUENTE: RGPD]

**2.1 Licitud, lealtad y transparencia (Art. 5.1.a)**
[Análisis: ¿existe base jurídica válida? ¿Se informa a los interesados?]

**2.2 Limitación de la finalidad (Art. 5.1.b)**
[Análisis: ¿los datos se usan solo para la finalidad declarada?
¿Hay riesgo de misuse o function creep?]

**2.3 Minimización de datos (Art. 5.1.c)**
[Análisis: ¿se recogen solo los datos estrictamente necesarios?
¿Podrían lograrse los mismos fines con menos datos o datos menos sensibles?]

**2.4 Exactitud (Art. 5.1.d)**
[Análisis: ¿hay mecanismos para mantener los datos exactos y actualizados?]

**2.5 Limitación del plazo de conservación (Art. 5.1.e)**
[Análisis: ¿los plazos de conservación están justificados y son los mínimos
necesarios? ¿Hay procedimiento de supresión al vencer el plazo?]

**2.6 Integridad y confidencialidad (Art. 5.1.f)**
[Análisis: ¿las medidas de seguridad son adecuadas al riesgo?]

**2.7 Proporcionalidad general**
[Conclusión: ¿el tratamiento es necesario y proporcionado a su finalidad?
¿Existe alguna alternativa menos intrusiva que logre el mismo objetivo?]

---

### SECCIÓN 3 — IDENTIFICACIÓN Y EVALUACIÓN DE RIESGOS

Para cada riesgo identificado, evalúa probabilidad e impacto
(escala: Bajo / Medio / Alto / Muy alto) y calcula el nivel
de riesgo inherente (antes de medidas mitigadoras).

**3.1 Catálogo de riesgos**

Analiza al menos los siguientes riesgos según el tipo de tratamiento:

| # | Riesgo | Descripción | Probabilidad | Impacto | Riesgo inherente |
|---|---|---|---|---|---|
| R1 | Acceso no autorizado | Acceso a los datos por personas no autorizadas (interno o externo) | [B/M/A/MA] | [B/M/A/MA] | [B/M/A/MA] |
| R2 | Filtración / divulgación | Divulgación accidental o malintencionada de datos a terceros | [B/M/A/MA] | [B/M/A/MA] | [B/M/A/MA] |
| R3 | Pérdida / destrucción | Pérdida o destrucción de datos (accidental, ataque, desastre) | [B/M/A/MA] | [B/M/A/MA] | [B/M/A/MA] |
| R4 | Alteración | Modificación no autorizada o accidental de los datos | [B/M/A/MA] | [B/M/A/MA] | [B/M/A/MA] |
| R5 | Uso indebido de finalidad | Uso de los datos para finalidades distintas a las declaradas | [B/M/A/MA] | [B/M/A/MA] | [B/M/A/MA] |
| R6 | Decisiones automatizadas erróneas | Decisiones incorrectas con impacto en interesados | [aplica si hay autom.] | | |
| R7 | Ejercicio de derechos impedido | Dificultad o imposibilidad de ejercer derechos ARSULIPO | [B/M/A/MA] | [B/M/A/MA] | [B/M/A/MA] |
| R8 | [Riesgo específico del tratamiento] | [según el contexto] | | | |

**3.2 Consecuencias para los interesados**

Para cada riesgo de nivel Alto o Muy alto, describe las consecuencias
concretas para los interesados afectados:
- Daño económico (fraude, robo de identidad)
- Discriminación
- Daño reputacional
- Pérdida de confidencialidad
- Consecuencias físicas o psicológicas
- Limitación de derechos

---

### SECCIÓN 4 — MEDIDAS PARA MITIGAR LOS RIESGOS

Para cada riesgo identificado, define las medidas mitigadoras y
recalcula el riesgo residual tras su aplicación.

**4.1 Medidas técnicas**

| Medida | Riesgos que mitiga | Estado | Responsable | Fecha implantación |
|---|---|---|---|---|
| Cifrado de datos en reposo y tránsito | R1, R2, R3 | [Implantada/Planificada/Pendiente] | [nombre] | DD/MM/AAAA |
| Control de acceso basado en roles (RBAC) | R1, R5 | | | |
| Registro de accesos y auditoría (logs) | R1, R5 | | | |
| Copias de seguridad y plan de recuperación | R3 | | | |
| Seudonimización donde sea posible | R1, R2 | | | |
| [Medida específica del tratamiento] | | | | |

**4.2 Medidas organizativas**

| Medida | Riesgos que mitiga | Estado | Responsable | Fecha implantación |
|---|---|---|---|---|
| Cláusulas de confidencialidad con personal | R1, R2, R5 | | | |
| Formación en protección de datos | R1, R2, R5 | | | |
| Procedimiento de gestión de brechas | R1, R2, R3 | | | |
| Contrato encargado (Art. 28 RGPD) con proveedores | R1, R2 | | | |
| Procedimiento de atención de derechos ARSULIPO | R7 | | | |
| [Medida específica del tratamiento] | | | | |

**4.3 Riesgo residual tras medidas**

| # | Riesgo | Riesgo inherente | Medidas aplicadas | Riesgo residual |
|---|---|---|---|---|
| R1 | Acceso no autorizado | [B/M/A/MA] | [lista] | [B/M/A/MA] |
| R2 | Filtración | [B/M/A/MA] | [lista] | [B/M/A/MA] |
| ... | | | | |

---

### SECCIÓN 5 — CONSULTA AL DPD

**5.1 ¿Existe DPD designado?**
[Sí — nombre + fecha designación / No designado]

**5.2 ¿Se ha consultado al DPD?**
[Sí — fecha consulta + resumen de su posición /
No — justificación (no es obligatoria si no hay DPD, pero sí recomendable)]

**5.3 Posición del DPD:**
[Favorable / Desfavorable — con condiciones / Pendiente]
[Resumen de observaciones del DPD si las hay]

---

### SECCIÓN 6 — CONCLUSIÓN Y DECISIÓN

**6.1 Nivel de riesgo residual global**

| Nivel de riesgo residual | Conclusión |
|---|---|
| Bajo / Medio | El tratamiento puede iniciarse con las medidas implantadas |
| Alto | El tratamiento puede iniciarse si se implantan las medidas pendientes antes del inicio |
| Muy alto | Consulta previa obligatoria a la AEPD antes de iniciar (Art. 36 RGPD) [FUENTE: RGPD] |

**6.2 ¿Se requiere consulta previa a la AEPD?**
[ ] No — riesgo residual aceptable
[ ] Sí — riesgo alto residual no mitigable → Art. 36 RGPD [FUENTE: RGPD]
    Plazo de respuesta AEPD: 8 semanas (prorrogables 6 semanas más)
    [FUENTE: AEPD]

**6.3 Condiciones para iniciar el tratamiento**

[Listar las medidas pendientes que deben implantarse antes del inicio,
con responsable y fecha límite para cada una]

**6.4 Revisión periódica**

Esta EIPD debe revisarse cuando:
- Cambie la finalidad o el alcance del tratamiento
- Se incorporen nuevas categorías de datos o interesados
- Cambien los encargados del tratamiento
- Se produzca una brecha de seguridad relacionada
- Como mínimo cada [2 años / según política del despacho]

---

### SECCIÓN 7 — APROBACIÓN Y CONTROL DE VERSIONES
┌─────────────────────────────────────────────────────┐
│ APROBACIÓN DE LA EIPD                               │
│                                                     │
│ Elaborado por:  ________________  Fecha: //____ │
│ Revisado por                                        │
│ (letrado):      ________________  Fecha: //____ │
│ DPD:            ________________  Fecha: //____ │
│ Aprobado por                                        │
│ (responsable):  ________________  Fecha: //____ │
│                                                     │
│ ESTADO: [ ] Borrador  [ ] En revisión  [ ] Aprobada │
└─────────────────────────────────────────────────────┘
Control de versiones:
v0.1 — DD/MM/AAAA — Borrador inicial (generado con Lexia)
v0.2 — DD/MM/AAAA — [próxima revisión]

---

## PASO 3 — Diferencial con política de privacidad

Tras generar la EIPD, compara el tratamiento documentado contra
la política de privacidad pública del despacho (URL en CLAUDE.md
sección 8):

**¿El tratamiento está recogido en la política de privacidad vigente?**
- [ ] Sí — coherente con lo publicado
- [ ] No — la política debe actualizarse antes de iniciar el tratamiento
- [ ] Parcialmente — indicar qué falta cubrir

Si la política debe actualizarse → ofrecer
`/privacy-legal-es:monitor-politica-privacidad` para generar
el diff y el borrador de actualización.

---

## Guardrails obligatorios

- **El tratamiento no puede iniciarse hasta que la EIPD esté aprobada**
  por el letrado responsable. [FUENTE: RGPD]
- **Si el riesgo residual es Muy alto: consulta previa a la AEPD
  obligatoria** antes de iniciar. No omitir este paso. [FUENTE: RGPD]
- **No generar EIPD si el triador ha emitido STOP** — una EIPD no
  subsana la falta de base jurídica del tratamiento.
- **DPD debe ser consultado siempre que exista** — su posición debe
  constar en la EIPD. [FUENTE: RGPD]
- Citar siempre [FUENTE: RGPD], [FUENTE: AEPD], [VERIFICAR].
- Marcar todos los outputs como borrador para revisión letrada.
- No reproducir más datos personales de los interesados de los
  estrictamente necesarios.