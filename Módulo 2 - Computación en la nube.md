
# Amazon Elastic Compute Cloud (EC2)

Son máquinas virtuales. 
* Es seguro.
* Modificable en capacidades. 
* Arranque de instancias de servidor en minutos.
* Pago sólo por el uso.

Las máquinas virtuales tienen:

* Coste por horas de procesamiento
* Coste por capacidad de disco duro
* Coste por consumo de ancho de banda hacia afuera de Amazon.


## Procedimiento de despliegue de máquina virtual

![[Pasted image 20240815175222.png]]

Lanzar la instancia a través de una imagen de una máquina virtual, que nos permite tener el sistema corriendo en minutos.

## Tipos de máquinas virtuales

Hay máquinas que van desde generalistas, para tener un monolito, hasta microservicios para tener una parte de nuestra aplicación.

* Propósito general: Para todo tipo de uso (p.e. Monolitos).
* Optimizado para procesar.
* Optimizado para memoria (p.e. SAP Hana - BBDD en RAM).
* Optimizado para aceleradores de gráficos.
* Optimizado para almacenamiento.

## Opciones de precios

* **On-Demand**: El precio más caro es bajo demanda (On-Demand). No tiene gastos por adelantado ni coste mínimo. Es ideal para cargas de trabajo cortas e irregulares.
* **Reserved**: Nos da un descuento respecto al precio On-Demand. Requiere de un compromiso de estancia de 1 a 3 años.
* **Spot**: Recursos ociosos que tiene *AWS*. Es ideal para cargas de trabajo con inicio y finalización flexibles. Nos ofrece un descuento sobre el precio On-Demand con descuentos de hasta el 90%.
* **Plan de ahorro de computación**: Se asemeja mucho a la reserva, pero se puede asignar a contenedores y no sólo a instancias EC2 como ocurre con la reserva. También requiere de un compromiso de estancia de 1 a 3 años.
* **Planes de tenencia o tenency**: Son los más caros. La máquina virtual se ejecuta en una máquina dedicada física con mis máquinas virtuales, o un alojamiento dedicado para mis máquinas virtuales. Son **Dedicated Instance** y **Dedicated Host** respectivamente.

## Escalabilidad Automática. Elasticidad en máquinas virtuales.

Podemos configurar nuestra instancia con Auto Scaling.
Este se configura estableciendo un valor mínimo de la instancia, un valor deseable de la instancia y un valor máximo para esta instancia que no se va a superar.

Si el auto scaling atiende clientes vamos a necesitar un balanceador de carga.

### El balanceador de carga (AWS Elastic Load Balancing)

Actúa para repartir la carga del servidor con sus dos roles:
* Distribuir el tráfico a través de múltiples recursos.
* Proveer de un punto único de contacto para tu grupo de auto escala.

### Trabajo en equipo: Combinación del balanceador con el grupo de auto escalado

![[Pasted image 20240815210537.png]]


Preguntas:

	¿Quien quita y agrega instancias?: Auto Scaling
	¿Quien distribuye la carga?: Elastic Load Balancing
	¿Quien se asegura de que no sea una única instancia EC2 la que tiene que cargar con la carga de trabajo?: Elastic Load Balancing
	¿Quien ajusta automáticamente el número de instancias EC2 para adaptarse a la demanda?: Auto Scaling
	¿Quién provee de un único punto de contacto para el tráfico?: Elastic Load Balancing

## Arquitectura de la aplicación


Aplicación Monolítica: Todos los componentes de mi aplicación se encuentra bajo el mismo servidor

Microservicios: Cada componente es independiente, tiene un servidor exclusivo para este componente. Contenerización. Los microservicios mejoran los costos. Permiten averiguar de donde viene el problema de manera más sencilla. Permiten las actualizaciones de cada componente por separado.

Para comunicar microservicios son necesarios **Servicios de Mensajería**
Uno muy conocido en On-Premises es Apache MQ, etc.

Amazón tiene dos servicios para las Notificaciones:

### Simple Notification Service

Se usa para gran variedad de cosas: Notificaciones por mail, Via Push para móviles, para web services, web hooks, SMS...

Permite distintos tipos de canales para distintos tipos de subscriptores.

### Simple Queue Service

Mandar, almacena y recibir mensajes ente componentes de software.
Pone en cola mensajes sin requerir a otros servicios estar disponibles.

Es comparable con un Apache MQ.

Nos permite desacoplamiento. Almacena una cola para cuando el servicio o instancia estén activos.


## Serverless Computing

Procesamiento sin servidores.

Nos permite centrarnos en el código de nuestra aplicación sin necesidad de preocuparse de los servidores y su sistema operativo.

El servicio principal de Serverless Computing es **Lambda** 

### Lambda

* Permite correr código sin provisionar o administrar servidores.
* Permite pagar sólo por tiempo de computación mientras que el código está corriendo.
* Permite usar otros servicios AWS para automatizar la activación del código.

Ciclo de uso:

Subir código a Lambda -> Fijar el código que dispara la función Lambda -> El código corre cuando se dispara -> Se paga sólo por el tiempo de computación.

El rendimiento es alto. Se puede disparar hasta 1000 veces de manera concurrente por región. No necesita auto escala.

## Servicio de Contenedores

A través de AWS podemos lanzar contenedores o incluso un clúster de contenedores.

El servicio de contenedores es: **Amazon Elastic Container Service (ECS)**
El servicio de clúster es: **Amazon Elastic Kubernetes Service (EKS)**

ECS es como un desarrollo propietario similar a Kubernetes de Amazon.


Estos sistemas tienen que correr al mismo tiempo en máquinas EC2.

**Si no queremos tener que lidiar con máquinas virtuales tenemos una opción de contenedores serverless: AWS Fargate

**AWS Fargate** nos permite correr contenedores serverless con Amazon ECS ó EKS











