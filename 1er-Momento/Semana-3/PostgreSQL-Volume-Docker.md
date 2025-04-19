# Práctica: Persistencia de Datos con Docker y PostgreSQL

## 1. Título  
**Persistencia de datos en PostgreSQL usando contenedores y volúmenes Docker**

## 2. Tiempo de duración  
**180 minutos (3 horas)**

## 3. Fundamentos

En esta práctica se explora el uso de contenedores Docker para ejecutar una base de datos PostgreSQL, y cómo utilizar volúmenes para asegurar la persistencia de datos aún después de eliminar el contenedor.

**Docker** permite crear, desplegar y ejecutar aplicaciones usando contenedores. Los contenedores son entornos livianos, portables y consistentes, útiles especialmente en entornos de desarrollo y producción.

Por otro lado, **PostgreSQL** es un sistema de gestión de bases de datos relacional de código abierto ampliamente utilizado. Al ejecutar PostgreSQL dentro de un contenedor, los datos generados por el servicio (bases de datos, tablas, registros) se almacenan por defecto dentro del sistema de archivos del contenedor. Si el contenedor se elimina, estos datos también se pierden.

Para evitar esa pérdida, Docker permite el uso de **volúmenes**, que son espacios de almacenamiento persistente. Al vincular un volumen a un contenedor, se puede asegurar que los datos permanezcan disponibles incluso si el contenedor se detiene o se borra.

<div align="center">
  <img src="https://miro.medium.com/v2/resize:fit:800/format:webp/1*zgn96VYrjCqW-iPGLuD49Q.png" width="800" />
  <br>
  Figura 3-1. Persistencia de datos con volúmenes Docker.
</div>

Esta práctica está dividida en dos partes:

- La primera sin volumen, donde se comprueba la pérdida de datos al eliminar el contenedor.
- La segunda con volumen, donde se verifica que los datos persisten.

 
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
