# Cosas

Las funciones capaces de recibir como parámetro otra función (_callback_) se denominan _**HOF**_ (High Order Function).

Cuando una callback utiliza un método es necesario bindearlo a quien lo llama (`this.handleSubmit.bind(this)`). Esto evita que se recoja sin contexto, lo cual genera problemas cuando se quiere utilizar lo que se ha recogido.

El bind permite que cuando llamemos a un método desde otro componente/archivo, ejecute el método en el contexto del padre, conservando toda la información.
