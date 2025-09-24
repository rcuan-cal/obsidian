
# Definición de actividades

## Cambios a realizar:

1. Modificar el Expense en el Modulo TimeSheet
	1. Relación de Expense con Workspace, Project y task.
		1. Como Expense, Quiero tener relacionados los expenses con los wokrspaces, proyectos y task, para realizar agrupaciones y análisis más detallados.
	2. 
2. Autotracker thel expenses (historial de modificaciones/auditoría)
	1. Como usuario, Quiero saber las modificaciones de un expense, el cuando sucedió y por quién, Para tener mayor transparencia en las operaciones.
3. Selector box en Expenses
	1. Como usuario, Quiero modificar múltiples expenses al mismo tiempo, para minimizar el tiempo y aumentar la utilidad de la herramienta.
4. Employee Tab
	2. Billable Rate
	3. Title
	4. Email
	5. Office
	6. etc (realmente son más, pero las que les interesa son las anteriores).
	7. Information only seen by admin
5. Generation of ROI Report 
	1. Filters
		1. Search/Filter:
			1. Timesheets (date/All time)
			2. Invoices (dates/Number)
			3. By Employee
			4. Office
		2. 
6. Small fixes
	1. Change color priorities

## Propuesta de Flavio 

Modificar el expense en el modulo timesheet  
- Creacion y edición de registro de expense  
    * Debe poder recibir un id seller, categoria y metodo de pago, los 3 opcionales  
    * Validar la existencia de estas entidades si fueron provistas  
    * El expense tambien debe poder relacionarse con un workspace y un board del workspace, ambos opcionales pero no se puede relacionar con un board sin relacionarse con el workspace  
    * Validar la existencia de workspace y board si fueron provistos  
    * El caso de uso de editar debe permitir lo mismo pero todo opcional

Modificar modulo usuario  
- Creacion y edicion de usuario  
    * En la creacion debe recibir el country y officeId obligatoriamente, validar existencia de officeId  
- Crear endpoint nuevo (con permiso manage.users) para modificar el hourlyRate  
- Crear endpoint nuevo (con permiso manage.users) para modificar el country  
- Crear endpoint nuevo (con permiso manage.users) para modificar el officeId

Libreria para subida de archivos a S3  
- Crear una libreria que permita subir archivos a S3 y aplicarla en:  
    * Nuevo endpoint para subir avatar de usuario (modulo usuario)  
    * Modificar el create y edit expense para que permita subir un archivo adjunto al expense (modulo timesheet)  
    * Modificar el create y edit board para que permita subir un archivo adjunto al board (modulo board)

Crear modulo de registro de historial de cambios (audit log)  
- Registrar cambios en los modulos:  
    * Timesheet: para timesheet entries y expenses  
    * Kanban: para las tasks

El ROI no tengo idea de como hacerlo debemos analizar el Excel


---



# CONSTANTES

```typescript
export const PAGINATION_LIMIT = 10;
export const TAX_RATE = 1.15;

export const EARLY_PAYMENT_DISCOUNT = 0.0255;
export const SALARY_INTEREST_RATE = 0.03;
export const FUTURE_SAVINGS_RATE = 0.005;
export const ROSEVILLE_STARTUP_COST = 5_000;
```

# Deuda técnica
- Monthly Maintence
- Testing

