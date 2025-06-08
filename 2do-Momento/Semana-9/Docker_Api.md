# Práctica Servidor Web


## 1. Título  
**Automatización del despliegue de una aplicación backend con Docker y Docker Compose, incluyendo PostgreSQL y pgAdmin**

## 2. Tiempo de duración  
**Aproximadamente 180 minutos (3 horas) fueron utilizados para completar la práctica, incluyendo configuración, construcción de imágenes y despliegue.**  

## 3. Fundamentos

Esta práctica se basa en el uso de tecnologías de contenedores para automatizar el despliegue de aplicaciones backend y bases de datos. Docker es una plataforma que permite empaquetar aplicaciones junto con todas sus dependencias en contenedores ligeros y portables. Esto facilita la replicación del entorno de desarrollo y producción, asegurando consistencia en su comportamiento.

Docker Compose es una herramienta que permite definir y ejecutar aplicaciones multi-contenedor mediante archivos YAML, simplificando la orquestación y el manejo de servicios interdependientes como bases de datos y paneles de administración.

La base de datos PostgreSQL es un sistema de gestión de bases de datos relacional potente y ampliamente utilizado en entornos empresariales. PgAdmin es una interfaz gráfica web que facilita la administración y gestión visual de bases de datos PostgreSQL.

La técnica de multi-stage builds en Docker permite optimizar la construcción de imágenes, reduciendo el tamaño final al separar las fases de compilación y ejecución. Esto mejora la eficiencia en la automatización y el despliegue continuo.

<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 005427.png" width="800" />
  <br>
  Figura 1.  Arquitectura básica de contenedores Docker y servicios.
</div>

Los conceptos de redes y volúmenes en Docker garantizan la persistencia de datos y la comunicación entre servicios, evitando pérdidas de información y facilitando la escalabilidad de la aplicación.

En resumen, esta práctica integra conocimientos de virtualización ligera, gestión de bases de datos, desarrollo backend y automatización de infraestructura, fundamentales para el desarrollo moderno de software.

---

## 4. Conocimientos previos  

Para realizar esta práctica el estudiante necesita tener claro los siguientes temas:  
- Comandos básicos de Linux (navegación, edición de archivos)  
- Uso básico de Docker y Docker Compose  
- Fundamentos de redes y puertos en aplicaciones web  
- Conceptos de REST API y programación backend  
- Manejo de navegadores para realizar pruebas de endpoints  
- Conocimientos básicos de bases de datos relacionales (PostgreSQL)  

## 5. Objetivos a alcanzar  

- Automatizar el despliegue de una aplicación backend con Docker y Docker Compose.  
- Crear servicios para PostgreSQL y pgAdmin asegurando persistencia y conectividad.  
- Construir una imagen optimizada para la aplicación backend con multi-stage builds.  
- Configurar correctamente variables de entorno y conexiones entre contenedores.  
- Verificar el funcionamiento de la API mediante pruebas de endpoints.  

## 6. Equipo necesario  

- Computador con sistema operativo Windows, Linux o MacOS.  
- Instalación de Docker y Docker Compose (versiones recientes).  
- Editor de texto o IDE para modificar código fuente (por ejemplo, Visual Studio Code).  
- Navegador web para acceder a pgAdmin y probar la API.  
- Acceso a internet para descargar imágenes Docker y documentación.  

## 7. Material de apoyo  

- Documentación oficial de Docker: https://docs.docker.com/  
- Documentación de PostgreSQL: https://www.postgresql.org/docs/  
- Guía de la asignatura y material proporcionado por el profesor.  
- Cheat sheet de comandos Linux.  
- Repositorio base del proyecto: https://github.com/maguaman2/tendencias-mar22-security.git  

## 8. Procedimiento  

**Paso 1:** Clonar el repositorio base desde GitHub.
> **Figura 8-1-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 230732.png" alt="drawing" width="800"/>

**Paso 2:** Acceder al directorio del proyecto clonado.
> **Figura 8-2-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 230732.png" alt="drawing" width="800"/>


**Paso 3:** Crear y configurar el archivo `docker-compose.yml` con los servicios necesarios.
> **Figura 8-3-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 233240.png" alt="drawing" width="800"/>


**Paso 4:** Definir las variables de entorno en un archivo `.env`.
> **Figura 8-4-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 232921.png" alt="drawing" width="800"/>
 

**Paso 5:** Crear un `Dockerfile` con estrategia de construcción multi-stage para la aplicación backend.
> **Figura 8-5-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 235132.png" alt="drawing" width="800"/>
 

**Paso 6:** Construir e iniciar los contenedores usando Docker Compose.
> **Figura 8-6-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 235647.png" alt="drawing" width="800"/>
 
> **Figura 8-6-2.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 000423.png" alt="drawing" width="800"/>

**Paso 7:** Acceder a pgAdmin desde el navegador y crear un nuevo servidor con los datos de conexión.
> **Figura 8-7-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 005716.png" alt="drawing" width="800"/>
 
> **Figura 8-7-2.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001104.png" alt="drawing" width="800"/>
 
> **Figura 8-7-3.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001125.png" alt="drawing" width="800"/>
 
> **Figura 8-7-4.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001135.png" alt="drawing" width="800"/>
 
**Paso 8:** Verificar la conexión de pgAdmin a PostgreSQL.
> **Figura 8-8-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001831.png" alt="drawing" width="800"/>


**Paso 9:** Comprobar que la aplicación backend se conecta correctamente a la base de datos.
> **Figura 9-9-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001250.png" alt="drawing" width="800"/>
 

**Paso 10:** Crear y configurar el archivo `CorsConfig.kt` para habilitar CORS en el backend.
> **Figura 8-10-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001935.png" alt="drawing" width="800"/>
 

**Paso 11:** Probar el endpoint `/users` desde el navegador o herramienta de prueba de APIs.
> **Figura 8-11-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 004720.png" alt="drawing" width="800"/>

> **Figura 8-11-2.**
  <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 012126.png" alt="drawing" width="800"/>


## 9. Resultados esperados  

Al finalizar la práctica, se espera que los siguientes resultados sean evidentes:  
- Contenedores de PostgreSQL, pgAdmin y backend corriendo sin errores.  
- Persistencia de datos garantizada mediante volúmenes.  
- Acceso a pgAdmin vía navegador y conexión exitosa a la base de datos.  
- Endpoint `/users` respondiendo con una lista en formato JSON de usuarios almacenados en la base de datos.  
- Imagen Docker optimizada y contenedores fácilmente replicables.  

Ejemplo de respuesta en navegador para `http://localhost:8081/users`:

```json
[
  {
    "id": 1,
    "username": "jdoe",
    "email": "jdoe@example.com",
    "passwordHash": "3c59dc048e8850243be8079a5c74d079",
    "isActive": "t",
    "createdAt": "2025-06-02 05:04:05.766085"
  },
  ...
]
```

  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/10UL3iFNJ-jRgvvaaBtAelhagdXRXs97M/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (s.f.). Docker Documentation. Recuperado de https://docs.docker.com/
- González, F. (2023). Guía de implementación de entornos web con contenedores. Universidad Sudamericana.
- dpage. (2024). phpMyAdmin documentation. Recuperado de https://www.phpmyadmin.net/docs/
