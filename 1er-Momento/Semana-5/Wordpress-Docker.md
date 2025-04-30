# Práctica: Implementación de un servidor WordPress con Docker


## 1. Título  
**Implementación de un entorno web WordPress usando contenedores Docker**

## 2. Tiempo de duración  
**120 minutos (2 horas)**

## 3. Fundamentos

Docker es una tecnología que permite la creación y ejecución de aplicaciones dentro de contenedores. Estos contenedores incluyen todos los componentes necesarios para ejecutar un servicio: sistema de archivos, bibliotecas, configuraciones y código de la aplicación. A través de esta tecnología, se puede garantizar la portabilidad y el aislamiento de los servicios sin necesidad de configurar entornos complejos.

En la presente práctica, se implementó un entorno de publicación web basado en WordPress, compuesto por tres contenedores:

- **MySQL**: motor de base de datos que almacena la información del sitio web.

- **phpMyAdmin**: interfaz gráfica que permite la administración de bases de datos.

- **WordPress**: sistema de gestión de contenidos (CMS) que permite construir y administrar sitios web de forma intuitiva.

Además, se utilizaron conceptos fundamentales como la creación de una red personalizada para permitir la comunicación entre contenedores, y la configuración de un volumen persistente, que evita la pérdida de datos al detener o eliminar los contenedores.

También se hizo uso de variables de entorno para automatizar configuraciones, lo cual permite desplegar servicios listos para funcionar con un solo comando. Esta práctica refuerza habilidades esenciales en redes, administración de sistemas y virtualización ligera.

<div align="center">
  <img src="./../../Tools/Photos/1er-Semana-5/image-removebg-preview (8).png" width="500" />
  <br>
  Figura 1. Docker con Wordpress.
</div>

<div align="center">
  <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 164952.png" width="650" />
  <br>
  Figura 1. Diagrama de los contenedores con los puertos utilizados.
</div>

 
## 4. Conocimientos previos

- Comandos de línea en entornos Linux o PowerShell.
- Conocimientos básicos sobre redes TCP/IP.
- Familiaridad con el uso del navegador web.
- Entendimiento del modelo cliente-servidor.
- Conceptos básicos de virtualización y contenedores.


## 5. Objetivos a alcanzar

- Implementar contenedores que permitan desplegar un servidor web WordPress.
- Configurar servicios que se comuniquen entre sí mediante redes personalizadas en Docker.
- Manipular archivos de configuración y volúmenes para asegurar persistencia de datos.
- Comprender el funcionamiento de un entorno de desarrollo basado en contenedores.



## 6. Equipo necesario

- Computador con sistema operativo Windows, Linux o macOS.
- Docker instalado (versión 20.8 o superior).
- Acceso a terminal PowerShell, Bash o CMD.
- Navegador web actualizado (Google Chrome, Mozilla Firefox, etc.).
- Conexión a Internet para descargar las imágenes necesarias desde Docker Hub.

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- Documentación oficial de WordPress (https://wordpress.org/support/)
- [Guía de Informe](https://github.com/maguaman2/informe-tendencias)
- Documentación oficial de phpMyAdmin: [https://docs.phpmyadmin.net/](https://docs.phpmyadmin.net/)
- Guía de comandos básicos de Linux.
- Guía video colocado en la plataforma de youtube https://www.youtube.com/watch?v=F_aL2Aw5wcE

## 8. Procedimiento

**Paso 1:**  Creación de la red personalizada

```bash
docker network create wordpress-net
```

> **Figura 8-1-1.** Se crea una red virtual para permitir la comunicación entre los contenedores:
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 152200.png" alt="drawing" width="800"/>

 

 **Paso 2:** Creación del volumen persistente

```bash
docker volume create wordpress-db-data
```

> **Figura 8-2-1.**Se crea un volumen para almacenar los datos de la base de datos de forma permanente:
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 152247.png" alt="drawing" width="800"/>

 
 
**Paso 3:** Creación del contenedor MySQL
```bash
docker run -d --name wordpress-mysql --network wordpress-net -v wordpress-db-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppass mysql:5.7
```

| Opción                                      | Significado                                                      |
|--------------------------------------------|------------------------------------------------------------------|
| `-d`                                        | *Ejecuta el contenedor en segundo plano*                   |
| `--name wordpress-mysql`                   | *Nombre del contenedor (sirve para que WordPress lo reconozca*)   |
| `--network wordpress-net`                  | *Lo conecta a la red personalizada*                                |
| `-v wordpress-db-data:/var/lib/mysql`      | *Usa el volumen para guardar datos*                               |
| `-e MYSQL_ROOT_PASSWORD=rootpass`          | *Contraseña del usuario administrador (`root`)*                   |
| `-e MYSQL_DATABASE=wordpress`              | *Crea una base de datos llamada `wordpress`*                     |
| `-e MYSQL_USER=wpuser` / `MYSQL_PASSWORD=wppass` | *Crea un usuario normal con acceso a la base de datos*        |

> **Figura 8-3-1.** Levantar el contenedor de la base de datos con las credenciales necesarias:
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 152608.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 152707.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 153155.png" alt="drawing" width="800"/>


**Paso 4:**  Creación del contenedor phpMyAdmin
```bash
docker run -d --name wordpress-phpmyadmin --network wordpress-net -e PMA_HOST=wordpress-mysql -p 8080:80 phpmyadmin/phpmyadmin
```

| Opción                                   | Significado                                                                 |
|------------------------------------------|-----------------------------------------------------------------------------|
| `--name wordpress-phpmyadmin`           | *Nombre del contenedor*                                                       |
| `--network wordpress-net`               | *Se conecta a la misma red (para que encuentre `wordpress-mysql`)*           |
| `-e PMA_HOST=wordpress-mysql`           | *Le dice a phpMyAdmin que el servidor MySQL está en ese contenedor*           |
| `-p 8080:80`                            | *Expone el puerto 80 del contenedor como 8080 en tu máquina*                  |


> **Figura 8-4-1.** Implementar el contenedor que permite administrar gráficamente la base de datos.
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 153145.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 153155.png" alt="drawing" width="800"/>

> **Figura 8-4-2.** Ver si phpMyAdmin corriendo en el navegador (localhost:8080)
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 153403.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 153429.png" alt="drawing" width="800"/>


 
**Paso 5:** Creación del contenedor WordPress
```bash
docker run -d --name wordpress-site --network wordpress-net -e WORDPRESS_DB_HOST=wordpress-mysql:3306 -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppass -p 8000:80 wordpress
```

| Opción                                               | Significado                                                        |
|------------------------------------------------------|--------------------------------------------------------------------|
| `--name wordpress-site`                              | *Nombre del contenedor WordPress*                                   |
| `--network wordpress-net`                            | *Se conecta a la misma red que MySQL*                               |
| `-e WORDPRESS_DB_HOST=wordpress-mysql:3306`          | *Dirección del servidor de base de datos*                          |
| `-e WORDPRESS_DB_NAME=wordpress`                     | *Nombre de la base de datos*                                        |
| `-e WORDPRESS_DB_USER=wpuser` y `WORDPRESS_DB_PASSWORD=wppass` | *Credenciales de acceso a MySQL*                         |
| `-p 8000:80`                                         | *Expone el sitio web WordPress en el puerto 8000*                  |


> **Figura 8-5-1.** Finalmente, se crea el contenedor WordPress, el cual será visible desde el navegador:
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 154111.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 154124.png" alt="drawing" width="800"/>

> **Figura 8-5-2.**Instalación inicial de WordPress (localhost:8000)
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 154206.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 154452.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 154518.png" alt="drawing" width="800"/>
 <img src="./../../Tools/Photos/1er-Semana-5/Captura de pantalla 2025-04-30 154701.png" alt="drawing" width="800"/>

## 9. Resultados esperados

Al finalizar la práctica, se obtuvieron los siguientes resultados:

- Acceso exitoso a la interfaz web de WordPress desde el navegador mediante la URL: `http://localhost:8000`.
- Visualización y administración de la base de datos MySQL desde phpMyAdmin en la URL: `http://localhost:8080`.
- Persistencia de los datos en el volumen creado para la base de datos, aún después de detener y reiniciar los contenedores.
- Comunicación exitosa entre los contenedores WordPress, phpMyAdmin y MySQL a través de la red personalizada `wordpress-net`.
  
  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/12Gb5MJWE1n1QDOJSKrgBs-D5jndHYhR8/view?usp=sharing

## 10. Bibliografía

- PostgreSQL: documentation. (s. f.). The PostgreSQL Global Development Group. https://www.postgresql.org/docs/
- Play with Docker. (s. f.). https://labs.play-with-docker.com/
- Microsoft. (s.f.). *Windows Subsystem for Linux Documentation*. Recuperado de [https://learn.microsoft.com/en-us/windows/wsl/](https://learn.microsoft.com/en-us/windows/wsl/)
- Docker Inc. (s.f.). Docker Documentation. Recuperado de https://docs.docker.com/
- WordPress Foundation. (s.f.). WordPress Support. Recuperado de https://wordpress.org/support/
- González, F. (2023). Guía de implementación de entornos web con contenedores. Universidad Sudamericana.
- dpage. (2024). phpMyAdmin documentation. Recuperado de https://www.phpmyadmin.net/docs/
