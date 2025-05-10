# Práctica Servidor Web


## 1. Título  
**Implementación de un entorno WordPress con MySQL y phpMyAdmin utilizando Docker Compose**

## 2. Tiempo de duración  
**120 minutos (2 horas)**

## 3. Fundamentos

En esta práctica se explora el uso de Docker Compose para implementar un entorno de desarrollo compuesto por tres servicios principales: WordPress, MySQL y phpMyAdmin. Cada uno de estos servicios se ejecuta en su propio contenedor, lo que permite una gestión modular, reutilizable y aislada de los componentes de la aplicación web.

**Docker** es una plataforma que permite desarrollar, enviar y ejecutar aplicaciones dentro de contenedores. Un contenedor es una unidad estándar de software que empaqueta el código y todas sus dependencias para que la aplicación se ejecute de manera rápida y confiable en diferentes entornos. Por su parte, **Docker Compose** es una herramienta que permite definir y ejecutar aplicaciones multicontenedor usando un archivo YAML.

**WordPress** es un sistema de gestión de contenido (CMS) de código abierto que facilita la creación y administración de sitios web. **MySQL** es un sistema de gestión de bases de datos relacional muy utilizado en aplicaciones web, y **phpMyAdmin** es una herramienta de administración para MySQL a través de una interfaz web amigable.

Mediante el archivo `docker-compose.yml`, se definen los servicios, las redes que los conectan, los volúmenes para persistencia de datos y las variables de entorno necesarias. Además, se asignan puertos específicos para acceder a WordPress (puerto 8080) y phpMyAdmin (puerto 8081) desde el navegador.

<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 225953.png" width="800" />
  <br>
  Figura 1. Representación de Docker.
</div>

<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 225917.png" width="700" />
  <br>
  Figura 2. Servidores con Docker.
</div>

 
## 4. Conocimientos previos

- Comandos básicos de Linux.
- Uso de terminal de comandos.
- Fundamentos de Docker: contenedores, imágenes, volúmenes y redes.
- Estructura y sintaxis de archivos YAML.
- Navegación y configuración básica de servicios web.
- Uso de herramientas como phpMyAdmin para administrar bases de datos.


## 5. Objetivos a alcanzar

- Implementar contenedores con WordPress y MySQL mediante Docker Compose.
- Configurar phpMyAdmin como interfaz gráfica para gestionar la base de datos.
- Definir una red personalizada y volúmenes persistentes en Docker.
- Automatizar la creación del entorno web con un archivo `docker-compose.yml`.


## 6. Equipo necesario

- Computador con sistema operativo Windows, Linux o Mac.
- Terminal o consola de comandos mejor opción Linux.
- Docker instalado (versión 24.0 o superior).
- Editor de texto (Visual Studio Code, Nano, Vim, entre otros).
- Navegador web moderno (Google Chrome, Firefox, Edge).
- Conexión a internet estable para la descarga de imágenes desde Docker Hub.

## 7. Material de apoyo

- Documentación oficial de Docker Compose: https://docs.docker.com/compose/
- Documentación oficial de WordPress (https://wordpress.org/support/)
- [Guía de Informe](https://github.com/maguaman2/informe-tendencias)
- Documentación oficial de phpMyAdmin: [https://docs.phpmyadmin.net/](https://docs.phpmyadmin.net/)
- Guía video colocado en la plataforma del Instituto: https://drive.google.com/file/d/1e0VJH8LXYfFsjNq7xtIZ6AgekXdXhCJa/edit
- Guía de comandos básicos de Linux.

## 8. Procedimiento

**Paso 1:** Crear la carpeta del proyecto

```bash
mkdir docker-yml
# Entrar a la carpeta:
cd docker-yml
```

 **Paso 2:** Crear un archivo docker-compose.yml

```bash
tuch docker-compose.yml
# Para verificar el archivo creado:
ls
```

> **Figura 8-2-1.**
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 221830.png" alt="drawing" width="800"/>

 
**Paso 3:** Editar el archivo con el siguiente contenido
```bash
# Vamos dentro de  Visual Studio Code
code .
# Comprobamos si toda la informacion agregada esta en el archivo
cat docker-compose.yml
```

> **Figura 8-3-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222420.png" alt="drawing" width="800"/>
 
> **Figura 8-3-2.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222401.png" alt="drawing" width="500"/>

**Paso 4:**  Iniciar los servicios definidos
```bash
docker compose up -d
```

> **Figura 8-4-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222547.png" alt="drawing" width="800"/>

**Paso 5:** Verificar que los contenedores estén activos
```bash
docker compose ls
docker compose ps
```
> **Figura 8-5-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 232047.png" alt="drawing" width="800"/>

**Paso 6:** Acceder a los servicios a través del navegador
```bash
# Wordpress
http://localhost:8080
# phpmyAdmin
http://localhost:8081
```
> **Figura 8-6-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 222721.png" alt="drawing" width="800"/>
 
> **Figura 8-6-2.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 224536.png" alt="drawing" width="800"/>

**Paso 7:** Ingresar a Wordpress
```bash
# User
FrankGC
# Password
franks123@suda
```
> **Figura 8-7-1.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 224728.png" alt="drawing" width="800"/>
 
> **Figura 8-7-2.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 224751.png" alt="drawing" width="800"/>
 
> **Figura 8-7-3.** 
 <img src="./../../Tools/Photos/2do-Semana-6/Captura de pantalla 2025-05-08 224942.png" alt="drawing" width="800"/>

## 9. Resultados esperados

Al finalizar la práctica, se obtuvieron los siguientes resultados:

- El servicio WordPress fuese accesible mediante el puerto 8080 mostrando la interfaz inicial de instalación. 
- phpMyAdmin funcionase correctamente en el puerto 8081, permitiendo gestionar la base de datos creada en MySQL.
- Los contenedores se comunicasen correctamente mediante la red personalizada definida.
- Los datos persistieran a través de los volúmenes, incluso si se reiniciaban los contenedores.
  
  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/19HMTFUnXDiodwtK5vzHwSk-hxH73Pl9a/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (s.f.). Docker Documentation. Recuperado de https://docs.docker.com/
- WordPress Foundation. (s.f.). WordPress Support. Recuperado de https://wordpress.org/support/
- González, F. (2023). Guía de implementación de entornos web con contenedores. Universidad Sudamericana.
- dpage. (2024). phpMyAdmin documentation. Recuperado de https://www.phpmyadmin.net/docs/
- «Docker compose». (2025, 28 abril). Docker Documentation. https://docs.docker.com/compose/
