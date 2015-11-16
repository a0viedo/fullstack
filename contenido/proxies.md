## Servidores Proxy
Los [servidores Proxy](http://en.wikipedia.org/wiki/Proxy_server) son comunmente utilizados en cuestiones de balanceo de carga o gateway (o compuerta) de infraestructuras. Un ejemplo del último caso es la arquitectura completa de [OpenShift](https://www.openshift.com), un proveedor de servicios en la nube, la cual concentra la entrada y salida de información de toda su granja de servidores por medio de un servidor proxy. Esto simplifica las cosas en cuestiones de configuración, tambien significa que se pueden concentrar las medidas de seguridad y reglas de networking en un único punto. 

Veamos un ejemplo de un simple servidor proxy:
```js
var http = require('http');
var server = http.createServer();
server.on('request', function(request, socket) {
  http.request({
    host: 'www.google.com.ar',
    method: 'GET',
    path: request.url,
    port: 80,
  }, function(response) {
    response.pipe(socket);
  }).end();
});
server.listen(8080);
```
El ejemplo anterior crea un servidor HTTP y por cada request que recibe realiza un pedido GET a **www.google.com.ar** con el mismo path que recibió. Es decir, si se hace un GET a **http://localhost:8080/**, el servidor nos respondería el resultado de un GET a **http://www.google.com.ar/**. Por lo tanto, al realizar un get a **http://localhost:8080/prueba** estaríamos obteniendo como respuesta el resultado de hacer un GET a **http://www.google.com.ar/prueba**. Esto nos permitiría realizar búsquedas dentro de nuestro servidor proxy, ya que, los elementos de la página web que contengan direcciones a paths relativos nos estarían respondiendo exactamente lo que el sitio de Google muestra.

![proxy](http://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Proxy_concept_en.svg/420px-Proxy_concept_en.svg.png)

Un servidor proxy propiamente dicho debería ser invisible al que lo utiliza.Una de las fallas del ejemplo anterior es que los headers no son enviados. El servidor proxy se deberia de encargar de asignar los headers de cada request recibido al pedido interno que realiza y, por otro lado, guardar los headers de la respuesta interna y asignarlos a la respuesta del cliente. En el caso anterior, un ejemplo sería si yo realizo un GET a **http://www.google.com.ar** con los headers `{ "Content-Type": "application/json"}` el servidor proxy debería hacer el request con los headers correspondientes:
```js
  http.request({
    host: 'www.google.com.ar',
    method: 'GET',
    path: request.url,
    port: 80,
    headers: { "Content-Type": "application/json" }
  }, ...;
```
Y lo mismo con la respuesta:
```js
...
socket.headers = response.headers;
response.pipe(socket);
...
```
