# Usando TypeScript

Typescrip nos añade el tipado a JS. Podemos utilizar un tipado estático o un tipado fuerte:

```typescript
  // Tipado estático
  let foo = 9
  foo = "Pepe" // Lo podemos hacer, pero nos sugerirá que no

  // Tipado fuerte mediante notación de tipos
  let bar: string;
  bar = 23 // Dará un error

  // Podemos compaginar ambos métodos
  let zoo: boolean = true // Algunos linters no lo permiten

 const s: number = 62

  // Podemos mezclar más de un tipo

  let boo: boolean | null

  // Podemos obligar a un array a tener un tipo de dato concreto

  const aData: Array<number> = [] // Esta forma no es tan buena práctica y algunos linters no la cogen.


  const aData2: number[] = []

  const aData3: (number | string)[] =
```

<!-- Vamos a convertir un archivo de JS a un archivo de TS:

**Archivo JS**

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


```typescript

class Person {
    name;
  age;
  private isLive;
  constructor(public name: string, age: number) {
    this.name = name;
    this.age = age;
    this.#isLive = true;
  }

  // Al usarlo dentro de "class", automáticamente crea la función en el objeto prototipo de la función Person

  greetings() {
    console.log(`Hola, soy ${this.name}`);
  }
}

class Student extends PersonClass {


  constructor (name:string, age:number, course: string){
    super
  }
} -->

En Typescript también podemos utilizar interfaces. Son variaciones de los types. Es una especie de molde con el que comparar los objetos que se crean (_todos los objetos de este **tipo** tienen que tener las propiedades..._). Hay gente que lo define como un _contrato_ (quienes asuman este interfaz se comprometen a...), si se incumple, TS nos mostrará advertencias:

```typescript

interface Live = {
  name: string
  specie: string

  greetings () => {
    return 'Hola'
  }
}

class Person implements Live {
  // Si no ponemos esto, nos dará un aviso
  private isLive: boolean
  species:string
  constructor(public name: string, age: number) {
    this.isLive = true
    this.species = 'human'
  }
}
```

> Los interfaces van asociados a items, que son objetos generados a través de una clase.

Los interfaces nos permiten hacer **_duck typing_**, es decir, si algo parece un pato y se mueve como un pato, es un pato (cambiar pato por tipo).

Además, podemos incorporar varios interfaces dentro de una clase.

```typescript
class Dog implements Live {
  constructor(public name: string, public species: string) {}
}

const x: Live = { name: "Pedro", species: "perro" };
const y: Person = new Person();
const z: Person = new Dog(); // Dará error
```

Además, en lugar de _interfaces_ podemos usar _tipos_ (`type`), que funcionarán aproximadamente igual. De momento, consideramos que son lo mismo.

> Los interfaces sólo transmiten el aspecto del objeto (propiedades), las clases extendidas, sin embargo, transmiten también los métodos implementados en la clase padre.

Si queremos que no pueda crearse un objeto de la clase padre comenzaremos por `abstract`. Si una clase abstracta no tiene métodos, se convierte en un interfaz.

```typescript
export abstract class Character ...
```

## Mock de los datos

Dentro de la carpeta src creamos la carpeta `mock`. Esto lo utilizaremos porque no tenemos datos reales que recibir, por lo que utilizaremos los de esta carpeta para testear nuestro trabajo.

Dentro de esta carpeta nos creamos un archivo `data.ts`.

```typescript
// MOCK_TASKS => Esta forma se utilizaba antes de la implementación de const para señalizar var que no debían cambiar.
export const mockTasks = [
  { id: 1, title: "Algo", responsible: "Pepe", isComplete: false },
  { id: 2, title: "Otro Algo", responsible: "Luisa", isComplete: false },
];

export const mockCharacters: Character[] = [
  new King("Joffrey", "Baratheon", 15, 1),
  new Fighter("Jaime", "Lannister", 38, "Sword", 8),
  ,
];

//No puedo crear dentro del array un item que referencia a otro que aún no ha sido creado, por lo que lo hacemos desde fuera.
mock.Characters.push(
  new Counselor("Tyrion", "Lannister", 25, mockCharacters[1]),
  new Squire("Bronn", "None", 35, mockCharacters[1], 3)
);
```

Creamos una carpeta `models` donde guardamos nuestros archivos a testear y creamos un archivo donde creamos un tipo para poder tipar el array del archivo mock.

```typescript
export type TaskStructure = {
  id: number;
  title: string;
  responsible: string;
  isCompleted: boolean;
};
```

Esto nos permite tipar el array creado en el archivo `mock`, restringiendo y garantiando que los elementos son exactamente como nosotros queremos.

```typescript
export const mockTasks: TaskStructure[] =...
```
