---
name: generador-clausulas-rgpd
description: >
  Genera cláusulas informativas y de consentimiento RGPD listas para insertar
  en webs, apps, formularios de contacto, newsletters, e-commerce, contratos
  y cualquier canal digital o físico donde se recojan datos personales.
  Adapta el texto al canal, a la audiencia (B2C, B2B, menores) y a la finalidad
  específica. Genera tanto la versión corta (layered notice / capa 1) como la
  versión larga (política de privacidad completa o sección de ella).
  Úsalo cuando el usuario diga "necesito las cláusulas de privacidad para mi
  web", "necesito el aviso legal", "necesito el texto del checkbox de
  consentimiento", "necesito la política de cookies", "necesito el texto de
  privacidad para un formulario", "necesito adaptar mi web al RGPD",
  o "necesito las cláusulas para un contrato con clientes".
argument-hint: "[describe el canal — web/app/formulario/contrato — y qué datos recoges y para qué]"
---

# /generador-clausulas-rgpd

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: identificación del responsable, DPD si existe, sistemas de datos,
   política de privacidad vigente.
2. Recopila la información necesaria del canal y el tratamiento (Paso 1).
3. Determina qué documentos/cláusulas son necesarios según el canal.
4. Genera todos los textos solicitados listos para copiar/insertar.
5. Marca con [COMPLETAR] los campos que dependen de datos del responsable
   no disponibles en el perfil.
6. Todos los outputs son borradores para revisión letrada antes de publicar.
/privacy-legal-es:generador-clausulas-rgpd
[describe el canal y qué datos recoges]

---

# Generador de Cláusulas RGPD

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`.
Si no existe el perfil, genera con marcadores [COMPLETAR] y etiqueta como
`[PERFIL NO CONFIGURADO]`.

**Marco jurisdiccional:** España.
- Cláusulas informativas: Arts. 13-14 RGPD [FUENTE: RGPD]
- Consentimiento: Arts. 4.11, 6.1.a, 7 RGPD [FUENTE: RGPD]
- Menores: Art. 8 RGPD + Art. 7 LOPDGDD (edad mínima: **14 años**) [FUENTE: AEPD]
- Cookies: Guía de uso de cookies AEPD 2023 + Art. 22 LSSI-CE [FUENTE: AEPD]
- Comunicaciones comerciales: Art. 21 LSSI-CE [FUENTE: BOE]

---

## PASO 1 — Intake del canal y tratamiento

Extrae de la descripción del usuario o pregunta lo que falte:

| Campo | Descripción |
|---|---|
| Tipo de canal | Web / App móvil / Formulario físico / Newsletter / E-commerce / Contrato / Otro |
| Responsable del tratamiento | Nombre + NIF + dirección + email de contacto |
| DPD (si existe) | Nombre + email de contacto del DPD |
| Datos que se recogen | Listar: nombre, email, teléfono, dirección, IP, cookies, datos bancarios... |
| Finalidades | Para qué se usan los datos (contacto, venta, marketing, analítica...) |
| Base jurídica | Consentimiento / Contrato / Interés legítimo / Obligación legal |
| Destinatarios | ¿Se comparten datos con terceros? ¿Cuáles? |
| Transferencias internacionales | ¿Datos fuera del EEE? |
| Plazo de conservación | ¿Cuánto tiempo se guardan los datos? |
| Menores | ¿Puede acceder o registrarse menores de 14 años? |
| Cookies | ¿La web/app usa cookies? ¿De qué tipo? |

---

## PASO 2 — Determinación de documentos necesarios

Según el canal, determina qué textos hay que generar:

| Canal | Documentos necesarios |
|---|---|
| Web con formulario de contacto | Política de privacidad + cláusula informativa corta en el formulario |
| Web con newsletter | Política de privacidad + cláusula consentimiento newsletter + gestión de bajas |
| E-commerce | Política de privacidad + aviso legal + cláusula en checkout + política de cookies |
| App móvil | Política de privacidad in-app + pantalla de consentimiento al registro + política de cookies |
| Formulario físico | Cláusula informativa en el reverso del formulario |
| Contrato con clientes | Cláusula de protección de datos para incluir en el contrato |
| Web con cookies | Política de cookies + banner de cookies + textos de los niveles de consentimiento |

---

## PASO 3 — Generación de textos

### A) CLÁUSULA INFORMATIVA CORTA (Capa 1 — layered notice)

Para formularios, checkboxes y espacios reducidos.
Debe contener: identidad del responsable, finalidad, base jurídica,
derechos y cómo ejercerlos. [FUENTE: AEPD]
PROTECCIÓN DE DATOS
[NOMBRE DEL RESPONSABLE], con NIF [COMPLETAR] y domicilio en
[COMPLETAR], trata los datos facilitados con la finalidad de
[FINALIDAD PRINCIPAL]. La base jurídica del tratamiento es
[BASE JURÍDICA]. Los datos se conservarán durante [PLAZO].
[Si hay cesiones: Sus datos podrán ser comunicados a [DESTINATARIOS].]
Puede ejercer sus derechos de acceso, rectificación, supresión,
limitación, portabilidad y oposición dirigiéndose a [EMAIL/DIRECCIÓN].
Puede presentar una reclamación ante la Agencia Española de Protección
de Datos (www.aepd.es). Para más información, consulte nuestra
[Política de Privacidad → ENLACE].

### B) TEXTO DE CHECKBOX DE CONSENTIMIENTO

Para formularios donde la base jurídica es el consentimiento:

**Versión estándar:**
☐ He leído y acepto la [Política de Privacidad] y consiento
el tratamiento de mis datos para [FINALIDAD ESPECÍFICA].

**Versión con finalidades separadas (cuando hay múltiples):**
☐ Acepto el tratamiento de mis datos para gestionar mi solicitud.
(Necesario para procesar tu consulta)
☐ Acepto recibir comunicaciones comerciales sobre productos y
servicios de [NOMBRE].
(Opcional — puedes darte de baja en cualquier momento)

**IMPORTANTE:** cada finalidad distinta requiere un checkbox separado.
No agrupar en un único consentimiento. [FUENTE: AEPD]

### C) POLÍTICA DE PRIVACIDAD COMPLETA

Genera la política de privacidad completa con los 12 elementos
obligatorios del Art. 13 RGPD: [FUENTE: RGPD]
POLÍTICA DE PRIVACIDAD
Última actualización: DD/MM/AAAA

RESPONSABLE DEL TRATAMIENTO

Denominación social:  [COMPLETAR]
NIF/CIF:              [COMPLETAR]
Domicilio:            [COMPLETAR]
Email de contacto:    [COMPLETAR]
[DPD: Delegado de Protección de Datos: [NOMBRE] — [EMAIL]]
[Si no hay DPD: No está obligado/a a designar DPD.]

DATOS QUE TRATAMOS Y FINALIDADES

[Para cada tratamiento, un bloque:]
■ [NOMBRE DEL TRATAMIENTO — ej: Formulario de contacto]
Datos tratados:    [listar]
Finalidad:         [describir]
Base jurídica:     [Art. 6.1.X RGPD — descripción en lenguaje claro]
Plazo de conservación: [plazo + criterio]
[Destinatarios si los hay: Sus datos serán comunicados a [X] para [fin].]
■ [NOMBRE DEL TRATAMIENTO — ej: Newsletter]
Datos tratados:    Email [y nombre si se recoge]
Finalidad:         Envío de comunicaciones comerciales sobre [X]
Base jurídica:     Consentimiento del interesado (Art. 6.1.a RGPD).
Puede retirar su consentimiento en cualquier momento
sin que ello afecte a la licitud del tratamiento
previo a su retirada.
Plazo de conservación: Hasta que retire su consentimiento o solicite
la baja. [Si hay plazo adicional: más [X] meses
para acreditar el cumplimiento normativo.]
Baja:              Puede darse de baja en cualquier momento pulsando
el enlace "Darse de baja" incluido en cada email,
o enviando un email a [COMPLETAR].

DESTINATARIOS Y TRANSFERENCIAS INTERNACIONALES

[Si no hay cesiones:]
Sus datos no serán cedidos a terceros, salvo obligación legal.
[Si hay cesiones:]
Sus datos podrán ser comunicados a:

[Nombre del destinatario]: [finalidad de la cesión] — [base jurídica]

[Si hay encargados del tratamiento:]
Para la prestación de nuestros servicios, utilizamos proveedores
que actúan como encargados del tratamiento y que tratan los datos
exclusivamente según nuestras instrucciones:

[Nombre del encargado] — [servicio] — [ubicación EEE/fuera EEE]

[Si hay transferencias internacionales:]
Algunos de nuestros proveedores pueden tratar datos fuera del Espacio
Económico Europeo. En tal caso, las transferencias se amparan en
[mecanismo: Decisión de adecuación / CCT Decisión (UE) 2021/914 /
EU-US Data Privacy Framework [VERIFICAR vigencia]].
[Si no hay transferencias:]
No realizamos transferencias internacionales de datos.

DERECHOS DE LOS INTERESADOS

Tiene derecho a:
— Acceder a sus datos personales.
— Rectificar los datos inexactos o incompletos.
— Solicitar la supresión de sus datos cuando ya no sean necesarios.
— Solicitar la limitación del tratamiento en determinadas circunstancias.
— Oponerse al tratamiento por motivos relacionados con su situación personal.
— Solicitar la portabilidad de sus datos en formato estructurado
(cuando la base jurídica sea el consentimiento o un contrato).
— Retirar el consentimiento en cualquier momento, sin que ello afecte
a la licitud del tratamiento previo a su retirada.
Para ejercer sus derechos, puede dirigirse a:
[EMAIL DE CONTACTO / DIRECCIÓN POSTAL]
Indicando su nombre, apellidos, DNI/NIE y el derecho que desea ejercer.
Responderemos a su solicitud en el plazo máximo de un mes
(Art. 12.3 RGPD), prorrogable dos meses adicionales en casos complejos.
Si no obtiene respuesta satisfactoria, tiene derecho a presentar
una reclamación ante la Agencia Española de Protección de Datos (AEPD):
Calle Jorge Juan, 6 — 28001 Madrid — www.aepd.es

SEGURIDAD

Aplicamos las medidas técnicas y organizativas apropiadas para
garantizar un nivel de seguridad adecuado al riesgo, conforme
al Art. 32 del RGPD.

CAMBIOS EN ESTA POLÍTICA

Nos reservamos el derecho a modificar esta política para adaptarla
a novedades legislativas o jurisprudenciales. Le informaremos de
los cambios significativos. La versión vigente es siempre la
disponible en [URL].

### D) CLÁUSULA PARA CONTRATO CON CLIENTES

Para incluir en contratos de prestación de servicios:
CLÁUSULA DE PROTECCIÓN DE DATOS
En cumplimiento del Reglamento (UE) 2016/679 del Parlamento Europeo
y del Consejo, de 27 de abril de 2016, relativo a la protección de
las personas físicas en lo que respecta al tratamiento de datos
personales (RGPD), y de la Ley Orgánica 3/2018, de 5 de diciembre,
de Protección de Datos Personales y garantía de los derechos digitales
(LOPDGDD), le informamos de que los datos personales facilitados en
el marco del presente contrato serán tratados por [NOMBRE DEL
RESPONSABLE], con NIF [COMPLETAR], como responsable del tratamiento.
Finalidad: gestión de la relación contractual y prestación de los
servicios contratados.
Base jurídica: ejecución del contrato (Art. 6.1.b RGPD).
Conservación: durante la vigencia del contrato y, una vez finalizado,
durante los plazos de prescripción de las acciones derivadas del mismo
[y las obligaciones legales aplicables, en particular [X] años conforme
a la Ley [X]].
Destinatarios: sus datos no serán cedidos a terceros, salvo obligación
legal [o: salvo a [X] para [fin], con base en [base jurídica]].
Puede ejercer sus derechos de acceso, rectificación, supresión,
limitación, portabilidad y oposición dirigiéndose a [EMAIL/DIRECCIÓN].
Tiene derecho a presentar una reclamación ante la AEPD (www.aepd.es).

### E) POLÍTICA DE COOKIES

Si la web/app usa cookies: [FUENTE: AEPD — Guía de uso de cookies 2023]
POLÍTICA DE COOKIES
¿Qué son las cookies?
Las cookies son pequeños archivos de texto que los sitios web instalan
en su dispositivo cuando los visita. Permiten que el sitio recuerde
sus acciones y preferencias durante un período de tiempo.
¿Qué cookies utilizamos?
■ COOKIES TÉCNICAS O NECESARIAS (no requieren consentimiento)
Son imprescindibles para el funcionamiento del sitio web.
[Listar: sesión, autenticación, carrito de compra...]
■ COOKIES ANALÍTICAS (requieren consentimiento)
Nos permiten conocer cómo los usuarios interactúan con el sitio
para mejorar su funcionamiento.
[Listar: Google Analytics / [alternativa] — finalidad — duración]
■ COOKIES DE MARKETING / PUBLICIDAD (requieren consentimiento)
Permiten mostrarle publicidad relevante en función de sus intereses.
[Listar: si aplica]
¿Cómo gestionar las cookies?
Puede aceptar, rechazar o configurar las cookies en cualquier momento
a través del [panel de preferencias de cookies / enlace a configuración].
También puede configurar su navegador para rechazar las cookies, aunque
esto puede afectar a la funcionalidad del sitio.
Para más información: [EMAIL DE CONTACTO]
Responsable del tratamiento: [NOMBRE] — [EMAIL]

**Texto del banner de cookies (primera visita):**
Utilizamos cookies propias y de terceros para analizar nuestros
servicios y mostrarte publicidad relacionada con tus preferencias.
Puedes aceptar todas las cookies, configurarlas o rechazar las
no necesarias.
[Aceptar todas] [Configurar] [Rechazar no necesarias]

**IMPORTANTE sobre cookies:** el rechazo de cookies no técnicas
debe ser tan sencillo como su aceptación — no vale el patrón
"Aceptar / Más información" sin opción clara de rechazo en la
primera capa. [FUENTE: AEPD]

### F) TRATAMIENTO DE DATOS DE MENORES

Si el servicio puede ser usado por menores: [FUENTE: AEPD]

**Edad mínima en España: 14 años** (Art. 7 LOPDGDD). [FUENTE: BOE]
Por debajo de 14 años se requiere consentimiento del titular de la
patria potestad o tutela.
MENORES DE EDAD
Nuestros servicios están dirigidos a mayores de 14 años.
Si tiene menos de 14 años, necesita el consentimiento de sus
padres o tutores para facilitarnos sus datos.
Si eres padre/madre o tutor y crees que tu hijo/a menor de 14 años
nos ha facilitado datos sin tu consentimiento, puedes contactar con
nosotros en [EMAIL] para proceder a su supresión.

**Para servicios expresamente dirigidos a menores de 14:**
añadir verificación de edad y consentimiento parental verificable.
[VERIFICAR — mecanismo de verificación adecuado según tipo de servicio]

---

## PASO 4 — Checklist de publicación

Antes de publicar, verifica:

| Item | ✅ |
|---|---|
| Política de privacidad accesible desde todas las páginas (footer) | |
| Enlace a política en todos los formularios donde se recogen datos | |
| Checkboxes de consentimiento desmarcados por defecto | |
| Checkbox de newsletter separado del de condiciones de uso | |
| Banner de cookies con opción de rechazo en primera capa | |
| Política de cookies enlazada desde el banner | |
| Mecanismo de baja de newsletter funcional | |
| Email/formulario de ejercicio de derechos operativo | |
| Fecha de última actualización visible en la política | |
| Menores: mecanismo de verificación de edad si aplica | |

---

## Guardrails obligatorios

- **Nunca agrupar consentimientos distintos en un único checkbox** —
  cada finalidad autónoma requiere consentimiento separado. [FUENTE: AEPD]
- **El rechazo de cookies debe ser tan fácil como la aceptación** —
  patrón "aceptar/más información" sin rechazo visible incumple la
  guía AEPD 2023. [FUENTE: AEPD]
- **Edad mínima en España: 14 años** — no 16 (que es el defecto del
  Art. 8 RGPD). La LOPDGDD la rebajó a 14. [FUENTE: BOE]
- **Casillas premarcadas no son consentimiento válido** — el
  consentimiento debe ser una acción positiva inequívoca. [FUENTE: RGPD]
- **Revisión letrada obligatoria antes de publicar** — especialmente
  si hay transferencias internacionales, datos de menores o
  categorías especiales.
- Citar siempre [FUENTE: RGPD], [FUENTE: AEPD], [FUENTE: BOE],
  [VERIFICAR].