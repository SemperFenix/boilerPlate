# Redux

Redux es una herramienta pensada para resolver proyectos de gran tamaño y complejidad. En nuestros proyectos será sobreingeniería.

## Qué es

Redux es un contenedor de estados predecible. Es una librería que simplifica la aplicación del modelo Flux a una aplicación.

## Cómo usarlo

Redux hace "lo mismo" que `useReducer`, pero desde dos hooks diferentes:

- useAppSelector => Devuelve el estado (que se encuentra dentro del store -> En la propiedad "reducer" (mal elegido el nombre) )
- useAppDistapch => Devuelve el dispatcher
