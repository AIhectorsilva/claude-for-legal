---
name: notificador-brecha-aepd
description: >
  Analiza un incidente de seguridad que afecte a datos personales, determina si existe
  obligación de notificar a la AEPD en el plazo de 72 horas (Art. 33 RGPD) y/o a los
  interesados afectados (Art. 34 RGPD), y genera el borrador del formulario de
  notificación a la AEPD y la comunicación a interesados si procede.
  Úsalo cuando el usuario describa un incidente de seguridad, un acceso no autorizado
  a datos, una pérdida de dispositivo con datos personales, un ransomware, un envío
  masivo erróneo de emails, una filtración de datos, o cualquier situación donde
  puedan haberse visto comprometidos datos personales.
  CRÍTICO: el plazo de 72 horas empieza a contar desde que el responsable tiene
  conocimiento del incidente. Ejecutar este skill sin demora.
argument-hint: "[describe el incidente — qué ocurrió, cuándo, qué datos y cuántas personas afectadas]"
---

# /notificador-brecha-aepd

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: rol del despacho, contacto de escalación urgente (teléfono), sistemas
   de datos, encargados del tratamiento.
2. Registra el timestamp de inicio del análisis — el plazo de 72h corre desde
   el momento en que el responsable tuvo conocimiento, no desde ahora.
3. Pregunta la fecha y hora exacta en que el despacho tuvo conocimiento del
   incidente si no consta en la descripción.
4. Ejecuta el flujo de análisis paso a paso.
5. Output: análisis de notificación + formulario AEPD borrador + comunicación
   a interesados si Art. 34 aplica.
6. NUNCA enviar directamente — revisión letrada obligatoria. Pero advierte
   activamente del tiempo restante para el plazo de 72h.

**URGENCIA:** si el tiempo transcurrido desde el conocimiento del incidente
se acerca o supera las 48 horas, indicarlo en rojo al inicio del output.
Las notificaciones extemporáneas a la AEPD deben incluir justificación
de la demora.
/privacy-legal-es:notificador-brecha-aepd
[describe el incidente]

---

# Notificación de Brechas de Seguridad — Art. 33-34 RGPD

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`.
Si no existe, aplica valores por defecto RGPD y etiqueta todo output como
`[PERFIL NO CONFIGURADO]`. Recomienda ejecutar
`/privacy-legal-es:cold-start-interview-es` antes de usar en producción.

---

## Finalidad del skill

Una brecha de seguridad que afecte a datos personales puede generar dos
obligaciones simultáneas con plazos distintos y consecuencias sancionadoras
graves si se incumplen. Este skill determina qué obligaciones aplican,
cuándo vencen y genera los documentos necesarios.

**Marco jurisdiccional:** España. RGPD (UE) 2016/679 + LOPDGDD (LO 3/2018).
Autoridad de control competente: AEPD.

---

## PASO 1 — Control de tiempo

Calcula y muestra de forma prominente:
⏱ CONTROL DE PLAZO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Conocimiento del incidente: [DD/MM/AAAA HH:MM]
Momento del análisis:       [DD/MM/AAAA HH:MM]
Tiempo transcurrido:        [X horas]
Tiempo restante (72h):      [Y horas]
Vencimiento plazo AEPD:     [DD/MM/AAAA HH:MM]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**Si tiempo transcurrido > 48h:** mostrar aviso destacado —
"⚠️ ATENCIÓN: quedan menos de 24 horas para el vencimiento del plazo de
notificación a la AEPD. La notificación extemporánea requiere justificación
de la demora en el propio formulario."

**Si tiempo transcurrido > 72h:** mostrar aviso crítico —
"🔴 PLAZO VENCIDO: el plazo de 72h ha expirado. La notificación debe
realizarse igualmente, incluyendo en el campo de observaciones la
justificación de la demora. [FUENTE: AEPD] Una notificación tardía
justificada es preferible a no notificar."

---

## PASO 2 — Clasificación de la brecha

Determina el tipo o tipos de brecha concurrentes:

| Tipo | Descripción | Ejemplos |
|---|---|---|
| Confidencialidad | Acceso o divulgación no autorizados | Filtración, acceso hacker, email erróneo |
| Integridad | Alteración no autorizada de datos | Modificación maliciosa, corrupción |
| Disponibilidad | Destrucción o pérdida de acceso | Ransomware, borrado accidental, pérdida dispositivo |

Una misma brecha puede ser de los tres tipos simultáneamente.

**Recopila la siguiente información** (pregunta lo que no conste):

1. ¿Qué ocurrió exactamente? (descripción del incidente)
2. ¿Cuándo se produjo? ¿Cuándo se detectó? ¿Cuándo tuvo conocimiento el responsable?
3. ¿Qué categorías de datos personales se han visto afectadas?
   - Datos identificativos básicos (nombre, email, teléfono, dirección)
   - Datos económicos (cuentas bancarias, tarjetas, facturas)
   - Categorías especiales Art. 9 RGPD (salud, ideología, religión, origen racial,
     vida sexual, datos biométricos, datos genéticos)
   - Datos de menores
   - Credenciales de acceso (contraseñas, tokens)
   - Datos de localización
4. ¿Cuántas personas afectadas aproximadamente?
5. ¿Se han tomado medidas de contención? ¿Cuáles?
6. ¿Hay encargados del tratamiento implicados?

---

## PASO 3 — Determinación de obligación de notificación a la AEPD

### Regla general (Art. 33.1 RGPD)

El responsable del tratamiento **debe notificar a la AEPD** salvo que sea
improbable que la brecha suponga un riesgo para los derechos y libertades
de las personas físicas. [FUENTE: RGPD]

**La carga de la prueba de "improbabilidad de riesgo" corresponde al responsable**
y debe documentarse. En caso de duda, notificar. [FUENTE: AEPD]

### Factores de evaluación de riesgo

Evalúa cada factor y determina nivel (bajo / medio / alto):

| Factor | Descripción | Nivel |
|---|---|---|
| Naturaleza de los datos | ¿Son categorías especiales Art. 9? ¿Credenciales? ¿Datos financieros? | [evaluar] |
| Número de afectados | A mayor número, mayor riesgo | [evaluar] |
| Facilidad de identificación | ¿Los datos permiten identificar directamente a personas? | [evaluar] |
| Consecuencias potenciales | Daño económico, discriminación, robo de identidad, daño reputacional | [evaluar] |
| Perfil de los afectados | ¿Menores, personas vulnerables, empleados? | [evaluar] |
| Medidas de seguridad previas | ¿Los datos estaban cifrados? ¿Seudonimizados? | [evaluar] |
| Intencionalidad | ¿Ataque deliberado o accidente? | [evaluar] |

### Decisión
DECISIÓN DE NOTIFICACIÓN A AEPD:
[ ] NOTIFICAR — riesgo no descartable → plazo 72h desde conocimiento
[ ] NO NOTIFICAR — riesgo improbable → documentar justificación
[ ] NOTIFICAR CON DEMORA JUSTIFICADA — plazo vencido, notificar igualmente

**Si la decisión es NO NOTIFICAR:** generar igualmente el registro
interno documentado de la decisión y su justificación. El Art. 33.5 RGPD
obliga a documentar cualquier brecha, se notifique o no. [FUENTE: RGPD]

---

## PASO 4 — Determinación de obligación de comunicación a interesados

### Regla (Art. 34 RGPD)

La comunicación a los interesados afectados es obligatoria cuando la brecha
**entrañe probable alto riesgo** para sus derechos y libertades. [FUENTE: RGPD]

El umbral es más alto que para la notificación a la AEPD.

### Excepciones que eliminan la obligación de comunicar (Art. 34.3 RGPD):

- Los datos afectados estaban **cifrados** con estándar robusto y la clave
  no se ha visto comprometida [FUENTE: RGPD]
- Se han adoptado medidas posteriores que hacen improbable el alto riesgo
- La comunicación individual supondría un esfuerzo desproporcionado →
  en este caso: comunicación pública igualmente requerida [FUENTE: RGPD]

### Decisión
DECISIÓN DE COMUNICACIÓN A INTERESADOS:
[ ] COMUNICAR — alto riesgo probable para los afectados
[ ] NO COMUNICAR — excepción Art. 34.3 aplicable (especificar cuál)
[ ] COMUNICACIÓN PÚBLICA — esfuerzo desproporcionado (Art. 34.3.c)

**Plazo:** "sin dilación indebida" — no hay plazo fijo en días pero
la AEPD considera que debe realizarse lo antes posible tras confirmar
la brecha y el alcance. [FUENTE: AEPD]

---

## PASO 5 — Formulario de notificación a la AEPD (borrador)

Genera el borrador adaptado al formulario electrónico de la AEPD.
[FUENTE: AEPD — sede electrónica notificación brechas: sedeagpd.gob.es]
NOTIFICACIÓN DE BRECHA DE SEGURIDAD — ART. 33 RGPD
Borrador para revisión letrada — NO ENVIAR sin validación
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TIPO DE NOTIFICACIÓN:
[ ] Notificación inicial (dentro de 72h)
[ ] Notificación complementaria (información adicional posterior)
[ ] Notificación extemporánea (fuera de plazo — justificación obligatoria)
SECCIÓN 1 — IDENTIFICACIÓN DEL RESPONSABLE
Nombre / Razón social:    [COMPLETAR — desde CLAUDE.md]
NIF/CIF:                  [COMPLETAR]
Dirección:                [COMPLETAR]
DPD (si existe):          [COMPLETAR o "No designado"]
Contacto notificación:    [COMPLETAR — nombre + email + teléfono]
SECCIÓN 2 — DESCRIPCIÓN DE LA BRECHA
Fecha y hora del incidente:         [DD/MM/AAAA HH:MM]
Fecha y hora de detección:          [DD/MM/AAAA HH:MM]
Fecha y hora de conocimiento
por el responsable:                 [DD/MM/AAAA HH:MM]
Tipo de brecha:                     [ ] Confidencialidad
[ ] Integridad
[ ] Disponibilidad
Descripción del incidente:
[Descripción clara y concisa de qué ocurrió, cómo se produjo y
qué sistemas/datos se vieron afectados]
SECCIÓN 3 — DATOS Y AFECTADOS
Categorías de datos afectados:      [listar]
Categorías especiales (Art. 9):     [ ] Sí → especificar: [...]
[ ] No
Número aproximado de afectados:     [número o rango]
Número aproximado de registros:     [número o rango]
Perfil de los afectados:            [ ] Clientes  [ ] Empleados
[ ] Menores   [ ] Otros: [...]
SECCIÓN 4 — CONSECUENCIAS PROBABLES
[Descripción de las posibles consecuencias para los afectados:
daño económico, discriminación, robo de identidad, daño reputacional,
pérdida de confidencialidad, otros]
SECCIÓN 5 — MEDIDAS ADOPTADAS
Medidas de contención adoptadas:
[Describir medidas técnicas y organizativas adoptadas o propuestas
para abordar la brecha y mitigar sus posibles efectos adversos]
Medidas para evitar recurrencia:
[Describir]
¿Los datos afectados estaban cifrados?  [ ] Sí  [ ] No  [ ] Parcialmente
¿Se ha recuperado el acceso/control?    [ ] Sí  [ ] No  [ ] Parcialmente
SECCIÓN 6 — COMUNICACIÓN A INTERESADOS
¿Se ha comunicado o se comunicará a los afectados?
[ ] Sí — fecha prevista: [DD/MM/AAAA]
[ ] No — justificación (Art. 34.3 RGPD): [...]
[ ] Comunicación pública (Art. 34.3.c)
SECCIÓN 7 — OBSERVACIONES
[Incluir aquí cualquier información relevante adicional.
Si la notificación es extemporánea, incluir justificación detallada
de la demora y medidas adoptadas durante el tiempo transcurrido]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  BORRADOR — Revisión letrada obligatoria antes de enviar
La notificación se realiza a través de la sede electrónica de la AEPD:
https://sedeagpd.gob.es → Trámites → Notificación de brechas

---

## PASO 6 — Comunicación a interesados (si Art. 34 aplica)
COMUNICACIÓN A INTERESADOS AFECTADOS
Borrador para revisión letrada — NO ENVIAR sin validación
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Membrete del despacho]
[Lugar], [DD/MM/AAAA]
Asunto: Comunicación sobre incidente de seguridad que afecta
a sus datos personales
Estimado/a Sr./Sra. [Apellido] / Estimado/a cliente:
Le comunicamos que [descripción del incidente en lenguaje claro
y comprensible, sin tecnicismos innecesarios].
Los datos que pueden haberse visto afectados son:
[listar categorías de datos del interesado concreto o categorías
generales si es comunicación masiva]
Las posibles consecuencias para usted son:
[descripción clara de los riesgos concretos]
Las medidas que hemos adoptado son:
[descripción de medidas de contención y mitigación]
Le recomendamos que adopte las siguientes medidas de protección:
[según el tipo de brecha: cambiar contraseñas, vigilar movimientos
bancarios, estar alerta ante comunicaciones sospechosas, etc.]
Para cualquier consulta o si desea más información, puede
contactar con [nombre del DPD o contacto de privacidad] en
[email] / [teléfono].
Asimismo, tiene derecho a presentar una reclamación ante la
Agencia Española de Protección de Datos (AEPD), con sede en
calle Jorge Juan, 6, 28001 Madrid (www.aepd.es).
[Nombre y firma del responsable]
[Cargo] · [Despacho]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  BORRADOR — Revisión letrada obligatoria antes de enviar

---

## PASO 7 — Registro interno de la brecha

Genera el registro obligatorio ex Art. 33.5 RGPD — independientemente
de si se notifica o no a la AEPD: [FUENTE: RGPD]
REGISTRO DE BRECHAS DE SEGURIDAD — Art. 33.5 RGPD
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Ref.:                     BRECHA-[AÑO]-[NÚM]
Fecha/hora incidente:     DD/MM/AAAA HH:MM
Fecha/hora detección:     DD/MM/AAAA HH:MM
Fecha/hora conocimiento
por responsable:          DD/MM/AAAA HH:MM
Tipo de brecha:           [Confidencialidad / Integridad / Disponibilidad]
Descripción:              [resumen]
Datos afectados:          [categorías]
Categorías especiales:    [Sí/No — especificar]
Nº afectados aprox.:      [número]
Decisión notificación
AEPD:                     [Notificada / No notificada — justificación]
Fecha notificación AEPD:  DD/MM/AAAA HH:MM
Nº expediente AEPD:       [si se dispone]
Decisión comunicación
a interesados:            [Sí / No — justificación / Pública]
Fecha comunicación:       DD/MM/AAAA
Medidas adoptadas:        [resumen]
Revisión letrada:         [Nombre + fecha]
Estado:                   [Abierta / Cerrada]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

## Guardrails obligatorios

- **Nunca enviar el formulario AEPD directamente** — siempre revisión letrada
  previa. El skill genera borradores, no envía.
- **Siempre registrar la brecha** aunque la decisión sea no notificar —
  el Art. 33.5 RGPD lo exige sin excepción. [FUENTE: RGPD]
- **Advertir activamente del tiempo restante** en cada output — el plazo de
  72h es el riesgo operativo más crítico de este skill.
- **En caso de duda sobre si notificar: recomendar notificar** — una
  notificación innecesaria tiene consecuencias menores que una omisión.
  [FUENTE: AEPD]
- **Notificación extemporánea es mejor que no notificar** — indicarlo
  siempre si el plazo ha vencido.
- Citar siempre con [FUENTE: RGPD], [FUENTE: AEPD], [FUENTE: BOE]
  o [VERIFICAR].
- No reproducir más datos personales de los afectados de los estrictamente
  necesarios en el output.