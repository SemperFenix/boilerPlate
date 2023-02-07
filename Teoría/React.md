# React

1. [Qué es](#id1)
2. [Instalación](#id2)
3. [Estados](#id3)
4. [Funciones](#id4)
5. [Estados](#id5)
6. [Hooks de react](#id6)

<div id="id1">

## Qué es

React es un _framework_ que nos permite diseñar SPA (Single Page Application). React utiliza el _Virtual Dom_ para renderizar, aumentando mucho la velocidad respecto a si tuviera que modificar el DOM cada vez.

Para trabajar con React utilizaremos CRA (Create React App).
</div>

<div id="id2">

## Instalación

Ejecutamos el siguiente commando **sustituyendo `my app`** por el nombre de nuestra carpeta:

  ```git
  npx create-react-app my-app --template typescript
  ```

</div>

>## Cuidado
>
>No podemos instalar eslint ni jest encima de esta instalación. Ya viene instalado como se puede ver dentro del package.json.

<div id="id3">

## Estados

Un estado es una "foto" de cómo están mis datos en el momento actual. Conjunto de datos de la información en el momento actual. El estado es lo que va a cambiar entre una página y otra. React nos da una especie de contrato donde le "garantizamos" que el estado no va a cambiar y, de esa manera, cuando el estado cambie, react se encargará de actualizar la página y hacer el render correspondiente.

>Los estados parecen inmediatos, pero en realidad React tarda un poco en actualizar los estados. Esto da problemas a la hora de testear. Para poder ver por consola correctamente es necesario utilizar el useEffect.

</div>

<div id="id4">

## Funciones

Las funciones de React reciben siempre un parámetro global denominado `props`. Esto es un objeto con tantas propiedades como sean necesarias.

```tsx
  export function Sample(props: {title:string, brand: string}) {
    const title: string = "Sample";
    return (
      <div className={title}>
        <p>
          <strong>{props.myTitle.toUpperCase()}</strong>
        </p>
      </div>
    );
  }
```

```tsx
root.render(
  <React.StrictMode>
    <App />
    <Sample brand="Lo que sea" myTitle="Desde fuera" />
  </React.StrictMode>
);
```

Esto lo utilizaremos para importar valores dentro de una función de React.

</div>

<div id="id5">

## Event Listener en React

```tsx
export function Counter() {
  let count = 0;
  const handlerClick = (incremento: number) => {
    count += incremento;
  };

  return (
    <div>
      <p>{count}</p>
      <button className="add" onClick={() => handlerClick(+1)}>
        ➕
      </button>
      <button className="minus" onClick={() => handlerClick(-1)}>
        ➖
      </button>
    </div>
  );
}
```

</div>

<div id="id6">

## Hooks de React

Cada hook tiene un funcionamiento diferente, hay 7 en total. Tres de ellos son fundamentales: useState, useEffect

### useState

Recibe un array de dos parámetros: el estado a cambiar y la función para cambiarlo.

```tsx
import { useState } from "react";

export function Counter() {
  const [count, setCount] = useState(0);

  const handlerClick = (incremento: number) => {
    setCount(count + incremento);
  };

  return (
    <div>
      <p>{count}</p>
      <button className="add" onClick={() => handlerClick(+1)}>
        ➕
      </button>
      <button className="minus" onClick={() => handlerClick(-1)}>
        ➖
      </button>
    </div>
  );
}
```

### useEffect

Con esto podemos ejecutar algo al mismo tiempo que se produce un cambio de estado. En el array de dependencias escribiremos lo que queramos "controlar" y, si esa dependencia cambia, se ejecutará el código dentro de la callback.

>El código dentro de la callback se ejecuta siempre una vez al inicio de la carga y, después, tantas veces como cambie cualquiera de sus dependencias

```tsx
  useEffect(() => {
    console.log(count);
  }, [count]);
```

>Si utilizamos useEffect con un array de dependencias vacío, ese código se ejecutará sólo una vez al principio de la página.

</div>

## Desestructuración de props

Para pasar props en React tenemos que desestructar la prop. Sólo podemos desestructurar al declarar una variable. Podemos quedarnos sólo con las partes que nos interesan de esa variable.

```typescript
const getData = () => 3
const x = getData() // x = 3

/* ============ */

const getData = () => ({a:3, b:4}) // Los paréntesis sirven para hacer el return de una arrow que es un objeto, para que no confunda las llaves de objeto con las llaves de return
}
const x = getData() // x = {a: 3, b: 4}

/* ============ */

const a = x.a
const b = x.b

// Esto es equivalente a:

const {a,b} = getData() // Esto crea dos variables con el mismo nombre de las propiedades que devuelve la función. Deben coincidir los nombres.
const {a: valor1, b: valor2} = getData() // Esto crearía las variables valor1 = a y valor2 = b

/* ============ */
const getData = (obj : {x: number, y: number}) => ({a: obj.x, b: obj.y})


const getData = ({x, y} : {x: number, y: number}) => ({a: x, b: y})

/* ============ */

const obj = {x: 3, y: 4}
const obj2 = {...obj, x: 5} // ... es el spread operator, que independiza las propiedades del objeto anterior.
// En este caso obj2 = {x:5, y:4}
```

## Componentes padres e hijos

En React los hijos se refieren a hijos de tipo HTML, no a propiedades extendidas. Hay dos maneras de que un componente contenga a otro:

1. Que un componente llame a otro desde su jsx.
2. Poner la llamada en jsx como si fuera HTML (composición de componentes // proyección de contenido).
        *Para esto, es necesario avisar a React de que lo vamos a colocar.
        * Necesitamos una prop especial que se llama "children".

Cómo hacerlo:

```jsx
import logo from "./logo.svg";
type HeaderProps = {
  children: JSX.Element;
};

export function Header({ children }: HeaderProps) {
  return (
    <header className="App-header">
      <img src={logo} className="App-logo" alt="logo" />
      <p>
        Edit <code>src/App.tsx</code> and save to reload.
      </p>
      <a
        className="App-link"
        href="https://reactjs.org"
        target="_blank"
        rel="noopener noreferrer"
      >
        Learn React
      </a>
      {children}
    </header>
  );
}
```

## Páginas

Una página es un componente más.

Las páginas las exportaremos como _default_. Esto se debe a los import Lazy.

El enrutamiento nos permite simular la navegación a través de páginas sin recargar realmente. Esto es algo propio de las SPA (Single Page Application).

React en sí mismo no puede enrutar, necesitamos una librería específica: `react router-dom`

Para utilizarlo, en index.tsx envolvemos App con `<BrowserRouter>`

Después, dentro de app creamos el elemento `<Routes>` y, dentro de éste, añadiremos el elemento `<Route>`. que tendrá como atributos `path= "pathname" element={<PageToLoad></PageToLoad>}`.

>Sólo con esto, aún no es suficiente para que sea SPA, ya que sigue recargando la página.

Para evitar esto, vamos a utilizar un componente de React llamado `<Link>`, que necesita un prop de tipo `to ="pathname"`, eliminando las etiquetas `<a>` de nuestro HMTL.

>Todo esto nos vale sólo cuando utilizamos ReactRouterDOM, hay otras maneras de llevar a cabo este tipo de proceso.

Este conjunto de elementos, lo vamos a meter dentro de un nuevo componente core que será el app router.

>Esto es lo que permitía hacer ReactRouterDOM hasta la versión 5. A partir de la versión 6 permite utilizar _lazy imports_ (loading diferido).

### Lazy imports

Este mecanismo lo que hace es importar el contenido la primera vez que se carga el elemento en lugar de cargar todo simultáneamente.

Esto lo hace a través de la importación condicional que introdujo JS.

Esto nos permite hacer importaciones sólo bajo determinadas circunstancias.

```jsx
const Home = lazy(() => import("../../../features/components/home/page/home"));
 // Home es una promesa hasta que lo envolvemos en lazy.
// Para poder importar de esta manera, tenemos que haber hecho export default.

export function AppRouter({ menuOptions }: AppRouterProps) {
  return (
    <Suspense>
      <Routes>
        <Route path="/" element={<Home></Home>}></Route>
        <Route path={menuOptions[0].path} element={<Home></Home>}></Route>
        ...
        </Suspense>)
}

```

Para el caso de que se intente entrar a una ruta que no corresponda con ninguna de nuestras páginas, podemos utilizar esta estructura:

    ```jsx
    <Route
      path={"*"}
      element={<Navigate to={"/"} replace={true}></Navigate>}
    ></Route>
    ```

El elemento Navigate nos sirve para que la ruta quede más limpia, el atributo replace sustituye la dirección errónea por el path que tengamos en el atributo "to".

## Usando los estados

Para inicializar un estado, usamos el `useState()`, si queremos cargar datos desde una API tenemos que utilizar `useEffect()` para que traiga los datos de forma asíncrona.

Use effect recibe dos parámentros, la callback que debe ejecutar y la función que dice cuándo hacerlo. Además, hay que decirle cuántas veces lo tiene que ejecutar.

Primero pinto vacío, después recojo los datos (useEffect) y vuelvo a pintar los datos.
