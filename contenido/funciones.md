# Ámbito de funciones
Una función crea un **ámbito**, y ese ámbito puede contener un grupo de variables. A su vez, en el momento de ejecución de la función se le asigna un valor a la palabra reservada **this**. Los valores que tendrá **this** dependerá de cómo se llame la función o, por ejemplo, si es un método de un objeto:
- Invocación de función `hola()` definirá *this* siempre con el ámbito global
- [call](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Function/call) `hola.call({}, param1,param2)`
- [apply](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Function/apply) `hola.apply({}, [param1, param2])`
- Invocación de método `obj.hola()` definirá *this* con valor de *obj*

Tengan en cuenta que a los métodos también se los puede invocar con *call* `obj.hola.call({})` para 'sobrescribir el valor de *this*.

# Immediately-Invoked Function Expression (IIFE)
O funciones inmediatamente invocadas. Por ejemplo:
```js
(function (){ console.log('hola')})() // "hola"
```

Se utilizan para no 'ensuciar' el ámbito global, se crea una función por lo tanto se genera un ámbito dónde se pueden definir variables y funciones que no van a ser compartidas con cualquier otro ámbito que no sea interno.

# Parámetros 
Los parámetros de tipo objeto, siempre son pasados por referencia a las funciones.
Por ejemplo:
```js
function hola(obj) { obj.a = 5;}
var temp = {};
hola(temp);
console.log(temp.a); // 5
```
En contraste, los tipos de datos primitivos -String, Number y Boolean- son siempre pasados por copia a las funciones. Es decir:
```js
function hola(n) { n.a = 5;}
var miNumero = 5;
hola(miNumero);
console.log(miNumero.a); // undefined
```

# new
El uso de new se caracteriza por **crear** instancias de *funciones constructoras*. A las funciones constructoras se las diferencia por su nombre empezando con mayúscula.
```js
function Table(){ this.prop1 = 'abc';}
var t = new Table();
console.log(t.prop1); // imprime 'abc'
```
Utilizando *instanceof* es una forma de asegurarnos que ese objeto **t** se creó utilizando la función constructora Table: `t instanceof Table // true`
