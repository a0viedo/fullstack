# Objetos
## Definición
Un objeto es un elemento que se puede pensar cómo un *"contenedor"* de llaves (keys) y valores (values).

Ejemplo:
```js
var ejemplo = { a: 1 };
```
En el ejemplo anterior se utilizó la forma literal para la creación de un objeto con una única llave ("a") que posee el valor 1. La segunda forma de crear objetos es mediante un [constructor](https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)): `new Object()`. Ésta última forma es utilizada en menor medida, pero es importante destacar su equivalencia con la forma literal.

## Accediendo a un objeto
Según la definición que usamos, los objetos se pueden imaginar cómo *contenedores*. Estos *contenederos* pueden constar de llaves y valores o, también llamadas, propiedades.

Ejemplo:
```js
var ejemplo = { a: 1 };
```
Si quisieramos acceder a la propiedad `a` de nuestro objeto creado en el ejemplo anterior, podríamos utilizar lo siguiente `ejemplo.a`.

```js
var ejemplo = { a: 1 };
console.log(ejemplo.a); // 1
```
El ejemplo anterior imprimirá a consola el valor 1.

## Modificando un objeto
Los objetos no son inmutables, es decir, una vez que se crearon pueden extenderse con propiedades nuevas.

Ejemplo:
```js
var ejemplo = {};
ejemplo.propiedad1 = 'una cadena de caracteres';
console.log(ejemplo); // {propiedad1: "una cadena de caracteres"}
```


## Iterando las propiedades de un objecto
**Object.keys** nos retorna un array con las llaves que contiene el objeto que recibe por parámetro. 

Ejemplo:
```js
var ejemplo = { propiedad2: 'una cadena de caracteres' };
console.log(Object.keys(ejemplo)); // ['propiedad2']
```

A su vez, un objeto puede poseer propiedades pero éstas estar definidas para que no sean enumerables. Una propiedad no-enumerable no es recorrida con loops `for...in` y no es considerada por `Object.keys`. La forma de definir propiedades no-enumerables es con [Object.defineProperty](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/defineProperty). Se puede saber también si una propiedad es enumerable usando [Object.prototype.propertyIsEnumerable](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Object/PropertyIsEnumerable), por ejemplo:

```javascript
console.log(Object.keys(Math)); // []
console.log(Math.propertyIsEnumerable('random')); // false
console.log(Object.getOwnPropertyNames(Math)); // ["E", "LN10", "LN2", "LOG2E", "LOG10E", "PI", "SQRT1_2", "SQRT2", "random", "abs", "acos", "asin", "atan", "ceil", "cos", "exp", "floor", "log", "round", "sin", "sqrt", "tan", "atan2", "pow", "max", "min", "imul", "sign", "trunc", "sinh", "cosh", "tanh", "asinh", "acosh", "atanh", "log10", "log2", "hypot", "fround", "clz32", "cbrt", "log1p", "expm1"]
```

Por lo tanto, si queremos obtener todas las propiedades de un objeto, ya sean enumerables o no, debemos utilizar **Object.getOwnPropertyNames**. Si lo aplicamos a un array vacío:

```javascript
console.log(Object.getOwnPropertyNames([])); // ["length"]
console.log([].forEach); // function forEach() { [native code] }
```
Entonces, ¿dónde reside la función *forEach*? ¿Cuando se setea en el array vacío?¿Pertenece realmente al array vacío?

# Prototype Chain
JavaScript es conocido por ser uno de los pocos lenguajes de programación *populares* en utilizar [herencia prototipada](http://en.wikipedia.org/wiki/Prototype-based_programming). Otros conocidos son Perl, Lua y Lisp. Esto significa básicamente que el reuso de componentes será dado por un link ascendente y uno descendente dentro de algo llamado *prototype chain*. Por ejemplo, cualquier objeto hereda de un único objeto que tiene predefinidas las propiedades que utilizamos comunmente. Para "subir" por la *prototype chain* se puede utilizar la utilidad `Object.getPrototypeOf()`. Por ejemplo:

```javascript
var obj = {};
Object.getOwnPropertyNames(obj); // []
Object.getOwnPropertyNames(Object.getPrototypeOf(obj)); // ["constructor", "toString", "toLocaleString", "valueOf", "hasOwnProperty", "isPrototypeOf", "propertyIsEnumerable", "__defineGetter__", "__lookupGetter__", "__defineSetter__", "__lookupSetter__", "__proto__"]
```

Dónde `Object.getPrototypeOf(obj)` referencia a **el** objeto del cual heredan todos los objetos. Lo mismo ocurre con arrays y funciones, que a su vez son objetos también.
Dada una función constructora, por ejemplo `Array`, si queremos referenciar al objeto que van a referenciar todos los arrays que se creen debemos utilizar la propiedad `prototype`. Por ejemplo:

```javascript
console.log(Object.getPrototypeOf([]) === Array.prototype) // true
```

Podemos visualizar que todo array creado linkea a través de la *prototype chain* (ascendente) a `Array.prototype`. Douglas Crockford comenta mucho acerca de este tema y hace incapié especialmente porque muchos desarrolladores mantienen la forma de pensar de "herencia clásica" y no aceptan la forma prototipada. [Según Douglas](http://javascript.crockford.com/prototypal.html), la mejor forma de verlo es objetos que heredan comportamiento de objetos.