# Cómo testear

Las clases abstractas se testean creando **en el archivo de test** una clase que extiende sus propiedades y es esa la que testeamos.

Los tipos y los interfaces no se testean porque no tienen implementaciones.

## Testeando componentes

Podemos utilizar la testing-library o [enzyme](https://enzymejs.github.io/enzyme/).

```typescript
import { Header } from "./header";
import { screen, Screen } from "@testing-library/dom"; // Nos dice que Did you mean to set the 'moduleResolution' option to 'node', or to add aliases to the 'paths' option?
// Así que editamos el archivo tsconfig.json como nos dice => mouleResolution = "node"
import "@testing-library/jest-dom"; // Nos proporciona matchers nuevos
import { Component } from "../component/component";

describe("Given Header component", () => {
  test("should first", () => {
    document.body.innerHTML = "<slot></slot>"; // Esto crea el punto de enganche para seleccionar con la clase. Puede ser la etiqueta que queramos.
    const mockTitle = "Test";
    const element = new Header("slot", mockTitle);
    expect(element).toBeInstanceOf(Component); // Totalmente irrelevante
    // const h1 = screen.getByText(/Holita/i) // Esto es una expresión regular y la i sirve para que busque ignorando case sensitive
    const h1 = screen.getByText(mockTitle); // Tenemos tres tipos de query de screen: get => algo que está en todo momento || query => elementos que pueden no estar
    // || find => para elementos asíncronos
    expect(h1).toBeInTheDocument();
    const element2 = new Header("slot");
    const h2 = screen.getByText(/Learning DOM/i);
    expect(h2).toBeInTheDocument();
  });
});
```

Es mejor si utilizamos la getByRole() ya que nos testea a la vez la accesibilidad. El rol de los distintos HTML tags los encontramos en mdn, dentro de la sección del tag

## Testear fetch

Para testear archivos que incluyen fetch, tenemos que _mockear_ esa función. Jest no la incorpora, ya que es una función de entorno Typescript.

  ```typescript
  // Esto mockea manualmente la devolución de una promesa
    global.fetch = jest.fn(()=>
    Promise.resolve({
      json: ()=> Promise.resolve*{rates:{ CAD: 1.42}}),
    })
    );
  ```

  ```typescript
    const pepito = jest.fn().mockImplementation()

    const juanito = () => { //Aquí va la implementación
    }
    pepito()
   ```

>Con `.mockResolvedValue()` podemos introducir el resultado de una promesa. **Así es como lo haremos, en vez de por el camino largo**.

Si queremos testear el error que da una función:

```typescript
global.fetch = jest.fn().mockedResolvedValue({json: jest.fn().mockResolvedValue({Datos que quiero simular}),
})
```

```typescript
const pepito = jest.fn().mockRejectedValue(new Error ('Hola'))

    const juanito = () => { //Aquí va la implementación
    }

    try
    const r = pepito()

    expect(()=> pepito()).toThrow() // Esto nos permite testear errores SÍNCRONOS

    expect(()=> pepito()).rejected()
```

Se recomienda leer [este artículo](https://www.leighhalliday.com/mock-fetch-jest).

## React - formularios

Tenemos tres elementos de test: get, query y find (find es asíncrono).

## Testear customHooks

Podemos utilzar [renderHook de la testing-library](https://kentcdodds.com/blog/how-to-test-custom-react-hooks), pero es un poco extraño de utilizar y no vamos a tener necesidad en general si nuestros componentes no son especialmente complejos.

Por otra parte, podemos crear una función que devuelve un fragmento de jsx (`<></>`)
