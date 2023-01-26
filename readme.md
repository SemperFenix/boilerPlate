# Boiler plate

- Añadir archivos base:

  - .editorconfig
  - .gitignore (con contenido node_modules)
  - readme.md
  - Ejecutar en el terminal:

    ```git
    npm init
    ```

- Ejecutar en el terminal:

  ```git
    git init
  ```

- Hacer el primer commit para poder pushear el repositorio a remoto:

  ```git
  git add .
  git commit -m'Initial commit'
  ```

- Crear el repositorio en github y ejecutar las tres líneas de código para sincronizar nuestro local con el remoto:

  ```git
  git remote add origin `url del repositorio`
  git branch -M main
  git push -u origin main
  ```

-
