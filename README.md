# Guía para integrar ESlint + Airbnb y Prettier con Visual Studio Code

**¿Para qué nos sirve Eslint?**
ESlint es una herramienta de linting que se encarga de que nuestro código sea mantenible, con el objetivo de que esté limpio y estructurado.
Para ello tiene una serie de reglas (en este caso usaremos las reglas de Airbnb) con las que nos dará algunos errores y avisos sobre la sintaxis de nuestro código.
También podemos crear las nuestras propias o sobrescribir las existentes. Algunos errores los podrá corregir automáticamente
y otros nos lo avisará el editor. Con estas pautas nos aseguraremos tener un código de gran calidad.

Reglas:
https://eslint.org/docs/rules/

**¿Qué son las reglas de Airbnb?**
Una guía de estilos base, la cuál incluye multitud de contenido.

Reglas:
https://github.com/airbnb/javascript

**¿Para qué nos sirve Prettier?**
Prettier es una herramienta cuya misión es formatear nuestro código para que tenga un formato concreto de forma automática, lo que lo hará más consistente.

Reglas:
https://prettier.io/docs/en/configuration.html

Con todo esto haremos que mediante ESlint + Air
bnb, nuestro código tenga un estilo siguiendo unos patrones y con Prettier le impondremos un formato.

# 1-Instalar el plugin ESlint en Visual Studio Code.

![ESlint Visual Studio Code](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/ESlint-VS.PNG)

# 2-Instalar el plugin Prettier en Visual Studio Code.

![Prettier Studio Code](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/Prettier-VS.PNG)

> Añadimos estas líneas al fichero de configuración de Visual Studio Code (settings.json) para que realice los cambios automáticamente :

```bash
  //ESlint
  {
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  //Prettier
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
  }
```

# 3- Instalamos ESlint en nuestro proyecto:

```bash
npm install --save-dev eslint
```

# 4- Creamos el fichero de configuración (.eslintrc):

```bash
npx eslint --init
```

- **How would you like to use ESLint?**<br />
  > Nos indica el modo en que funcionará el linter:

To check syntax only. (Solo revisa la sintaxis del código)<br />
To check syntax and find problems. (Revisión de la sintaxis y problemas del código)<br />
To check syntax, find problems, and enforce code style. (Es como la opción número 2 pero añadiendo un estilo base, que en nuestro caso será el de Airbnb)<br />

![Modo uso linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-1.PNG)

- **What type of modules does your project use?**<br />
  > Nos indica el tipo de módulos que vamos a usar:

JavaScript modules (import/export). (Elegimos esta forma ya que nuestro proyecto usará Babel para React, Angular, Vue...)
CommonJS (require/exports). (Para proyectos con nodejs y o cualquier otro proyecto javascript)
None of these.

![Modulo linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-2.PNG)

- **Which framework does your project use?**><br />
  > Nos indica si vamos a utilizar un framework:

React.<br />
Vue.js<br />
None of these.<br />

![Framework linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-3.PNG)

- Does your project use TypeScript? (y/N)<br />
  > Nos indica si vamos a utilizar Typescript en nuestro proyecto.

![TypeScript linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-4.PNG)

- **Where does your code run?**<br />
  > Nos indica donde se ejecutará nuestro código:

Browser.<br />
Node.<br />

![Visualización linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-5.PNG)

- **How would you like to define a style for your project?**<br />
  > Nos indica el estilo base que usará el linter:

Use a popular style guide<br />
Answer questions about your style<br />
Inspect your JavaScript file(s)<br />

![Guia estilo linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-6.PNG)

![Airbnb linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-7.PNG)

- **What format do you want your config file to be in?**<br />
  > Nos indica el formato del fichero de configuración:

Javascript.<br />
YAML.<br />
JSON.<br />

![Formato fichero configuración linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-8.PNG)

- **Would you like to install them now with npm?**<br />
  > Nos indica si queremos instalar las dependencias necesarias en nuestro proyecto

![Dependencias linter](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/config-eslint-9.PNG)

# 5- Si queremos utilizar Typescript o la última sintaxis de ECMAScript deberemos instalar babel como parseador:

```bash
npm install babel-eslint --save-dev
```

# 6- Instalamos Prettier en nuestro proyecto:

```bash
npm install --save-dev prettier
```

# 7- Inclumos el plugin de Prettier para ESlint

```bash
npm install eslint-plugin-prettier
```

# 8- Desactivamos las reglas que puedan entrar en conflicto entre ESlint y Prettier:

```bash
npm install eslint-config-prettier
```

# 9- Configuramos el fichero de ESlint (.eslintrc.json)

```bash
{
  "env": {
    "browser": true,
    "es6": true
  },
  "extends": ["airbnb-base", "plugin:prettier/recommended"],
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parser": "babel-eslint",
  "parserOptions": {
    "ecmaVersion": 2017
  },
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "endOfLine": "auto"
      }
    ]
  }
}

```

# 10- Configuramos el fichero de Prettier para ello debemos crearlo en la raíz del proyecto(.prettierrc)

```bash
{
  "printWidth": 80,
  "singleQuote": true,
  "trailingComma": "es5",
  "bracketSpacing": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2
}
```

# 11- Comprobar errores con ESlint

![Error-1 Eslint](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/error-eslint-1.PNG)
![Error-2 Eslint](https://github.com/Pdominguez15/eslint-prettier/raw/master/content/error-eslint-2.PNG)
