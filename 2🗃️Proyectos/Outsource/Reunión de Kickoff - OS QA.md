
## Sobre el proyecto

- **Objetivo**:
	- 
- **Alcance**:
	- 
- **Entender el proyecto**
	- 
- **Listado de API de interés y a lista de recursos buscado**
	- 

## Acuerdos del proyecto

- **Criterio de aceptación para los test.**
	- _Cuáles son los estándares de calidad que debe cumplir la aplicación?_
	- 
- **Entregables del proyecto**
	- 

## Solicitudes

- **Credenciales de los ambientes de QA**
	- _Duración de que nos creen los accesos al ambiente_
	- 
- **Documentación que describa cómo debe de funcionar la app**
	- _Plan de pruebas, casos de prueba, reportes de bugs, informe de resultados final_
- 


---

1. Objective of the presentation is to clarify key questions of the tests.
2. Check the type of tests requested for each ticket
	1. If automated tests are requested, request access to their existing test projects
3. Check if they have existing test documentation to follow their standards
4. Request test users
	1. Two roles: One Admin and One Normal

---

ASIF - Tech Lead.
Anima - Designer - Product designer 


Good morning, everyone. Thank you for joining. We're excited to start the QA process for Nimble 2's Sprint 22. My name is Ricardo Cuan, Senior developer at Calteks from Panama. Our goal today is to clarify key questions of the tests to align times and activities.



Based on the Scope of Work document, we understand the primary goal of this sprint is to deliver a more secure, insightful, and performant Nimble 2 platform. 
- We've broken this down into three main pillars: 
	1. first, tightening security by fixing permissions for the Member role; 
	2. second, enhancing business intelligence by integrating Kronos hours into the metrics view
	3. Third, delivering a significantly better user experience through critical performance upgrades. 
1. One focus for each jira ticket

Alright.

Next, The document states "No automation is planned." Our previous experience often includes API-level automation to accelerate regression testing. 

**To align, we'd like to ask:** For Sprint 22, should we focus on a 100% manual testing approach, or is there an opportunity for targeted automation to improve efficiency and long-term stability?

**To ensure an efficient start, we need to clarify:**

- **Test Environment:** So, what I understand, we should use a test environment. Can you confirm access details for a stable QA environment that mirrors production? Who is our technical point of contact for environment issues?
- **Test Users:** We will require users with different permission levels (specifically 'Member' and 'Member+'). Will QA be provided with these, or can we create them? 
- **Test Data (for APP-492):** Who will be responsible for populating the test environment with the necessary Kronos and Nimble work hours data?

Types of tests:
- Manual QA
- Automate QA

- Manual QA - require end to end 
	- All Automated.
	- UI Component automated
	- WIM Pipeline
	- All entry point
	- Performance test

- This Sprint
	- To automate the first portion is the middleware
		- They have a lot of band width
		- Better is the manual is taking out so they can make QA Automate
	- Frontend (not jet)
- Nimble
	- Anteriormente querían que el equipo hiciera la parte manual y esta parte se pasa por detrás.
	- 

- Bitbucket 
- Resources app sources

- Two request: 
	- Request the user account:
		- name and last name
		- contact information
		- email
		- phone number
		- one year, and then renew process
		- it take 3 to 4 days to be created (it stay)
		- email to clain the account and then get the account
		- id logging to all resources
		- after is claimed it will have access 
- Access to jira software

- Good coverage
- Good Deployment 
- Golden middleware branch (moving target)
- Cuando vayan añadiendo funcionalidad, se van moviendo hasta que haga merge


And to be clear, who from our team have an account right now? 

Ricardo Cuan
rcuan@calteks.com
+50763781321
