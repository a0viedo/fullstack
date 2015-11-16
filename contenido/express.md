# Express.js
Express es un framework para construir aplicaciones web con Node.js. Utiliza una serie de abstracciones para facilitar las funcionalidades comunmente utilizadas. Encontraremos que dentro de los componentes de Express, varios elementos con respecto al flujo de datos no varian, por ejemplo los objetos *request* y *response*. Estos objetos serán extendidos con métodos nuevos, cómo en el caso particular de *response* y los métodos [`response.send`](http://expressjs.com/4x/api.html#res.send) o [`response.json`](http://expressjs.com/4x/api.html#res.json). Leer la [documentación](http://expressjs.com/4x/api.html) para ver una lista de los métodos agregados por el framework.

Se puede separar las funcionalidades de Express en tres grandes partes: el **sistema de rutas**, los **middlewares** y los **template engines**.

## Middlewares
Es uno de los conceptos más importantes, ya que las rutas podrían considerarse un subset de middleware. Básicamente cualquier aplicación Express es una serie de llamadas a diferentes middlewares.
**Definición**: es una función con acceso al objeto request, al objeto response y al siguiente middleware de la aplicación.

Un middleware puede:
* Ejecutar cualquier código
* Realizar cambios a los objetos request y response
* Terminar el ciclo request-response
* Invocar al siguiente middleware de la aplicación

**Si el middleware actual no finaliza el ciclo request-response, deberá invocar al siguiente middleware de lo contrario hará que la solicitud quede colgada sin respuesta**.

Ejemplo:
```js
// middleware que se ejecuta por cada solicitud realizada
// e imprime a consola el tiempo actual
app.use(function (req, res, next) {
  console.log('Time:', Date.now());
  next();
});
```

## Rutas
Las rutas son un caso particular de middlewares. Básicamente están compuestas por dos componentes: el **path** y un **handler**. El handler será la función que se ejecutará para esa ruta y tiene acceso al objeto request, al objeto response y al siguiente middleware.

Ejemplo:
```js
// ruta que escucha para los verbos GET
// en el "root" de la aplicación y envia el texto "Hello World!"
app.get('/', function (req, res) {
  res.send('Hello World!');
});
```

Hay varias alternativas a la hora de definir el path, se pueden utilizar strings comunes, strings con parámetros o incluso expresiones regulares.
Por ejemplo:
```js
// ruta que escucha en el path "/user/:userId" para el verbo GET
app.get('/user/:userId', function (req, res) {
  res.send('Se recibió una solicitud para el usuario con id ' + req.params.userId);
});
```
El ejemplo anterior accede al parámetro que fué definido en el path y tomará valores dinámicos. Es decir, si se hace un GET a `/user/123` imprimirá "*Se recibió una solicitud para el usuario con id 123*".

## Template engines
O en otros contextos llamado [template processor](https://en.wikipedia.org/wiki/Template_processor) sirve para mediante una data y un template, generar contenido HTML.


<p align="center"><img src ="https://upload.wikimedia.org/wikipedia/commons/c/c7/TempEngGen015.svg" /></p>

Algunos de los más conocidos son: Jade, Handlebars, EJS, etc.

Para utilizar cualquiera de los nombrados previamente se deberá utilizar un código similar al siguiente:
```js
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'jade');
```
dónde uno indicará el directorio dónde se encuentran las vistas y qué tipo de template engine está utilizando.
