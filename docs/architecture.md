# Arquitectura

Spring Tunes está desplegada en diversos componentes conformados por un frontend en Angular, un backend en Spring Boot, una base de datos PostgreSQL, y múltiples servicios administrados en AWS para autenticación, almacenamiento de archivos y escalabilidad.

La comunicación entre el cliente y los componentes AWS se realiza a través de una API Gateway, lo que permite centralizar el tráfico, aplicar reglas de seguridad y facilitar la integración de lambdas o servicios adicionales.

## ⚙️ Backend Service (Spring Boot)

El backend está construido con Spring Boot y se encarga de:

- Gestionar artistas, álbumes, pistas y playlists.
- Validar tokens de acceso generados por AWS Cognito.
- Conectarse a una base de datos PostgreSQL (en RDS o local, según el entorno).
- Proporcionar endpoints RESTful.
- Servir como capa central para la lógica del negocio y persistencia de datos.

El backend también define roles y contextos de seguridad adicionales, y delega la carga de archivos directamente a S3 utilizando URLs prefirmadas generadas por una Lambda.

## ☁️ AWS

Se han utilizado varios servicios de AWS para lograr una arquitectura serverless, segura y escalable:

### 🔐 Cognito

- Gestiona el registro, autenticación y autorización de usuarios.
- Emite tokens JWT que son validados por el backend.

### 🗂️ S3

- Almacena los archivos multimedia del sistema: avatares de artistas, carátulas, canciones, portadas de playlists.
- El acceso a los archivos se gestiona a través de URLs prefirmadas, garantizando seguridad y control.

### 🧠 Lambda

- Genera URLs prefirmadas para carga de archivos desde el frontend, evitando que el backend maneje archivos binarios.
- Permite delegar esta responsabilidad de forma segura y desacoplada.
- (Trabajo a futuro) Enviar correos

### 🌐 API Gateway

- Expone endpoints de algunos servicios AWS como funciones Lambda de forma centralizada.
- Aplica políticas de autenticación para validar tokens Cognito antes de permitir acceso a servicios internos.
- (Trabajo a futuro) Exponer los endpoints del servicio backend de Spring Boot

### 🐘 PostgreSQL (RDS o EC2) (trabajo a futuro)

- Almacena toda la información estructurada del sistema.
- En producción puede estar gestionado con Amazon RDS; en desarrollo, se puede ejecutar como contenedor en EC2.

### 💻 EC2 (trabajo a futuro)

- Se utiliza para desplegar y ejecutar el backend de Spring Boot.
- Permite controlar el entorno de ejecución y escalar verticalmente según las necesidades del sistema.
- Se puede usar junto con Docker para contenerizar la aplicación y facilitar su despliegue.
- Su tráfico está protegido detrás de API Gateway y puede configurarse para aceptar únicamente llamadas autenticadas, así mismo desacoplar lógica de seguridad muy específica en Spring Boot
