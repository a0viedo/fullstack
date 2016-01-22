# Truthyness y Falseyness
Un tema muy polémico es la coersión de tipos de datos dentro del lenguaje. Coersión significa que se podría forzar una transformación de tipo ante ciertas operaciones. 

Los valores que, mediante coerción, son transformados a un valor verdadero son los siguientes:
- cualquier objeto (de acá se desprenden por lo tanto funciones y arrays)
- una string no vacía
- un número distinto de cero
- +/- Infinity

Dado lo explicado en el párrafo anterior, podríamos utilizar el siguiente código:

```js
if(miVariable) {
  // sé que miVariable es alguno de estos: objeto, string no vacía, +/- Infinity o un número distinto de cero
}
```

Los valores que, mediante coerción, son transformados a un valor falso son los siguientes:
- el número cero
- un string vacío
- null
- undefined
- NaN

Entonces podríamos escribir el siguiente código:
```js
if(!miVariable) {
  // sé que miVariable es alguno de los siguientes: null, string vacío, el número cero, NaN o undefined
}
```
