# Monorepo

En un monorepo tendremos un package.json en la raíz y cada proyecto lo tendremos en su carpeta con su package json.

NodeModules estará en la raíz, no dentro de las carpetas de proyectos.

Las github actions y husky tendrán que estar en la raíz también.

En el package root le diremos:

```json
{
...
"private":"true", // Esto sólo es importante de cara a subirlo a npm
"workspaces":[
"api", "app"]
...
}
```

Dentro de Workspaces le diremos el nombre de las carpetas con los proyectos.

Cuando instalamos algo con npm podemos utilizar el modificador `-w` para indicar el workspace que queremos.
`npm i -D instalacion -w api`

En la action de sonar habrá que separar dos secciones de job, donde a cada uno le damos un working-directory y un projectBaseDir (básicamente, la action de sonar estará duplicada dentro del mismo archivo en la sección de `job`, cada uno con unas propiedades).
Además, tendremos que renombrar el Sonar Token (tanto en github como en la action).
Cada fichero tendrá su archivo sonar-project.properties

## Proyectos

Cada proyecto tendrá sus propios archivos de configuración de los paquetes (eslintr, jest.config, etc.)

## Turborepo

Es una herramienta que ayuda en la creación de monorepos.
