# DOM

Document Object Model. El DOM no es más que un Objeto de javascript lleno de propiedades que Modelan nuestro Documento HTML.

Podemos acceder a estas propiedades desde un archivo Javascript utilizando `document.`.

## Localizar elementos

Para acceder a los elementos utilizaremos `document.querySelectorAll()`, que nos devuelve un NodeList, que es un elemento parecido a un array pero sin muchas propiedades de éstos. Esto nos sirve para

```typescript
const element = document.querySelector(); // Devuelve un elemento
const elements = document.querySelectorAll(); // Devuelve un array de elementos
```

A un _querySelector_ le puedo pasar como parámetro un _selector_ (como los de CSS) entre comillas.

```typescript
const element = document.querySelector("p"); // Devuelve el primer elemento p del HTML
const elements = document.querySelectorAll(".red"); // Devuelve un NodeList con todos los elementos de clase .red del HTML
elements.forEach(); // Al ser un NodeList, podemos aplicarle algunos de los métodos de los arrays
```

```typescript
const elements = [...document.querySelectorAll(".red")]; // Devuelve un array normal con los elementos de clase .red
Array.from(document.querySelectorAll(".red")); // Esto sería equivalente
```

## Modificar elementos

Para acceder al contenido de los elementos HTML, utilizaremos `element.innerHTML`

```typescript
const element = document.querySelector("p") as HTMLParagraphElement; // Esto es una **aserción de tipo**, indica que sabemos que va a tener un valor.
element?.innerHTML = ""; // Utiliza el operador ? porque element podría ser null, si hemos hecho la aserción de tipo, el operador ? no es necesario.

// ==============
// Si queremos asegurarnos de que nunca lo coge si es null, hacemos una guarda (programación defensiva). Tanto esto como la aserción de tipo nos protegen de errores desesctructurados (los que da el sistema).

if (!element) throw new Error("");
element.innerHTML = "";
```

> El HTML de nuestras webs se va a generar a partir de JS, nuestro index.html contendrá sólo la estructura básica de enganche, que normalmente será `<div type="app">` o algo similar.

Dentro de un innerHTML podemos poner todo lo que queramos, incluyendo etiquetas HTML.

```typescript
element.innerHTML = `Esto está en <strong>${variable}</strong>`; // Podemos utilizar las backsticks para introducir variables dentro del contenido.
```

Si queremos sustituir un elemento del HTML por otra cosa utilizaremos `element.outerHTML`:

```HTML

<body>
  <div id ='root'>
  <p id="p1"></p>
  <p id="p2"></p>
  </div>
  </body>
```

```typescript
const element1 = document.querySelector("#p1"); // Devuelve el primer elemento p del HTML
const element2 = document.querySelectorAll("#p2");

element1.innerHTML = "Escribo esto";
element2.outerHTML = `ESTO ESTÁ EN OUTER`;
```

```HTML

<body>
  <div id = 'root'>
  <p id="p1">Escribo esto</p>
  ESTO ESTÁ EN OUTER
  </div>
  </body>
```

> No obstante, estos métodos no los utilizaremos apenas, ya que existe otro método mejor: **insert**

### insertAdjacentHTML

```typescript
element1.insertAdjacentHTML(); // Nos preguntará por la posición donde queremos colocar el contenido, por lo que sustituye a los otros.
```

## Creando un sitio dinámico

Hasta ahora, todo lo visto eran webs estáticas, si queremos que el usuario interaccione con la página, ésta debe ser dinámica.

### addEventListener

Este método es fundamental para escuchar las peticiones del usuario.

```typescript
// Localizar el elemento

const button = document.querySelector("button"); // Lo encontramos con el selector que queramos (clase, id, selectores combinados...)

const handlerClick = () => {
  element1.innerHTML = "Escribo esto";
  element2.outerHTML = `ESTO ESTÁ EN OUTER`;
};

// AddEventListener pide como argumentos un texto (evento) y un listener (una función)

button.addEventListener("click", handlerClick);
```
