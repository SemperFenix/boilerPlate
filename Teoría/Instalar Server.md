# Server

## Instalación

1. Creamos una nueva carpeta en una ruta sencilla de acceder (por ejemplo, en el escritorio o en la carpeta raíz de VSCode).
2. Abrimos esa carpeta con vscode.
3. Ejecutamos npm init -y
4. Instalamos el server con `npm i -D json-server`
5. Abrimos el package.json y añadimos este script:

```json
    "start": "json-server --watch -p 5080 db.json",
```

6. Ejecutamos el script en el terminal con `npm run start`. Esto creará el archivo db.json en esa carpeta.

## Uso del server

1. Abrimos un nuevo terminal en nuestro proyecto.
2. Utilizando el comando cd navegamos hasta la carpeta donde hemos instalado el server:

    ```shell
      <!-- Si estuviera en el escritorio -->
      cd C:/Users/NombreDeTuUsario/Desktop
      ```

3. En ese terminal, ejecutamos `npm start`
4. Ya tenemos el server funcionando.
