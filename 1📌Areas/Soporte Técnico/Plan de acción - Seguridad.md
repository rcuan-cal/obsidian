# Plan de Acción de Seguridad Integral para Equipos de Tecnología

Este documento presenta un plan de acción unificado para integrar la seguridad en todas las fases del ciclo de vida del desarrollo de software (SSDLC) y en la cultura del equipo.

### Fase 0: Políticas Generales de Seguridad Física y de Equipos

Estas políticas son fundamentales para la seguridad general, aunque no se enmarcan directamente en una fase específica del ciclo de vida del desarrollo de software.

- **Política:** `El equipo proporcionado (Laptop) debe estar únicamente en un lugar seguro`
- **Política:** `El equipo proporcionado (Laptop) debe usarse únicamente para fines laborales`
- **Política:** `Política de Escritorio Limpio`

## Fase 1: Cultura, Capacitación y Procesos Fundamentales

El primer paso es establecer una base sólida donde la seguridad sea una responsabilidad compartida y existan procesos claros.

1. **Fomentar una Cultura de Seguridad:**
    - **Acción:** Promover la mentalidad de que la seguridad es una responsabilidad de todos, no solo de un rol específico.
    - **Métrica:** Incluir objetivos de seguridad en las evaluaciones de desempeño del equipo.
2. **Capacitación Continua:**
    - **Acción:** Implementar un programa de capacitación anual obligatorio para todo el personal de desarrollo sobre prácticas de codificación segura, diseño seguro y las últimas amenazas relevantes para las tecnologías utilizadas.
    - **Métrica:** Tasa de finalización del 100% en la capacitación anual.
3. **Establecer y Documentar un SSDLC (Ciclo de Vida de Desarrollo Seguro):**
    - **Acción:** Crear, documentar y formalizar un proceso de desarrollo que integre puntos de control de seguridad en cada fase (diseño, desarrollo, pruebas, despliegue).
    - **Acción:** Revisar y actualizar la documentación del SSDLC anualmente o tras cambios significativos en tecnologías o procesos.
    - **Métrica:** Documentación del SSDLC publicada y accesible para todo el equipo.

- **Política**: `Capacitar a los Desarrolladores en Conceptos de Seguridad de Aplicaciones y Codificación Segura`
- **Política**: `Establecer y Mantener un Proceso de Desarrollo Seguro de Aplicaciones`

## Fase 2: Diseño y Arquitectura Segura (Prevención Temprana)

Identificar y mitigar riesgos antes de escribir la primera línea de código.

1. **Modelado de Amenazas:**
    - **Acción:** Integrar el modelado de amenazas como un paso obligatorio en la fase de diseño de nuevas funcionalidades o aplicaciones críticas.
    - **Acción:** Identificar y documentar posibles riesgos, vectores de ataque y contramedidas.
    - **Métrica:** Existencia de un modelo de amenazas para todos los proyectos nuevos.
2. **Aplicar Principios de Diseño Seguro:**
    - **Acción:** Diseñar arquitecturas basadas en el principio de **mínimo privilegio**.
    - **Acción:** Planificar la **reducción de la superficie de ataque** (desactivar servicios, puertos y funciones innecesarias).
    - **Acción:** Definir y validar estrictamente todas las entradas de datos del sistema.
    - **Métrica:** Revisiones de arquitectura que verifiquen la aplicación de estos principios.

- **Política:** `Aplicar Principios de Diseño Seguro en las Arquitecturas de Aplicaciones`
- **Política:** `Realizar Modelado de Amenazas`

## Fase 3: Desarrollo y Codificación Segura

Construir seguridad directamente en el código y las dependencias.

1. **Estándares de Codificación Segura:**
    - **Acción:** Definir y mantener estándares de codificación segura para los lenguajes y frameworks utilizados.
    - **Métrica:** Adopción de linters y herramientas de análisis de código configuradas con reglas de seguridad.
2. **Gestión de Componentes de Terceros (Cadena de Suministro de Software):**
    - **Acción:** Crear y mantener un inventario de software actualizado (SBOM - Software Bill of Materials) para todos los proyectos.
    - **Acción:** Implementar herramientas automatizadas para escanear dependencias en busca de vulnerabilidades conocidas.
    - **Acción:** Establecer una política para usar componentes solo de fuentes confiables y mantenerlos actualizados.
    - **Métrica:** Reducción del número de vulnerabilidades críticas/altas en dependencias de terceros.
3. **Uso de Módulos de Seguridad Verificados:**
    - **Acción:** Priorizar el uso de servicios y librerías estándar y auditadas para funciones críticas como autenticación, gestión de sesiones, cifrado y logging.
    - **Métrica:** Cero implementaciones "caseras" de algoritmos criptográficos o de autenticación.

- **Política:** `Establecer y Gestionar un Inventario de Componentes de Software de Terceros`
- **Política:** `Utilizar Componentes de Software de Terceros Actualizados y de Confianza`
- **Política:** `Aprovechar Módulos o Servicios Verificados para los Componentes de Seguridad de las Aplicaciones`

## Fase 4: Pruebas y Verificación de Seguridad

Validar que las aplicaciones son robustas frente a ataques.

1. **Análisis Automatizado de Código (SAST y DAST):**
    - **Acción:** Integrar herramientas de Análisis de Seguridad de Código Estático (SAST) y Dinámico (DAST) en los pipelines de Integración Continua (CI/CD).
    - **Métrica:** Bloqueo automático de compilaciones (builds) que introduzcan nuevas vulnerabilidades críticas.
2. **Pruebas de Penetración:**
    - **Acción:** Realizar pruebas de penetración periódicas (internas o externas) en aplicaciones de alto riesgo o expuestas a internet.
    - **Métrica:** Reportes de pruebas de penetración con planes de remediación definidos.

- **Política:** `Implementar Verificaciones de Seguridad a Nivel de Código`
- **Política:** `Realizar Pruebas de Penetración de Aplicaciones`

## Fase 5: Despliegue y Operaciones Seguras

Asegurar la infraestructura y los entornos donde se ejecutan las aplicaciones.

1. **Fortalecimiento de la Infraestructura (Hardening):**
    - **Acción:** Utilizar plantillas de configuración seguras y estandarizadas (hardening) para servidores, contenedores, bases de datos y servicios en la nube (PaaS/SaaS).
    - **Métrica:** Auditorías periódicas de configuración de la infraestructura.
2. **Separación Estricta de Entornos:**
    - **Acción:** Mantener una separación lógica y de red completa entre los entornos de producción y no producción (desarrollo, pruebas, staging).
    - **Métrica:** Cero incidentes de seguridad causados por la mezcla de datos o configuraciones entre entornos.

- **Política:** `Utilizar Plantillas de Configuración de Fortalecimiento (Hardening) Estándar para la Infraestructura de Aplicaciones`
- **Política:** `Separar los Sistemas de Producción y de No Producción`
- **Política:** `Reglas de Uso de la VPN`

## Fase 6: Gestión Continua de Vulnerabilidades

Responder y aprender de las vulnerabilidades descubiertas.

1. **Proceso de Gestión de Vulnerabilidades:**
    - **Acción:** Implementar un proceso formal para recibir, evaluar y remediar reportes de vulnerabilidades (internos y externos).
    - **Acción:** Utilizar un sistema de seguimiento con calificaciones de severidad (ej. CVSS) para priorizar la corrección.
    - **Métrica:** Definir y medir Acuerdos de Nivel de Servicio (SLAs) para la remediación de vulnerabilidades según su severidad (ej. Críticas < 15 días, Altas < 30 días).
        
2. **Análisis de Causa Raíz (RCA):**
    - **Acción:** Para vulnerabilidades de severidad alta o crítica, realizar un análisis de causa raíz para identificar y corregir el problema subyacente en los procesos o la formación, evitando su recurrencia.
    - **Métrica:** Documentos de RCA compartidos con el equipo de desarrollo.

- **Política:** `Establecer y Mantener un Proceso para Aceptar y Abordar las Vulnerabilidades del Software`
- **Política:** `Establecer y Mantener un Sistema de Calificación de Severidad y un Proceso para las Vulnerabilidades de las Aplicaciones`
- **Política:** `Realizar Análisis de Causa Raíz en las Vulnerabilidades de Seguridad`


---

## Ver más:
- Este pan de acción nace de las [[Políticas de seguridad]] dadas por el lídear de [[Soporte Técnico]] el señor [[Luis Gonzalez]] 

