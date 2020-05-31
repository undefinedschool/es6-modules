# ✨ ES6: Modules


<div align="center">  
  <p align="center">
  <sub>Hola! Soy Nico (<strong>nhsz</strong>), <strong>Dev Full Stack JavaScript y mentor</strong>.</sub>
  </p>
  
  <p align="center">
    <sub>
      Hace un tiempo (principios de 2019) empecé un proyecto llamado <a href="https://undefinedschool.io"><strong>undefined school</strong></a>, una <strong>escuela de Desarrollo Web Full Stack JavaScript</strong>, 100% Open Source, con mentorías personalizadas para grupos reducidos y el foco puesto en los <strong>fundamentos</strong> y <strong>conceptos avanzados</strong>.
    </sub>
  </p>

  <p align="center">
    <sub>
      Me interesa mucho la intersección entre la educación y la tecnología, por eso también participo en proyectos como <a href="https://freecodecampba.org">freeCodeCampBA</a> (co-founder y co-organizador) y <a href="https://twitter.com/LXBA_">Learning Experience BA</a> (co-founder y co-organizador).
    </sub>
  </p>

 <p align="center">
    <sub>
  👉 Si estás arrancando en el mundo del desarrollo web y necesitás una mano, podés encontrarme en <a href="https://twitter.com/_nhsz/">Twitter</a> (también para hablar sobre cualquier tema relacionado a JavaScript o <em>#nerdeadas</em> en general 😛).
  </sub>
  </p>
  
  <p align="center">
  <sub>
    Por último, te cuento que soy muy fan del café (obvio que negro y sin azúcar), asi que si las notas te resultaron útiles y querés colaborar para que no me quede dormido y siga escribiendo guías, apuntes y más <strong>contenido Open Source en español</strong>, podés invitarme uno, gracias! ❤️
  </sub>
  </p>
  
  <p align="center">
  ☕
  <code> 
  <a href="https://cafecito.app/nhsz">
    <strong>Invitame 1 café!</strong>
  </a>
  </code>
  </p>
  <hr>
</div>

👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

---

## ¿Para qué sirven?

- Los módulos nos permiten exportar e importar diferentes partes de código, entre diferentes archivos, lo cual nos permite modularizar el código
- Un módulo no es más que un archivo (en este caso JS) que importamos/exportamos desde o hacia otro archivo para utilizarlo
- _Definición cheta:_ un módulo es una unidad independiente (autocontenida) de código reutilizable, que podemos exportar para luego importarla y utilizarla en otro archivo (ó módulo)
- _Otra:_ los módulos nos permiten _encapsular_ funcionalidad y exponerla a otros archivos JS, como si se tratase de _librerías_ (biliotecas)

## Motivación (o sea... ¿por qué usarlos?)

- **Para organizar mejor nuestro código.**
- Igual, si, **código más organizado => código más legible, simple, conciso, más fácil de razonar => más mantenible** ✨

![](https://media.makeameme.org/created/clean-code-clean.jpg)

### Otros problemas que resuelven los módulos

- Duplicación de código
- Namespacing (evitar la colisión de nombres de variables, funciones, clases, etc)
- Dependency Tree (cargar las dependencias necesarias, en el orden correcto)
- etc

## Antes de ES6 Modules

- Cargábamos los diferentes `script` tags a mano en el HTML
  - Si los cargábamos en orden incorrecto (según las dependencias), no funcionaba
  - Genera problemas de performance/usabilidad: hasta que no se termina de cargar un `script`, no se carga el siguiente y así, porque es _render-blocking_
  - _tl;dr_ Hacer esto a mano es bastante molesto, perdemos mucho tiempo y casi siempre _sale mal_ (la palabra técnica para eso es _error-prone_ 😁)
- Antes de _ES6 Modules_, No teníamos una forma nativa (y standard) de cómo usar módulos en JS 
- Más tarde fueron apareciendo diferentes soluciones de terceros (_CommonJS, AMD, UMD, Browserify, etc_) y era medio un complejo por temas de compatibilidad, etc
- Aparecen los _package bundlers/module loaders_ que nos simplifican un poco la vida y hacen el trabajo sucio por nosotros, pero agregamos más herramientas y capas de complejidad a nuestro código

## Dependencias e interfaz

- Llamamos **dependencias** a la funcionalidad/valores que importamos en un archivo. Cuando un _módulo_ importa funcionalidad de otro módulo, decimos que _depende_ o _tiene como dependencia_ a ese otro módulo
- Llamamos **interfaz** a la funcionalidad/valores que un módulo provee (exporta) al resto. Un módulo sólo puede importar funcionalidad que forme parte de la _interfaz_ de otor módulo. Todo lo que no se exporta es _privado_ dentro de un módulo y no puede ser usado fuera del mismo

## ¿Qué podemos exportar? (e importar)

- variables/constantes
- objetos
- funciones
- clases

## Soporte

Recíen a mediados del 2018 esta feature comenzó a tener más [soporte](https://caniuse.com/#feat=es6-module), por lo que en algunos browsers posiblemente tengamos que usar herramientas (aka _package bundlers_) como [Webpack](https://webpack.js.org/) o [Parcel](https://parceljs.org/), para compilar nuestros módulos de ES6 a una sintaxis que el browser entienda.

## Uso

- **Named export:** Lo usamos cuando queremos indicar explícitamente qué exportamos y con qué nombre. Permite exportar múltiples valores por archivo. Necesitamos usar `{}` en el `import` y llamarlo con el mismo nombre con el que fue exportado (ó usar un _alias_). Si el nombre no matchea con ningún `export`, va a importar el `default`

```js
export const package = {};

import { package } from './module-name.js';
```

```js
// Podemos exportar múltiples valores
const a = 1;
const b = 2;
const c = 3;

export { a, b, c };

// Y después importar sólo los que vamos a usar (con destructuring!)
import { a, b } from './module-name.js'

// En el caso de ser necesario, podemos renombrar los imports, suando 'as'
import { a as one } from './module-name.js'
```

- **Default export:** Lo usamos generalmente cuando exportamos un único valor. Sólo puede haber un _default export_ por módulo. No necesitamos usar `{}` en el `import` y podemos ponerle el nombre que querramos

```js
export default const package = {};

import package from './module-name.js';
```

- ✨ **Nota:** podemos usar _named_ y _default exports_ en el mismo módulo

- **Wildcard export:** Lo usamos si queremos importar _todo_ lo que otro módulo exporta

```js
const a = 1;
const b = 2;
const c = 3;

export { a, b, c };

// Importamos a, b y c
import * from './module-name.js'
```

```js
// Exportar todos los _named export_ a un objeto
import * as MainComponents from "./MyComponent";
// Usamos MainComponents.MyComponent y MainComponents.MyComponent2 por ejemplo
```

- **Absolute path:** También podemos usar _paths absolutos_ para referenciar módulos que se encuentran en otro dominio

```js
import toUpperCase from 'https://git.io/fjjGt'
```

## Usando ES6 modules en el browser

- Tenemos que agregar el atributo `type="module"` a nuestros tags `script` para que el browser los cargue como _ES6 Modules_
- Ojo con el tema de [_CORS_](https://www.youtube.com/watch?v=JVZIhCVFJ9c), necesitamos levantar los archivos en un server. Algunas opciones: [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer), [http-server](https://www.npmjs.com/package/http-server)
- Para browsers sin soporte, podemos definir un `script` con al atributo `nomodule` como fallback

```js
<script type="module" src="module.js"></script>
<script nomodule src="fallback.js"></script>
```

## Node

- Node utiliza _CommonJS_ como sistema de módulos desde hace mucho tiempo

```js
const package = require('module-name');
```

- Gracias a esta feature de ES6, podemos estandarizar y unificar la forma de usarlos. En la versión 12, el [soporte para ES6 modules](https://blog.logrocket.com/es-modules-in-node-js-12-from-experimental-to-release/) mejoró mucho

## Tips

- Poner los _imports_ siempre al inicio del archivo JS
- Si el archivo exporta una sola cosa, usar `export default`
- Los _Named imports_ llevan `{}`, los _default_ no
- Si el _path_ no es absoluto, no olvidarnos de usar `./` o `/` antes del nombre del módulo
- No olvidarnos de ponerle la extensión `.js` al módulo que importamos

```js
// Esto no funciona ❌
import { something } from './moduleName';

// Esto si ✅
import { something } from './moduleName.js';
```

[![JavaScript Modules in 100 Seconds](https://img.youtube.com/vi/qgRUr-YUk1Q/0.jpg)](https://www.youtube.com/watch?v=qgRUr-YUk1Q)

- [Cheatsheet](https://www.samanthaming.com/tidbits/79-module-cheatsheet/)
