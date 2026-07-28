# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary (mercado objetivo: Colombia - considera scaffoldear con `/add-portal` para búsqueda directa vía CLI):
- **elempleo.com** - uno de los portales de empleo más grandes de Colombia
- **linkedin.com/jobs** - LinkedIn job listings (filter: Colombia / Bogotá); ya cubierto por el CLI `linkedin-search`
- **computrabajo.com.co** - portal de empleo masivo en Colombia, fuerte en roles administrativos/operativos
- **magneto365.com** - portal de empleo colombiano, buena cobertura en salud y BPO

Secondary (páginas de carreras de empresas vía Google):
- Búsquedas directas en Google con filtros `site:` para EPS/IPS y empresas objetivo (ej. site:sura.com, site:compensar.com, site:nuevaeps.com.co)

## Query Categories

Queries are grouped by priority. Each query should be combined with your location terms (e.g. your city, region, or metro area) where the site supports it.

### Priority 1: Analista de Datos / BI

These match your strongest and most desired career direction.

```
site:elempleo.com "analista de datos" Bogotá
site:elempleo.com "analista Power BI" Bogotá
site:computrabajo.com.co "analista BI" OR "business intelligence" Bogotá
site:linkedin.com/jobs "analista de datos" Colombia
site:linkedin.com/jobs "Power BI" analista Colombia
```

### Priority 2: PQRS / Servicio al cliente en salud

These match your domain expertise.

```
site:elempleo.com "analista de PQRS" Bogotá OR Colombia
site:computrabajo.com.co "analista PQRS" salud Bogotá
site:magneto365.com PQRS salud Bogotá
site:linkedin.com/jobs "PQRS" salud Colombia
```

### Priority 3: Roles adyacentes (coordinación / calidad / auditoría en salud)

Adjacent roles you could pivot into.

```
site:elempleo.com "coordinador PQRS" Power BI Bogotá
site:elempleo.com "analista de calidad" salud Bogotá
site:computrabajo.com.co "auditor en salud" Bogotá
```

### Priority 4: Analista de Requerimientos / Business Analyst

Wider net for general analyst/business roles.

```
site:elempleo.com "analista de requerimientos" Bogotá
site:linkedin.com/jobs "business analyst" Excel Power BI Colombia
site:computrabajo.com.co "analista de procesos" Bogotá
```

## Location Filter

When evaluating results, verify the job location is within reasonable commute distance from your home. Define acceptable areas:
- Bogotá y área metropolitana
- Remoto (Colombia o LatAm) - siempre PASS independientemente de la ciudad
- Cundinamarca cercana (ej. Chía, Soacha, Fusagasugá) - aceptable si es híbrido con pocos días presenciales
- Otras ciudades de Colombia con reubicación - solo si la oferta la financia o es explícitamente atractiva
- Fuera de Colombia sin modalidad remota - descartar (nivel de inglés aún básico + sin plan de reubicación confirmado)

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
