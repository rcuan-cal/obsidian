- Reunión para definir el despliegue de la [[Infraestructura]] con [[Ronoaldo Lasso|Ronoaldo]] 

Azure: [Pipelines - Recent](https://dev.azure.com/calteks-dev/CalEngs/_build)
AWS: https://us-east-2.console.aws.amazon.com/ecs/v2/clusters?region=us-east-2

- Container aps (azure) == elastic container (aws)
- 1 cluster = 1 proyecto
- 1 cluster = multiples servicios 

Caloop
- - task definitions = manifiesto
	- imagen
	- variable
	- capacidad
	- autoescalado
	- cantidad de contenedores


## Creación

Requisitos:
1. Docker. imagen de origen sea de la nube (azure, aws)
2. Multistage
3. buildspec-dev.yml

Build project: Caloop-api-dev
- En Operating System:
	- Amazon linux


## Pipelines

- Se crea


## Revisión de PR

1. Que me lo muestre en persona
2. Revisión de variable y lógica

1 PR = 1 Commit

Cuando PR se completa, enviar mensaje al teams.


## Caso Website

- Se tiene en un Amplify de AWS

1. github
2. Branch en específico
3. buildea solito
4. despliega solito

Los errores de build.

