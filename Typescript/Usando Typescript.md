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
