# Asincronía

La asincronía es el concepto donde se recogen los eventos que suceden en un tiempo concreto en lugares diferentes

```javascript
function makeAsync() {
  setTimeout(() => {
    const data = 232;
    return data;
  }, 1000);
}

const x = MakeAsync(); // Output 'undefined'
```

Esto no puede funcionar nunca. Para conseguir la información de una función asíncrona, utilizamos una callback.

```javascript
function makeAsync(callback) {
  setTimeout(() => {
    const data = 232;
    callback(data);
  }, 1000);
}

makeAsync((x) => {
  console.log(x * 2);
});
```

Si comenzamos a anidar de esta manera, terminaremos teniendo un _callback hell_, que es una esctructura compleja de hacer, de sentender y, sobre todo, de mantener.

Para evitar eso, utilizaremos las promises.

Cuando en JS tenemos una función que detiene el programa, se llama al _bucle de eventos_, este bucle busca en el procesador la capacidad para ejecutar el código asíncrono.

Javascript es un lenguaje monohilo, por lo que el programa principal pasa por el procesador con prioridad absoluta (no hay procesos paralelos), el bucle de eventos se lleva la ejecución de los procesos asíncronos al final de la ejecución del código síncrono.

> Asincronía en JS no significa aplazar en el tiempo, sino pasar por el bucle de eventos. Primero ejecuta las funciones síncronas y, después, ejecuta las asíncronas (incluso si su delay es 0).

## Promesas

Las promesas son objetos (de la clase `new Promise`) que se resuelven a futuro. Tienen incluido un método para el caso de que no se pueda ejecutar la función.

```javascript
function makeAsync() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const n = Math.random();
      const data = 232;

      if (n > 0.5) {
        resolve(data);
      } else {
        reject(new Error("Bad luck"));
      }
    }, 1000);
  });
  {
  }
}

makeAsync() // Al ser una instancia de Promise, tiene disponibles los métodos then y catch, asociados a resolve y reject respectivamente.
  .then((x) => {
    console.log(x * 2);
  })
  .catch((error) => {
    console.log(error.message);
  });
```

A menos que programemos algo para IE6 (o alguna mierda similar), lo haremos siempre con promesas.

## Async

A partir de ES2018 se introdujo la palabra reservada `async`, esto convierte cualquier función en _Promise_. El uso de `async`sin más no es nada habitual.

## Await

Normalmente, lo que vamos a utilizar es `async` en conjunto con la palabra reservada `await`; esto nos permite simular una función asíncrona como si fuera una función normal:

```javascript
function makeAsync() {...} // Dentro contiene la estructura new Promise

async function main() {
  try {
    const x = await makeAsync(); //
    console.log(x * 2);
  } catch (error) {
    console.log(error.message);
  }
}
```

En ES2022 podemos utilizar un awake sin haber declarado un async:

```javascript
try {
  const x = await makeAsync(); // se denomina await de máximo nivel (Top Level Await)
  console.log(x * 2);
} catch (error) {
  console.log(error.message);
}
```

> En estos momentos, jest no entiende esta estructura de programacion, por lo que no podriamos testear la funcion.
