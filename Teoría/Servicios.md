# Servicios

Creamos la carpeta services dentro de src; dentro de esta carpeta, creamos otra llamada repository. Dentro, creamos el archivo task.storage.repo.ts.

```typescript
const key = localStorage.getItem(); // Nos pide un nombre y trae del local storage cualquier elemento almacenado con esa key.
localStorage.setItem(); // Nos pide la clave y el valor de la clave para almacenarlo.
localStorage.removeItem(); // Nos pide la clave para eliminar la entrada (incluyendo su valor).
// Estos métodos almacenan un string (y lo devuelven al ser llamados), pero si los estructuramos cuando los introducimos, podremos utilizar un parse
// (o equivalente) para estructurarlos en forma de objeto

export class TaskStorageRepo {
  constructor(public storeName: string = "Tasks") {}

  getTasks(): TaskStructure[] {
    const data = localStorage.getItem(this.storeName);
    if (!data) return []; // Aquí podemos devolver el mockArray (TASKS)
    this.setTasks(TASKS);
    return JSON.parse(data);
  }

  setTasks(tasks: TaskStructure[]) {
    const data = JSON.stringify(tasks);
    return localStorage.setItem(this.storeName, data);
  }

  removeTasks() {
    localStorage.removeItem(this.storeName);
  }
}
```

Esto es capaz de hacerlo el navegador, la consola de Node no.

## Inyección de dependencias

En el index le decimos que en new Task introduzca una instancia de la nueva clase. Inyectar dependencias es introducir un valor que viene de fuera.

```typescript
new Tasks("main", new TaskStorageRepo());

// En la definici'on de Tasks tendemos que modificar el valor del par'ametro que recibe a public repogit ad: TaskStorageRepo
```
