# Charla Moisés

GitHub: moisesrj97

## Arquitectura de software

En estas arquitecturas las carpetas se basan en conceptos.

Dentro de cada carpeta siempre tendremos las mismas tres carpetas: Dominio, aplicación e infraestructura.

En estas carpetas tendremos los modelos. En este caso, los modelos los creamos como clases.

Tendremos también un interfaz, que va a definir las operaciones que podemos hacer sobre la entidad a la que nos estemos refiriendo. Esto va a estar dentro de un repositorio.

Creamos una interfaz de repo para la entidad.

La infraestructura contiene el repo en sí, mientras que el dominio sólo contiene los "modelos".

En aplicación tendremos los casos de uso. Estos casos de uso son clases que se encargan de cada acción que se pueda ejecutar sobre el usuario.

El server, por ejemplo, va a tener sólo infrastructure debido a que la mayoría de servidores tienen demasiadas diferencisa entre ellos como para poder crear un dominio.

Podemos crear el servidor como una clase donde el constructor contendrá app, config y routes.
