# Usando clases

Cuando dentro del constructor le ponemos la definición de ámbito (public, private o protected) no hace falta explicitar los this.arg:

```typescript
class Character {
  // Podemos asignar posibilidades
  // public isAlive: 'vivo' | 'muerto' | 'resucitado'
  isAlive: boolean = true;
  constructor(public name: string, public family: string, public age: number) {}

  talk(phrase: string) {
    return phrase;
  }
}

const pj1 = new Character("Iñigo", "Montoya", 32); // Nos devuelve el objeto {name: Iñigo, family: Montoya, age: 32, isAlive: true}
```

Cuando extendemos una propiedad, los argumentos correspondientes no necesitan ser declarados como públicos.

```typescript
class Druid extends Character {
  constructor(
    name: string,
    family: string,
    age: number,
    public nature: string
  ) {
    super(name, family, age);
  }
}
```

Podemos apuntar propiedades a otros objetos:

```typescript
class Servant extends Character {
  constructor(name: string, family: string, age: number, public master: Druid) {
    super(name, family, age);
  }
}

const wood = new Druid("elrond", "Magister", 109, "wood");
const serv1 = new Servant("Pedro", "Periquez", 25, wood);
const serv2 = new Servant(
  "Jose",
  "Ramon",
  20,
  new Druid("Lorem", "Ipsum", 205, "text")
);

const text = serv2.master;
text.age += 20;
console.log(text); // {name: Lorem, family: Ipsum, isAlive: true, age: 205, element: text}
```
