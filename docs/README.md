# 🎵 Spring Tunes

**Spring Tunes** es un clon simplificado de Spotify, desarrollado como proyecto de portafolio que abarca distintas áreas como el backend con Spring Boot, la nube con AWS y Frontend con Angular.

Permite a los usuarios explorar, escuchar y organizar música, mientras integra un sistema de aprobación para artistas y contenido.

## Repositorios

- [Backend](https://github.com/edwbadillo/springtunes-api) desarrollado con Spring Boot 3.5, PostgreSQL 16, Docker.
- [Frontend](https://github.com/edwbadillo/springtunes-ui) desarrollado en Angular 20.


## 🛠️ Tecnologías principales

- **Backend**: Java 21, Spring Boot 3.5, API Docs (Swagger)
- **Frontend**: Cliente web con Angular 20
- **Base de datos**: PostgreSQL
- **Docker**: Contenedores Docker para despliegue de los servicios Spring Boot y PostgreSQL
- **AWS**: 
  - Cognito: Autenticación de usuarios.
  - S3: Almacenamiento de archivos.
  - Lambda: Funciones de backend como correos y generación de enlaces pre firmados para S3.
  - API Gateway: Enrutamiento seguro para comunicarse con las lambdas y otros servicios.

## 🔑 Funcionalidades  

- Registro y autenticación segura mediante AWS Cognito.
- Autorización de usuarios basado en un sistema de roles (`USER`, `ARTIST`, `ADMIN`)
- Solicitud y aprobación de perfiles de artista.
- Subida y revisión de canciones antes de su publicación.
- Reproducción de audio vía streaming.
- Creación de playlists, favoritos.

## 🔗 Arquitectura general

<img src="./assets/arquitectura-general.jpg" alt="Architecture" width="550" />
