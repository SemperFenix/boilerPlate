# Servidores

Un servidor es un programa que permite la comunicación con otro programa.

Recibe `requests` y da `responses`.

Un servidor puede estar escrito en cualquier lenguaje de programación.

## Instalaciones

Para crear nuestro backend tendremos que instalar como hacíamos al prinvicpio, instalando typeScript, etc.

## Variables de entorno

Desde JS podemos acceder al proceso que ejecuta node, para ello podemos utilizar la "variable" `process`. A través de esto, podemos acceder a las variables del entorno con `process.env._nombre_de_variable_`. Process.env es un objeto.

En el package.json podemos añadir variables de entorno en el script directamente (el de start:nodemon, en este caso). Esto tiene un problema, y es que las instrucciones de terminal no son iguales para todos los sistemas, por lo que no podríamos asegurar que el comando funcionara en distintas máquinas.

Para resolver este problema utilizamos `cross-env`. Tras instalarlo, añadiremos en el script `cross-env` justo antes de la variable a declarar.

Para asignar las variables que ejecutaremos con el cross-env creamos un archivo con nombre `.env`, en este archivo pondremos las variables que irán con el nombre en mayúsculas. Además, tampoco puede haber espacios. El archivo .env tiene que ir en la raíz.

Si necesitamos una variable de entorno desde Netlify la podemos añadir como variable local en Netlify (en el servicio que necesitemos usar tendremos la opción de alguna manera).

Además, tendremos que crear un archivo `sample.env` con las instrucciones necesarias para utilizar el fichero .env

Para utilizar el archivo .env necesitamos instalar por npm el `dotenv`.

Dotenv lo vamos a utilizar para las variables críticas (pass, user, datos sensibles...)

Los servers tienen un método `on` que es el equivalente al `addEventListener` de HTML.

render railway
