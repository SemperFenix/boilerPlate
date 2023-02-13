# Cosas

Las funciones capaces de recibir como parámetro otra función (_callback_) se denominan _**HOF**_ (High Order Function).

Cuando una callback utiliza un método es necesario bindearlo a quien lo llama (`this.handleSubmit.bind(this)`). Esto evita que se recoja sin contexto, lo cual genera problemas cuando se quiere utilizar lo que se ha recogido.

El bind permite que cuando llamemos a un método desde otro componente/archivo, ejecute el método en el contexto del padre, conservando toda la información.

Las instancias de una nueva clase deben ir envueltas en un try-catch. La estructura try-catch coge cualquier error lanzado bien por nuestro componente o bien por las llamadas o métodos que ejecute éste. Dentro del catch debemos dar el feedback al usuario. Este feedback se suele dar a través de un _modal_.

## Modal

Un modal es un pop-up que bloquea la pantalla hasta que se cierra. Es un componente más.

Se crea a través de la etiqueta HTML `<dialog></dialog>`, que es una de las dos etiquetas interactivas.

## Patrón singleton

Conseguir una sola instancia de una llamada (memonización), lo hacemos a través de useCallback o useMemo.
