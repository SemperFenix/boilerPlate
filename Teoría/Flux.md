# Flux

Flux es un modelo organizativo del c'odigo que mejora la escalabilidad, el testeo y la predictabilidad de nuestra aplicación.

El objetivo de Flux es evitar la bidireccionalidad entre la vista y el estado de los datos. Para eso, el modelo se basa en que Acción -> Dispatcher -> Store -> View -> Action (cíclico).

## Action

La acción encapsula los eventos y los traduce a lógica de negocio (le da un nombre reconocible).

>Una acción es un **objeto** y tiene que tener **como mínimo** la propiedad `type`, indicando lo que hace (su nombre). Además, puede tener una propiedad llamada payload (o data), que contendrá un objeto con la información correspondiente.

## Dispatcher

Es un solo elemento que contiene callbacks, encargándose de mandar la información procesada de action a store (el estado).

## Store

Contiene el estado de la aplicación, lógica y solicita los datos.

**No es un modelo**, contiene modelos. Puede haber uno o varios stores (en Redux sólo habrá uno).

## React (o view)
