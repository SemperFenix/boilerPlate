# MongoDB

Es una BBDD no relacional que nos aporta un entorno online donde podemos alojar nuestra BBDD (Atlas)

Mongo nos va a dar un link que incluirá nuestra contraseña, esto lo pondremos en el archivo `.env`

## DEBUG

Debug es una herramienta para la consola de VSCode que depende de variables de entorno que le daremos a través del package.json.

El nombre de la variable será DEBUG = \<nombre que queramos\>

En loas archivos importamos createDebug from debug y, en cada archivo le daremos un nombre distinto (relacionado con la variable de entorno), para saber de dónde viene el debug.

## Autenticación

[JSON Web Tokens](http://jwt.io)
