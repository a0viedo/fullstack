# Módulos
Todo el ecosistema Node está basado en una filosofía modular, esto significa que se construyen pequeños módulos que resuelven cosas puntuales. Por ejemplo el módulo [Request](https://www.npmjs.org/package/request), se encarga de realizar requests HTTP y bajo esta filosofía se consideraría inadecuado que intente encapsular más tareas.<br>
Esto logra crear un árbol de dependencias para módulos que resuelven problemas grandes, cómo [Express](https://www.npmjs.org/package/express). De esta forma se logra reutilizar gran parte de las funcionalidades contenidas en un módulo.

Cualquier aplicación también podría subdividirse en módulos sin la necesidad de que cada uno esté publicado en npm.
Si quisieramos crear un módulo, y desde nuestro módulo exponer ciertos métodos, podríamos escribir el siguiente código:

```js
module.exports = {
    get: function(){ console.log('se llamó a get');},
    set: function(){ console.log('se llamó a set');}
}
```

Entonces estaríamos exportando un objeto, el cual contiene dos métodos: set y get.

## Módulos Core
Node.js incorpora varios módulos JavaScript los cuales podemos utilizar cómo cualquier otro, por ejemplo:
`var net = require('net');`
La [documentación](http://nodejs.org/api/) lista, entre otras cosas, el comportamiento de los módulos core. La idea de los módulos core es que permitan al desarrollador utilizar el File System por ejemplo, comunicarse usando distintos protocolos cómo TCP/UDP a traves de módulos desarrollados por los contribuidores core. Muchos de estos módulos core ya se encuentran *congelados*, lo que significa que nos aseguran que su interfaz no va a tener cambios en el futuro. Esto no quiere decir que no se puedan hacer mejoras y/o cambios radicales en su implementación, sino que esos cambios deberían ser invisibles para aquel que use el módulo.


## npm
[**npm**](https://www.npmjs.com/) es un package manager el cual nos permite descargar, instalar y resolver dependencias todo en un mismo comando. Por ejemplo, si quisieramos instalar la herramienta ESLint, deberíamos escribir en la terminal `npm install eslint -g`. <br>
Un módulo o paquete puede instalarse de dos maneras, de forma local o global. La instalación global únicamente tendrá sentido con módulos que son utilizados cómo herramientas de [CLI](http://es.wikipedia.org/wiki/CLI) (o de consola), por ejemplo ESLint.
La instalación local es lo utilizado para el resto de los casos. En el caso de una instalación local, npm descargará el módulo y lo colocará dentro de la carpeta *node_modules*. Cómo vimos en clase, a su vez cada módulo puede tener dependencias hacia otros módulos.

### Cómo crear y publicar un módulo

Inicialmente para crear un módulo (que uno quisiera luego publicar) se debe crear un archivo **package.json** el cual definirá las dependencias del módulo, la versión, su descripción, su nombre, entre muchas otras cosas más. Esto se puede lograr mediante el comando `npm init`. <br>
Luego debemos crear un archivo el cual se ejecute al requerir el módulo (por default index.js). Dentro de index.js podemos escribir lo siguiente:
```js
module.exports = function (){
    console.log('esto es un módulo');
};
```

Por último, si quisieramos publicarlo en npm, solo deberíamos ejecutar el comando `npm publish`. Supongamos que nuestro módulo se llama **mimodulo** y se encuentra publicado en npm, entonces lo utilizaríamos de la siguiente forma:
```js
var modulo = require('mimodulo');
modulo(); //imprime "esto es un módulo"
```