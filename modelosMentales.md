# Modelos mentales de objetos

Las propiedades de un objeto, son otro objeto. Si nosotros referenciamos la propiedad de un objeto al valor de la propiedad de otro, cuando modifiquemos una, modificaremos ambas.

Si intentamos acceder a una propiedad de objeto que no existe, nos devuelve undefined; si intentamos entrar a una propiedad de una propiedad que no existe, nos devuelve un TypeError (cannot read properties of undefined).

Para evitar errores de tipo utilizamos el operador **?** (conditional chaining) -> Sólo hace lo siguiente si lo anterior es truthy.

```javascript
console.log(sherlock.age?.foo);
```

> Si existe .foo continúa, si no existe, no.

En los objetos si el valor y la clave de la propiedad coinciden, se escribe sólo una vez:

```javascript
let capitan = "Pepe";
const ship = { capitan }; // Esto equivale a const ship = {capitan: capitan}
```

Cuidado a la hora de "copiar" objetos:

```javascript
const double = (array) => {
  for (let i = 0; i < array.length; i++) {
    array[i] = 2 * array[i];
  }
};
const aData = [1, 3, 5];
double(aData);
console.log(aData);
// Result [2, 6, 10] => El array original ha mutado.
```

```javascript
const double = (array) => {
  const internalData = array;
  for (let i = 0; i < array.length; i++) {
    internalData[i] = 2 * internalData[i];
  }
  return internalData;
};

const aData = [1, 3, 5];
double(aData);
console.log(aData);
// Result [2, 6, 10] => El array original ha mutado => No se copia con el operador de asignación
```

```javascript
const double = (array) => {
  const internalData = [...array]; // La desestructuración sí permite clonar el array (separa los valores del array) y con los [] los metemos dentro de un array
  for (let i = 0; i < array.length; i++) {
    internalData[i] = 2 * internalData[i];
  }
  return internalData;
};

const aData = [1, 3, 5];
double(aData);
console.log(aData);
// Result [1, 3, 5] => El array original no ha mutado
```

```javascript
const double = ([...array]) => {
  for (let i = 0; i < array.length; i++) {
    array[i] = 2 * array[i];
  }
};
const aData = [1, 3, 5];
double(aData);
console.log(aData);
// Result [1, 3, 5] => El array original NO ha mutado.
```

También se puede hacer esta clonación usando JSON

```javascript
const obj = { name: "Pepe", age: 22 };

console.log(obj);
console.log(JSON.stringify(obj)); //Convierte un objeto en una string con estructura "JSON" (también se conoce como serializar)

JSON.parse(JSON.stringify(obj)); // => Devuelve un objeto a partir de una estructura ("opuesto" a stringify)

// Estos dos métodos (JSON.stringify y JSON.parse) son fundamentales para el intercambio de información en red. Siempre que se envía información a un servidor, se hace en forma de string, para que esté estructurado y al recibirlo se pueda trabajar con él, se utiliza el JSON.stringify.
```
