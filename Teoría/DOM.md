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

## Linkando archivos al HTML

Creamos nuestra plantilla en HTML, podemos linkear archivos TS:

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script type="module" src="./src/day2.ts"></script>
  <title>Document</title>
</head>
<body>
  <div id="root"> </div>

</body>
</html>
```

```typescript
console.log("dia2");
const root = document.querySelector("#root") as HTMLDiv; // Esto puede ser más genérico, por ejemplo con HTMLElement, sirve para asegurarle al código que este elemento no va a ser null
const headerTemplate = `
  <header class="header">
      <h1>Learning Dom</h1>
      <p>Segundo día</p>
    </header>
`;

// El método insertAdjacent permite introducir elementos, HTML o sólo texto
// Revisar la documentación para ver sus argumentos
root.insertAdjacentHTML("afterbegin", headerTemplate);

// Como mockTasks es un array de Task, item será de tipo Task
let tasksTemplate = '<div class="lista">';
mockTasks.forEach((item) => {
  tasksTemplate += `<p>
id:${item.id}, title: ${item.title}, responsible: ${item.responsible}, isCompleted:${item.isCompleted}
<button data-id='${item.id}'>🗑 ${item.id}</button>
</p>
</div>`; // El atributo data-id es un atributo que creamos para poder referirnos al botón desde JS, ya que los id que comienzan por número dan problema desde el punto de vista semántico
});

root.insertAdjacentHTML("beforeend", tasksTemplate);

const handlerDelete = (event: Event) => {
  const element = event.target as HTMLButtonElement;
  const id = Number(element.dataset.id); // Con esto estamos haciendo referencia al campo data-id del botón. Si ponemos el nombre de la variable entre {} cogen el dato por desestructuración, no es necesario, pero nos da el clg más sencillo de leer.
  console.log("click"); // Al tener el id, ya no necesitaríamos el console.dir()
  // Si queremos hacer un console.log de un elemento HTML usamos console.dir
  console.dir(id); // Esto nos mostrará en la consola la información del Elemento clickado

  const data = mockTasks.filter((item) => item.id !== id); // Convertimos id en number al declararlo porque todo elemento que viene de HTML es un string
  console.log(data);
  document.querySelector("lista")!.innerHTML = "";
  renderList(data); // Llamamos a la función para que "actualice" la página con los nuevos valores que han cambiado
};

const buttons = document.querySelectorAll("button"); // Devuelve una nodeList, por eso el nombre es button-S
buttons.forEach((item) => item.addEventListener("click", handlerDelete)); // Esto nos añade un eventListener para todos los botones del archivo
console.log(data); // Nos devuelve un array de datos
// El nombre de los handler podemos llamarlos de dos maneras: 1º siguiendo el tipo de evento que disparan (click, hover...), 2º refiriendo a la función que tienen (delete, send...)
```

Podemos convertir todo esto en una función:

```Typescript
const renderList = (data: TaskStructure []) => {
  let taskTemplate = ''
  data.forEach((item)...) // De esta manera parametrizamos la entrada de datos
}
```

> Realmente, no vamos a organizar nuestro código de esta manera, sino a separarlo en grupos con los que será mucho más cómodos con los que trabajar (**componentes**). Todos los frameworks de front-end trabajan usando componentes, por lo que comprender estas estructuras básicas será fundamental.
