# Docker para Ambiente de Desarrollo Laravel
## Descripción
Este es mi primer Docker creado específicamente para facilitar el desarrollo dentro de Laravel. La imagen Docker incluye un servidor Apache, PHP, MySQL y todas las extensiones necesarias para ejecutar Laravel. Además, se instalan Composer y Git para gestionar dependencias y versiones.

## Instalación
Para utilizar esta imagen Docker, sigue los siguientes pasos:

## 1. Clonar el repositorio:
Crea una carpeta para tu proyecto (por ejemplo, /Users/diego/Documents/proyecto_x/) y clona este repositorio en esa carpeta.

## 2. Construir la imagen Docker:
Abre una terminal y navega hasta la carpeta de tu proyecto. Ejecuta el siguiente comando para construir la imagen Docker:

```bash
docker build -t imagen_proyecto_x .
```

## 3. Ejecutar el contenedor Docker:
Una vez construida la imagen, ejecuta el contenedor con el siguiente comando:

```bash
docker run --name docker_proyecto_x -p 8080:80 -v /Users/diego/Documents/proyecto_x/public_html:/var/www/html imagen_proyecto_x
```
Esto mapeará el puerto 8080 de tu máquina local al puerto 80 del contenedor y sincronizará tu carpeta de trabajo local con la del servidor Apache dentro del contenedor.



# Instalar Laravel en el servidor docker
Si recien comienzas tu proyecto, tendras que instalar laravel y para ello tendras que hacerlo dentro del docker, una vez que tengas instalado todo te recomiendo hacer una version en un repositorio github. Si en tu caso no necesitas instalar laravel aqui tendrias que clonar tu repositorio laravel para continuar trabajando.

## 1. Ingresar al docker por bash
```bash
docker exec -it docker_proyecto_x bash
```
docker_proyecto_x es el nombre de tu docker que se esta ejecutando

## 2. Ejecutar la instalacion de laravel usando composer que lo teniamos previamente cargado en el docker.
```bash
composer create-project --prefer-dist laravel/laravel proyecto_x
```
Remplazar proyecto_x por el nombre de tu proyecto.
Esta instalacion en el servidor docker se vera reflejada en la carpeta de tu maquina local donde estas trabajando porque se sincronizan.

*si todo marcha bien tu proyecto estaria en : http://localhost:8080/proyecto_x/public/index.php



# Activemos Mod_Rewrite
Este proceso hace que redireccionemos el trafico de localhost:8080 a la carpeta que /public de tu proyecto laravel para ingrese directamente sin necesidad de escribir toda la ruta completa.

## 1. Modificar apache con nano
```bash
nano /etc/apache2/sites-available/000-default.conf
```
Esto te abrira un editor nano para modificar el archivo de configuracion de apache2

## 2. Modificar DocumentRoot
DocumentRoot /var/www/html/proyecto_x/public
Para guardar y salir : Ctrl+x - Enter - Y

## 3 Reiniciar apache2
service apache2 restart
*TALVEZ TENGAS QUE REINCIAR TU DOCKER.

## 4. Intenta ingresar
http://localhost:8080/

## Modo de Uso
Después de ejecutar el contenedor, puedes empezar a trabajar en tu proyecto Laravel dentro de la carpeta /Users/diego/Documents/proyecto_x/public_html en tu máquina local. Los cambios que realices se reflejarán automáticamente en el servidor Docker, accesible en http://localhost:8080. 


