# just-another-docker-php-env
Ambiente de desarrollo en Docker y Docker Compose para PHP y Laravel.

*El ambiente de desarrollo en Docker cuenta con los siguientes servicios: MySQL, PHP-FPM, Nginx*

---

## Pre requisitos

Para poder levantar este entorno de desarrollo se deben tener instalados en la PC lo siguiente:

1. Docker y Docker Compose(v2).
2. En el caso de Windows, se necesita WSL2 y Ubuntu >= 22.04(Microsoft Store).
3. Git

---

## Instalar el ambiente de desarrollo

1. Clonar el repo del ambiente de desarrollo: **git clone https://github.com/krsrk/just-another-docker-php-env.git**
2. Navegar a la carpeta del proyecto: **cd just-another-docker-php-env**
2. Copiar el archivo .env: **cp .env.example .env**
3. Cambiar los valores del archivo .env
4. Clonar e instalar tu codigo en el directorio ./src.
2. Regresar al directorio raíz del proyecto y ejecutar: **docker compose build**
7. Levantar el ambiente: **docker compose up -d**.
8. Revisar el estatus de los servicios: **docker compose ps**

---

## Variables de Entorno(.env)

El ambiente cuenta con un archivo de configuración(.env) el cual tiene variables que se pueden configurar facilmente, de acuerdo a las necesidades de la maquina y red del usuario. A continuación se explican detalladamente:

### Configuración de Base de datos.

1. **MYSQL_VERSION**: Versión de la imagen de Docker de MySQL. Solo puede tener los siguientes valores listados en esta pagina: https://hub.docker.com/_/mysql. Por default viene cargada la version 8.0.
2. **DB_FORWARD_PORT**: Puerto externo del contenedor de MySQL al Host(Pc). Se tiene que revisar que la maquina donde se instala tenga el puerto libre indicado. Por default viene el puerto 3312.
3. **DB_DATABASE**: Nombre de la base de datos. Por default cuando se crea el servicio, crea la base de datos "test"
4. **DB_PASS**: Password del usuario del server de MySQL. Por default viene con el valor: P@ssw0rd.
5. **DB_ROOT_PASS**: Password de root en el server de MySQL. Por default viene con el valor: P@ssw0rd.
6. **DB_USER**: Usuario del server de MySQL. Por default viene con el valor: appdev

---

### Configuración de la Aplicación

1. **APP_USER**: User del Host(Pc). Se tiene que poner el mismo usuario del Host(PC) sino se tendran problemas de permisos en los archivos.
2. **APP_UID**: Id del Usuario en el Host.
3. **APP_DIR**: Directorio del codigo fuente instalado en /src. Por default viene el directorio "app"
4. **APP_FORWARD_PORT**: Puerto externo del contenedor de Nginx(Servidor Web) al Host(Pc). Se tiene que revisar que la maquina donde se instala tenga el puerto libre indicado. Por default viene el puerto 8088.
5. **RUNTIME_VERSION**: Versión del runtime de PHP. Solo puede tener los valores actuales de los tags de las imagenes de Docker de PHP-FPM. Por lo regular solo soporta versión 7.4>=. Por default estara activada la versón mas actual de PHP.
---

## Ejemplo de instalación de Laravel

Se asume que ya se tiene clonado el codigo fuente en la carpeta /src del ambiente de desarrollo y levantado el ambiente de desarrollo, con eso seguiremos los siguientes pasos:

1. Navegamos hasta el directorio de la app, ej: **cd src/app**
2. Copiamos el archivo de configuración de Laravel: **cp .env.example .env**
3. Modificamos los valores de .env para que se comunique con los servicios de Docker.
4. Instalamos las dependencias de Laravel: **docker compose exec app composer install**
5. Generamos el app key de Laravel: **docker compose exec app php artisan key:generate**
6. Ejecutamos migraciones(Si es necesario): **docker compose exec php artisan migrate**
7. Instalamos las dependencias de Node: **docker compose exec app npm install**
8. Compilamos los assets de Js: **docker compose exec app npm run dev**

---
