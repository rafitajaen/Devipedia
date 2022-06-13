---
description: Explicación de los pasos necesarios para configurar nuestro proyecto de TS
---

# Instalación

### 0. Instalación lista para usar

{% file src="../.gitbook/assets/00-ts-ready.zip" %}

### 1. Instalación de dependencias

```bash
# Comprobar instalación de node (https://nodejs.org) y npm (Gestor de dependencias de proyectos).
> node --version
> npm --version

# Inicializaremos el archivo de configuración de dependencias
> npm init

# Instalaremos como dependencias de desarrollo 
> npm i --save-dev @types/node nodemon ts-node typescript rimraf
```

* `@types/node` : Dependencias de desarrollo de Typescript para nodejs
* `nodemon` : Herramienta para recargar nodejs cada vez se detecten cambios en los archivos
* `ts-node` : Ejecuta archivos .ts sin tener que transpilar el codigo a .js
* `typescript` : Transpila .ts a JS standard
* `rimraf` : Rimraf

### 2. Generar archivo de configuración de Typescript: `tsconfig.json`

Archivo en el que definimos como debe transpilarse el código de TS a JS.

```bash
# OPCION 1: Generar el archivo de configuración básico
> npx tsc --init

# OPCIÓN 2: Crear archivo de configuración personalizado
> npx tsc --init --rootDir src --outDir build --esModuleInterop --resolveJsonModule --lib es6 --module commonjs --allowjs --noImplicitAny
```

#### 2.1. Typescript CLI Documentation&#x20;

{% embed url="https://www.typescriptlang.org/docs/handbook/compiler-options.html" %}

### 3. Archivo de configuración de `nodemon.json`

Crear archivo nodemon.json en la carpeta del proyecto

```json
{
    "watch": ["src"],
    "ext": ".ts, .js",
    "ignore": ["node_modules"],
    "exec": "ts-node ./src/index.ts"
}
```

### 4. Scripts para `package.json`

```json
"scripts" : {
 "tsnode" : "cd src && ts-node index.ts",
 "start" : "nodemon",
 "transpilation" : "tsc",
 "build:prod" : "rimraf ./build && tsc",
 "start:prod" : "npm run build:prod && node build/index.js"
}
```

Podemos ejecutar nuestros <mark style="color:red;">scripts</mark> con el siguiente código:

```bash
> npm run tsnode
```

### Extra: VSCode Extensions para TS

* <mark style="background-color:green;">Básico</mark> : Material Icon Theme (by Philipp Kief)
* <mark style="background-color:red;">Obligatorio</mark> : JavaScript and TypeScript Nightly (by Microsoft)
* <mark style="background-color:green;">Básico</mark> : ESLint (by Microsoft)
* <mark style="background-color:green;">Básico</mark>  : npm (by Microsoft)
* <mark style="background-color:green;">Básico</mark> : npm Intellisense (by Christian Kohler)
* <mark style="background-color:green;">Básico</mark> : Path Intellisense (by Christian Kohler)
* <mark style="background-color:green;">Básico</mark> : Rainbow Brackets (by 2gua)
* <mark style="background-color:yellow;">Opcional</mark> : TODO Hightlight (by Wayou Liu)
* <mark style="background-color:yellow;">Opcional</mark> : Todo Tree (by Gruntfuggly)
