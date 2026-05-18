---
name: cold-start-interview-es
description: >
  Entrevista de configuración inicial del plugin privacy-legal-es. Aprende
  el playbook del despacho o cliente mediante una serie de preguntas
  estructuradas y genera el perfil de práctica personalizado en
  ~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md.
  Una vez completado, todos los skills del plugin leen ese perfil y
  dejan de usar valores por defecto — el membrete, los sistemas de datos,
  los umbrales de triaje, las posiciones en contratos de encargado y el
  estilo de redacción quedan calibrados al despacho concreto.
  Úsalo cuando el usuario diga "configurar el plugin", "hacer el onboarding",
  "personalizar Lexia para mi despacho", "rellenar el perfil de práctica",
  o cuando cualquier skill indique "ejecuta cold-start-interview-es".
  Solo necesita ejecutarse UNA VEZ por despacho/cliente. El perfil
  sobrevive a las actualizaciones del plugin.
argument-hint: "[di 'empezar' o describe brevemente tu despacho para arrancar]"
---

# /cold-start-interview-es

1. Explica brevemente al usuario qué va a pasar y cuánto tarda.
2. Conduce la entrevista en bloques — no lanzar todas las preguntas
   a la vez. Un bloque cada vez, esperando respuesta.
3. Al final, genera el CLAUDE.md personalizado completo.
4. Escribe el archivo en
   ~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md
5. Confirma al usuario que el perfil está activo y qué skills
   pueden usarse ya.
/privacy-legal-es:cold-start-interview-es
empezar

---

# Onboarding — Perfil de Práctica privacy-legal-es

## Introducción al usuario

Antes de empezar, explica:
Bienvenido al onboarding de Lexia · Área LOPD/Privacidad.
Esta entrevista tarda entre 5 y 15 minutos según el nivel de
detalle que quieras configurar. Puedes responder con lo que
tengas ahora — los campos que dejes en blanco quedarán como
[COMPLETAR] para rellenar después.
Al terminar, todos los skills de privacidad quedarán calibrados
a tu despacho: membrete, sistemas de datos, umbrales de triaje,
posiciones en contratos de encargado y estilo de redacción.
Empezamos. Responde con la información que tengas — sin presión.

---

## BLOQUE 1 — Identificación del despacho

Pregunta en un solo mensaje:
BLOQUE 1 de 6 — Identificación básica

Nombre completo del despacho o razón social
NIF/CIF
Dirección completa (calle, número, ciudad, CP)
Email de contacto principal (el que aparecerá en la política)
Teléfono (opcional)
Web (si existe)
Tipo de despacho:
a) Despacho individual / abogado autónomo
b) Sociedad profesional (SLP, SL, SA)
c) Departamento jurídico interno de empresa
d) Otro: [describir]


---

## BLOQUE 2 — Rol y sectores
BLOQUE 2 de 6 — Rol y sectores de práctica

¿Cómo actúa habitualmente el despacho respecto a los datos
de sus clientes?
a) Como RESPONSABLE del tratamiento (decides para qué se usan)
b) Como ENCARGADO del tratamiento (tratas datos por cuenta de otros)
c) Ambos según el caso
¿En qué sectores trabajan principalmente vuestros clientes?
(marca todos los que apliquen)
a) Despachos y profesionales jurídicos
b) Pymes tecnológicas / startups
c) Sector sanitario / salud
d) E-commerce / retail
e) Sector financiero / seguros
f) Administración pública
g) Recursos humanos / empleo
h) Inmobiliario
i) Otros: [describir]
¿Tenéis clientes que sean a su vez responsables del tratamiento
y os contraten como asesores de privacidad?
Sí / No


---

## BLOQUE 3 — DPD y contactos
BLOQUE 3 de 6 — DPD y escalación

¿Tenéis Delegado de Protección de Datos (DPD) designado?
a) Sí, interno — nombre + email + teléfono
b) Sí, externo — nombre + organización + email + teléfono
c) No estamos obligados / no tenemos
Contacto de escalación para casos urgentes (brechas 72h,
requerimientos AEPD):
Nombre: ___
Email:  ___
Teléfono (imprescindible para urgencias): ___
¿Quién firma habitualmente las respuestas a interesados
(ARSULIPO) y las notificaciones a la AEPD?
Nombre + cargo: ___


---

## BLOQUE 4 — Sistemas y encargados
BLOQUE 4 de 6 — Sistemas de datos y encargados

¿Qué sistemas usáis que traten datos personales?
(marca los que apliquen y añade el proveedor si lo sabes)
[ ] CRM                    → Proveedor: ___
[ ] Software de gestión    → Proveedor: ___
[ ] Email corporativo      → Proveedor: ___
[ ] Email marketing        → Proveedor: ___
[ ] Videollamadas          → Proveedor: ___
[ ] Mensajería interna     → Proveedor: ___
[ ] Almacenamiento cloud   → Proveedor: ___
[ ] Facturación/contabilidad → Proveedor: ___
[ ] Videovigilancia        → Proveedor: ___
[ ] Firma digital          → Proveedor: ___
[ ] Otros: ___
¿Alguno de estos proveedores tiene servidores fuera del EEE
(Europa)? Sí / No / No sé
¿Tenéis contratos de encargado del tratamiento (DPA/Art. 28)
firmados con todos ellos?
a) Sí, con todos
b) Con algunos — faltan: ___
c) Con ninguno


---

## BLOQUE 5 — Posiciones en contratos de encargado
BLOQUE 5 de 6 — Posiciones en contratos de encargado
(esto calibra el revisor-dpa-encargado)
Cuando el despacho actúa como RESPONSABLE contratando un encargado:

Auditorías: ¿qué aceptáis?
a) Solo cuestionarios/certificaciones (ISO 27001, ENS, SOC 2)
b) Auditoría directa con preaviso
c) Auditoría directa sin restricciones
Subencargados: ¿qué posición tomáis?
a) Autorización general previa (lista anexa)
b) Autorización específica caso a caso
c) Sin restricción
Localización de datos: ¿dónde aceptáis que estén?
a) Solo dentro del EEE
b) Fuera del EEE con garantías adecuadas (DPF, CCT)
c) Sin restricción
Plazo para suprimir/devolver datos al finalizar el contrato:
a) 30 días
b) 60 días
c) 90 días
d) Otro: ___
¿Exigís certificaciones específicas a los encargados?
[ ] ISO 27001
[ ] ENS (Esquema Nacional de Seguridad)
[ ] SOC 2
[ ] Ninguna en particular


---

## BLOQUE 6 — Documentos semilla y umbrales
BLOQUE 6 de 6 — Documentos de referencia y umbrales

URL de vuestra política de privacidad pública (si existe): ___
¿Tenéis una plantilla de contrato de encargado estándar?
a) Sí — ruta local o descripción: ___
b) No
¿Tenéis alguna EIPD ya aprobada que pueda usarse como referencia?
a) Sí — descripción: ___
b) No
Umbral de interesados a partir del cual recomendáis hacer EIPD
aunque no sea obligatoria:
a) 100 interesados
b) 500 interesados
c) 1.000 interesados
d) Solo cuando sea legalmente obligatoria
¿Tenéis registro de actividades de tratamiento (RAT)?
a) Sí, actualizado
b) Sí, desactualizado
c) No
Estilo de redacción preferido en los outputs:
a) Técnico-jurídico formal (para documentos oficiales)
b) Claro y accesible (para comunicaciones a clientes)
c) Ambos según el contexto (recomendado)


---

## GENERACIÓN DEL CLAUDE.md

Con las respuestas de los 6 bloques, genera el archivo de perfil
de práctica personalizado:

```bash
# Escribe el archivo en la ruta de configuración del plugin
cat > ~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md << 'PERFIL'
# Perfil de práctica — Privacidad y Protección de Datos (España)
# Generado por cold-start-interview-es · Lexia/Demalia
# Fecha de generación: [FECHA]
# Próxima revisión recomendada: [FECHA + 12 meses]

---

## 1. Identificación del despacho

- **Nombre**: [respuesta pregunta 1]
- **NIF/CIF**: [respuesta pregunta 2]
- **Dirección**: [respuesta pregunta 3]
- **Email de contacto**: [respuesta pregunta 4]
- **Teléfono**: [respuesta pregunta 5 o "No facilitado"]
- **Web**: [respuesta pregunta 6 o "No facilitada"]
- **Tipo**: [respuesta pregunta 7]
- **Rol habitual**: [respuesta pregunta 8]
- **Sectores de clientes**: [respuesta pregunta 9]
- **Asesora a responsables del tratamiento**: [respuesta pregunta 10]
- **Ámbito territorial**: España
- **Autoridad de control competente**: AEPD

---

## 2. Marco normativo aplicable

Marco base obligatorio para todos los skills:
- Reglamento (UE) 2016/679 (RGPD)
- Ley Orgánica 3/2018, de 5 de diciembre (LOPDGDD)

Normativa sectorial adicional según sectores declarados:
[generar automáticamente según respuesta pregunta 9]

INSTRUCCIÓN PARA TODOS LOS SKILLS: Nunca cites CCPA, HIPAA, COPPA
ni ninguna ley estadounidense. Nunca references la FTC ni state
attorneys general. Toda cita normativa debe ir con referencia BOE
cuando exista.

---

## 3. Plazos críticos RGPD/LOPDGDD

[reproducir tabla completa de plazos del CLAUDE.md template]

---

## 4. DPD y contactos de escalación

- **DPD designado**: [respuesta pregunta 11]
- **Email DPD**: [email de pregunta 11]
- **Teléfono DPD**: [teléfono de pregunta 11]
- **Escalación urgente (brechas 72h)**: [respuesta pregunta 12]
- **Firmante habitual de respuestas/notificaciones**: [respuesta pregunta 13]

---

## 5. Sistemas de datos y encargados

Sistemas declarados:
[generar lista a partir de respuesta pregunta 14]

Transferencias internacionales conocidas:
[generar a partir de respuesta pregunta 15]

Estado de contratos de encargado:
[respuesta pregunta 16]

---

## 6. Posiciones en contratos de encargado

Cuando el despacho actúa como RESPONSABLE:
- **Auditorías**: [respuesta pregunta 17]
- **Subencargados**: [respuesta pregunta 18]
- **Localización de datos**: [respuesta pregunta 19]
- **Plazo supresión/devolución**: [respuesta pregunta 20]
- **Certificaciones exigidas**: [respuesta pregunta 21]

---

## 7. Umbrales de triaje

- **Umbral EIPD recomendada**: [respuesta pregunta 25]
- **EIPD obligatoria**: según lista positiva AEPD + Art. 35 RGPD
  (no configurable — siempre aplica)

---

## 8. Documentos semilla

- **Política de privacidad vigente**: [respuesta pregunta 22]
- **Plantilla DPA estándar**: [respuesta pregunta 23]
- **EIPD de referencia**: [respuesta pregunta 24]
- **RAT (Registro de Actividades)**: [respuesta pregunta 26]

---

## 9. Estilo de redacción

- **Preferencia**: [respuesta pregunta 27]
- **Idioma**: español jurídico profesional — redacción nativa
- **Tratamiento**: usted/ustedes en comunicaciones formales
- **Citas normativas**: artículo completo + nombre de la norma
  en primera mención
- **Citas de fuente**:
  - [FUENTE: BOE] para normas publicadas en BOE
  - [FUENTE: AEPD] para guías y resoluciones AEPD
  - [FUENTE: CENDOJ] para señal de búsqueda manual
  - [FUENTE: RGPD] para artículos del Reglamento
  - [VERIFICAR] cuando no hay fuente oficial verificable

---

## 10. Escalación y revisión humana

Requieren revisión letrada obligatoria antes de enviar:
- Toda comunicación a la AEPD
- Toda respuesta ARSULIPO con denegación total o parcial
- Contratos de encargado con cláusulas no estándar
- Cualquier output con etiqueta [VERIFICAR]
- EIPDs completas

---

*Perfil generado por Lexia · Demalia · hector@demaliaconsulting.com*
*Marco jurisdiccional: España · Autoridad de control: AEPD*
*Generado: [FECHA] · Próxima revisión: [FECHA + 12 meses]*
PERFIL
```

---

## Confirmación final al usuario

Tras escribir el archivo, confirma:
✅ Perfil de práctica configurado correctamente.
Guardado en:
~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md
Todos los skills están ahora calibrados a [NOMBRE DEL DESPACHO].
Skills disponibles:
/privacy-legal-es:respondedor-arsulipo-es
/privacy-legal-es:notificador-brecha-aepd
/privacy-legal-es:triador-privacidad-es
/privacy-legal-es:generador-pias-aepd
/privacy-legal-es:revisor-dpa-encargado
/privacy-legal-es:generador-clausulas-rgpd
/privacy-legal-es:analizador-gap-regulatorio
/privacy-legal-es:monitor-politica-privacidad
Recomendaciones:

Guarda una copia del CLAUDE.md en tu repositorio como backup.
Revisa el perfil cada 12 meses o cuando cambien los tratamientos.
Para actualizar un campo concreto sin re-ejecutar el cold-start,
edita directamente el CLAUDE.md o dile a cualquier skill
"actualiza el perfil con [cambio]".


---

## Guardrails obligatorios

- **No inventar datos del despacho** — si el usuario no facilita
  un dato, marcarlo como [COMPLETAR], nunca rellenarlo con valores
  ficticios.
- **No escribir el archivo hasta tener todos los bloques** — esperar
  a que el usuario haya respondido los 6 bloques antes de generar
  el CLAUDE.md.
- **Confirmar antes de escribir** — mostrar el CLAUDE.md generado
  al usuario y pedir confirmación antes de escribirlo en disco.
- **El perfil no contiene datos de terceros** — solo datos del
  propio despacho, nunca de sus clientes.
- **Informar de la ruta exacta** donde se guarda el archivo para
  que el usuario pueda hacer backup.