# Formularios

Los formularios son la única entidad capaz de utilizar el atributo `onsubmit`. Esto permite pasar de campo en los formularios con el tabulador y que al pulsar enter se active el efecto de _submit_.

Un botón dentro de un formulario es automáticamente de tipo submit.

Los atributos `id` y `name` de la etiqueta `input` en formularios vienen de cuando se gestionaban solos (el `id` nos permitirá enlazarlo al `label`), sin embargo nosotros queremos gestionar el formulario a través de javascript.

Cuando el formulario ejecuta el evento submit recarga la página, lo cual gestionando la creación del HTML desde JS no nos interesa.

Para evitarlo, podemos capturar el evento submit con `preventDefault`.

En los formularios, la información de todos los campos se almacena en el objeto `form` en propiedades numéricas. Por lo tanto, podríamos acceder a los campos con:

`event.target[0]`
