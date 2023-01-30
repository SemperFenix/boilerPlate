# BoilerPlate rápido de un repo

1.  Crear carpeta con `git init`
2.  Crear package.json con `npm init`
3.  Añadir .gitignore, .editorconfig y readme.
4.  Instalar todo lo necesario para el proyecto (en nuestro caso): `npm i -D husky eslint eslint-config-prettier jest @types/jest ts-jest jest-environment-jsdom @types/node @babel/plugin-transform-modules-commonjs typescript`
5.  Ahora comenzamos la configuración:

          1. `npx eslint --init`

          2. `npx husky install`

          - Creamos los huskys que necesitemos con `npx husky add .husky/nombre-del-husky

          3. Editamos el archivo package.json añadiendo las instrucciones necesarias:

    ```json
    {
      "name": "boiler",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "start": "tsc -w",
        "test": "jest --watchAll --coverage",
        "test:prod": "jest --coverage",
        "prepare": "husky install"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "@babel/plugin-transform-modules-commonjs": "^7.20.11",
        "@types/jest": "^29.4.0",
        "eslint": "^8.32.0",
        "eslint-config-prettier": "^8.6.0",
        "eslint-config-xo": "^0.43.1",
        "husky": "^8.0.0",
        "jest": "^29.4.0"
      },
      "babel": {
        "env": {
          "test": {
            "plugins": ["@babel/plugin-transform-modules-commonjs"]
          }
        }
      }
    }
    ```

          4. Editamos el archivo _eslintrc.json_ para que quede:

    ```json
        {
      "env": {
        "browser": true,
        "es2021": true,
        "node": true,
        "jest": true
      },
      "extends": ["xo", "prettier"],
      "overrides": [
        {
          "extends": ["xo-typescript"],
          "files": ["*.ts", "*.tsx"]
        }
      ],
      "parser": "@typescript-eslint/parser",
      "parserOptions": {
        "ecmaVersion": "latest",
        "sourceType": "module"
      },
      "plugins": ["@typescript-eslint"],

      "rules": {}
    }

    ```

        5. Crear el archivo _jsconfig.json_ con este contenido: [^1]

        `{ "typeAcquisition": { "include": ["jest"] } }`

6.  Añadimos el archivo `jest.config.js`:

    ```javascript
    /** @type {import('ts-jest').JestConfigWithTsJest} */
    export default {
      preset: "ts-jest",
      testEnvironment: "jsdom",
      testPathIgnorePatterns: ["dist"],
      resolver: "jest-ts-webcompat-resolver",
    };
    ```

7.  Ejecutamos el comando `npm i -D ts-jest @types/jest jest-environment-jsdom`
