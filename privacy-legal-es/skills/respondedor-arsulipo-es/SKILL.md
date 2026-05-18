---
name: respondedor-arsulipo-es
description: >
  Gestiona y redacta respuestas a solicitudes de derechos de protección de datos
  (Acceso, Rectificación, Supresión, Limitación, Portabilidad y Oposición — ARSULIPO)
  conforme al RGPD y la LOPDGDD. Verifica identidad del solicitante, clasifica el tipo
  de solicitud, calcula el plazo aplicable, redacta la carta de respuesta en español
  jurídico profesional y genera el registro interno de la gestión.
  Úsalo cuando llegue una solicitud de derechos, el usuario diga "me ha llegado una
  solicitud de acceso / supresión / portabilidad / rectificación / oposición /
  limitación", "un cliente quiere sus datos", "derecho al olvido", o pegue directamente
  el texto de la solicitud recibida.
argument-hint: "[pega aquí la solicitud recibida o descríbela]"
---

# /respondedor-arsulipo-es

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: rol del despacho (responsable/encargado), método de verificación de identidad,
   contacto de escalación urgente, sistemas de datos del despacho.
2. Ejecuta el flujo siguiente paso a paso.
3. Clasifica el tipo de solicitud. Comprueba triggers de escalación — si alguno aplica,
   escala antes de continuar.
4. Recorre: verificar identidad → localizar datos → analizar excepciones → redactar.
5. Output: borrador de respuesta. NO enviar — revisión letrada obligatoria antes de
   cualquier envío.
6. Registra la gestión en el log interno.

**Antes de pegar la solicitud:** el documento contendrá datos personales del interesado.
Confirma que el almacenamiento de la sesión cumple con tus requisitos de tratamiento.
No guardes el nombre del interesado en nombres de fichero. Redacta cualquier dato
que no sea necesario para la gestión.
/privacy-legal-es:respondedor-arsulipo-es
[pega aquí el texto de la solicitud recibida]

---

# Respuesta a Solicitudes ARSULIPO

## Contexto de práctica

**Contexto de práctica.** Lee `## 1. Identificación del despacho` y
`## 7. Escalación y revisión humana` del CLAUDE.md activo. Si no existe el archivo
de configuración en `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`,
indica al usuario que ejecute `/privacy-legal-es:cold-start-interview-es` antes de
continuar — sin perfil de práctica, los plazos y procedimientos se aplicarán con
valores por defecto que pueden no ajustarse a su despacho.

---

## Finalidad del skill

Una solicitud ARSULIPO tiene un plazo legal perentorio, un procedimiento de
verificación de identidad, un proceso de localización de datos y un conjunto de
excepciones aplicables. Este skill recorre cada paso y redacta la respuesta.

**Marco jurisdiccional:** España. RGPD (UE) 2016/679 + LOPDGDD (LO 3/2018).
Autoridad de control competente: AEPD. Si el interesado, los datos o el responsable
del tratamiento tienen conexión con otra jurisdicción, indícalo — puede requerir
análisis adicional antes de continuar.

---

## PASO 1 — Clasificación de la solicitud

Identifica el tipo o tipos de derecho ejercitados. Una misma solicitud puede
acumular varios derechos simultáneamente.

| Derecho | Base legal | Denominación común |
|---|---|---|
| Acceso | Art. 15 RGPD | "quiero saber qué datos tenéis" |
| Rectificación | Art. 16 RGPD | "mis datos son incorrectos" |
| Supresión | Art. 17 RGPD | "quiero que borréis mis datos" / "derecho al olvido" |
| Limitación | Art. 18 RGPD | "quiero que dejéis de tratar mis datos temporalmente" |
| Portabilidad | Art. 20 RGPD | "quiero mis datos en formato descargable" |
| Oposición | Art. 21 RGPD | "me opongo a que uséis mis datos para X" |

**Nota portabilidad:** solo aplica cuando la base jurídica del tratamiento es
consentimiento (Art. 6.1.a RGPD) o ejecución de contrato (Art. 6.1.b RGPD) y el
tratamiento se realiza por medios automatizados. [FUENTE: AEPD]

**Nota supresión:** no es absoluta. Verificar si aplica alguna excepción del
Art. 17.3 RGPD (obligación legal, interés público, ejercicio de acciones legales).

---

## PASO 2 — Verificación de identidad

Antes de procesar cualquier solicitud, verificar que el solicitante es quien dice ser.

**Método por defecto** (ajustable en CLAUDE.md sección 4):
- Si la solicitud llega por canal autenticado (área cliente, email corporativo
  verificado): identidad suficientemente acreditada → continuar.
- Si la solicitud llega por canal no autenticado (formulario web, email no verificado,
  carta): solicitar documento acreditativo de identidad (DNI/NIE/pasaporte).

**Representación:** si actúa un representante legal o voluntario, verificar además
la acreditación de la representación (poder notarial, autorización firmada).

**Plazo para verificación:** el plazo de respuesta (1 mes) empieza a correr desde
que se tiene certeza de la identidad del solicitante. Si se solicita documentación
adicional de identidad, el plazo queda en suspenso hasta su recepción. [FUENTE: AEPD]

**Trigger de escalación — ESCALA ANTES DE CONTINUAR si:**
- La solicitud proviene de un menor de edad
- El solicitante manifiesta representar a un colectivo o actuar en nombre de
  varios interesados
- Hay indicios de que la solicitud es parte de una reclamación ante la AEPD
  ya presentada o anunciada
- El volumen de datos afectados es inusualmente alto

---

## PASO 3 — Cálculo de plazos

| Situación | Plazo | Referencia |
|---|---|---|
| Caso estándar | **1 mes** desde recepción (o desde verificación de identidad si se solicitó) | Art. 12.3 RGPD |
| Caso complejo o múltiples solicitudes simultáneas | **3 meses** desde recepción, notificando la prórroga en el primer mes | Art. 12.3 RGPD |
| Solicitud manifiestamente infundada o excesiva | Puede cobrarse tasa razonable o negarse — justificación obligatoria | Art. 12.5 RGPD |

**Calcula y muestra la fecha límite** en formato DD/MM/AAAA partiendo de la fecha
de recepción de la solicitud que indique el usuario.

**Advertencia de prórroga:** si el caso es complejo, generar también la carta de
notificación de prórroga, que debe enviarse dentro del primer mes.

---

## PASO 4 — Localización de datos

Solicita al usuario (o extrae del CLAUDE.md si está configurado) la lista de
sistemas donde podrían existir datos del interesado:

- CRM / base de datos de clientes
- Sistema de facturación / ERP
- Correo electrónico (incluidos archivos)
- Copias de seguridad
- Sistemas de terceros / encargados del tratamiento
- Registros físicos (expedientes en papel)
- Sistemas de videovigilancia (si aplica)
- Logs y registros de acceso

Para cada sistema: ¿existen datos? → ¿qué datos? → ¿base jurídica del tratamiento?
→ ¿plazo de conservación aplicable?

---

## PASO 5 — Análisis de excepciones

Antes de redactar la respuesta, verificar si aplica alguna excepción que permita
limitar o denegar total o parcialmente la solicitud:

**Supresión — excepciones Art. 17.3 RGPD:**
- Obligación legal de conservación (ej: Ley 58/2003 General Tributaria — 4 años;
  Ley 10/2010 blanqueo de capitales — 10 años) [FUENTE: BOE]
- Ejercicio o defensa de reclamaciones legales
- Interés público (archivos, investigación científica)

**Acceso — limitaciones:**
- Datos de terceros cuya revelación afectaría sus derechos (anonimizar o redactar)
- Información privilegiada o confidencial del despacho

**Oposición — excepciones Art. 21.1 RGPD:**
- Motivos legítimos imperiosos que prevalezcan sobre los intereses del interesado
- Ejercicio o defensa de reclamaciones legales

**Si se va a denegar total o parcialmente:** la denegación debe ser motivada,
informar del derecho a reclamar ante la AEPD y del derecho a ejercitar acciones
judiciales. [FUENTE: AEPD] → **ESCALA — revisión letrada obligatoria antes de
enviar cualquier denegación.**

---

## PASO 6 — Redacción de la respuesta

Genera la carta de respuesta con la siguiente estructura:
[Membrete del despacho — según CLAUDE.md]
[Lugar], [fecha DD/MM/AAAA]
Ref. interna: ARSULIPO-[AÑO]-[NÚMERO SECUENCIAL]
A/A: [Nombre del interesado]
[Dirección si consta]
Asunto: Respuesta a solicitud de ejercicio del derecho de [TIPO] en relación
con sus datos personales
Estimado/a Sr./Sra. [Apellido]:
En relación con su solicitud recibida el [fecha], mediante la que ejercita
su derecho de [TIPO] al amparo del artículo [X] del Reglamento (UE) 2016/679
del Parlamento Europeo y del Consejo, de 27 de abril de 2016, relativo a la
protección de las personas físicas en lo que respecta al tratamiento de datos
personales (en adelante, RGPD), le comunicamos lo siguiente:
[BLOQUE PRINCIPAL — según tipo de solicitud, ver plantillas abajo]
La presente respuesta se emite en el plazo establecido en el artículo 12.3 del
RGPD. En caso de disconformidad con la presente respuesta, le informamos de su
derecho a presentar una reclamación ante la Agencia Española de Protección de
Datos (AEPD), con sede en calle Jorge Juan, 6, 28001 Madrid, a través de su
sede electrónica en www.aepd.es.
Atentamente,
[Nombre y firma del responsable]
[Cargo]
[Despacho]
[Fecha]

### Plantillas de bloque principal por tipo de derecho

**ACCESO (Art. 15 RGPD):**
Adjuntamos a la presente comunicación copia de los datos personales que obran
en nuestros sistemas en relación con su persona, así como la siguiente
información: [finalidad del tratamiento / categorías de datos / destinatarios
o categorías de destinatarios / plazo de conservación previsto / origen de los
datos si no fueron facilitados directamente por usted].

**RECTIFICACIÓN (Art. 16 RGPD):**
Hemos procedido a rectificar los datos personales indicados en su solicitud.
Los datos [descripción de los datos incorrectos] han sido actualizados a
[descripción de los datos correctos] con fecha [DD/MM/AAAA].

**SUPRESIÓN — estimada (Art. 17 RGPD):**
Hemos procedido a la supresión de sus datos personales de nuestros sistemas
con fecha [DD/MM/AAAA], salvo aquellos respecto de los que existe obligación
legal de conservación, en concreto: [indicar datos conservados + base legal
+ plazo], que serán bloqueados y únicamente accesibles a requerimiento de
autoridades competentes.

**SUPRESIÓN — denegada parcialmente (Art. 17.3 RGPD):**
[REQUIERE REVISIÓN LETRADA — usar bloque de denegación motivada]

**LIMITACIÓN (Art. 18 RGPD):**
Hemos procedido a bloquear el tratamiento de sus datos personales con fecha
[DD/MM/AAAA], conservándolos únicamente a disposición de las autoridades
competentes para el ejercicio o la defensa de reclamaciones. Le notificaremos
cuando se levante la limitación.

**PORTABILIDAD (Art. 20 RGPD):**
Adjuntamos a la presente sus datos personales en formato [CSV/JSON/XML],
estructurado y de uso común, que permite su transmisión a otro responsable
del tratamiento. Los datos incluidos son: [descripción].

**OPOSICIÓN — estimada (Art. 21 RGPD):**
Hemos cesado en el tratamiento de sus datos personales para la finalidad de
[finalidad], con fecha [DD/MM/AAAA]. Sus datos han sido [suprimidos /
bloqueados para dicha finalidad], salvo que concurra alguna causa legalmente
prevista que justifique el mantenimiento del tratamiento.

---

## PASO 7 — Registro interno de la gestión

Genera el siguiente registro para el archivo del despacho:
REGISTRO DE GESTIÓN ARSULIPO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Ref.:           ARSULIPO-[AÑO]-[NÚM]
Fecha recepción: DD/MM/AAAA
Tipo de derecho: [ARSULIPO]
Interesado:     [iniciales o código — no nombre completo en el registro]
Canal de entrada: [email / formulario web / carta / presencial]
Identidad verificada: [Sí / No / Pendiente] — método: [...]
Fecha verificación: DD/MM/AAAA
Plazo máximo respuesta: DD/MM/AAAA
Prórroga solicitada: [Sí / No]
Datos localizados en: [sistemas]
Excepciones aplicadas: [Ninguna / Art. X RGPD — descripción]
Decisión: [Estimada / Estimada parcialmente / Denegada]
Fecha respuesta enviada: DD/MM/AAAA
Revisión letrada: [Nombre letrado + fecha]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

## Guardrails obligatorios

- **Nunca enviar la respuesta directamente** — siempre marcar como borrador
  para revisión letrada antes de cualquier envío al interesado.
- **Nunca denegar una solicitud sin revisión letrada previa** — la denegación
  incorrecta puede derivar en sanción de la AEPD.
- **Siempre informar del derecho a reclamar ante la AEPD** en la carta,
  independientemente de si la respuesta es estimatoria o denegatoria.
- **Citar siempre las fuentes** con etiquetas [FUENTE: RGPD], [FUENTE: AEPD],
  [FUENTE: BOE] o [VERIFICAR] si no hay fuente oficial verificable.
- **No reproducir más datos personales del interesado** de los estrictamente
  necesarios en el output de este skill.
  