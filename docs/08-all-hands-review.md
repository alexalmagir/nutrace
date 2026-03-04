# Nutrace — All-Hands Review Session

**Document:** docs/08-all-hands-review.md
**Date:** 2026-03-03
**Phase:** D — Build
**Session:** All-hands (Founder + CPO + CDO + CMO + CTO + Chief of Staff)
**Constraint:** MVP en 4 semanas
**Status:** Final — signed off by Alexandre Maravilla

---

## CHIEF OF STAFF — Apertura

Tenemos docs/00 a docs/07 producidos. Hipótesis H1 y H2 validadas. GO decision confirmada. Arquitectura y plan de ejecución entregados.

**Pero el plan actual tiene 6 semanas. El constraint es 4.**

Y más importante: hemos estado construyendo un *producto*. Hoy revisamos un *negocio*.

**Regla de la sesión:** Si no puedes justificar una feature desde la perspectiva del modelo de negocio (no del usuario), va al backlog.

---

## FOUNDER — Oportunidad y Riesgos de Negocio

### Lo que valido sin cambios

El mercado es real y grande. 40% de la población global con trastornos GI funcionales. IBS casi duplicada post-COVID (6.1% → 11%). Cara Care ha salido del mercado. La ventana de 12-18 meses es real.

El problema es doloroso. 6.6 años de media hasta diagnóstico de IBS. 3.6 días de trabajo perdidos al mes. Las hipótesis H1 y H2 están validadas.

### Riesgos identificados

**Riesgo 1 — Cero señal de negocio a 4 semanas.**
El plan actual produce un producto gratuito con 3 usuarios beta. No hay señal de que alguien pagaría por esto. El doctor que recibe el PDF fue validado con un mock — no con el producto real.

**Ask:** La beta no termina con "3 usuarios logeando". Termina con al menos **1 HCP que recibe un PDF real de un paciente real y da feedback cualitativo**.

**Riesgo 2 — No hay mecanismo de descubrimiento.**
¿Cómo encuentra Nutrace su primer usuario que no sea Alex? App Store no funciona para herramientas clínicas.

**Ask al CMO:** estrategia de seeding de HCPs en paralelo al build, no después.

**Riesgo 3 — El flywheel B2B2C no arranca solo.**
El modelo "gratis para pacientes, suscripción para HCPs" solo funciona si los HCPs recomiendan la app. Para que eso pase, algún HCP tiene que haber usado un PDF real antes de la Semana 4.

**Veredicto del Founder:** Oportunidad válida. Modelo de negocio creíble. El plan de ejecución trata el lanzamiento como un evento de producto, no como el inicio de un ciclo comercial. La beta debe incluir HCPs desde el día 1.

---

## CPO — Problema, ICP y PRD

### Lo que defiendo sin cambios

- El problem statement es correcto y validado
- El ICP primario (Segmento A) es el correcto
- La proactive trigger alert es el único feature verdaderamente único en el mercado
- El patrón a 3 días es el motor de retención

### Lo que cambio

**Scope honesto para 4 semanas:** Segmento A es el foco. Los demás segmentos son bienvenidos pero el producto no está optimizado para ellos en V1.

**Métricas de éxito revisadas:**

| Métrica anterior | Métrica revisada |
|-----------------|-----------------|
| 3 usuarios beta 3+ días | 10 usuarios beta, D7 retention ≥ 40% |
| Al menos 1 PDF exportado | Al menos 3 PDFs compartidos con un HCP real |
| No P0 crashes | Se mantiene |
| GPT Vision p95 < 5s | Se mantiene |
| *(ausente)* | 1 HCP da feedback cualitativo positivo sobre utilidad clínica del PDF |

**Riesgo que añado:** Si el usuario logea meals pero no añade síntomas, el pattern algorithm no tiene con qué trabajar y nunca surfea un pattern. El usuario llega al día 4 sin insight y churna.

**Ask al CTO:** nudge push notification si usuario lleva 2+ días sin ningún symptom entry.

### Lo que corto del PRD para 4 semanas

| Feature | Decisión |
|---------|----------|
| Segmento F — prior diagnosis field | Mantener — 1 campo de texto, coste mínimo, alta diferenciación |
| Segmento C/D/E — optimizaciones específicas | Diferir — todos pueden usar la app, no está optimizada para ellos |
| Custom date range PDF (Segmento C) | Diferir |
| Confidence indicator UI (Segmento D) | Diferir — modelo lo soporta, UI en V1.1 |
| Pattern comparison view (Segmento F) | V2 — data model diseñado |

---

## CMO — GTM, Posicionamiento y Diferenciación

### Lo que defiendo sin cambios

- Posicionamiento top-right (low friction + clinical): nadie está ahí, no se mueve
- One-liner: *"The food diary that warns you before you eat — and gives your doctor a log they can actually use."* — no se toca
- Modelo freemium para pacientes: correcto estratégicamente

### GTM en 4 semanas — 3 tracks paralelos al build

**Track A — Seeding de pacientes (Semanas 1-3):**
- Reddit: r/ibs (500k+ members), r/FODMAP, r/GutHealth. Post honesto de builder buscando 10 beta testers con síntomas digestivos reales.
- Red personal de Alex: los mejores beta testers son personas que el fundador conoce.
- Twitter/X: build-in-public, 1 post/semana.
- Target Semana 4: 10-15 usuarios beta activos.

**Track B — Seeding de HCPs (Semanas 1-4):**
- Semana 1: identificar 10 HCPs en LinkedIn (gastros + dietistas con perfil activo)
- Semana 2: DM a 5 de ellos — texto personalizado, sin pitch agresivo
- Semana 3: call/demo de 15 minutos con quien responda positivamente
- Semana 4: envío de PDF real via share link (feature del CTO)
- Target: 1 HCP con feedback positivo cualitativo

**Track C — Build-in-public (Semanas 1-4):**
- Post Semana 1: "Por qué construyo Nutrace" (el problema, no el producto)
- Post Semana 2: "El modelo de IA que detecta ingredientes — y sus límites"
- Post Semana 3: "El algoritmo de patrones: 3 días de datos para el primer insight"
- Post Semana 4: "Beta live. Aquí está el PDF que genera Nutrace."

**App Store keywords:** "IBS food diary", "gut symptom tracker", "food trigger finder", "digestive diary"

---

## CDO — UX Flows

### Lo que defiendo sin cambios

- Jerarquía 3 tabs (Log / My Log / Export): correcta
- Todos los constraints de Phase B: no-negociables
- Screen 2.5 (confirmación + day counter): motor de habit loop, no se simplifica

### Lo que cambio para 4 semanas

**Flow 6 (Trigger Alert Detail) — versión mínima:**
```
⚠️ About Parmesan

Meals with parmesan in your log:    5
Meals with symptoms afterward:      3

[Remove from this entry]   [Continue →]

"This is a pattern from your log, not a diagnosis."
```
Sin timeline chart. Solo números. Mismo valor clínico, 80% menos complejidad.

**PDF — versión MVP sin bar chart:**
```
SYMPTOM OVERVIEW — 14 DAYS
Symptomatic days: 8 / 14   |   Average severity: 3.2 / 5

TOP PATTERNS
● Dairy: symptoms in 4 of 5 meals (80%)
● Wheat: symptoms in 2 of 3 meals (67%)
```
Tabla de texto en lugar de SVG chart. Bar chart vuelve en V1.1.

**Delayed check-in (Flow 3):** Se mantiene. Basic send sin retry logic en V1.

### Commit del CDO

Revisaré el template PDF con un HCP real (si Alex consigue 15 minutos con un gastro o dietista antes del fin de Semana 3) para validar el layout antes de que llegue a los HCPs en Semana 4.

### Lo que corto

| Elemento | Decisión |
|----------|----------|
| Flow 6 timeline chart | Reemplazado por tabla de números |
| PDF bar chart SVG | Reemplazado por tabla de texto |
| Confidence indicator UI | Diferir — data model lo soporta |
| APScheduler retry logic | Diferir |
| Empty states elaborados | Solo los críticos (My Log 0 entries, Export sin datos) |

---

## CTO — Arquitectura y Plan de Ejecución

### Lo que defiendo sin cambios

- Stack: React Native + Expo, FastAPI, Supabase EU, GPT-4o (benchmark-first)
- Data model con hcp_links desde día 1
- Supabase EU region — GDPR no es opcional

### Compresión 6 → 4 semanas

**Lo que se corta:**

| Feature técnico | Decisión |
|-----------------|----------|
| GitHub Actions CI | Diferir — V1.1 |
| structlog completo | print() con timestamps es suficiente para 10 users |
| APScheduler retry logic | Diferir |
| PDF bar chart SVG | Cortado por CDO |
| Flow 6 timeline chart | Cortado por CDO |
| Rate limiting en API | Diferir — no aplica a 10-15 users |

**Lo que añado:**

- **Nudge de síntomas (Semana 3):** push notification si usuario lleva 2+ días sin symptom entry. Texto: *"How did you feel after your last meal? Add a symptom note — your doctor needs this data."*
- **HCP PDF share link (Semana 4):** `GET /share/pdf/{share_token}` — URL pública read-only con consentimiento del usuario. UUID de 32 chars, TTL 7 días, revocable desde la app. El HCP abre el PDF en el browser sin crear cuenta. El footer del PDF incluye *"Generated by Nutrace · nutrace.app"*.

**Benchmark de modelos (Semana 2):**
- 50 fotos reales (25 caseras + 25 restaurante)
- GPT-4o + GPT-4.5 (si disponible) + Gemini 2.5 Pro
- Criterio: ≥70% precisión, menor latencia, menor coste
- Winner va a producción

---

## TENSIONES IDENTIFICADAS

| Tensión | Entre | Resolución |
|---------|-------|------------|
| Producto vs. negocio | Founder ↔ CPO | Beta success = 1 HCP con feedback positivo real, no solo 3 users logeando |
| GTM vacío | CMO ↔ Chief of Staff | CMO ejecuta 3 tracks desde Semana 1, no después del lanzamiento |
| Pattern sin síntomas | CPO ↔ CTO | Nudge push notification si 2 días sin symptom entry |
| PDF es el producto real | Founder ↔ CDO | PDF tiene prioridad igual o mayor que UI de la app |
| 4 semanas con 1 developer | CTO ↔ todos | Check-in de riesgo al final de cada semana; si Semana 1 no cumple milestone, recalibramos |

---

## VEREDICTO FINAL

### SE MANTIENE ✅

| Elemento | Agente |
|----------|--------|
| Core value prop: proactive alert + clinical PDF | CPO |
| One-liner de posicionamiento | CMO |
| Posicionamiento top-right | CMO |
| Stack: React Native, FastAPI, Supabase EU, GPT-4o benchmark-first | CTO |
| Pattern algorithm: ≥3 días, ≥60% correlación, ≥2 entradas sintomáticas | CTO |
| Multi-tenancy (hcp_links) en data model | CTO |
| Regulatory framing | Founder + CPO |
| Monetización: gratis pacientes, suscripción HCP en V1.5 | CPO + CMO |
| Eating disorder contraindication screen | CPO + CDO |
| Delayed check-in 2h/4h (basic) | CDO + CTO |
| Segmento F: prior diagnosis field → PDF header | CPO + CDO |
| Los 5 flows principales (1-5) completos | CDO |

### SE CAMBIA ✏️

| Elemento | Cambio | Agente |
|----------|--------|--------|
| Definición de éxito beta | 3 users → 10 users + 1 HCP con feedback real | Founder + CPO |
| Flow 6 — Trigger Alert Detail | Pantalla completa → tabla de números | CDO |
| PDF summary | Bar chart SVG → tabla de texto | CDO + CTO |
| Pattern nudge | Añadir push si usuario no añade síntomas tras 2 días | CPO + CTO |
| GTM | Sin plan → 3 tracks desde Semana 1 | CMO |
| Benchmark modelo | GPT-4o solo → GPT-4o + GPT-4.5 + Gemini 2.5 Pro | CTO |
| Plan de ejecución | 6 semanas → 4 semanas | CTO |
| HCP loop en beta | No existía → HCP PDF share link (Semana 4) | CTO |

### SE CORTA ❌

| Elemento | Razón |
|----------|-------|
| GitHub Actions CI | 10 usuarios beta no lo necesitan |
| structlog + observabilidad completa | print() suficiente para private beta |
| APScheduler retry logic | Basic send suficiente |
| Flow 6 timeline chart | Sustituido por tabla |
| PDF bar chart SVG | Sustituido por tabla de texto |
| Rate limiting en API | No aplica a 10-15 users |
| Confidence indicator UI (Segmento D) | Data model lo soporta; UI en V1.1 |
| Segmento C/D/E — optimizaciones específicas | V1.1 |
| Custom date range PDF | V1.1 |

---

## PLAN REVISADO — 4 SEMANAS

### Semana 1 — Foundation + Auth + Onboarding + GTM start

**Build:** FastAPI skeleton, Supabase setup completo (schema incluyendo hcp_links), Railway deploy. Auth: email + Apple SSO + Google SSO. Onboarding completo (Flows 1.1–1.7) + campo prior diagnosis (Segmento F). Photo upload → Supabase Storage. `POST /meals`, `POST /meals/{id}/save` (basic).

**GTM:** Post Reddit en r/ibs y r/FODMAP. LinkedIn Post 1. Identificar 10 HCPs target.

**Milestone check-in:** ¿Backend deployed y onboarding funcional en device? Si no → escalar y recalibrar.

**Milestone:** Usuario puede crear cuenta, completar onboarding, hacer upload de foto con meal entry en DB.

---

### Semana 2 — AI Core + Pattern Engine

**Build:** `POST /meals/{id}/detect` (GPT-4o structured output). Benchmark de modelos (50 fotos, 2-3 horas). `POST /meals/{id}/voice` (Whisper). Pattern engine (SQL query completo). `GET /patterns` + `GET /trigger-alert`. `PUT /meals/{id}/ingredients`. Screens 2.2, 2.3 State A y B.

**GTM:** DM a 5 HCPs target. Onboard manualmente primeros 3-5 beta users.

**Milestone:** Foto → detección < 5s → lista editable → alert si pattern.

---

### Semana 3 — Meal Log Completo + Notifications + Pattern View

**Build:** Screens 2.4 (voice), 2.5 (confirmación + day counter). Notification scheduler APScheduler basic (2h/4h). Screen 3.1 (symptom check-in). Nudge de síntomas (push si 2 días sin symptom entry). My Log Tab completo: Screens 4.1, 4.2, 4.3. Screen 6.1 simplificada (tabla de números).

**GTM:** 5-7 beta users activos. Primera llamada/DM de feedback. Revisión PDF con HCP si posible.

**Milestone:** Flow 2 completo. Pattern card aparece a 3 días. Notificación llega a las 2h.

---

### Semana 4 — PDF + HCP Loop + Private Beta

**Build (días 1-3):** WeasyPrint template clínico completo (header, tabla patrones, log diario, disclaimer). Screens 5.1 y 5.2. `POST /export/pdf` + signed URL + cleanup job.

**Build (días 4-5):** HCP PDF share link (`GET /share/pdf/{share_token}`). Error states críticos. `DELETE /account` (GDPR). Expo EAS: TestFlight + Android internal track.

**GTM:** 10+ beta users activos. PDF share link enviado a 3-5 HCPs con mensaje de feedback. LinkedIn Post 4: "Beta live. Aquí está el PDF que genera Nutrace."

**Milestone de negocio:** ≥1 HCP da feedback cualitativo positivo sobre el PDF. ≥3 PDFs generados y compartidos por usuarios beta reales.

---

## MÉTRICAS DE ÉXITO — VERSIÓN FINAL

| Métrica | Target | Tipo |
|---------|--------|------|
| D7 retention (beta users) | ≥ 40% | Producto |
| Meals logged per active user/day | ≥ 1.5 | Producto |
| AI correction rate | ≤ 30% | AI quality |
| GPT Vision p95 latency | < 5s | Técnico |
| Pattern card fired (% users con ≥3 días) | ≥ 80% | Retención |
| PDFs generados y compartidos | ≥ 3 | Negocio |
| HCP feedback positivo cualitativo | ≥ 1 | Negocio — GO/NO-GO V1.5 |
| Beta users activos Semana 4 | ≥ 10 | GTM |

---

## CHIEF OF STAFF — Cierre

El plan es más robusto. Los recortes son de complejidad técnica, no de valor. Lo que cambia:

1. Definición de éxito de negocio, no solo de producto
2. GTM que empieza en Semana 1, no en Semana 5
3. Loop con HCPs desde la beta — que es el canal de crecimiento real
4. Scope honesto: 4 semanas, features esenciales primero

**La única cosa que el Founder necesita ver al final de Semana 4:**
> *Un HCP real ha leído un PDF de un usuario beta real y ha dicho — en cualquier forma — que lo recomendaría a sus pacientes.*

**Próximo paso:** CTO arranca Semana 1 en la próxima sesión.

---

*Prepared by: All agents, coordinated by Chief of Staff.*
*Date: 2026-03-03 · Session 006*
