# Firebase

Los archivos multimedia en general, son archivos multimedia. Suelen tener tamaños muy grandes como para almacenarse en una DB como la de mongo. Por tanto, nosotros en la DB guardaremos un string que nos indicará dónde está el archivo en cuestión.

Los HTML input de tipo file se guardan en un apartado especial llamado _Files_ (console.dir(formElement)).

Para guardarlo hay dos opciones:
1.Subirlo a nuestro servidor Node (podemos utilizar el fs de node).
    -
Para que Node sea capaz de gestionar los archivos, utilizaremos un middleware llamado `Multer`.
2.Almacenar las fotos en algún servicio de hospedaje de fotos que permita recibir código y devolver una URL
    - Firebase
        - Basado en DB no relacionales
    - Supabase // Versión libre de Firebase
        - Basado en Postgrase (DB relacional)
    - Cloudinary // Especializado en guardar fotos

## Usando Firebase

Para utilizar firebase en nuestro proyecto seguimos las instrucciones que nos da Firebase al registrar una aplicación.

Aún así sería conveniente mover algunos datos al fichero .env (apiKey, Ids...).

Una vez dentro, entramos en todas las opciones de compilación y seleccionamos Storage.

Al acceder, le damos a comenzar y podremos elegir "modo producción" o "modo de pruebas". Si utilizamos el modo producción habría que mirar cómo funcionan las reglas de seguridad / permisos de Firebase.

El modo prueba permitiría a cualquiera con la URL acceder a los datos guardados. De momento nos sirve.

Para ver el código que necesitamos para entrar desde VScode a nuestra colección de archivos, podemos mirar la documentación (<https://firebase.google.com/docs/storage/web/start?hl=es&authuser=0>).

Funcionaremos a través de referencias.
