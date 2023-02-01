# Tipado de objetos

```typescript

type MenuOption = {
  {label: string;
  path: string;}
}

const menuOptions: MenuOption[] = [{label: 'Inicio', path:'/home'}, {label: 'Tareas', path:'/tasks'}, {label: 'Acerca de', path:'/about'}]

type MenuOptions = typeof menuOptions // Crea un tipo que infiere el del array menuOptions
```
