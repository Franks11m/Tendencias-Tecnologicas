# Práctica Servidor Web


## 1. Título  
**Despliegue de una Aplicación Web Fullstack en Producción utilizando Contenedores Docker y Nginx**

## 2. Tiempo de duración  
**Aproximadamente 180 minutos**

## 3. Fundamentos

El despliegue de aplicaciones web modernas requiere de una correcta separación de responsabilidades, estandarización del entorno y escalabilidad. Para lograr esto, se utilizan tecnologías como **Docker** para contenerizar los servicios y **Nginx** como servidor web en producción.

**Docker** permite empaquetar una aplicación junto con todas sus dependencias en contenedores aislados, asegurando que funcione de manera consistente en cualquier entorno. Al contenerizar tanto el *frontend* como el *backend*, se puede controlar de manera más precisa cómo se ejecuta cada parte del sistema.

**Nginx** es un servidor web ligero y de alto rendimiento utilizado comúnmente para servir archivos estáticos como los generados por frameworks frontend como React. También puede actuar como proxy inverso para redirigir peticiones a otros servicios.

Además, se emplea **docker-compose** para orquestar múltiples contenedores, permitiendo levantar con un solo comando todo el entorno: frontend, backend, base de datos, e incluso herramientas adicionales como pgAdmin.

La comunicación entre servicios está gestionada por una red interna de Docker, y se configuran variables de entorno mediante archivos `.env` para mantener la seguridad y flexibilidad.

El siguiente diagrama representa la arquitectura general de la solución:

<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 223158.png" width="400" />
  <br>
  Figura 1. Diagrama de arquitectura con contenedores
</div>

<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 223210.png" width="400" />
  <br>
  Figura 2. Flujo de despliegue con Docker y Nginx
</div>

---

```bash
# Este modelo permite desplegar un sistema completo en producción con tan solo ejecutar el comando:

docker-compose up --build
```
---

## 4. Conocimientos previos  

Para realizar esta práctica el estudiante necesita tener claro los siguientes temas:  
- Comandos basicos de Linux
- Fundamentos de redes y puertos
- Navegación en sistemas de archivos
- Conceptos básicos de Docker
- Fundamentos de React y Node.js
- Uso de PostgreSQL
- Lectura de logs y errores
- Manipulación de archivos .env y configuración de Nginx

## 5. Objetivos a alcanzar  

- Implementar contenedores para frontend y backend con Docker
- Implementar contenedores Docker para el backend, frontend y base de datos.
- Realizar el build de una aplicación frontend con Node.js y servirla con Nginx.
- Orquestar todos los servicios con un archivo docker-compose.yml.
- Configurar archivos .env y variables de entorno.
- Comprobar la correcta comunicación entre frontend y backend en modo producción.

## 6. Equipo necesario  

- Computador con sistema operativo Windows, Linux o macOS
- Visual Studio Code
- Docker Desktop
- Node.js v18+
- PostgreSQL v15 (contenedor)
- Navegador web
- Editor de código (VS Code recomendado)

## 7. Material de apoyo  

- Documentación oficial de Docker: https://docs.docker.com/  
- Documentación de PostgreSQL: https://www.postgresql.org/docs/  
- Guía de la asignatura y material proporcionado por el profesor.  
- Repositorios y documentacion en clase
- Documentación de React
- Documentación oficial de Nginx: https://nginx.org/en/docs/

## 8. Procedimiento  

**Paso 1:**  Crear estructura del proyecto
```bash
PROYECT_CARNICERIA/
│
├── frontend/ (React app)
├── backend/ (Express + TypeScript)
├── docker-compose.yml

```
> **Figura 8-1-1.**
> Organizar el proyecto con las carpetas:
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 223959.png" alt="drawing" width="400"/>


**Paso 2:**  Configurar el Dockerfile del frontend
> **Figura 8-2-1.**
> Utilizar una imagen **node:18-alpine** para construir la app, y luego una imagen **nginx:stable-alpine** para servirla.
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 224147.png" width="800"/>


**Paso 3:**  Configurar el backend con Express
> **Figura 8-3-1.**
> Asegurar que el backend esté preparado para recibir peticiones desde el frontend con CORS configurado.
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 224304.png" alt="drawing" width="800"/>


**Paso 4:** Configurar el archivo docker-compose.yml
> **Figura 8-4-1.**
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 224415.png" alt="drawing" width="800"/>
 

**Paso 5:** Ejecutar el proyecto
```bash
docker-compose up --build
```
> **Figura 8-5-1.**
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 224559.png" alt="drawing" width="800"/>
 

**Paso 6:** Verificar resultados
> **Figura 8-6-1.**
> Abrir en el navegador **http://localhost:3000** para visualizar el frontend desplegado por Nginx.
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 225755.png" alt="drawing" width="800"/>
 
> **Figura 8-6-2.**
 <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 225838.png" alt="drawing" width="800"/>
 
> **Figura 8-6-3.**
> Estructura de servicios corriendo.
  <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 224824.png" alt="drawing" width="800"/>
  
> **Figura 8-6-4.**
  <img src="./../../Tools/Photos/2do-Semana-10/Captura de pantalla 2025-06-12 224618.png" alt="drawing" width="800"/>


 
## 9. Resultados esperados

Al finalizar esta práctica se espera que el estudiante haya logrado desplegar correctamente una aplicación web fullstack. El frontend debe estar disponible en http://localhost y servir los archivos estáticos usando Nginx, mientras que el backend responde correctamente a las peticiones realizadas por la interfaz.- Contenedores de PostgreSQL, pgAdmin y backend corriendo sin errores.

Entre los logros verificados están:
- Build exitoso del frontend 
- Comunicación correcta con el backend 
- Acceso a datos desde la base de datos 
- Uso adecuado de variables de entorno y configuración modular


  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/130vniyp-lyZTDa9CT1sCE7c0071x4jSZ/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (2024). Docker Documentation. https://docs.docker.com/
- Nginx. (2024). Nginx Documentation. https://nginx.org/en/docs/
- React Team. (2024). React Documentation. https://react.dev/
- Node.js Foundation. (2024). Node.js Documentation. https://nodejs.org/
- PostgreSQL Global Development Group. (2024). PostgreSQL Documentation. https://www.postgresql.org/
