# Flux

Flux es un modelo organizativo del código que mejora la escalabilidad, el testeo y la predictabilidad de nuestra aplicación.

El objetivo de Flux es evitar la bidireccionalidad entre la vista y el estado de los datos. Para eso, el modelo se basa en que Acción -> Dispatcher -> Store -> View -> Action (cíclico).

## Action

La acción encapsula los eventos y los traduce a lógica de negocio (le da un nombre reconocible).

>Una acción es un **objeto** y tiene que tener **como mínimo** la propiedad `type`, indicando lo que hace (su nombre). Además, puede tener una propiedad llamada payload (o data), que contendrá un objeto con la información correspondiente.

Una acción es un objeto que se activa a través de eventos sistémicos. Los eventos los puede disparar el usuario o una API (backend).

## Dispatcher

Es un solo elemento que contiene callbacks, encargándose de mandar la información procesada de action a store (el estado).

## Store

Contiene el estado de la aplicación, lógica y solicita los datos.

**No es un modelo**, contiene modelos. Puede haber uno o varios stores (en Redux sólo habrá uno).

## React (o view)

## Patrón Flux

La `acción` le pasa información al `dispatcher`, éste procesa la información a través de un _addEventListener_ y ejecuta el _callback_ correspondiente (handler). El _handler_ modifica la información como corresponda y se la manda al `store` y éste lo envía para que se refleje en la `view`.

El _usuario_ sólo tiene acceso a `view`, donde al hacer algo activa un evento, ejecutando de nuevo el patrón.

Cuando se crea el patrón flux es tremendamente complejo de implementar utilizando vanilla JS o la versión de React disponible en aquel momento. Debido a esto, se crea Redux.

## Redux

Es una librería que permite montar una aplicación utilizando el patrón Flux. En Redux, las callbacks para el dispatcher se almacenaban en un componente llamado _Reducer_ (de ahí el nombre).

En ese momento, React implementó los Hooks y Redux implementó los suyos propios (useSelect y useDispatcher).

En esta competencia, React creó el hook `useReducer`, que permitió dejar de utilizar la librería Redux.

Ante esto, Redux añadió una pieza nueva, el RTK (Redux Tool Kit).
