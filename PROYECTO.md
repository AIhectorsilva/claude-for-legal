# PROYECTO Lexia · Documentación maestra

> Este archivo es la fuente de verdad del proyecto.
> Cualquier chat nuevo que ayude a desarrollar Lexia debe leerlo primero.
> Última actualización: 19/05/2026 · Autor: Héctor Silva (CTO)

---

## 1. Qué es Lexia

Lexia es un software web de IA legal para despachos de abogados y abogados
autónomos españoles. Automatiza los flujos de trabajo jurídicos más repetitivos
— respuesta a solicitudes de derechos, evaluaciones de impacto, revisión de
contratos, notificaciones a autoridades — mediante agentes de IA especializados
en el ordenamiento jurídico español (RGPD, LOPDGDD, AEPD, BOE).

El producto está desarrollado por Demalia Consulting (Héctor Silva, CTO +
Izan, CEO) y se dirige a despachos individuales y pequeñas/medianas firmas
en España. El modelo de negocio es SaaS B2B con onboarding por despacho:
cada cliente configura su perfil de práctica (playbook) una vez y los agentes
quedan calibrados a su operativa concreta.

Lexia no es un chatbot genérico. Es un conjunto de agentes especializados
por área legal, cada uno con conocimiento profundo de la normativa española
aplicable, que trabajan sobre el contexto del despacho y producen outputs
listos para revisión letrada — nunca decisiones definitivas.

---

## 2. Stack técnico definitivo

| Capa | Tecnología | Notas |
|---|---|---|
| Frontend | Next.js 14 + TypeScript | App Router |
| Estilos | Tailwind CSS + shadcn/ui | |
| Auth + DB | Supabase | Row Level Security multi-tenant |
| Storage | Supabase Storage | Documentos de clientes |
| IA | Anthropic API — Claude Opus 4.7 | `claude-opus-4-7` |
| Engine | claude-for-legal fork | SKILL.md como system prompts |
| IDE | Cursor + Claude Code CLI | Claude Max (zero API cost en dev) |
| Repo engine | github.com/AIhectorsilva/claude-for-legal | Fork de anthropics/claude-for-legal |
| Repo app | github.com/AIhectorsilva/lexia-app | Pendiente crear |
| Hosting | Vercel | |
| Dominio | lexia.demalia.es | Pendiente |

---

## 3. Estructura de repos

```
~/dev/lexia/
├── claude-for-legal/          # Lexia Engine — plugins + skills
│   ├── PROYECTO.md            # Este archivo
│   ├── TODO.md                # Roadmap y tareas pendientes
│   ├── privacy-legal-es/      # Área LOPD/Privacidad ✅ COMPLETA
│   ├── employment-legal-es/   # Área Laboral 🔜 Próxima
│   ├── commercial-legal-es/   # Área Mercantil 📋 Planeada
│   ├── litigation-legal-es/   # Área Litigios 📋 Planeada
│   ├── [area]-legal-es/       # Patrón para áreas futuras
│   └── .claude-plugin/
│       └── marketplace.json   # Registro de plugins
│
└── lexia-app/                 # Panel web — Next.js (pendiente)
    ├── app/
    ├── components/
    └── ...
```

El repo `claude-for-legal` es un fork de `anthropics/claude-for-legal`
(Apache 2.0). Los plugins `*-legal-es` son originales de Demalia —
reescritos desde cero adaptando la arquitectura del repo original al
ordenamiento jurídico español.

---

## 4. Áreas legales y estado actual

| Área | Estado | Carpeta | Skills | Notas |
|---|---|---|---|---|
| LOPD/Privacidad | ✅ COMPLETA | `privacy-legal-es` | 9 | Cold-start + 8 skills operativos |
| Laboral | 🔜 Próxima | `employment-legal-es` | 9 planeados | Forkear `employment-legal` original |
| Mercantil/Contratos | 📋 Planeada | `commercial-legal-es` | 9 planeados | Forkear `commercial-legal` original |
| Litigios | 📋 Planeada | `litigation-legal-es` | 9 planeados | Forkear `litigation-legal` original |
| Societario | 📋 Planeada | `corporate-legal-es` | 9 planeados | Forkear `corporate-legal` original |
| Propiedad Intelectual | 📋 Planeada | `ip-legal-es` | 9 planeados | Forkear `ip-legal` original |
| Regulatorio | 📋 Planeada | `regulatory-legal-es` | 9 planeados | Forkear `regulatory-legal` original |

### Skills del área LOPD/Privacidad (privacy-legal-es)

| # | Skill | Función | Estado |
|---|---|---|---|
| 0 | `cold-start-interview-es` | Onboarding — genera el playbook del despacho | ✅ |
| 1 | `respondedor-arsulipo-es` | Respuesta a solicitudes ARSULIPO (Art. 15-21 RGPD) | ✅ |
| 2 | `notificador-brecha-aepd` | Análisis y notificación de brechas 72h (Art. 33-34 RGPD) | ✅ |
| 3 | `triador-privacidad-es` | Triaje EIPD obligatoria / recomendada / proceder / STOP | ✅ |
| 4 | `generador-pias-aepd` | Generación de EIPDs completas (metodología AEPD) | ✅ |
| 5 | `revisor-dpa-encargado` | Revisión contratos encargado Art. 28 RGPD + CCT 2021 | ✅ |
| 6 | `generador-clausulas-rgpd` | Cláusulas informativas, consentimiento, cookies | ✅ |
| 7 | `analizador-gap-regulatorio` | Gap analysis normativa vs. política actual | ✅ |
| 8 | `monitor-politica-privacidad` | Detecta deriva política vs. práctica real | ✅ |

---

## 5. Convenciones del proyecto

### Naming

```
Plugins:     [nombre-original]-es        (ej: privacy-legal-es)
Skills:      [nombre-descriptivo-es]     (ej: respondedor-arsulipo-es)
Archivos:    kebab-case
Variables:   camelCase
Tablas DB:   snake_case
```

### Estructura de un plugin

```
[area]-legal-es/
├── .claude-plugin/
│   └── plugin.json          # name, version, description, author (objeto)
├── .mcp.json                # MCP servers (Sprint 2)
├── CLAUDE.md                # Template del perfil de práctica
├── README.md                # Documentación del plugin
├── hooks/
│   └── hooks.json
└── skills/
    ├── cold-start-interview-es/
    │   └── SKILL.md
    ├── [skill-1]/
    │   └── SKILL.md
    └── ...
```

### plugin.json — formato correcto

```json
{
  "name": "privacy-legal-es",
  "version": "0.1.0",
  "description": "Descripción del plugin.",
  "author": {
    "name": "Demalia",
    "email": "hector@demaliaconsulting.com"
  },
  "license": "Apache-2.0"
}
```

⚠️ El campo `author` debe ser un **objeto**, no un string. Claude Code
rechaza el plugin si es string.

### marketplace.json — añadir un plugin nuevo

```json
{
  "name": "[area]-legal-es",
  "source": "./[area]-legal-es",
  "description": "Descripción.",
  "author": { "name": "Demalia" }
}
```

Añadir al array `plugins` de `.claude-plugin/marketplace.json` en la
raíz del repo. Sin esto, `/plugin install` no encuentra el plugin.

### Estructura de un SKILL.md

```markdown
---
name: nombre-del-skill
description: >
  Descripción detallada de qué hace y cuándo se activa.
  Esto es el trigger de activación — debe ser exhaustivo.
  Incluir frases exactas que diría el usuario para activarlo.
argument-hint: "[hint del argumento esperado]"
---

# /[plugin]:[skill]

1. Paso de inicialización (cargar CLAUDE.md del perfil)
2. Pasos del flujo numerados
3. ...
N. Guardrail final

[Bloque de invocación de ejemplo]

---

# Título descriptivo del skill

## Contexto de práctica
[Lee el perfil · marco jurisdiccional · instrucción de fallback]

## PASO 1 — [Nombre]
[Contenido del paso]

## PASO N — [Nombre]
[Contenido del paso]

## Guardrails obligatorios
[Lista de restricciones que nunca se saltan]
```

---

## 6. Sistema de citaciones — regla central

Todos los SKILL.md y todos los outputs deben usar este sistema.
Es arquitectura de Sprint 1, no un añadido posterior.

| Etiqueta | Significado | Cuándo usar |
|---|---|---|
| `[FUENTE: BOE]` | Norma publicada en BOE | Leyes, RD, órdenes ministeriales españolas |
| `[FUENTE: AEPD]` | Guía, resolución o criterio de la AEPD | Guías, resoluciones sancionadoras, criterios |
| `[FUENTE: RGPD]` | Artículo del Reglamento (UE) 2016/679 | Cualquier cita del RGPD |
| `[FUENTE: CENDOJ]` | Señal de búsqueda manual en CENDOJ | Jurisprudencia de tribunales españoles |
| `[VERIFICAR]` | Sin fuente oficial verificable en este momento | Cuando el modelo aplica conocimiento sin fuente confirmable |

En Sprint 2, los MCP conectarán BOE y AEPD para verificación en tiempo
real. `[VERIFICAR]` se reducirá pero nunca desaparecerá — es la señal
para el letrado revisor.

---

## 7. CENDOJ — decisión de arquitectura permanente

**CENDOJ NO se conecta vía MCP. NUNCA.**

Razones:
- Licencia comercial — el uso automatizado requiere acuerdo con el CGPJ
- CAPTCHA anti-IA activo en la web pública
- Riesgo legal de scraping en fuente oficial

**Modo de integración correcto:**
1. El skill usa `[FUENTE: CENDOJ]` como señal al letrado
2. El letrado localiza la sentencia manualmente en `cendoj.poderjudicial.es`
3. La arrastra/sube a Lexia
4. Lexia analiza el documento, extrae ratio decidendi, aplica al caso

Este modo es una decisión de diseño, no una limitación técnica temporal.

---

## 8. Marco jurisdiccional — regla absoluta

Lexia es 100% para el mercado español. Sin excepciones.

- Marco normativo: RGPD (UE 2016/679) + LOPDGDD (LO 3/2018)
- Autoridad de control: AEPD (nunca FTC, nunca ICO, nunca CNIL)
- Plazos: los del RGPD/LOPDGDD (nunca plazos US)
- Jurisprudencia: AEPD + tribunales españoles (nunca US case law)
- Idioma de outputs: español jurídico profesional nativo

Cuando se forkea un skill del repo original (en derecho americano):
**NO traducir literalmente. REESCRIBIR** adaptando conceptos, normativa,
plazos y ejemplos al equivalente español más cercano.

---

## 9. Cómo se construyó el área LOPD/Privacidad

### Proceso seguido (replicar para áreas nuevas)

1. **Fork del repo original** — `gh repo fork anthropics/claude-for-legal`
2. **Duplicar el plugin** — `cp -r privacy-legal privacy-legal-es`
3. **Renombrar skills** — nombres descriptivos en español
4. **Crear skills nuevos** sin equivalente en el original
5. **Actualizar `marketplace.json`** — añadir entrada del nuevo plugin
6. **Instalar en Claude Code** — `/plugin install [plugin]@claude-for-legal`
7. **Escribir `CLAUDE.md`** — perfil de práctica template
8. **Escribir cada `SKILL.md`** — uno por sesión, validar con caso real
9. **Validar** — caso real en Claude Code antes de hacer commit
10. **Commit** — `feat: [skill] — SKILL.md completo [normativa]`

### Decisiones técnicas tomadas en esta área

- Los skills nuevos sin equivalente (`notificador-brecha-aepd`,
  `generador-clausulas-rgpd`) se construyeron desde cero
- El sistema `[FUENTE: X]` / `[VERIFICAR]` es capa central desde el día 1
- CENDOJ: modo asistente manual desde el inicio (ver sección 7)
- MCP conectores de BOE + AEPD + BORME + TC: reservados para Sprint 2

---

## 10. Cómo construir un área nueva

Sigue estos pasos exactos. No saltar ninguno.

### Paso 1 — Scaffold del plugin

```bash
cd ~/dev/lexia/claude-for-legal

# Duplicar el plugin original del repo base
cp -r [nombre-original] [nombre-original]-es
cd [nombre-original]-es/skills

# Renombrar skills existentes
mv [skill-original] [skill-es]
# ...para cada skill

# Crear skills nuevos sin equivalente
mkdir [nuevo-skill-es]
touch [nuevo-skill-es]/SKILL.md

cd ../..
```

### Paso 2 — Actualizar plugin.json

```json
{
  "name": "[area]-legal-es",
  "version": "0.1.0",
  "description": "Descripción en español.",
  "author": {
    "name": "Demalia",
    "email": "hector@demaliaconsulting.com"
  },
  "license": "Apache-2.0"
}
```

### Paso 3 — Registrar en marketplace.json

```bash
node -e "
const fs = require('fs');
const path = process.env.HOME + '/dev/lexia/claude-for-legal/.claude-plugin/marketplace.json';
const data = JSON.parse(fs.readFileSync(path, 'utf8'));
data.plugins.push({
  name: '[area]-legal-es',
  source: './[area]-legal-es',
  description: 'Descripción.',
  author: { name: 'Demalia' }
});
fs.writeFileSync(path, JSON.stringify(data, null, 2));
console.log('OK');
"
```

### Paso 4 — Instalar en Claude Code

```bash
claude
/plugin install [area]-legal-es@claude-for-legal
/reload-plugins
```

### Paso 5 — Escribir CLAUDE.md

El `CLAUDE.md` del plugin es el template del perfil de práctica.
Estructura obligatoria (ver `privacy-legal-es/CLAUDE.md` como referencia):

1. Identificación del despacho
2. Marco normativo aplicable al área
3. Plazos críticos específicos del área
4. Posiciones del despacho (negociación, umbrales)
5. Estilo de redacción
6. Escalación y revisión humana
7. Documentos semilla

### Paso 6 — Escribir los SKILL.md

Para cada skill, en orden de criticidad legal:

1. Analizar el skill original del repo base (si existe)
2. Identificar qué hay que reescribir vs. qué hay que crear desde cero
3. Escribir el SKILL.md siguiendo la estructura estándar (sección 5)
4. Validar con un caso real en Claude Code
5. Commit individual por skill

### Paso 7 — Cold-start

El `cold-start-interview-es` es siempre el último skill en escribirse
porque depende de conocer todos los demás. Su función es generar el
`~/.claude/plugins/config/claude-for-legal/[area]-legal-es/CLAUDE.md`
con los datos reales del despacho.

---

## 11. Arquitectura del panel web (lexia-app)

> Sección pendiente de desarrollo. Se completa en la próxima sesión.

### Estructura de rutas prevista

```
/                          Landing / login
/onboarding                Cold-start web (formulario paso a paso)
/dashboard                 Panel principal — 8 skills como cards
/skill/[nombre]            Interfaz de cada skill
/perfil                    Ver/editar el perfil de práctica
/historial                 Outputs generados anteriores
/admin                     Gestión de despachos (Demalia)
```

### Cómo conectar un skill con la API

```typescript
// El SKILL.md se usa como system prompt
const response = await anthropic.messages.create({
  model: 'claude-opus-4-7',
  max_tokens: 4096,
  system: skillMdContent,        // Contenido del SKILL.md
  messages: [
    {
      role: 'user',
      content: `${perfilDespacho}\n\n${inputDelUsuario}`
    }
  ]
})
```

El perfil de práctica del despacho (equivalente al `CLAUDE.md`) se
guarda en Supabase y se inyecta como contexto en cada llamada.

### Multi-tenant — Row Level Security

Cada despacho tiene su propio aislamiento en Supabase.
Patrón: todas las tablas tienen columna `despacho_id` con RLS policy.

```sql
-- Política RLS tipo para todas las tablas
CREATE POLICY "Despacho solo ve sus datos"
ON [tabla]
FOR ALL
USING (despacho_id = auth.jwt() ->> 'despacho_id');
```

---

## 12. Sprint 2 — MCP conectores

Conectores planificados para verificación normativa en tiempo real:

| Conector | URL | Objetivo |
|---|---|---|
| BOE | `boe.es/datosabiertos` | Citas `[FUENTE: BOE]` verificadas en tiempo real |
| AEPD sede | `sedeagpd.gob.es` | Resoluciones, guías, estado notificaciones |
| BORME | `boe.es/borme` | Verificación datos registrales |
| Tribunal Constitucional | `tribunalconstitucional.es` | Jurisprudencia constitucional |
| Diarios autonómicos | Varios | Normativa autonómica sectorial |

**CENDOJ: NO conectar.** Ver sección 7.

Proceso de actualización en Sprint 2:
1. Conectar MCP para cada fuente
2. Actualizar `.mcp.json` de cada plugin
3. Revisar todos los `SKILL.md` — promover `[VERIFICAR]` → `[FUENTE: X]`
   donde el MCP ya pueda resolver la cita

---

## 13. Costes y API

- **Modelo**: Claude Opus 4.7 (`claude-opus-4-7`)
- **Desarrollo**: Claude Max subscription (zero API cost en dev via Claude Code)
- **Producción**: Anthropic API standard — pay per token
- **Estimación por skill invocado**: variable según longitud del SKILL.md
  y del output. EIPDs completas pueden ser llamadas largas.
- **Enterprise**: pendiente solicitud para volumen

---

## 14. Contactos y responsables

| Nombre | Rol | Responsabilidad en Lexia |
|---|---|---|
| Héctor Silva | CTO + co-fundador | Arquitectura, desarrollo, AI |
| Izan | CEO + co-fundador | Ventas, BD, go-to-market |
| Dani | Copywriting | Contenido, emails, comunicación |
| Leo | Abogado colaborador | Revisión letrada de outputs críticos |

**Contacto técnico**: hector@demaliaconsulting.com · 660414059

---

## 15. Decisiones técnicas registradas

| Decisión | Alternativa descartada | Razón |
|---|---|---|
| SKILL.md como system prompts | Base de datos de prompts | Versionable en git, editable por letrados sin código |
| CENDOJ modo manual | MCP conector | Licencia comercial + CAPTCHA anti-IA |
| Claude Opus 4.7 | Modelos más baratos | Calidad jurídica — no negociable |
| Fork de anthropics/claude-for-legal | Construir desde cero | Arquitectura probada + convenciones establecidas |
| Supabase RLS | Auth custom | Multi-tenant seguro con mínimo código |
| `author` como objeto en plugin.json | String | Claude Code rechaza el plugin si es string |

---

*Demalia Consulting · hector@demaliaconsulting.com*
*Documento vivo — actualizar tras cada sesión de desarrollo*
