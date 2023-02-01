# Cómo testear

Las clases abstractas se testean creando **en el archivo de test** una clase que extiende sus propiedades y es esa la que testeamos.

Los tipos y los interfaces no se testean porque no tienen implementaciones.

## Testeando componentes

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
