# React

## Qué es

React es un _framework_ que nos permite diseñar SPA (Single Page Application). React utiliza el _Virtual Dom_ para renderizar, aumentando mucho la velocidad respecto a si tuviera que modificar el DOM cada vez.

Para trabajar con React utilizaremos CRA (Create React App).

## Instalación

Ejecutamos el siguiente commando **sustituyendo `my app`** por el nombre de nuestra carpeta:

  ```git
  npx create-react-app my-app --template typescript
  ```

>## Cuidado
>
>No podemos instalar eslint ni jest encima de esta instalación. Ya viene instalado como se puede ver dentro del package.json.

## Estados

Un estado es una "foto" de cómo están mis datos en el momento actual. Conjunto de datos de la información en el momento actual. El estado es lo que va a cambiar entre una página y otra. React nos da una especie de contrato donde le "garantizamos" que el estado no va a cambiar y, de esa manera, cuando el estado cambie, react se encargará de actualizar la página y hacer el render correspondiente.

>Los estados parecen inmediatos, pero en realidad React tarda un poco en actualizar los estados. Esto da problemas a la hora de testear. Para poder ver por consola correctamente es necesario utilizar el useEffect.

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
