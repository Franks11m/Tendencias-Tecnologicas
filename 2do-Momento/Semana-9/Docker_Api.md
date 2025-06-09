# Práctica Servidor Web


## 1. Título  
**Contenerización de Aplicación Web: React + API REST con Docker Compose**

## 2. Tiempo de duración  
**Aproximadamente 180 minutos**

## 3. Fundamentos

La contenerización es una tecnología clave en el desarrollo moderno de software. Permite encapsular una aplicación y todas sus dependencias en un contenedor que puede ejecutarse de forma consistente en diferentes entornos. En esta práctica se emplea Docker para contenerizar una aplicación frontend construida con React, que consume datos desde una API REST construida con Express y conectada a una base de datos PostgreSQL. Todo esto se orquesta con Docker Compose.

Docker es una plataforma que automatiza el despliegue de aplicaciones dentro de contenedores de software. Un contenedor es una unidad estándar de software que empaqueta el código y todas sus dependencias. Docker Compose permite definir y correr aplicaciones con múltiples contenedores mediante un archivo YAML.

React es una biblioteca de JavaScript para construir interfaces de usuario. En esta práctica, el frontend utiliza React para renderizar una tabla con los datos de clientes obtenidos de la API. La API, por su parte, se construye con Node.js y Express, y expone una ruta para listar los clientes desde una base de datos PostgreSQL.

El propósito de esta práctica es comprender el flujo de trabajo completo desde el desarrollo de los servicios hasta su despliegue en contenedores. Se refuerzan conocimientos sobre redes de contenedores, puertos, dependencias y comunicación entre servicios.

---

## 4. Conocimientos previos  

Para realizar esta práctica el estudiante necesita tener claro los siguientes temas:  
- Comandos Linux
- Navegación en sistemas de archivos
- Conceptos básicos de Docker
- Fundamentos de React y Node.js
- Uso de PostgreSQL
- Lectura de logs y errores

## 5. Objetivos a alcanzar  

- Implementar contenedores para frontend y backend con Docker
- Orquestar los servicios con Docker Compose
- Conectar una aplicación React a una API REST
- Visualizar datos desde una base de datos PostgreSQL
- Aplicar estilos modernos con Tailwind CSS

## 6. Equipo necesario  

- Computador con Windows 10/11
- Visual Studio Code
- Docker Desktop
- Node.js v18+
- PostgreSQL v15 (contenedor)
- Navegador web

## 7. Material de apoyo  

- Documentación oficial de Docker: https://docs.docker.com/  
- Documentación de PostgreSQL: https://www.postgresql.org/docs/  
- Guía de la asignatura y material proporcionado por el profesor.  
- Repositorios y documentacion en clase
- Documentación de React

## 8. Procedimiento  

**Paso 1:** Crear estructura de carpetas
> **Figura 8-1-1.**
> Se crea una carpeta principal con dos subcarpetas: backend/ y frontend/, como proyectos independientes.
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 224106.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-09 003844.png" alt="drawing" width="800"/>


**Paso 2:**  Crear API REST en Express
> **Figura 8-2-1.**
> Se configura un servidor con Node.js y Express, y se conectan rutas a una base de datos PostgreSQL.

 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 224106.png" width="800"/>
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 224035.png" width="800"/>


**Paso 3:**  Crear archivo Dockerfile en backend
> **Figura 8-3-1.**
> Se especifica una imagen base de Node.js, se copian archivos del backend y se ejecuta el proceso de build con TypeScript.
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-09 004820.png" alt="drawing" width="800"/>


**Paso 4:** Crear docker-compose.yml para backend
> **Figura 8-4-1.**
> Se define una red de contenedores incluyendo servicios db, pgadmin y backend, con sus variables de entorno y volúmenes.
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 224123.png" alt="drawing" width="800"/>
 

**Paso 5:** Crear frontend con React + TypeScript
> **Figura 8-5-1.**
> Se utiliza create-react-app con plantilla TypeScript para generar el proyecto.
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 230821.png" alt="drawing" width="800"/>
 

**Paso 6:** Diseñar componente de tabla ClientesTable.tsx

**Paso 7:** Crear docker-compose.yml para frontend
> **Figura 8-7-1.**
> Se define el contenedor para la aplicación React y se expone el puerto 3000.
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-09 003831.png" alt="drawing" width="800"/>
 
> **Figura 8-7-2.**
> Se crea dockerfile
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-09 003844.png" alt="drawing" width="800"/>

 
**Paso 8:**  Levantar servicios
```
docker compose up --build -d
```
> **Figura 8-8-1.**
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-09 003859.png" alt="drawing" width="800"/>


**Paso 9:** Verificar comunicación entre contenedores
> **Figura 9-9-1.** BACKEND
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 223956.png" alt="drawing" width="800"/>
 
 > **Figura 9-9-2.** FRONTEND
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-09 000846.png" alt="drawing" width="800"/>
 
 
## 9. Resultados esperados

Al finalizar la práctica, se espera que los siguientes resultados sean evidentes:  
- Contenedores de PostgreSQL, pgAdmin y backend corriendo sin errores.  
- Persistencia de datos garantizada mediante volúmenes.  
- Acceso a pgAdmin vía navegador y conexión exitosa a la base de datos.  
- Endpoint `/api/clientes` respondiendo con una lista en formato JSON de clientes almacenados en la base de datos.  
- Imagen Docker optimizada y contenedores fácilmente replicables.  

Ejemplo de respuesta en navegador para `http://localhost:5000/api/clientes`:

```json
[
  {
    "id": 1,
    "nombre": "Franks Gonzalez",
    "direccion": "El salado Mayancela",
    "telefono": "0959906392",
    "email": "gonzafranks777@gmail.com"
  },
  ...
]

```
> **Figura 8-10-1.**
 <img src="./../../Tools/Photos/2do-Semana-9/Captura de pantalla 2025-06-08 224011.png" alt="drawing" width="800"/>

  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/12510_U2kNw7Rpc80HEWK43ArxXppr53h/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (2024). Docker Documentation. https://docs.docker.com/
- Facebook. (2024). React Docs. https://reactjs.org/
- Tailwind Labs. (2024). Tailwind CSS Documentation. https://tailwindcss.com/docs
- Node.js Foundation. (2024). Node.js Documentation. https://nodejs.org/
- PostgreSQL Global Development Group. (2024). PostgreSQL Documentation. https://www.postgresql.org/

