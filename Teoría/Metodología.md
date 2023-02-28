# Metodología

## Patrones

Soluciones conocidas a situaciones variadas.

## Principios

Los principios nos dan unas guías de trabajo para llevar a cabo buenas prácticas que mejoren la calidad de nuestro código (código funcional !== buen código).

Principios SOLID:

- Single responsability
  - Cada clase/módulo... es responsable de una sola parte del programa // Una parte del código sólo puede encargarse de que cambie una cosa.
- Open closed:
  - Las funcionalidades deben estar abiertas para la expansión pero cerradas a la modificación (lo que funcionaba debe seguir funcionando)
- Liskov substitution
  - Nuestas aplicaciones tienen que estar construidas de forma que podamos intercambiar distintas partes (adheridas a ciertos "contratos" - interfaces -.)
- Interface segregation
  - Tenemos que tener tantos interfaces como sean necesarios para poder crear elementos similares pero diferentes
- Dependency inversion / injection
  - Loos detalles deben provenir de abstracciones. No declaramos dentro, inyectamos desde fuera

### Objetivos

- Código más mantenible
- Código flexible (fácil de cambiar)
- Código capaz de ampliarse
- Código más comprensible

SOLID es una *herramienta*, si complica el código de forma innecesaria no merece la pena usarlo.
