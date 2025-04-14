# Práctica: Despliegue de Servidores Web con NGINX usando Docker

## 1. Título  
**Despliegue de dos servidores web personalizados con NGINX y Docker en Ubuntu**

## 2. Tiempo de duración  
**120 minutos (2 horas)**

## 3. Fundamentos

Docker es una plataforma que permite automatizar el despliegue de aplicaciones dentro de contenedores de software. En esta práctica se utilizó la imagen oficial de **NGINX**, que es un servidor web liviano, de alto rendimiento y ampliamente utilizado.

Un contenedor es una instancia ejecutable de una imagen Docker. Cada contenedor es un entorno aislado donde se puede ejecutar una aplicación sin preocuparse por conflictos de dependencias.

NGINX se ejecuta por defecto en el puerto **80**, y al mapearlo con diferentes puertos del sistema host, se pueden desplegar múltiples instancias de servidores con contenido personalizado. En esta práctica se crearon dos servidores:
- El primero muestra información institucional.
- El segundo contiene información personal del estudiante.

A través del comando `docker cp`, se manipularon los archivos `index.html` dentro del contenedor, lo que permite editar el contenido web sin modificar directamente la imagen base.
> **Figura 1-1.** Logotipo de Docker.
 <img src="Tools/Photos/Captura de pantalla 2025-04-13 224123.png" alt="drawing" width="500"/>

> **Figura 1-2**: Diagrama de contenedores desplegados con NGINX  
 <img src="Tools/Photos/1er-Semana-2/s2-servidores ngx-tarea.png" alt="drawing" width="500"/>

 
## 4. Conocimientos previos

Para desarrollar correctamente esta práctica, se requiere que el estudiante tenga conocimiento de:

- Comandos básicos de Linux.
- Navegación de archivos desde terminal.
- Uso de navegadores web.
- Instalación de herramientas desde consola (npm, Angular CLI).
- Instalacion de paquetes de manera manual.


## 5. Objetivos a alcanzar

- Configurar un entorno de desarrollo web sobre Linux.
- Ejecutar y comprobar un servidor Angular desde terminal.
- Manipular archivos de configuración dentro de un proyecto Angular.


## 6. Equipo necesario

- Computador con sistema operativo Windows, Linux o macOS.
- Ubuntu instalado (en máquina real, virtual o WSL).
- Terminal Bash.
- Node.js v18 o superior.
- Angular CLI (última versión estable).
- Navegador actualizado (Chrome, Firefox, etc.).


## 7. Material de apoyo

- [Documentación de Angular](https://angular.io/)
- [Documentación de WSL](https://learn.microsoft.com/en-us/windows/wsl/)
- Guía de comandos básicos de Linux.
- Guía video colocado en la plataforma virtual del Instituto https://drive.google.com/file/d/1OitqZ02pX7VHaVx3qH9eF31mQent65rk/view

## 8. Procedimiento

**Paso 1:** Crea el primer contenedor Nginx llamado nginx1 exponiendo el puerto 8089: docker run -d --name nginx1 -p 8089:80 nginx

```bash
wsl --install -d Ubuntu
```
> **Figura 8-1-1.** Instalación de Ubuntu.
 <img src="photos/Captura de pantalla 2025-04-03 160647.png" alt="drawing" width="600"/>
 
> **Figura 8-1-2.** Instalación wsl.
 <img src="photos/Captura de pantalla 2025-04-04 155905.png" alt="drawing" width="600"/>


**Paso 2:** Abrir Ubuntu e instalar Node.js y npm si no están instalados.  
```bash
sudo apt update
sudo apt install nodejs npm
```
> **Figura 8-2-1.** Instalacion de Node.js.
 <img src="photos/Captura de pantalla 2025-04-04 150416.png" alt="drawing" width="600"/>
 
> **Figura 8-2-2.** Actualizaciones por ejecutarse.
 <img src="photos/Captura de pantalla 2025-04-04 150430.png" alt="drawing" width="600"/>


**Paso 3:** Instalar Angular CLI.
```bash
npm install -g @angular/cli
```
> **Figura 8-3-1.** Instalar Angular CLI globalmente..
 <img src="photos/Captura de pantalla 2025-04-04 150632.png" alt="drawing" width="600"/>
 
> **Figura 8-3-2.** Se cargan los recursos nesesarios.
 <img src="photos/Captura de pantalla 2025-04-04 150702.png" alt="drawing" width="600"/>
 
> **Figura 8-3-3.** Obtenemos Angular CLI ultima versión.
 <img src="photos/Captura de pantalla 2025-04-04 150822.png" alt="drawing" width="600"/>

 
**Paso 4:** Crear un nuevo proyecto Angular.
```bash
mkdir linux-franks
ng new "nombre-del-proyecto" en mi caso lo llame "y"
```
> **Figura 8-3-1.** Creamos carpeta de proyectos.
 <img src="photos/Captura de pantalla 2025-04-04 151005.png" alt="drawing" width="600"/>
 
> **Figura 8-3-2.** Creamos un proyecto Angular dentro de ese directorio.
 <img src="photos/Captura de pantalla 2025-04-04 151025.png" alt="drawing" width="600"/>
 
> **Figura 8-3-3.** Instalacion de recursos nesesarios del proyecto.
 <img src="photos/Captura de pantalla 2025-04-04 151119.png" alt="drawing" width="600"/>


**Paso 5:** Iniciar el servidor de desarrollo.  
```bash
ng serve
```
> **Figura 8-5-1.** Instalacion de recursos nesesarios del proyecto.
 <img src="photos/Captura de pantalla 2025-04-04 153237.png" alt="drawing" width="800"/>


**Paso 6:**  Abrir el navegador y acceder a http://localhost:4200 para ver la app funcionando. 

## 9. Resultados esperados


Al finalizar la práctica, se lograron los siguientes resultados:

- **Configuración exitosa del entorno de desarrollo** en Linux utilizando Ubuntu, demostrando que es posible trabajar con Angular desde la terminal sin necesidad de interfaces gráficas.

- **Instalación y configuración de Angular CLI** mediante `npm`, lo cual permitió crear y gestionar proyectos Angular fácilmente.

- **Creación de un nuevo proyecto Angular funcional**, con la estructura básica correctamente generada y sin errores en la instalación de dependencias.

- **Ejecución del servidor local de Angular**, confirmando que el proyecto podía ser servido correctamente en el navegador a través de `http://localhost:4200`.

- **Verificación visual del funcionamiento del proyecto**, mostrando la pantalla de bienvenida de Angular en el navegador.

- **Comprensión del flujo de trabajo básico en Angular**, desde la instalación hasta la visualización del proyecto, reforzando conocimientos sobre desarrollo frontend y uso de herramientas modernas.

- **Familiarización con la terminal de Linux**, permitiendo  ganar soltura en la ejecución de comandos, manejo de errores comunes (como `ENOENT` o permisos) y navegación de directorios.
  
> **Figura 9-1.** Resultado de practica.
 <img src="photos/Captura de pantalla 2025-04-06 181905.png" alt="drawing" width="600"/>

  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/1xNT2Qkx8xS4YYcOW_1rXk8FEmomSqs9i/view?usp=sharing

## 10. Bibliografía

- Angular Developers. (s.f.). *Angular Documentation*. Recuperado de [https://angular.io/docs](https://angular.io/docs)
- Microsoft. (s.f.). *Windows Subsystem for Linux Documentation*. Recuperado de [https://learn.microsoft.com/en-us/windows/wsl/](https://learn.microsoft.com/en-us/windows/wsl/)
