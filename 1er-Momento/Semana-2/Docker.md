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
 <img src="../../Tools/Photos/1er-Semana-2/images.png" alt="drawing" width="500"/>

> **Figura 1-2**: Diagrama de contenedores desplegados con NGINX  
 <img src="../../Tools/Photos/1er-Semana-2/s2-servidores ngx-tarea.png" alt="drawing" width="500"/>

 
## 4. Conocimientos previos

Para desarrollar correctamente esta práctica, se requiere que el estudiante tenga conocimiento de:

- Uso de comandos básicos en terminal Linux
- Instalación y uso de Docker
- Manipulación de archivos en Linux
- Edición de archivos HTML con editores como `nano` o `vi`
- Comprensión básica de puertos y redes en servicios web


## 5. Objetivos a alcanzar

- Implementar dos contenedores con NGINX que expongan diferentes puertos
- Personalizar el contenido del archivo `index.html` dentro de cada contenedor
- Comprender el uso de Docker para desplegar servidores web rápidamente



## 6. Equipo necesario

- Computador con Ubuntu 22.04 (en WSL)
- Docker v26.1.3
- Acceso a terminal con permisos sudo
- Editor de texto (`nano`, `vi`, etc.)
- Navegador web para visualizar los servidores


## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Guía de Informe](https://github.com/maguaman2/informe-tendencias)
- Guía de comandos básicos de Linux.
- Guía video colocado en la plataforma virtual del Instituto https://drive.google.com/file/d/15wFqPb-kXV2pF-hzqubjN56eNScP-OB4/view

## 8. Procedimiento

**Paso 1:** Instalar Docker en el terminal

```bash
docker -v
```
> **Figura 8-1-1.** Verificación del Docker en Ubuntu.
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 223628.png" alt="drawing" width="600"/>
 
**Paso 2:** Probar si el Docker funciona correctamente  
```bash
docker run hello-world
```
> **Figura 8-2-1.** Docker funcionando.
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 223645.png" alt="drawing" width="600"/>
 
**Paso 3:** Crear el primer contenedor.
```bash
docker run -d --name nginx1 -p 8089:80 nginx
```
**Paso 4:**  Crear el segundo contenedor.
```bash
docker run -d --name nginx2 -p 8090:80 nginx
```
> **Figura 8-4-1.** Contenedores creados.
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 224123.png" alt="drawing" width="600"/>

**Paso 5:** Copiar archivo desde el contenedor nginx1.
```bash
docker cp nginx1:/usr/share/nginx/html/index.html ./index1.html
```
> **Figura 8-5-1.** 
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 224242.png" alt="drawing" width="800"/>

**Paso 6:**  Instalar nano en la terminal de Ubuntu
```bash
sudo apt install nano
```
> **Figura 8-6-1.** 
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 224459.png" alt="drawing" width="800"/>

**Paso 7:**  Editar el archivo index1.html.
```bash
nano index1.html
```
> **Figura 8-7-1.** Editar con información del Instituto
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 224915.png" alt="drawing" width="800"/>

**Paso 8:** Volver a copiar el archivo editado al contenedor
```bash
docker cp index1.html nginx1:/usr/share/nginx/html/index.html
```
> **Figura 8-8-1.** Editar con información del Instituto
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 225953.png" alt="drawing" width="800"/>

**Paso 9:**  Repetir el proceso para nginx2
```bash
docker cp nginx2:/usr/share/nginx/html/index.html ./index2.html
nano index2.html
docker cp index2.html nginx2:/usr/share/nginx/html/index.html

```
> **Figura 8-9-1.** Copiar archivo desde el contenedor nginx2
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 230205.png" alt="drawing" width="800"/>
 
> **Figura 8-9-2.** Editar el archivo index2.html "Se personaliza con información personal del estudiante"
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 230722.png" alt="drawing" width="800"/>
 
> **Figura 8-9-3.**Volver a copiar el archivo editado al contenedor
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 230712.png" alt="drawing" width="800"/>
 

**Paso 10:**  Verificación de Servidores Web
```bash
Acceder a http://localhost:8089 para el primer servidor
Acceder a http://localhost:8090 para el segundo servidor
```
> **Figura 8-10-1.** Primer servidor 
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 232414.png" alt="drawing" width="800"/>
 
> **Figura 8-10-2.** Segundo servidor 
 <img src="../../Tools/Photos/1er-Semana-2/Captura de pantalla 2025-04-13 232439.png" alt="drawing" width="800"/>


## 9. Resultados esperados


Al finalizar la práctica, se espera que el estudiante haya logrado implementar correctamente un **servidor web utilizando contenedores Docker con la imagen oficial de NGINX**. Se debe haber cumplido con los siguientes objetivos:

- **Implementar contenedores con NGINX:** Se logró desplegar dos contenedores de NGINX, exponiendo sus puertos correctamente para acceder desde el navegador web local a través de `localhost:8089` y `localhost:8090`.
  
- **Manipular archivos de configuración:** Se realizó la extracción del archivo `index.html` desde el primer contenedor `nginx1`, se modificó su contenido localmente, y se volvió a utilizar como página web personalizada en el segundo contenedor `nginx2`.

- **Validación de la configuración:** Al ingresar a los puertos mapeados en el navegador, se visualizó la página original de NGINX desde el primer contenedor y la página modificada desde el segundo contenedor, lo que demuestra la correcta manipulación del contenido del servidor web.


Estos resultados confirman que se cumplió con éxito el despliegue de servidores web en contenedores Docker, así como la edición de sus archivos internos.


  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/1znu-cUfQQpujFQ9_oJb6P0acfJBsstPN/view?usp=sharing

## 10. Bibliografía

- Play with Docker. (s. f.). https://labs.play-with-docker.com/
- nano – Documentation. (s. f.). https://www.nano-editor.org/docs.php
- Official Ubuntu Documentation. (s. f.). https://help.ubuntu.com/
- Microsoft. (s.f.). *Windows Subsystem for Linux Documentation*. Recuperado de [https://learn.microsoft.com/en-us/windows/wsl/](https://learn.microsoft.com/en-us/windows/wsl/)
