---
tags:
  - Proyecto
---


## Especificaciones a implementar

```md
# Nimble 2 - Sprint 22 Scope of Work

- **Sprint Duration**: September 15 – October 30, 2025
- **Target Release**: October 30, 2025 (Production Go-Live)
- **Beta Releases**: Incremental releases planned prior to Production (dates TBD).
- **Bug Fix Policy**: Critical bugs identified in Beta or Production will be resolved and released
outside of the sprint cycle. These require proactive QA retesting as insurance, in addition to
internal developer validation and limited user confirmation.


## 1. Sprint Overview

The goal of Sprint 22 is to improve the **Nimble 2 platform** through performance enhancements,
production metrics improvements, and permission fixes. QA will be responsible for verifying
functionality, validating performance outcomes, and ensuring no regressions are introduced.
Full details are outlined within each Jira Issue (Description).

## 2. Scope of Work by Jira Ticket

### APP-493 (Bug) – Member Role Permissions on Work Requests

- **Summary:** Remove the ability for the Member role to import Work Requests via CSV.
- **Expected Behavior:**
    - Members can no longer import Work Requests via CSV.
    - Adding new Work Requests directly remains restricted to Member+ and above.
- **QA Focus:**
    - Confirm that CSV import option is no longer available for the Member role.
    - Verify that Member+ and higher retain ability to add Work Requests.
    - **Regression:** Ensure other Member role permissions are unchanged.

### APP-492 (Task) – Nimble 2 Production Metrics Work Hours

- **Summary:** Introduce side-by-side visibility of Kronos hours and Work hours for
Engineering production metrics.
- Test Data Setup:
    - Create sample users with known Kronos hours (e.g., 8h).
    - Log corresponding work hours in Nimble 2 (e.g., 2h Task A, 6h Task B).
    - Include mismatched values (e.g., Kronos 8h vs. Nimble 7.5h).
- **QA Focus:**
    - Visibility: Both Kronos and Work hours display correctly side by side.
    - Accuracy: Values match source data; decimals/rounding are consistent.
    - Filtering/Segmentation: Filters (cost center, project, user) preserve both columns
and update correctly.
    - Edge Cases:
        - No Kronos hours available → work hours display, Kronos empty.
        - Kronos hours but no work hours logged → correct zero/null handling.
        - Multi-day / split-shift entries aggregate correctly.
    - Rollups: Totals align at project/team aggregation levels.
- **Regression:** Ensure no double-counting when summing multiple tasks.

### APP-491 (Task) – Nimble 2 Performance Enhancements

- **Summary:** Improve data refresh performance and end-user load times through
infrastructure migration and incremental refresh logic.
- Phase 1 – Infrastructure & Pipeline (Validation):
    - Migrate workloads to GCP CloudRun + MongoDB (same region).
    - Benchmark pipeline refresh times before/after migration.
    - Validate reduced latency, improved stability, and simplified architecture.
    - **QA Focus:**
        - Confirm environment spins up successfully in GCP.
        - Validate data pipeline refresh times decrease (~15 min → ~2 min).
        - Verify no data loss, corruption, or inconsistency.
- Phase 2 – Application Retrieval Improvements:
    - Introduce `LastUpdateDateTime` for incremental refresh.
    - Implement caching to support rapid data availability.
    - **QA Focus:**
        - Validate incremental updates process only new/modified records.
        - Confirm application loads near-instantly after new data is available.
        - Validate correct handling of cached data (no stale data served).
- **Regression:** Ensure functionality is unchanged for existing data flows.

## 3. Out of Scope

- Features or modules outside of APP-491, APP-492, APP-493, unless instructed
otherwise (Bugs).

## 4. Risks & Assumptions

- Incremental Beta release dates TBD; QA may need to test multiple drops before Oct 30.
- Critical bug fixes outside sprint scope may divert QA resources.
- Performance improvements dependent on successful GCP migration and infrastructure stability

```


## Recursos y Equipo

Conocer los recursos humanos y materiales disponibles es fundamental para una planificación realista.

- **Equipo de QA Asignado:**
    - **Roles y Responsabilidades:** 
	    - [[Ronoaldo Lasso]] y [[Ricardo Cuan]] Gestores del proyecto
	    - [[Didiel Saenz]] Experto en QA. 
	    - [[Jairo Cespedes]] QA jr.
	    - [[Miguel Lombardi]] QA jr.
    - **Nivel de Experiencia:** 
	    - Didiel tiene alta experiencia en QA
	    - Jairo y Miguel no tiene experiencia en QA.
    - **Disponibilidad:** 
	    - Es una dedicación de 8 días a la semana de lunes a viernes.
- **Equipo de Desarrollo:** 
	- Líder técnico: Ricardo
	- QA: Didiel, Jairo, Miguel
- **Herramientas Disponibles:**
    - **Gestión de Proyectos y Casos de Prueba:**
	    - Uso de Jira para seguimiento
	    - Uso de herramientas dadas por el cliente
    - **Herramientas de Automatización (si aplica):** _Si se planea automatizar, ¿qué herramientas se utilizarán? (Ej: Cypress, Playwright, Jest, React Testing Library)._
	    - No se planea automatizar
    - **Navegadores y Dispositivos:** Lista de navegadores (Chrome, Firefox, Safari, Edge) y dispositivos (móviles, tabletas, resoluciones de pantalla) en los que se debe garantizar el correcto funcionamiento.
		- Chrome
		- Firefox
		- Safari


## Anteriormente se ha trabajado en un proyecto similar y se ha seguido el siguiente esquema

Levantamiento de requisitos

Ejemplo:
- Proyecto de Nimble:
	- Lista de tareas con el flujo a analizar

Procedimiento:
- Revisión de casos de prueba
- Revisión de entornos de prueba
- Análisis y planificación de pruebas

1. Revisión de pruebas automatizadas de API
2. Pruebas automatizadas de UI
3. Pruebas de Performance

- Gestión de defectos
- Documentación de Pruebas
- Ejecución de pruebas de regresión
- Integración CI/CD
	- Pruebas integradas con bitbucket / jetkins
- Generación de reportes

Utilizar xUnit y RestSharp

---

### Registro de tareas

Se tiene un flujo de Jira:
- Está por completar
- En progreso de QA
- Si necesita revisión
- Si está completado (QA Complete)

---

Se tiene un cronograma de activiades en la que se separa en 

- Planning
- Implementación
- Cierre

En la parte de implementación, cada ticket se vería estas tareas:
Pruebas Visuales (Definir Documento de Pasos de prueba)
Reporte al cliente (mover tarea en jira)
Análisis y Diseño de escenario para pruebas automatizadas
Implementación: Escribir las pruebas (Escenarios)
Ejecutar pruebas 
Reporte al cliente (mover tarea en jira)
Levantar reporte de pruebas
Integración de pruebas automáticas a su sistema
Prueba de regresión
Prueba de Rendimiento. Medición y comparación de tiempos
Reporte de Pruebas realizadas

Pero no se sabe si se debe de hacer implementación de pruebas automáticas. 

---

Se realizará una reunión con el cliente, qué preguntas deberíamos de hacerle para poder empezar con el proyecto?

Por el momento tenemos:

- Consultar tipo de pruebas solicitadas
	- En caso de pedir pruebas automatizadas solicitar acceso a sus proyectos de prueba existentes
- Consultar si cuentan con documento de prueba existente para seguir sus estándares
- Recordar solicitud de usuarios de prueba

Coméntanos más preguntas


[[Reunión de Kickoff - OS QA]] 