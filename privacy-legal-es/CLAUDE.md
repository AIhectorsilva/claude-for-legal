# Perfil de práctica — Privacidad y Protección de Datos (España)

> Este archivo es la plantilla de perfil de práctica del plugin privacy-legal-es.
> El skill cold-start-interview-es lo copia a
> ~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md
> y lo rellena con los datos reales del despacho.
> Edítalo directamente para ajustes puntuales sin re-ejecutar el cold-start.

---

## 1. Identificación del despacho

- **Nombre**: [COMPLETAR EN COLD-START]
- **Tipo**: [ ] Despacho individual  [ ] Sociedad profesional  [ ] Departamento jurídico interno
- **Rol habitual**: [ ] Responsable del tratamiento  [ ] Encargado del tratamiento  [ ] Ambos
- **Sectores de clientes**: [COMPLETAR — ej: pymes tecnológicas, sector sanitario, e-commerce]
- **Ámbito territorial**: España (RGPD + LOPDGDD como marco base)
- **Autoridad de control competente**: AEPD (Agencia Española de Protección de Datos)

---

## 2. Marco normativo aplicable

Marco base obligatorio para todos los skills:
- Reglamento (UE) 2016/679 (RGPD)
- Ley Orgánica 3/2018, de 5 de diciembre (LOPDGDD)
- Real Decreto 1720/2007 (aplicable en lo no derogado)

Normativa sectorial adicional (marcar la aplicable):
- [ ] Ley 34/2002 (LSSI-CE) — servicios de la sociedad de la información
- [ ] Ley 9/2014 / Ley 9/2021 — sector telecomunicaciones
- [ ] Ley 41/2002 — autonomía del paciente (sector sanitario)
- [ ] Real Decreto-ley 12/2018 (NIS) — seguridad redes y sistemas
- [ ] Normativa CNMV / Banco de España — sector financiero
- [ ] Otra: [COMPLETAR]

**INSTRUCCIÓN PARA TODOS LOS SKILLS**: Nunca cites CCPA, HIPAA, COPPA ni ninguna
ley estadounidense. Nunca references la FTC ni state attorneys general.
Toda cita normativa debe ir con referencia BOE cuando exista.

---

## 3. Plazos críticos RGPD/LOPDGDD

Estos plazos son de aplicación obligatoria en todos los outputs:

| Procedimiento | Plazo | Base legal |
|---|---|---|
| Respuesta solicitudes ARSULIPO | 1 mes (prorrogable 2 meses más en casos complejos) | Art. 12.3 RGPD |
| Notificación brecha a AEPD | 72 horas desde conocimiento | Art. 33 RGPD |
| Notificación brecha a interesados | Sin dilación indebida | Art. 34 RGPD |
| Respuesta a reclamaciones ante AEPD | Según requerimiento AEPD | LOPDGDD |
| Registro de actividades de tratamiento | Permanente / actualización continua | Art. 30 RGPD |
| Conservación datos — general | Según finalidad + prescripción aplicable | Art. 5.1.e RGPD |

---

## 4. Posiciones del despacho en contratos de encargado

Posición por defecto cuando se actúa como **responsable** contratando encargados:
- Auditorías: [ ] Derecho de auditoría directa  [ ] Solo cuestionarios/certificaciones
- Subencargados: [ ] Autorización general previa  [ ] Autorización específica caso a caso
- Localización datos: [ ] Solo UE/EEE  [ ] Acepta transferencias con garantías adecuadas
- Plazo supresión tras contrato: [COMPLETAR — ej: 30 días]
- Certificaciones exigidas: [COMPLETAR — ej: ISO 27001, ENS]

Posición por defecto cuando se actúa como **encargado**:
- Subencargados propios: [COMPLETAR]
- Medidas técnicas mínimas que ofrecemos: [COMPLETAR]

---

## 5. Umbrales de triaje (triador-privacidad-es)

El skill triador-privacidad-es usa estos umbrales salvo instrucción contraria:

**EIPD OBLIGATORIA** (Art. 35 RGPD + lista AEPD) cuando concurra alguno de:
- Tratamiento a gran escala de categorías especiales (Art. 9 RGPD)
- Evaluación sistemática y exhaustiva mediante decisiones automatizadas con efectos jurídicos
- Videovigilancia a gran escala de zonas de acceso público
- Tratamiento combinado de datos de múltiples fuentes a gran escala
- Datos de personas vulnerables (menores, pacientes, empleados)
- Nuevas tecnologías con alto riesgo no evaluado previamente
- Cualquier actividad en la lista positiva publicada por la AEPD [FUENTE: AEPD]

**PIA RECOMENDADA** (no obligatoria legalmente pero sí por buenas prácticas):
- Tratamientos nuevos con datos de más de [COMPLETAR — ej: 500] interesados
- Cualquier tratamiento con datos sensibles aunque no sea a gran escala
- Nuevos encargados accediendo a datos de clientes

**PROCEDER** (sin evaluación formal):
- Tratamientos consolidados sin cambio de finalidad ni de escala
- Datos no personales o correctamente anonimizados

---

## 6. Estilo de redacción jurídica

Todos los outputs del plugin deben cumplir:
- Idioma: español jurídico profesional — redacción nativa, no traducción del inglés
- Tratamiento: usted / ustedes en comunicaciones formales
- Citas normativas: artículo completo + nombre de la norma en primera mención
  (ej: "artículo 13 del Reglamento (UE) 2016/679, de 27 de abril (RGPD)")
- Citas de fuente:
  - [FUENTE: BOE] para normas publicadas en BOE
  - [FUENTE: AEPD] para guías, resoluciones y criterios de la AEPD
  - [FUENTE: CENDOJ] para jurisprudencia de tribunales españoles
  - [VERIFICAR] cuando no hay fuente oficial verificable
- Tono: técnico-jurídico sin ser críptico — comprensible para el cliente no jurista
- Formato de fechas: DD/MM/AAAA
- Nunca dar consejo jurídico definitivo — siempre marcar como borrador para revisión letrada

---

## 7. Escalación y revisión humana

**Requieren revisión letrada obligatoria antes de cualquier envío:**
- Toda comunicación a la AEPD (notificaciones de brecha, respuestas a requerimientos)
- Toda respuesta a solicitudes ARSULIPO que implique denegación total o parcial
- Contratos de encargado con cláusulas no estándar
- Cualquier output con etiqueta [VERIFICAR]
- EIPDs completas antes de iniciar el tratamiento

**Contacto de escalación del despacho:**
- Responsable privacidad / DPD: [COMPLETAR — nombre + email]
- Escalación urgente (brechas 72h): [COMPLETAR — teléfono]

---

## 8. Documentos semilla del despacho

Rutas a los documentos de referencia que los skills usan para calibrar outputs:
- Política de privacidad vigente: [COMPLETAR — URL pública]
- Plantilla DPA/contrato encargado estándar: [COMPLETAR — ruta local o URL interna]
- EIPD de referencia aprobada: [COMPLETAR — ruta local]
- Registro de actividades de tratamiento: [COMPLETAR — ruta local]
- Cláusulas contractuales tipo aprobadas (si aplica): [COMPLETAR]

---

*Plugin desarrollado por Demalia · hector@demaliaconsulting.com*
*Marco jurisdiccional: España · Autoridad de control: AEPD*
*Versión: 0.1.0 · Última revisión: Mayo 2026*
