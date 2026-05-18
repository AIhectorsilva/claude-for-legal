---
name: revisor-dpa-encargado
description: >
  Revisa contratos de encargado del tratamiento (DPA — Data Processing Agreement)
  conforme al Art. 28 RGPD. Auto-detecta si el despacho actúa como responsable
  del tratamiento (contratando un encargado) o como encargado (siendo contratado
  por un responsable). Revisa el contrato cláusula a cláusula contra el checklist
  del Art. 28 RGPD y las posiciones del despacho, propone redlines y marca las
  cláusulas que requieren escalación letrada.
  Úsalo cuando el usuario diga "tengo un contrato de encargado para revisar",
  "me mandan un DPA", "tengo que firmar un contrato de tratamiento de datos",
  "quiero revisar las cláusulas de protección de datos de un proveedor",
  "necesito un contrato de encargado para mi proveedor de cloud/SaaS/gestoría".
argument-hint: "[pega el contrato o describe las cláusulas principales]"
---

# /revisor-dpa-encargado

1. Carga `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md` →
   extrae: rol habitual del despacho, posiciones en contratos de encargado
   (sección 4), contacto de escalación.
2. Auto-detecta la dirección del contrato (responsable contratando encargado /
   encargado siendo contratado). Si no es claro, pregunta.
3. Revisa el contrato contra el checklist obligatorio del Art. 28 RGPD.
4. Compara cada cláusula contra las posiciones del despacho (CLAUDE.md sección 4).
5. Output: revisión cláusula a cláusula + redlines propuestas + items a escalar.
6. Nunca enviar redlines directamente — revisión letrada obligatoria.
/privacy-legal-es:revisor-dpa-encargado
[pega el contrato o describe las cláusulas]

---

# Revisión de Contratos de Encargado del Tratamiento — Art. 28 RGPD

## Contexto de práctica

Lee `~/.claude/plugins/config/claude-for-legal/privacy-legal-es/CLAUDE.md`
sección 4 (posiciones del despacho en contratos de encargado).
Si no existe el perfil, aplica posiciones por defecto conservadoras y
etiqueta outputs como `[PERFIL NO CONFIGURADO]`.

**Marco jurisdiccional:** España. Art. 28 RGPD + guía de la AEPD sobre
contratos de encargado del tratamiento. [FUENTE: AEPD]
Transferencias internacionales: Cláusulas Contractuales Tipo (CCT) de la
Comisión Europea, Decisión de Ejecución (UE) 2021/914. [FUENTE: AEPD]

---

## PASO 1 — Detección de dirección y contexto

**Determina:**

| Pregunta | Respuesta |
|---|---|
| ¿Quién es el responsable del tratamiento? | [extraer del contrato] |
| ¿Quién es el encargado del tratamiento? | [extraer del contrato] |
| ¿Actúa el despacho como responsable o como encargado? | [auto-detectar] |
| ¿Cuál es el objeto del encargo? | [extraer] |
| ¿Hay subencargados mencionados? | [extraer] |
| ¿Hay transferencias internacionales? | [extraer] |

**Dirección del análisis:**
- **Modo responsable** (despacho contrata encargado): objetivo es proteger
  la posición del responsable — verificar que el encargado asume todas las
  obligaciones del Art. 28, que los derechos de auditoría están garantizados,
  y que la cadena de subencargados está controlada.
- **Modo encargado** (despacho es contratado): objetivo es proteger la
  posición del encargado — verificar que las obligaciones son asumibles,
  que no se imponen responsabilidades desproporcionadas, y que los plazos
  son realistas.

---

## PASO 2 — Checklist obligatorio Art. 28 RGPD

Verifica la presencia y corrección de cada elemento obligatorio.
[FUENTE: RGPD]

| # | Elemento obligatorio (Art. 28.3 RGPD) | ¿Presente? | ¿Correcto? | Observación |
|---|---|---|---|---|
| 1 | Objeto y duración del tratamiento | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 2 | Naturaleza y finalidad del tratamiento | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 3 | Tipo de datos personales tratados | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 4 | Categorías de interesados | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 5 | Tratamiento solo según instrucciones del responsable | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 6 | Confidencialidad del personal autorizado | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 7 | Medidas de seguridad Art. 32 RGPD | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 8 | Régimen de subencargados (autorización previa) | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 9 | Asistencia al responsable en derechos ARSULIPO | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 10 | Asistencia al responsable en obligaciones Arts. 32-36 | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 11 | Supresión o devolución de datos al finalizar el contrato | ✅/⚠️/❌ | ✅/⚠️/❌ | |
| 12 | Puesta a disposición de información + derecho de auditoría | ✅/⚠️/❌ | ✅/⚠️/❌ | |

**Elementos ausentes o deficientes:** listar con referencia al artículo
y propuesta de redline. Un contrato sin los 12 elementos no cumple el
Art. 28 RGPD y expone al responsable a sanción. [FUENTE: RGPD]

---

## PASO 3 — Análisis cláusula a cláusula

Para cada cláusula relevante del contrato, genera la siguiente ficha:
CLÁUSULA [N] — [Título/Materia]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Texto original:   "[extracto relevante]"
Evaluación:       [ ] OK  [ ] Mejorable  [ ] Problemática  [ ] Ausente
Problema:         [descripción del problema si lo hay]
Referencia legal: [Art. X RGPD / Guía AEPD / CCT 2021]
Posición despacho:[confrontar con CLAUDE.md sección 4]
Redline propuesta:"[texto alternativo propuesto]"
Escalar:          [ ] Sí — [motivo]  [ ] No

### Cláusulas de especial atención

**Subencargados (Art. 28.2 y 28.4 RGPD):**
- ¿Autorización general previa o específica caso a caso?
- ¿Lista de subencargados aprobados anexa al contrato?
- ¿Obligación del encargado de notificar cambios con antelación suficiente?
- ¿Derecho del responsable a oponerse a nuevos subencargados?
- ¿Los subencargados asumen las mismas obligaciones que el encargado
  mediante contrato? [FUENTE: RGPD]

**Auditorías (Art. 28.3.h RGPD):**
- ¿Se reconoce el derecho de auditoría directa o solo mediante
  cuestionarios/certificaciones?
- ¿Preaviso razonable (30-60 días es estándar)?
- ¿Quién asume los costes? [VERIFICAR — posición AEPD]
- Posición por defecto: derecho de auditoría directa con preaviso
  razonable. Aceptar solo certificaciones (ISO 27001, ENS, SOC 2)
  si expresamente se configura así en CLAUDE.md.

**Medidas de seguridad (Art. 28.3.c + Art. 32 RGPD):**
- ¿Se listan medidas concretas o solo referencias genéricas?
- ¿Se incluye cifrado, seudonimización, disponibilidad, resiliencia?
- ¿Hay obligación de notificar brechas al responsable con plazo
  suficiente para que este cumpla sus 72h ante la AEPD? [FUENTE: RGPD]
  Plazo razonable en el contrato: máximo 24-48h desde detección.

**Supresión/devolución al finalizar (Art. 28.3.g RGPD):**
- ¿Se especifica el plazo para suprimir o devolver?
- ¿Se incluyen backups y sistemas de archivo?
- ¿Se exige certificado de destrucción?
- Plazo por defecto del despacho: ver CLAUDE.md sección 4.

**Transferencias internacionales:**
- ¿Los datos se tratan fuera del EEE?
- ¿Existe mecanismo de transferencia adecuado?
  - Decisión de adecuación de la Comisión Europea [VERIFICAR vigencia]
  - CCT Decisión (UE) 2021/914 [FUENTE: AEPD]
  - Normas corporativas vinculantes (BCR)
- Si hay transferencia sin mecanismo adecuado → **ESCALA** —
  es una infracción grave del Art. 44 RGPD. [FUENTE: RGPD]

**Responsabilidad y régimen de daños:**
- ¿El reparto de responsabilidad es equilibrado?
- ¿Hay limitaciones de responsabilidad desproporcionadas?
- ¿Se establece el régimen del Art. 82 RGPD (responsabilidad solidaria
  frente al interesado)? [FUENTE: RGPD]

---

## PASO 4 — Comparación con posiciones del despacho

Confronta cada cláusula relevante con las posiciones configuradas en
CLAUDE.md sección 4:

| Materia | Posición del despacho | Cláusula del contrato | Diferencia | ¿Aceptable? |
|---|---|---|---|---|
| Auditorías | [desde CLAUDE.md] | [del contrato] | [delta] | Sí/No |
| Subencargados | [desde CLAUDE.md] | [del contrato] | [delta] | Sí/No |
| Localización datos | [desde CLAUDE.md] | [del contrato] | [delta] | Sí/No |
| Plazo supresión | [desde CLAUDE.md] | [del contrato] | [delta] | Sí/No |
| Certificaciones | [desde CLAUDE.md] | [del contrato] | [delta] | Sí/No |

---

## PASO 5 — Resumen ejecutivo y redlines

Genera el resumen final:
RESUMEN DE REVISIÓN — CONTRATO ENCARGADO DEL TRATAMIENTO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Contrato:         [nombre/descripción]
Partes:           [Responsable] → [Encargado]
Dirección:        [Despacho como responsable / como encargado]
Fecha revisión:   DD/MM/AAAA
[PERFIL NO CONFIGURADO si aplica]
ELEMENTOS OBLIGATORIOS ART. 28:
Presentes y correctos:  [N]/12
Ausentes o deficientes: [lista]
CLÁUSULAS PROBLEMÁTICAS:    [N]
CLÁUSULAS A ESCALAR:        [N]
REDLINES PROPUESTAS:        [N]
RECOMENDACIÓN GLOBAL:
[ ] Aceptable con redlines menores
[ ] Requiere renegociación — redlines significativas
[ ] No aceptable — infracción grave del Art. 28 RGPD
[ ] No aceptable — transferencia internacional sin garantías
ITEMS A ESCALAR (revisión letrada obligatoria):

[item] — [motivo]
[item] — [motivo]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  BORRADOR — Revisión letrada obligatoria antes de
firmar, enviar redlines o rechazar el contrato.


---

## Guardrails obligatorios

- **Nunca recomendar firmar un contrato que incumpla el Art. 28 RGPD** —
  el responsable que contrata a un encargado sin contrato adecuado responde
  solidariamente de las infracciones del encargado. [FUENTE: RGPD]
- **Transferencia internacional sin mecanismo → ESCALA siempre** —
  es infracción grave Arts. 44-49 RGPD, sancionable con hasta 20M€ o
  4% facturación global. [FUENTE: RGPD]
- **Nunca usar CCT anteriores a la Decisión (UE) 2021/914** — las CCT
  antiguas (2001, 2004, 2010) quedaron derogadas. [FUENTE: AEPD]
- **Revisión letrada obligatoria antes de firmar, rechazar o enviar
  redlines** — el skill genera borradores, no decisiones definitivas.
- Citar siempre [FUENTE: RGPD], [FUENTE: AEPD], [VERIFICAR].
- Si el contrato contiene datos personales de terceros (clientes,
  empleados), manejar con la misma cautela que el respondedor-arsulipo-es.