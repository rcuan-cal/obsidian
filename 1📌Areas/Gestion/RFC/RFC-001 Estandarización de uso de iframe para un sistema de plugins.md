# Estandarización del Uso de `iframe` para un Sistema de Extensiones (Plugins)

- Autores:  - [[Flavio Sánchez|Flavio]] @fsanchezcalteks

## 1. TL;DR

Se propone la adopción de `<iframe>` como el mecanismo estándar para la integración de extensiones (plugins) de primera y tercera parte en nuestra plataforma. Este sistema permitirá añadir nuevas funcionalidades y personalizar la interfaz de usuario sin modificar el código base de la aplicación principal. Se definirá una API de comunicación basada en `postMessage` para que los plugins puedan renderizar componentes de UI en áreas predefinidas y persistir datos de forma segura y estructurada.

## 2. Motivación

La necesidad de evolucionar nuestra plataforma y adaptarla a casos de uso específicos ha crecido significativamente. Actualmente, cualquier personalización o nueva funcionalidad requiere una intervención directa en el código base, lo cual es lento, costoso y riesgoso. Esta propuesta busca resolver tres objetivos clave:

1. **Permitir Interfaces de Usuario Personalizadas:** Otorgar a los desarrolladores (internos y externos) la capacidad de crear vistas y componentes a medida que se integren de forma nativa en la experiencia de usuario.
    
2. **Habilitar un Ecosistema de Terceros:** Abrir la puerta a que desarrolladores externos puedan construir y ofrecer extensiones, enriqueciendo nuestra plataforma sin desviar recursos de nuestro _core business_.
    
3. **Facilitar el Desarrollo Interno:** Permitir a nuestros propios equipos desarrollar nuevas funcionalidades como "plugins", desacoplando su ciclo de vida del de la aplicación principal y fomentando la modularidad.
    

El uso de `<iframe>` ofrece un _sandbox_ de seguridad robusto, aislando el entorno del plugin del de la aplicación anfitriona, lo cual es fundamental para mitigar riesgos de seguridad.

## 3. Propuesta de implementación

El núcleo de la propuesta es utilizar un `<iframe>` para cargar el contenido del plugin. La aplicación anfitriona y el plugin se comunicarán de forma asíncrona a través de la API `Window.postMessage()`. Esto asegura un acoplamiento bajo y un contrato de comunicación explícito.

### 3.1. Arquitectura General

El flujo de trabajo será el siguiente:

1. La aplicación anfitriona determina qué plugins deben cargarse en la vista actual.
    
2. Para cada plugin, la aplicación renderiza un `<iframe>` apuntando a la URL del `index.html` del plugin.
    
3. Una vez cargado, el plugin inicia un "handshake" con la aplicación anfitriona para establecer un canal de comunicación seguro.
    
4. A partir de ese momento, toda la interacción (eventos, solicitudes de datos, renderizado de UI) se realiza mediante mensajes.
    

```
+---------------------------------+
|      Aplicación Anfitriona      |
|                                 |
|      +---------------------+    |
|      |       <iframe>      |    |
|      |                     |    |
|      | Contenido del Plugin|    |
|      | (HTML, JS, CSS)     |    |
|      |                     |    |
|      +---------------------+    |
|                                 |
+---------------------------------+
      ^             |
      | postMessage |
      v             |
+---------------------------------+
|      API de Comunicación        |
+---------------------------------+
```

### 3.2. Puntos de Extensión (Display Areas)

Los plugins podrán solicitar ser mostrados en distintas áreas predefinidas de la interfaz. La aplicación anfitriona será responsable de gestionar el renderizado y ciclo de vida de estas vistas.

- **Página Completa (`Page`):** El plugin ocupa el área de contenido principal.
- **Ventana Modal (`Modal`):** El plugin se renderiza dentro de una ventana modal superpuesta.
- **Elemento Emergente (`Popup`):** Ideal para acciones contextuales, renderizado cerca del elemento que lo invocó.
- **Panel Lateral (`Panel`):** El plugin se muestra en un panel lateral persistente.

### 3.3. API de Integración de UI

Para evitar inconsistencias visuales y dar control a la aplicación anfitriona, los plugins no modificarán el DOM directamente. En su lugar, enviarán mensajes solicitando el renderizado de componentes de UI predefinidos en ubicaciones específicas (hooks).

**Ejemplo de mensaje desde el Plugin:**

```JavaScript
// Desde el código del plugin dentro del iframe
window.parent.postMessage({
  type: 'ui.render',
  payload: {
    component: 'Button',
    location: 'Card.header', // Hook predefinido
    props: {
      label: 'Archivar Tarea',
      icon: 'archive',
      actionId: 'archive-card-123' // ID para recibir el evento de clic
    }
  }
}, 'https://url-de-la-app-anfitriona.com');
```

**Componentes Soportados:** `Button`, `Badge`, `Select`, `MenuItem`, etc. **Hooks Soportados:** `Column-header`, `Board-nav`, `Card.header`, `Card.details`, etc.

### 3.4. API de Persistencia de Datos

Los plugins necesitarán almacenar estado. Para ello, se ofrecerá una API de almacenamiento tipo `clave:valor` que persistirá los datos en el backend de la aplicación anfitriona, asociados a la instalación del plugin.

La estructura de la clave será jerárquica y forzada por la API para mantener el orden y evitar colisiones.

**Estructura de la Clave:**

1. `clavePredefinida`: Un namespace general (ej. `settings`, `userData`, `cache`).
2. `idElemento` (opcional): El ID del objeto al que se asocian los datos (ej. el ID de una tarjeta o tablero).
3. `scope`: El alcance del dato (`user` o `organization`).
4. `nombreDato`: El nombre específico del dato (con un límite de caracteres, ej. 64).

**Ejemplo de Guardado (desde el Plugin):**

```JavaScript
// Desde el código del plugin
window.parent.postMessage({
  type: 'data.set',
  payload: {
    key: {
      predefinedKey: 'settings',
      elementId: 'card-xyz-123',
      scope: 'user',
      dataName: 'isCollapsed'
    },
    value: true // El valor puede ser cualquier tipo serializable a JSON
  }
}, 'https://url-de-la-app-anfitriona.com');
```

**Ejemplo de Lectura (desde el Plugin):**

JavaScript

```
// El plugin envía una solicitud de lectura
window.parent.postMessage({
  type: 'data.get',
  payload: {
    key: { ... },
    requestId: 'get-collapse-state-456' // ID para correlacionar la respuesta
  }
}, 'https://url-de-la-app-anfitriona.com');

// La aplicación anfitriona responderá con un mensaje
// { type: 'data.get.response', payload: { requestId: '...', value: true } }
```

## 4. Métricas

Para evaluar el éxito y el impacto de esta implementación, se monitorearán las siguientes métricas:

- **Rendimiento:**
    
    - Tiempo de carga de los `<iframe>` de los plugins.
        
    - Latencia de las llamadas a la API `postMessage` (ida y vuelta).
        
    - Uso de memoria y CPU por parte de los plugins.
        
- **Adopción y Uso:**
    
    - Número de plugins activos por usuario/organización.
        
    - Frecuencia de uso de los puntos de extensión (qué `hooks` son los más utilizados).
        
    - Volumen de datos almacenados a través de la API de persistencia.
        
- **Salud del Sistema:**
    
    - Tasa de errores en la comunicación `postMessage`.
        
    - Errores de ejecución dentro de los `<iframe>` de los plugins.
        

## 5. Riesgos e Inconvenientes

- **Seguridad:** A pesar del sandboxing del `<iframe>`, existe el riesgo de que un plugin malicioso intente ataques de _phishing_ o ingeniería social. Es crucial validar el origen (`origin`) en todos los `postMessage` y utilizar el atributo `sandbox` en el `<iframe>` para restringir permisos.
    
- **Rendimiento:** Un número elevado de plugins o plugins mal optimizados pueden degradar significativamente el rendimiento de la aplicación principal. Se deben establecer límites en el consumo de recursos.
    
- **Experiencia de Usuario (UX):** La calidad y el diseño de los plugins de terceros pueden ser inconsistentes con nuestra aplicación, generando una experiencia fragmentada. Será necesario publicar guías de estilo y buenas prácticas.
    
- **Complejidad de Depuración:** Depurar la comunicación entre la ventana principal y un `<iframe>` puede ser complejo. Se necesitarán herramientas y documentación adecuadas para los desarrolladores.
    

## 6. Alternativas

- **Inyección Directa de Componentes/Scripts:** Implicaría cargar el código JavaScript de los plugins directamente en el contexto de la aplicación principal.
    
    - **Ventajas:** Integración más profunda y potencialmente mayor rendimiento.
        
    - **Desventajas:** Riesgo de seguridad catastrófico (acceso total al DOM y a los datos del usuario), conflictos de dependencias y estilos, y mayor fragilidad ante cambios en la aplicación anfitriona. Se descarta por motivos de seguridad y estabilidad.
        
- **Web Components:** Utilizar componentes web encapsulados.
    
    - **Ventajas:** Estandarización y encapsulación de estilos (Shadow DOM).
        
    - **Desventajas:** No proporciona el mismo nivel de aislamiento de seguridad que un `<iframe>`. El código se sigue ejecutando en el mismo hilo y contexto que la aplicación principal.
        

El enfoque de `<iframe>` ofrece el mejor equilibrio entre flexibilidad, aislamiento de seguridad y control.

## 7. Impacto potencial y dependencias

- **Sistemas Afectados:**
    
    - **Frontend:** Será el principal afectado, requiriendo la implementación del gestor de `<iframe>` y la API `postMessage`.
        
    - **Backend:** Necesitará un nuevo servicio para gestionar el almacenamiento de datos de los plugins y un registro de los plugins instalados.
        
- **Consideraciones de Seguridad:**
    
    - Se debe implementar una estricta Política de Seguridad de Contenidos (CSP) para limitar lo que los `<iframe>` pueden hacer.
        
    - El atributo `sandbox` del `<iframe>` debe configurarse con los mínimos privilegios necesarios.
        
    - La validación del origen del `postMessage` es obligatoria en ambas direcciones (anfitrión y plugin).
        
- **Impacto en Soporte al Cliente:**
    
    - Será necesario definir una política clara sobre el soporte a problemas originados por plugins de terceros. El equipo de soporte deberá poder identificar si un error proviene de la plataforma o de una extensión.
        

## 8. Preguntas sin resolver

- ¿Cuál será el proceso de revisión y publicación para los plugins de terceros?
    
- ¿Cómo se gestionará el versionado de la API de plugins para evitar romper la compatibilidad?
    
- ¿Se impondrán límites de uso (rate limiting) a la API de datos? ¿Cuáles serán los límites de almacenamiento por plugin?
    
- ¿Cómo manejarán los plugins la autenticación y autorización para realizar acciones en nombre del usuario?
    

## 9. Conclusión

La estandarización del uso de `<iframe>` para un sistema de extensiones es una solución robusta y segura que nos permitirá escalar la funcionalidad de nuestra plataforma de manera controlada. Aunque presenta desafíos en términos de rendimiento y experiencia de usuario, los beneficios del aislamiento de seguridad y la capacidad de crear un ecosistema de desarrolladores superan con creces los riesgos. Esta propuesta sienta las bases para un futuro más modular, flexible y extensible.

---

## Ver más
- [[RFC]]
