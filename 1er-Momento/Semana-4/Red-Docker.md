# Práctica: Implementación de contenedores Docker: MySQL y phpMyAdmin en red personalizada


## 1. Título  
**Persistencia de datos en PostgreSQL usando contenedores y volúmenes Docker**

## 2. Tiempo de duración  
**120 minutos (2 horas)**

## 3. Fundamentos

Docker es una plataforma de contenedores que permite empaquetar aplicaciones y sus dependencias en unidades portables. En esta práctica se utilizaron contenedores de **MySQL**, un motor de bases de datos relacional de código abierto, y **phpMyAdmin**, una herramienta cliente para la administración visual de bases de datos MySQL y MariaDB.

La creación de una red personalizada en Docker permite que varios contenedores se comuniquen entre sí de forma aislada del resto de la red del host. Gracias a este concepto, es posible establecer comunicación entre contenedores utilizando el nombre del contenedor como hostname.

**MySQL** proporciona almacenamiento estructurado, mientras que **phpMyAdmin** facilita su administración vía web, evitando la necesidad de interactuar únicamente por línea de comandos.

Durante el desarrollo de la práctica, se aplicaron conocimientos sobre comandos básicos de Docker, tales como `docker network create`, `docker run`, `docker ps`, `docker exec`, entre otros.

<div align="center">
  <img src="./../../Tools/Photos/1er-Semana-3/1_Ub4SunP72TpHuqyQuwCPWw.jpg" width="500" />
  <br>
  Figura 1. Persistencia de datos con volúmenes Docker.
</div>

Esta práctica está dividida en dos partes:

- La primera sin volumen, donde se comprueba la pérdida de datos al eliminar el contenedor.
- La segunda con volumen, donde se verifica que los datos persisten.

 
## 4. Conocimientos previos

Para desarrollar correctamente esta práctica, se requiere que el estudiante tenga conocimiento de:

- Comandos en terminal o consola (`docker`, `ps`, `rm`, etc.)
- Conexión a bases de datos usando herramientas como DataGrip o pgAdmin
- Conceptos básicos de bases de datos relacionales (crear bases, tablas, registros)
- Uso de Docker y sus conceptos principales: imágenes, contenedores, volúmenes


## 5. Objetivos a alcanzar

- Implementar contenedores Docker con PostgreSQL.
- Conectar herramientas de administración a bases de datos dentro de contenedores.
- Comprobar el comportamiento de los datos sin volumen.
- Asociar un volumen al contenedor y verificar la persistencia.
- Documentar el proceso con evidencia.



## 6. Equipo necesario

- Computador con Windows 10 o superior (o Linux/Mac equivalente).
- Docker Desktop instalado (v20.10 o superior).
- Cliente de base de datos como DataGrip, pgAdmin o DBeaver.
- Conexión a internet.
- Terminal o consola habilitada.


## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Documentación de PostgreSQL](https://www.postgresql.org/docs/)
- [Guía de Informe](https://github.com/maguaman2/informe-tendencias)
- Guía de comandos básicos de Linux.
- Guía video colocado en la plataforma virtual del Instituto https://drive.google.com/file/d/13lwPiwJhDIXRYozfBBqYqVWaXaVPA1pI/view

## 8. Procedimiento

### Parte 1: Base de datos sin volumen

**Paso 1:** Crear un contenedor PostgreSQL sin volumen.

```bash
docker -v
docker run --name server_db1 -e POSTGRES_PASSWORD=1234 -p 5435:5432 -d postgres
```
> **Figura 8-1-1.** Comprobar si esta instalado docker y ejecutar comando
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 150643.png" alt="drawing" width="800"/>
 
> **Figura 8-1-2.** Verificar si el contenedor esta ejecutandose
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 160929.png" alt="drawing" width="800"/>

 
**Paso 2:** Conectar un administrador de base de datos DataGrip al contenedor server_db1
```bash
 localhost:  5435
 usuario:    postgres
 contraseña: 1234
```
> **Figura 8-2-1.** Revisar conexión 
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 160817.png" alt="drawing" width="500"/>
 
**Paso 3:** Crear una base de datos test y dentro de ella una tabla customer.
```bash
CREATE DATABASE test;
```

> **Figura 8-3-1.** Crear base de datos test en consola
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 161230.png" alt="drawing" width="800"/>

 ```bash
CREATE TABLE customer (
  id SERIAL PRIMARY KEY,
  fullname VARCHAR(100),
  status BOOLEAN
);
```

> **Figura 8-4-1.** Creamos la tabla **customer**
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 162802.png" alt="drawing" width="800"/>
 
**Paso 4:**   Insertar un registro de prueba.
```bash
INSERT INTO customer (fullname, status) VALUES ('Franks González', true);
```
> **Figura 8-4-1.** 
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 162857.png" alt="drawing" width="800"/>

**Paso 5:** Verificar que los datos existen.
```bash
SELECT * FROM customer;
```
> **Figura 8-5-1.** 
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 162928.png" alt="drawing" width="800"/>

**Paso 6:**  Eliminar contenedor
```bash
docker rm 565
```
> **Figura 8-6-1.** 
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 163215.png" alt="drawing" width="800"/>

**Paso 7:**  Volver a crear el contenedor con el mismo nombre, y verificar que la base de datos test ya no existe.
```bash
docker run --name server_db1 -e POSTGRES_PASSWORD=1234 -p 5435:5432 -d postgres
```
> **Figura 8-7-1.** Verificar si el contenedor se creo con otro ID 
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 163352.png" alt="drawing" width="800"/>

> **Figura 8-7-2.** Ver si los datos no se conservaron
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 163632.png" alt="drawing" width="800"/>



### Parte 2: Base de datos con volumen

**Paso 1:** Crear un volumen.
```bash
docker volume create pgdata
```
> **Figura 8-1-1.** Editar con información del Instituto
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 164603.png" alt="drawing" width="800"/>

> **Figura 8-1-2.** Crear un contenedor usando el volumen.
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=1234 -p 5436:5432 -v pgdata:/var/lib/postgresql/data -d postgres
```
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 164804.png" alt="drawing" width="800"/>

> **Figura 8-1-3.** Verificar el contenedor en Docker
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 164815.png" alt="drawing" width="800"/>

**Paso 2:**  Conectar un administrador de base de datos DataGrip al contenedor server_db2
```bash
 localhost:  5436
 usuario:    postgres
 contraseña: 1234
```
> **Figura 8-9-1.** Revisar conexión
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 165042.png" alt="drawing" width="500"/>
 

**Paso 3:**  Repetir el proceso: crear la base test, la tabla customer, y registrar datos.
```bash
CREATE DATABASE test;
```
> **Figura 8-3-1.** Crear base de datos test
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 165234.png" alt="drawing" width="800"/>
 
```bash
CREATE TABLE customer (
  id SERIAL PRIMARY KEY,
  fullname VARCHAR(100),
  status BOOLEAN
);
```

> **Figura 8-3-2.** Crear tabla customer en base de datos test
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 165455.png" alt="drawing" width="800"/>
 
```bash
INSERT INTO customer (fullname, status) VALUES ('Samantha Murillo', true);
```

> **Figura 8-3-3.** Registrar datos a la tabla
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 165540.png" alt="drawing" width="800"/>
 
 ```bash
SELECT * FROM customer;
```

> **Figura 8-3-4.** Ver datos guardados
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 165638.png" alt="drawing" width="800"/>


**Paso 4:** Eliminar contenedor server_db2
```bash
docker stop d9a  =  Detener
docker ps -a     =  Revisar
docker rm d9a    =  Eliminar
```
> **Figura 8-4-1.** Detener, revisar y eliminar contenedor server_db2
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 170136.png" alt="drawing" width="800"/>

 > **Figura 8-4-1.** Verificar conexión que este perdida
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 170203.png" alt="drawing" width="800"/>


**Paso 5:** Volver a crear el contenedor con el mismo volumen
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=1234 -p 5436:5432 -v pgdata:/var/lib/postgresql/data -d postgres
```
> **Figura 8-5-1.** Editar con información del Instituto
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 170203.png" alt="drawing" width="800"/>

**Paso 5:** Verificar que los datos persisten.

> **Figura 8-5-1.** Ver  la tabla y su registró
 <img src="./../../Tools/Photos/1er-Semana-3/Captura de pantalla 2025-04-19 170420.png" alt="drawing" width="800"/>

## 9. Resultados esperados

- Se implementaron contenedores PostgreSQL correctamente con y sin volúmenes.
- Se logró la conexión desde DataGrip a los contenedores utilizando las credenciales del entorno.
- Sin volumen, los datos insertados en la base `test` se perdieron al eliminar el contenedor.
- Con volumen (`pgdata`), los datos persistieron incluso después de eliminar y recrear el contenedor.
- Se documentó todo el proceso con capturas de pantalla y se redactó el informe siguiendo la plantilla.

  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/109Zl1GZlASSyH5Dj9RvkdaQh_P1ynPc0/view?usp=sharing

## 10. Bibliografía

- PostgreSQL: documentation. (s. f.). The PostgreSQL Global Development Group. https://www.postgresql.org/docs/
- Play with Docker. (s. f.). https://labs.play-with-docker.com/
- Official Ubuntu Documentation. (s. f.). https://help.ubuntu.com/
- Microsoft. (s.f.). *Windows Subsystem for Linux Documentation*. Recuperado de [https://learn.microsoft.com/en-us/windows/wsl/](https://learn.microsoft.com/en-us/windows/wsl/)
