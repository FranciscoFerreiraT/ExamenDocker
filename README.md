# ExamenDocker

Utiliza docker para poner en marcha Prestashop según esta imagen.

Describe el proceso en un documento Readme. Utiliza capturas para demostrar el funcionamiento en el navegador.

Se valorará:

El uso de docker-compose

Base de datos enlazados al PhpStorm

Claridad en la explicación

## Creacion del docker compose

Lo primero que hariamos es la creacion de un archivo de configuración docker-compose

```bash
version: '3' 

services: # Aquí definimos los servicios que compondrán nuestra aplicación.

  prestashop: # Definición del servicio 
    image: prestashop/prestashop # La imagen Docker que se utilizará para este servicio
    ports: # Mapeo de puertos
      - "8080:80"
    environment: # Variables de entorno necesarias para configurar PrestaShop.
      - PS_DOMAIN=localhost # Configura el dominio
      - DB_SERVER=db # Indica que el servidor de la base de datos está en el servicio "db".
      - DB_NAME=prestashop # Nombre de la base de datos.
      - DB_USER=root # Usuario de la base de datos.
      - DB_PASSWD=root # Contraseña del usuario de la base de datos.
    networks: 

  db: # Aqui se ejecutara la base de datos MySQL
    image: mysql:5.7 # La imagen de la base de datos
    environment: # Variables de entorno necesarias para configurar la base de datos MySQL.
      - MYSQL_ROOT_PASSWORD=root # Contraseña del usuario root de MySQL.
      - MYSQL_DATABASE=prestashop # Nombre de la base de datos.
    volumes: # Configuramos un volumen para al macenar los datos
      - prestashop-db-data:/var/lib/mysql
    networks: 

networks:
  prestashop-network: 

volumes: 
  prestashop-db-data: 

```
Una vez hecho el docker compose hacemos un ``` docker compose up -d``` para levantar el contenedor de docker

<img width="567" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/a61718c1-a8a5-4fdd-bbd6-b9fbac1f4a3b">

Una vez hecho esto podemos ver que los contenedores de la base de datos y del prestashop estan levantados y funcionando

<img width="202" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/7272f18f-5777-40c0-81fe-ca76b89f2477">

## Instalacion del prestashop

Una vez el contenedor esta levantado tenemos que dirigirnos al puerto que le asignamos a nuestro prestashop, en este caso : ```http://192.168.56.1:8080 ```

<img width="968" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/3a9baa42-1860-4d05-a011-bb3773513dbb">


Seguimos rellenando la configuracion de la tienda con nuestros datos

<img width="899" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/a9da21a0-2238-4103-95c7-4c57e536e46b">

Creacion de nuestra base de datos

<img width="903" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/0b6185d9-dcd7-4a02-abef-09fcde6df744">

Ahora comienza la instalacion y configuracion de la tienda con los datos dados anteriormente

<img width="830" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/55999659-5f20-4a36-abb4-44f1dbaadedb">

Una vez finalice la instalacion ya estaria acabada

<img width="935" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/ba7a551f-5239-4471-9c90-5ff09eb9d0fe">


## Demostracion funcionamiento de prestashop

Una vez la configuracion finalice ya podriamos ver la interfaz de usuario  de nuestra tienda ```Dam2Shop``` con articulos de prueba

### Interfaz de usuario

<img width="910" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/c3366998-892f-4d94-820a-39c731a2e5bf">

### Interfaz administrador

Por razones de seguridad tenemso que hacer algunas modificaciones en nuestro volumen

<img width="587" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/96956ccd-7040-4d7d-b115-1e21b467fc7d">

#### Modificaciones
çLo primero es entrar en nuestro volumen de prestashop

<img width="818" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/16cfa237-c6c7-407f-b207-6e7cd5e13361">

Y eliminar la carpeta install 

<img width="342" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/97b795b1-95cb-4357-83d5-1e4c7100a965">

Y luego renombrar la carpeta admin a la que nos decia prestashop

<img width="551" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/9e45c448-e0f3-432d-9924-e687fb523ebc">

Una vez hecho esto ya podriamos acceder a nuestra interfaz de adminstrador

<img width="699" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/fbf041a0-8cd4-4c3e-9ffd-d62fa287e28a">

Y aqui tendriamos una vista de nuestra interfaz administrador con nuestro unario logeado

<img width="1231" alt="image" src="https://github.com/FranciscoFerreiraT/ExamenDocker/assets/92456485/a86a64f5-583d-4a79-af71-c2361cd35e6b">








