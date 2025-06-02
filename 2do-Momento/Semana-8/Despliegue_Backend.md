# Práctica Servidor Web


## 1. Título  
**Automatización del despliegue de una aplicación backend con Docker y Docker Compose, incluyendo PostgreSQL y pgAdmin**

## 2. Tiempo de duración  
**Aproximadamente 180 minutos (3 horas) fueron utilizados para completar la práctica, incluyendo configuración, construcción de imágenes y despliegue.
**  

## 3. Fundamentos

Esta práctica se basa en el uso de tecnologías de contenedores para automatizar el despliegue de aplicaciones backend y bases de datos. Docker es una plataforma que permite empaquetar aplicaciones junto con todas sus dependencias en contenedores ligeros y portables. Esto facilita la replicación del entorno de desarrollo y producción, asegurando consistencia en su comportamiento.

Docker Compose es una herramienta que permite definir y ejecutar aplicaciones multi-contenedor mediante archivos YAML, simplificando la orquestación y el manejo de servicios interdependientes como bases de datos y paneles de administración.

La base de datos PostgreSQL es un sistema de gestión de bases de datos relacional potente y ampliamente utilizado en entornos empresariales. PgAdmin es una interfaz gráfica web que facilita la administración y gestión visual de bases de datos PostgreSQL.

La técnica de multi-stage builds en Docker permite optimizar la construcción de imágenes, reduciendo el tamaño final al separar las fases de compilación y ejecución. Esto mejora la eficiencia en la automatización y el despliegue continuo.

![Diagrama básico de contenedores Docker](https://docs.docker.com/engine/images/engine-overview.svg)  

<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 111057.png" width="800" />
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

**Paso 1:** Configurar docker-compose.yml con servicios para PostgreSQL, pgAdmin y la aplicación backend.  
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 
**Paso 2:** Crear volúmenes y redes para asegurar persistencia y comunicación entre contenedores. 
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 
**Paso 3:** Construir la imagen Docker de la aplicación backend con Dockerfile (incluyendo multi-stage build para optimización).  
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 
**Paso 4:** Levantar los contenedores con `docker-compose up --build -d`.  
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 
**Paso 5:** Acceder a pgAdmin para configurar la conexión a PostgreSQL (host: `db`, puerto: `5432`, usuario: `postgres`, contraseña: `S3cr3t`).  
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 
**Paso 6:** Probar los endpoints expuestos por la API backend, por ejemplo, `http://localhost:8081/users` para listar usuarios.  
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 
**Paso 7:** Verificar los logs y estado de los contenedores para asegurar correcto funcionamiento.
> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-7/Captura de pantalla 2025-05-16 113338.png" alt="drawing" width="800"/>
 

![Diagrama de servicios y contenedores](https://user-images.githubusercontent.com/placeholder/docker-compose-diagram.png)  
*Figura 8-1. Diagrama de servicios desplegados con Docker Compose.*

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
