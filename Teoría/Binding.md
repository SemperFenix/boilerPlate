# Binding

```javascript
'use strict' // Se activa por defecto al trabajar por m'odulos
// Patrones de invocacion

// En JS las funciones tienen execution scope, es decir, su valor depende de cuando se ejecutan, no de cuando se declaran

function foo (){
console.log(this)
}

// Patron function

foo() // Return Object [global] si no estamos en strict mode

// Patron method

const obj = {
    name: 'Prueba',
    method: foo
}

obj.method() // Return obj

// Patron constructor

new foo() // Return foo {} (Objeto de la "clase" foo)

// Patron apply

const obj2 = {
    name: 'Prueba2'
}

foo.apply(obj2) // Return obj2
// apply es la version anterior de bind
// Nos permite asignar manualmente el valor de "this"
// La funcion se "coloca" dentro de obj2, por eso this coge sus propiedades

// Bind crea la vinculación de una función para que se ejecute en el contexto en el que se la llame. Es un "apply a futuro". Es decir, bind se vincula dinámicamente.

setTimeout(foo, 1000) // Return {setTimeout} => This entiende que es setTimeout

//==============//

const bar = () => {
    console.log(this)
}

bar() // Return {} . This hace referencia a la propia función, ya que las arrow functions utilizan lexical scope, es decir, están vinculadas al momento en que se declaran.

setTimeout(bar, 1000) // Return {} . El valor de this no cambia ya que depende del momento en que se declara.

new bar() // => No tiene sentido ya que el "this" de una arrow no puede cambiar. Return error
```
