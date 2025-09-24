[[Flavio Sánchez|Flavio]] propone lo siguiente:

# PARA LOS PLUGGINS  

## Motivación
- Para UI mas personalizadas por el mismo dev utilizar iframes. 
- Incluir plugin a terceros.
- Nosotros ofrecer plugin como iframe.

## Propuesta
Pueden estar a distintos niveles:
  - Page
  - Modal
  - Pupup
  - Panel lateral

### Aplicación

Para elementos de UI sobre la misma aplicación ofrecer una API con hooks para renderizar elementos controlados y predefinidos sobre áreas de la interfaz también controladas y ya predefinidas  

#### Ejemplos:  
- Hooks para agregar: Buttons, Badges, Selects, etc.
	- Estos elementos se agregan sobre zonas ya predefinidas en hooks: Column-header, Board-nav, Card, etc.
* En la API ofrecer funciones para almacenar y recuperar data generada por los Pluggins, pero con ciertas limitaciones:
  - Guardar la data de los Pluggins en un JSON o base de datos de tipo `clave:valor`
  - Ofrecer un listado definido de claves en las que se puede guardar información, con la siguiente jerarquía:  
	  1. claves predefinidas 
	  2. ID de elemento (solo si lo requiere) 
	  3. scope del dato
	  4. nombre del dato (debe tener limite) 
	  5. valor del dato

---

## Ver más
- Dado esta conversación, se crea el [[RFC-001 Estandarización de uso de iframe para un sistema de plugins]] 