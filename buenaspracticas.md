# Buenas prácticas no evidentes

## Cuando separar funciones en archivos

- Si las funciones que contiene no tienen coherencia entre ellas, mejor separarlas en archivos distintos, si no, es correcto que todas estén en el mismo archivo.

- Si lo que se van a crear son varias clases, siempre van en archivos separados.

## IIFE

Funciones invocadas inmediatamente:

```javascript
((num) => {
  doWhatever;
})(35);
// Llamamos a la función sin haberle dado nombre, sólo si es la función inmediatamente anterior.
```
