# Práctica Servidor Web


## 1. Título  
**Despliegue de una Aplicación Web en Contenedores usando Nginx y Docker**

## 2. Tiempo de duración  
**240 minutos**  

## 3. Fundamentos

Para comprender esta práctica es fundamental entender los principios de la **virtualización ligera mediante contenedores** y cómo se puede utilizar **Docker** para aislar y desplegar aplicaciones. A diferencia de las máquinas virtuales tradicionales, los contenedores no requieren un sistema operativo completo por instancia, lo cual los hace más eficientes.

Docker permite empaquetar aplicaciones junto con todas sus dependencias dentro de una imagen. Estas imágenes se ejecutan como contenedores, los cuales son instancias aisladas que se ejecutan sobre el mismo sistema operativo del host. En este ejercicio, se usa **Node.js** como entorno de desarrollo para construir una aplicación frontend, y **Nginx** como servidor web para servir el contenido estático generado.

Nginx, por su parte, es un servidor web de alto rendimiento y ampliamente utilizado en entornos de producción. Su configuración es sencilla, y es ideal para servir archivos estáticos, hacer balanceo de carga, o actuar como proxy inverso.

La combinación de estas herramientas permite crear entornos reproducibles y fáciles de desplegar, ideales para entornos de desarrollo y producción.

Además, se debe comprender el flujo de construcción de una imagen Docker:
1. Uso del `Dockerfile` para definir instrucciones.
2. Uso del comando `docker build` para generar la imagen.
3. Uso de `docker run` para lanzar un contenedor.

Todo esto se realiza desde la terminal o desde entornos como **Visual Studio Code**, con extensiones que permiten integrarse fácilmente con Docker Desktop.

---
<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 225953.png" width="800" />
  <br>
  Figura 1. Representación de Docker.
</div>

 
## 4. Conocimientos previos

- Uso de comandos básicos de Linux (`cd`, `ls`, `mkdir`, etc.)
- Manejo básico del navegador web.
- Conocimientos de HTML, CSS y JavaScript.
- Entendimiento de cómo funciona un servidor web.
- Conceptos básicos de redes y puertos.
- Instalación y uso básico de Docker.
- Edición de archivos con Visual Studio Code u otro editor.

## 5. Objetivos a alcanzar

- Implementar contenedores para el despliegue de una aplicación web.
- Configurar Nginx como servidor web para una aplicación frontend.
- Manipular archivos de configuración de Nginx.
- Construir imágenes Docker usando un `Dockerfile`.
- Desplegar la aplicación desde Visual Studio Code utilizando Docker Desktop.


## 6. Equipo necesario

- Computadora con sistema operativo **Windows 10/11** con **WSL2** habilitado o **Linux**.
- Docker Desktop instalado y funcionando correctamente.
- Visual Studio Code con extensión de Docker instalada.
- Conexión a Internet estable.
- Cuenta en Docker Hub (opcional, para subir imágenes).
- Navegador web (Google Chrome, Firefox, etc.).

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com)
- Repositorio del proyecto frontend a desplegar
- [Guía de Informe](https://github.com/maguaman2/informe-tendencias)
- Guía video colocado en la plataforma del Instituto: 
- Guía de comandos básicos de Linux.

## 8. Procedimiento

**Paso 1:**  Verificar Docker instalado y funcionando


```bash
docker info


```

 **Paso 2:** Clonar el proyecto frontend

```bash
gIT HUB DESCKTOP
```

> **Figura 8-2-1.**
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 221830.png" alt="drawing" width="800"/>

 
**Paso 3:** Crear el Dockerfile
```bash
# Etapa 1: Construcción
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

# Etapa 2: Servidor NGINX
FROM nginx:stable-alpine

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]



```

> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222420.png" alt="drawing" width="800"/>
 
> **Figura 8-3-2.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222401.png" alt="drawing" width="500"/>

**Paso 4:**  Construir la imagen
```bash
docker build -t suda-frontend .
```

> **Figura 8-4-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222547.png" alt="drawing" width="800"/>

**Paso 5:** Ejecutar el contenedor
```bash
docker run -d -p 80:80 suda-frontend
```
> **Figura 8-5-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 232047.png" alt="drawing" width="800"/>

**Paso 6:** Acceder desde el navegador
```bash
docker run -d -p 3000:80 suda-frontend
http://localhost:8080
```
> **Figura 8-6-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222721.png" alt="drawing" width="800"/>
 
> **Figura 8-6-2.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 224536.png" alt="drawing" width="800"/>

## 9. Resultados esperados

Al finalizar la práctica, se obtuvieron los siguientes resultados:

Se logró empaquetar y desplegar la aplicación web frontend utilizando contenedores Docker. La aplicación se sirvió de forma eficiente desde Nginx, confirmando el correcto funcionamiento del Dockerfile, el servidor y la configuración de red.
Además, se resolvieron errores comunes relacionados con permisos, conexión al demonio de Docker y lentitud en la construcción.

  
  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/1DORAk9nhrTca9psRohPginv9_Lqtlzts/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (s.f.). Docker Documentation. Recuperado de https://docs.docker.com/
- González, F. (2023). Guía de implementación de entornos web con contenedores. Universidad Sudamericana.
- dpage. (2024). phpMyAdmin documentation. Recuperado de https://www.phpmyadmin.net/docs/
