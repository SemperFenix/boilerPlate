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

## Entendiendo las Clases en JS

---

Javascript tiene un mecanismo que se denomina _**relación prototípica**_, esto hace que las propiedades de los distintos objetos se creen en un almacén común, siendo parte de todos los objetos creados. Por lo tanto, todos los objetos disponen de una propiedad oculta de sistema **\_\_proto\_\_** . Si asignamos una propiedad de esta manera:

```javascript
let human = { teeth: 32 };
let gwen = {
  __proto__: human, // Hacemos que gwen tenga también todas las propiedades de human
  age: 19,
};
gwen.__proto__human;
console.log(gwen.teeth); // Output 32
```

Los _proto_ **no son bidireccionales**. Podemos crear un objeto padre con las propiedades que queremos que los demás elementos hereden y las llamaremos con `__proto__: nombreDelPadre`.

Esto nos permite crear árboles de descendencia:

```javascript
let mammal = { hair: true };
let human = { teeth: 32 };
human.__proto__ = mammal;
let gwen = {
  __proto__: human, // Hacemos que gwen tenga también todas las propiedades de human
  age: 19,
};
gwen.__proto__human;
console.log(gwen.teeth); // Output 32
console.log(gwen.hair); // Output true
```

Además, para los descendientes JS utiliza el **_shadowing_**, es decir, si modificamos una propiedad heredada dentro de un objeto, JS prima el valor concreto (el valor asignado en el objeto).

```javascript
let mammal = { hair: true };
let human = { teeth: 32 };
human.__proto__ = mammal;
let gwen = {
  __proto__: human, // Hacemos que gwen tenga también todas las propiedades de human
  age: 19,
};
gwen.__proto__human;
gwen.teeth = 30;
console.log(gwen.teeth); // Output 30
console.log(gwen.hair); // Output true
```

El método `.hasOwnProperty` nos permite preguntar al objeto si la propiedad le pertenece o es heredada.

A pesar de todo, este mecanismo de \_\_proto\_\_ no se utiliza, ya que es algo más interno del sistema.

> Para utilizar la herencia, utilizaremos `Object.create(objeto prototipo)`.

```javascript
let mammal = { hair : true }
let human = Object.create(mammal)
human.teeth: 32
let gwen = Object.create(human)
let gwen = { age : 19 }
gwen.teeth = 30
console.log(gwen.teeth) // Output 30
console.log(gwen.hair) // Output true
.
```

> **Realmente no vamos a utilizar este tipo de asignaciones**, pero nos sirve para comprender cómo funcionan las clases dentro de JS.

Todos los objetos tienen una propiedad \_\_proto\_\_ que apunta a un "objeto" padre. Para finzalizar esta cadena, existe un objeto _"tapón"_ (_Objeto Prototipo_) que su proto apunta a null.

El _Objeto Prototipo_ tiene además otras propiedades (los métodos de instancia de los objetos).

A este objeto podemos acceder y podríamos añadirle la propiedad que quisiéramos (`nombre.__proto__.propiedad = "valor"`), haciendo que a partir de ese momento todos los objetos contuvieran esa propiedad. Es una **mala práctica** y se denomina `Polución del prototipo` (_Polluting the Prototype_).

> Los métodos de objeto no son más que propiedades del objeto prototipo cuyo valor es una función concreta.

## Creando objetos

### Método literal

```javascript
const obj = {}; // Crea un objeto vacío
const objChild = Object.create(obj); // Crea un objeto que hereda todas las propiedades de obj
```

### Patrón factory

Esto nos permite crear objetos con las condiciones iniciales, propiedades, etc. que nosotros queramos.

```javascript
function createFoo() {
  // To do...
  return {};
}

const arrowCreate = () => ({});
```

### Patrón de ejecución

```javascript
function bar() {
  console.log('Soy bar)
}

Cuando una propiedad de un objeto apunta a una función, lo denominamos **método**

// Uso: patrón método
const obj = { tururu: bar, } // El nombre de la propiedad siempre va a ser un string

obj.bar() // Cuando una propiedad de un objeto apunta a una función, lo denominamos método
```

### Patrón constructor

Este patrón hace lo siguiente:

1. Crea un objeto
2. Lo usa como `this` dentro de la función
3. Retorna el objeto
4. Modifica el proto al objeto prototype de la función.

```javascript
function bar() {
  // Lo que haga la función
}

new bar();
```

---

---

> Las clases son funciones a las que llamamos con la instrucción **`new`**

---

---

## Usando el patrón constructor

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const p3 = new Person("Luisa", 34);
const p4 = new person("María", 28);

console.log(p3, p4); // Person {name: Luisa, age: 34} Person {name: María, age: 28}
```

> Los objetos creados con un constructor tienen un parámetro que identifica la función a través de la cual se han construido.

---

Las funciones son objetos y, como tal, también apuntan a un _objeto prototype_ propio de la función (cada una apunta al suyo) y es **éste** quien apunta al **_Objeto Prototype_** (que apunta a null).

> Los objetos creados a través de una función apuntan **al mismo objeto prototipo que la función**, **NO** al _Object Prototype_

---

> ## IMPORTANTE
>
> El elemento `Object` en JS es una función cuyo objeto prototipo es el _Object prototype_ al que apuntan todos los objetos.

---

---

<div align ="center">
Los objetos creados de esta manera tienen una propiedad llamada `constructor` que apunta a la función que lo ha creado.</div>

---

---

### Creando los métodos

Para crear métodos podemos aprovecharnos del objeto prototipo al que apunta la función. Para acceder a él lo llamamos con .prototype:

```javascript
Person.prototype.greetings = function () {};
```

De esta manera los métodos no se almacenan en cada objeto creado a través del constructor, sino que sólo se encuentran en el prototype y podemos acceder a ellos gracias a la herencia (pues todos los objetos creados de esta manera apuntan a ese objeto prototipo).

## Cómo utilizar el método constructor en la práctica

Para utilizar este método constructor utilizamos una herramienta que es:

```javascript
class Person {
  // Se pueden declarar aquí las propiedades
  name;
  age;
  #isLive; // La almohadilla indica que la propiedad es privada
  constructor(name, age) {
    this.name = name;
    this.age = age;
    this.#isLive = true;
  }

  // Al usarlo dentro de "class", automáticamente crea la función en el objeto prototipo de la función Person

  greetings() {
    console.log(`Hola, soy ${this.name}`);
  }
}
```

> De cara a trabajar, cada clase irá en su **propio archivo** que exportaremos e importaremos donde lo necesitemos.

> Las propiedades privadas sólo se pueden modificar desde un método de la clase.
>
> ## No tienen importancia en front-end

Podemos hacer que una clase herede el constructor y métodos de otra clase:

```javascript
class Student extends Person {
  course;
  constructor(nae, age, course) {
    super(name, age); // Le pasa a la clase padre los argumentos para su constructor
    this.course = course;
  }

  greetings() {
    super.greetings();
    console.log(`Estudio ${this.course}.`);
  }
}

const s1 = new Student("Juan", 25, "Angular");

s1.greetings(); // Output: Hola, soy Ramón. Estudio Angular.
```

> No se puede extender más de una clase.
