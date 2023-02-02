# BoilerPlate rápido de un repo

1. Crear carpeta vacía en el PC.

2. Abrirla con VSCode.

3. Inicializar el repo con `git init`.

4. Crear package.json con `npm init`.

5. Añadir .gitignore, .editorconfig y readme.

6. Editamos el archivo package.json **a partir de la línea donde pone _"main"_ (línea 6)** y añadimos este código:

   ```json
   "type": "module",
   "scripts": {
     "start": "tsc -w",
     "test": "jest --watchAll --coverage",
     "test:prod": "jest --watchAll --coverage --watchAll=false",
     "dev": "vite",
     "build": "tsc && vite build",
     "preview": "vite preview"
   },
   "keywords": [],
   "author": "",
   "license": "ISC",
   "devDependencies": {
     "@testing-library/dom": "^8.20.0",
     "@testing-library/jest-dom": "^5.16.5",
     "@types/jest": "^29.4.0",
     "@types/node": "^18.11.18",
     "@typescript-eslint/eslint-plugin": "^5.49.0",
     "@typescript-eslint/parser": "^5.49.0",
     "eslint": "^8.32.0",
     "eslint-config-prettier": "^8.6.0",
     "eslint-config-xo": "^0.43.1",
     "identity-obj-proxy": "^3.0.0",
     "jest": "^29.4.1",
     "jest-environment-jsdom": "^29.4.1",
     "sass": "^1.57.1",
     "ts-jest": "^29.0.5",
     "typescript": "^4.9.4",
     "vite": "^4.0.0"
   },
   "prettier": {
     "singleQuote": true
    }
   }
   ```

7. Ahora comenzamos la configuración:

   - Creamos el archivo .eslintrc.json con este contenido:

     ```json
     {
       "env": {
         "browser": true,
         "es2021": true,
         "node": true,
         "jest": true
       },
       "extends": ["xo", "prettier"],
       "parser": "@typescript-eslint/parser",
       "parserOptions": {
         "ecmaVersion": "latest",
         "sourceType": "module"
       },
       "plugins": ["@typescript-eslint"],

       "rules": {}
     }
     ```

   - Modificamos el package.json:

   - Creamos el archivo `tsconfig.json` con este contenido:

     ```json
     {
       "compilerOptions": {
         /* Visit https://aka.ms/tsconfig to read more about this file */

         /* Projects */
         // "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */
         // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
         // "tsBuildInfoFile": "./.tsbuildinfo",              /* Specify the path to .tsbuildinfo incremental compilation file. */
         // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects. */
         // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
         // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

         /* Language and Environment */
         "target": "ESNext" /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */,
         // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
         // "jsx": "preserve",                                /* Specify what JSX code is generated. */
         // "experimentalDecorators": true,                   /* Enable experimental support for TC39 stage 2 draft decorators. */
         // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
         // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h'. */
         // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
         // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using 'jsx: react-jsx*'. */
         // "reactNamespace": "",                             /* Specify the object invoked for 'createElement'. This only applies when targeting 'react' JSX emit. */
         // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
         // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */
         // "moduleDetection": "auto",                        /* Control what method is used to detect module-format JS files. */

         /* Modules */
         "module": "ESNext" /* Specify what module code is generated. */,
         "rootDir": "./src" /* Specify the root folder within your source files. */,
         "moduleResolution": "node" /* Specify how TypeScript looks up a file from a given module specifier. */,
         // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
         // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
         // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
         // "typeRoots": [],                                  /* Specify multiple folders that act like './node_modules/@types'. */
         // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
         // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
         // "moduleSuffixes": [],                             /* List of file name suffixes to search when resolving a module. */
         // "resolveJsonModule": true,                        /* Enable importing .json files. */
         // "noResolve": true,                                /* Disallow 'import's, 'require's or '<reference>'s from expanding the number of files TypeScript should add to a project. */

         /* JavaScript Support */
         // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
         // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */
         // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from 'node_modules'. Only applicable with 'allowJs'. */

         /* Emit */
         // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
         // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
         // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
         // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
         // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
         "outDir": "./dist" /* Specify an output folder for all emitted files. */,
         // "removeComments": true,                           /* Disable emitting comments. */
         // "noEmit": true,                                   /* Disable emitting files from a compilation. */
         // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
         // "importsNotUsedAsValues": "remove",               /* Specify emit/checking behavior for imports that are only used for types. */
         // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
         // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
         // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
         // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
         // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
         // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
         // "newLine": "crlf",                                /* Set the newline character for emitting files. */
         // "stripInternal": true,                            /* Disable emitting declarations that have '@internal' in their JSDoc comments. */
         // "noEmitHelpers": true,                            /* Disable generating custom helper functions like '__extends' in compiled output. */
         // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
         // "preserveConstEnums": true,                       /* Disable erasing 'const enum' declarations in generated code. */
         // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */
         // "preserveValueImports": true,                     /* Preserve unused imported values in the JavaScript output that would otherwise be removed. */

         /* Interop Constraints */
         // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
         // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
         "esModuleInterop": true /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */,
         // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
         "forceConsistentCasingInFileNames": true /* Ensure that casing is correct in imports. */,

         /* Type Checking */
         "strict": true /* Enable all strict type-checking options. */,
         // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
         // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
         // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
         // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
         // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
         // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
         // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */
         // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
         // "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
         // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read. */
         // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
         // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
         // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
         // "noUncheckedIndexedAccess": true,                 /* Add 'undefined' to a type when accessed using an index. */
         // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
         // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type. */
         // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
         // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

         /* Completeness */
         // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
         "skipLibCheck": true /* Skip type checking all .d.ts files. */
       }
     }
     ```

   - Añadimos el archivo `jest.config.js` con este contenido:

     ```javascript
     /** @type {import('ts-jest').JestConfigWithTsJest} */
     export default {
       preset: "ts-jest",
       testEnvironment: "jsdom",
       testPathIgnorePatterns: ["dist"],
       moduleNameMapper: {
         "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$":
           "<rootDir>/mocks/assetsMock.js",
         "\\.(css|scss)$": "identity-obj-proxy",
       },
       // TEMP resolver: "jest-ts-webcompat-resolver",
     };
     ```

   - Creamos la carpeta `.github` y dentro la carpeta `workflows`. Creamos dentro los archivos `Audit.yml` y `sonar.yml` con estos contenidos:

     > ## CUIDADO
     >
     > Recuerda volver a guardar todos los archivos después de copiarlos para que prettier los modifique de acuerdo a nuestras normas; si no, al hacer pull request la github action de **Audit** puede fallar para archivos como _jest.config.js_, _.eslintrc.json_, etc.

     ```yml
     name: Audit # Nombre del fichero .yml
     on: push
     jobs:
       audit:
         runs-on: ubuntu-latest
         name: Audit
         steps:
           - name: Git checkout
             uses: actions/checkout@v2
           - name: Check if .editorconfig exists
             uses: andstor/file-existence-action@v1
             with:
               files: ".editorconfig"
               allow_failure: true
           - name: EditorConfig validation
             uses: snow-actions/eclint@v1.0.1
           - name: Ensure node_modules is ignored by Git
             uses: dkershner6/gitignore-parser@v1
             with:
               must_deny: "node_modules/"
           - name: Install modules
             run: npm ci
           - name: ESLint validation
             run: npx eslint --ignore-path .gitignore .
           - name: Check commit message length
             uses: gsactions/commit-message-checker@v1
             with:
               pattern: "^[^#].{10,74}"
               error: "The commit message length must be between 10 and 72"
               excludeDescription: "true" # optional: this excludes the description body of a pull request
               excludeTitle: "true" # optional: this excludes the title of a pull request
               checkAllCommitMessages: "true" # optional: this checks all commits associated with a pull request
     ```

     ```yml
     name: Sonar #Nombre del fichero
     on:
       push:
         branches:
           - main
       pull_request:
         types: [opened, synchronize, reopened]
     jobs:
       sonarcloud:
         name: SonarCloud
         runs-on: ubuntu-latest
         steps:
           - uses: actions/checkout@v2
             with:
               fetch-depth: 0 # Shallow clones should be disabled for a better relevancy of analysis
           - name: Install modules
             run: npm ci
           - name: Testing in production with coverage
             run: npm run test:prod #Ejecuta los tests que hayamos hecho desde el servidor.
           - name: SonarCloud Scan
             uses: SonarSource/sonarcloud-github-action@master
             env:
               GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # Needed to get PR information, if any
               SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
     ```

   - Dentro del proyecto de sonar, vamos a `Administration => Analysis method` y desactivamos el check de análisis automático. Elegimos debajo `GitHub Actions` pinchando en el link de "Follow the tutorial" que hay justo debajo.

   - Seguimos las instrucciones para añadir en gitHub el secret correspondiente al TOKEN.

   - Creamos el archivo `sonar-project.properties` en la carpeta raíz con el contenido que nos da la web de sonar en `Administrate => Analysis Method => GitHub Actions (follow the tutorial) => Create or update a build file (Others - JS...)`. El contenido del archivo será **_parecido_** a este (cambiando el valor de `projectKey` y de `organization`):

     ```properties
     sonar.projectKey=SemperFenix_boilerPlate
     sonar.organization=semperfenix
     sonar.javascript.lcov.reportPaths=coverage/lcov.info
     sonar.coverage.exclusions = /src/models/*.test.*

     # Los asteriscos dependerán de dónde estén los archivos de test, ** sirve para indicar 'Cualquier nombre de carpeta' y * sirve para indicar 'Cualquier palabra en el nombre del archivo'.

     # En este caso podríamos haber escrito **/**/*.test.*


     # This is the name and version displayed in the SonarCloud UI.
     #sonar.projectName=202301-W3CH1-ivan-duran
     #sonar.projectVersion=1.0

     # Path is relative to the sonar-project.properties file. Replace "\" by "/" on Windows.
     #sonar.sources=.

     # Encoding of the source code. Default is default system encoding
     #sonar.sourceEncoding=UTF-8
     ```

- Para que Sonar coja correctamente el valor del coverage del archivo, incluimos esta línea:

  ```properties
  sonar.javascript.lcov.reportPaths=coverage/lcov.info
  ```

- Para evitar que Sonar busque coverage de los archivos de test incluimos en ese mismo archivo esta línea:

  ```properties
  sonar.coverage.exclusions = **/*.test.ts, **/*.test.js
  ```

  [^1]

## Huskys

Si queremos instalar huskys:

1. `npm i -D husky`

2. Ejecutamos `npm run prepare`

3.Creamos los huskys que necesitemos con `npx husky add .husky/nombre-del-husky`. Los dos que tenemos son:

- commit-msg:

  ```shell
    #!/usr/bin/env sh

  . "$(dirname "$0")/_/husky.sh"

  while read line; do
      # Skip comments
      if [ "${line:0:1}" == "#" ]; then
          continue
      fi
      if [ ${#line} -ge 72 ] || [ ${#line} -le 10 ]; then
          echo -e "\033[0;31mThe length of the message has to be between 10 and 72 characters."
          exit 1
      fi
  done < "${1}"

  exit 0
  ```

- pre-push

  ```shell
    #!/usr/bin/env sh

    . "$(dirname "$0")/_/husky.sh"

    local_branch_name="$(git rev-parse --abbrev-ref HEAD)"

    valid_branch_regex='^((hotfix|bugfix|feature)\/[a-zA-Z0-9\-]+)$'

    message="Please check your branch name."

    if [[ ! $local_branch_name =~ $valid_branch_regex ]]; then
      echo -e "\033[0;31m$message"
      exit 1
    fi

    exit 0
  ```

[^1]: Para más información sobre cómo utilizar los \* y otros caracteres comodín, utilizar [esta referencia](https://docs.sonarcloud.io/advanced-setup/analysis-scope/#restrict-the-scope-of-coverage-detection).
