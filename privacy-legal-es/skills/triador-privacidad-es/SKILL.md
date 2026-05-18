---
name: triador-privacidad-es
description: >
  Determina si una actividad de tratamiento de datos personales requiere
  Evaluación de Impacto en la Protección de Datos (EIPD) obligatoria,
  evaluación recomendada por buenas prácticas, o puede proceder directamente
  sin evaluación formal. Aplica los criterios del Art. 35 RGPD, la lista
  positiva de la AEPD y las directrices WP248 del Comité Europeo de
  Protección de Datos.
  Úsalo cuando el usuario describa un nuevo tratamiento de datos, una nueva
  funcionalidad, un nuevo sistema, un nuevo proyecto con datos personales,
  o pregunte "¿necesito hacer una EIPD?", "¿puedo proceder con este
  tratamiento?", "¿qué evaluación necesito?", o "¿este tratamiento es legal?".
  Es la puerta de entrada al flujo completo de privacidad — cuando el
  resultado es EIPD OBLIGATORIA, ofrece arrancar el generador-pias-aepd
  en la misma conversación.
argument-hint: "[describe el tratamiento o actividad de datos — qué datos, para qué, cómo, sobre quién]"
---

# /triador-privacidad-es

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: rol del despacho, sectores de clientes, umbrales de triaje
   configurados en sección 5.
2. Si no existe el perfil, aplica umbrales por defecto RGPD/AEPD y etiqueta
   outputs como `[PERFIL NO CONFIGURADO]`.
3. Recopila la información necesaria del tratamiento (ver Paso 1).
4. Aplica el árbol de decisión paso a paso.
5. Emite la decisión con justificación completa y tabla de condiciones.
6. Si resultado = EIPD OBLIGATORIA o EIPD RECOMENDADA: ofrece arrancar
   `/privacy-legal-es:generador-pias-aepd` en la misma conversación.
7. Si resultado = STOP: escala antes de continuar — no generar documentación
   que legitime un tratamiento potencialmente ilícito.
/privacy-legal-es:triador-privacidad-es
[describe el tratamiento propuesto]

---

# Triaje de Privacidad — EIPD vs. Evaluación vs. Proceder

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`
sección 5 (umbrales de triaje). Si no existe, aplica los umbrales por defecto
del Art. 35 RGPD y la lista positiva de la AEPD.

**Marco jurisdiccional:** España. RGPD (UE) 2016/679 + LOPDGDD (LO 3/2018).
Autoridad de control: AEPD. Lista positiva de tratamientos que requieren EIPD
publicada por la AEPD. [FUENTE: AEPD]

---

## PASO 1 — Recopilación de información del tratamiento

Antes de triarlo, necesitas conocer el tratamiento. Extrae de la descripción
del usuario o pregunta lo que falte:

| Campo | Descripción | ¿Consta? |
|---|---|---|
| Finalidad | ¿Para qué se tratan los datos? | |
| Categorías de datos | ¿Qué datos personales se recogen/usan? | |
| Interesados | ¿Sobre quién? (clientes, empleados, usuarios, menores...) | |
| Base jurídica prevista | ¿Consentimiento, contrato, interés legítimo, obligación legal...? | |
| Escala | ¿Cuántas personas afectadas? ¿Volumen de registros? | |
| Tecnología | ¿Qué sistemas, herramientas, IA, sensores se usan? | |
| Decisiones automatizadas | ¿El sistema toma decisiones sin intervención humana? | |
| Terceros / encargados | ¿Intervienen proveedores externos? ¿Transferencias internacionales? | |
| Contexto | ¿Es tratamiento nuevo o modificación de uno existente? | |

Si el usuario ha dado suficiente información para triarlo, procede
directamente sin preguntar lo que ya consta.

---

## PASO 2 — Verificación de base jurídica

Antes de evaluar la necesidad de EIPD, verifica que el tratamiento
tiene base jurídica legítima bajo el Art. 6 RGPD:

| Base jurídica | Art. RGPD | Aplica cuando |
|---|---|---|
| Consentimiento | 6.1.a | El interesado ha dado consentimiento libre, específico, informado e inequívoco |
| Contrato | 6.1.b | Necesario para ejecutar un contrato con el interesado |
| Obligación legal | 6.1.c | Exigido por norma jurídica aplicable al responsable |
| Intereses vitales | 6.1.d | Para proteger la vida del interesado u otra persona |
| Interés público | 6.1.e | Misión en interés público o ejercicio de poderes públicos |
| Interés legítimo | 6.1.f | Interés legítimo del responsable o tercero, salvo que prevalezcan derechos del interesado |

Para datos de categorías especiales (Art. 9 RGPD): se requiere base
jurídica adicional del Art. 9.2 RGPD. [FUENTE: RGPD]

**Si no hay base jurídica clara → STOP antes de continuar.**
No triarlo como si fuera un problema de evaluación de impacto cuando
el problema de fondo es de licitud del tratamiento.

---

## PASO 3 — Árbol de decisión EIPD

### Nivel 1 — ¿Está en la lista positiva de la AEPD?

La AEPD ha publicado una lista de tipos de tratamiento que requieren
EIPD obligatoria. [FUENTE: AEPD] Verificar si el tratamiento encaja
en alguna de las siguientes categorías:

| Categoría AEPD | Descripción |
|---|---|
| 1 | Tratamientos que impliquen elaboración de perfiles con efectos jurídicos o significativos |
| 2 | Tratamientos a gran escala de categorías especiales (Art. 9) o datos penales (Art. 10) |
| 3 | Observación sistemática a gran escala de zonas de acceso público (videovigilancia) |
| 4 | Tratamientos de datos de personas vulnerables (menores, pacientes, empleados, personas con discapacidad) a gran escala |
| 5 | Tratamientos que impliquen uso de nuevas tecnologías o uso innovador de tecnologías existentes |
| 6 | Transferencias internacionales de datos a gran escala |
| 7 | Tratamientos que impidan a los interesados ejercer sus derechos o utilizar un servicio |
| 8 | Tratamientos con datos biométricos para identificación unívoca |
| 9 | Tratamientos con datos genéticos |

Si encaja en una o más categorías → **EIPD OBLIGATORIA** directamente.
[FUENTE: AEPD]

### Nivel 2 — Criterios WP248 del CEPD

Si no está en la lista positiva, aplicar los 9 criterios del WP248
revisado del Comité Europeo de Protección de Datos. [VERIFICAR — WP248rev.01]

Puntúa cada criterio (0 = no aplica / 1 = aplica):

| # | Criterio | Puntuación |
|---|---|---|
| 1 | Evaluación o puntuación de personas (scoring, profiling) | |
| 2 | Toma de decisiones automatizada con efectos jurídicos o significativos | |
| 3 | Observación sistemática de interesados | |
| 4 | Datos sensibles o de naturaleza muy personal (categorías especiales, datos financieros detallados, localización precisa) | |
| 5 | Tratamiento a gran escala | |
| 6 | Combinación o cotejo de conjuntos de datos de distintas fuentes | |
| 7 | Datos de personas vulnerables | |
| 8 | Uso innovador o aplicación de nuevas tecnologías (IA, IoT, biometría, reconocimiento facial) | |
| 9 | Tratamiento que impide ejercer derechos o acceder a servicios/contratos | |

**Regla general CEPD:** si concurren **2 o más criterios** →
EIPD OBLIGATORIA. [VERIFICAR — WP248rev.01 CEPD]

**Con 1 criterio:** EIPD RECOMENDADA por buenas prácticas, no
obligatoria legalmente salvo que el responsable decida realizarla.

### Nivel 3 — Umbrales del despacho (CLAUDE.md sección 5)

Aplicar los umbrales adicionales configurados por el despacho:
- Número mínimo de interesados para recomendar PIA
- Sectores con evaluación sistemática obligatoria
- Encargados nuevos accediendo a datos de clientes

---

## PASO 4 — Decisión y justificación

Emite la decisión en el siguiente formato:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DECISIÓN DE TRIAJE DE PRIVACIDAD
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Tratamiento analizado: [descripción breve]
Fecha del análisis:    DD/MM/AAAA
RESULTADO: [ ] PROCEDER  [ ] EIPD RECOMENDADA
[ ] EIPD OBLIGATORIA  [ ] STOP
Base de la decisión:

Lista positiva AEPD: [Aplica categoría X / No aplica]
Criterios WP248:     [N criterios concurrentes — listar]
Umbrales despacho:   [Aplica / No aplica]

Base jurídica del tratamiento: [Art. 6.1.X RGPD — descripción]
[Si categorías especiales: Art. 9.2.X RGPD]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

### Tabla de condiciones (siempre incluir)

Independientemente de la decisión, genera la tabla de condiciones
que el tratamiento debe cumplir para ser lícito:

| Condición | Cumplida | Acción requerida |
|---|---|---|
| Base jurídica identificada | ✅/⚠️/❌ | [acción] |
| Información a interesados (Art. 13/14 RGPD) | ✅/⚠️/❌ | [acción] |
| Registro de actividades actualizado (Art. 30 RGPD) | ✅/⚠️/❌ | [acción] |
| Contrato encargado si hay terceros (Art. 28 RGPD) | ✅/⚠️/❌ | [acción] |
| Medidas de seguridad adecuadas (Art. 32 RGPD) | ✅/⚠️/❌ | [acción] |
| EIPD (si obligatoria) | ✅/⚠️/❌ | [acción] |
| DPD informado (si existe) | ✅/⚠️/❌ | [acción] |

---

## PASO 5 — Instrucciones según resultado

### Si PROCEDER:
Indica las condiciones que deben cumplirse antes de iniciar el
tratamiento (tabla de condiciones). El tratamiento puede arrancar
sin EIPD formal pero debe cumplir el resto de obligaciones RGPD.

### Si EIPD RECOMENDADA:
Explica por qué se recomienda aunque no sea obligatoria legalmente.
Ofrece arrancar `/privacy-legal-es:generador-pias-aepd` para
realizarla de forma simplificada. Indica que proceder sin EIPD
es posible pero el responsable asume el riesgo regulatorio.

### Si EIPD OBLIGATORIA:
Indica que el tratamiento **no puede iniciarse** hasta completar
la EIPD. [FUENTE: RGPD] Si la EIPD concluye en alto riesgo residual
no mitigable, debe realizarse consulta previa a la AEPD antes de
iniciar el tratamiento (Art. 36 RGPD). [FUENTE: RGPD]

Ofrece arrancar `/privacy-legal-es:generador-pias-aepd`
inmediatamente en la misma conversación.

### Si STOP:
El tratamiento no puede proceder en su forma actual.
Razones posibles:
- No hay base jurídica legítima identificable
- Datos de categorías especiales sin base Art. 9.2 aplicable
- Tratamiento manifiestamente desproporcionado
- Tratamiento de datos de menores sin habilitación legal

**ESCALA — revisión letrada obligatoria antes de cualquier paso.**
No generar documentación que legitime el tratamiento.
Indicar qué cambios en el diseño del tratamiento podrían
desbloquearlo (privacy by design, Art. 25 RGPD). [FUENTE: RGPD]

---

## Guardrails obligatorios

- **Nunca legitimar un tratamiento sin base jurídica** — si no hay
  base jurídica clara, STOP antes de evaluar nada más.
- **En caso de duda entre EIPD RECOMENDADA y EIPD OBLIGATORIA:
  recomendar EIPD OBLIGATORIA** — es más seguro para el responsable.
  [FUENTE: AEPD]
- **No iniciar tratamientos con EIPD OBLIGATORIA pendiente** —
  indicarlo explícitamente.
- **La lista positiva de la AEPD puede actualizarse** — en Sprint 2
  se conectará MCP a sede AEPD para verificación en tiempo real.
  Hasta entonces, aplicar la lista conocida y añadir [VERIFICAR]
  si hay duda sobre si una categoría nueva ha sido añadida.
- Citar siempre [FUENTE: RGPD], [FUENTE: AEPD], [VERIFICAR].
- Revisión letrada obligatoria en decisiones STOP y en EIPDs
  antes de iniciar el tratamiento.