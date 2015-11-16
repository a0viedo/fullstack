# Redes
Dentro de un sistema operativo existen muchas capas las cuales nos permiten conectarnos ya sea por un cable a una red LAN o por un dispositivo WiFI. A continuación un gráfico de las distintas capas:
![network stack](http://i.imgur.com/Btzm9GW.png)

Se las denomina [modelo OSI](http://es.wikipedia.org/wiki/Modelo_OSI) y es realmente importante entender las diferencias entre cada uno de sus componentes. Por ejemplo, los browsers en general acceden a los sitios web utilizando el protocolo [HTTP](http://es.wikipedia.org/wiki/Hypertext_Transfer_Protocol), pero también soportan otros protcolos cómo [FTP](http://es.wikipedia.org/wiki/File_Transfer_Protocol) o [WS](http://es.wikipedia.org/wiki/WebSocket). Si leemos un poco la descripción de Websockets, en la primer oración nos encontramos que a más bajo nivel la comunicación es por sockets TCP.<br>
Más adelante entraremos en detalle sobre cómo funcionan los Websockets y qué problemáticas resuelven.

## TCP/UDP
[TCP](http://es.wikipedia.org/wiki/Transmission_Control_Protocol) es un protocolo de transmisión de datos que consiste en sockets (conexiones) los cuales pueden transmitir data bidireccionalmente. Varios protocolos cómo HTTP o FTP utilizan TCP internamente para la transmisión de datos. Es importante notar qué la comunicación se realiza entre Servidor-Cliente y no está pensado para utilizarse entre Cliente-Cliente.

[UDP](http://es.wikipedia.org/wiki/User_Datagram_Protocol) es otro protocolo utilizado para la transmisión de datos y está enfocado en la transmisión unidireccional. Una importante diferencia entre UDP y **TCP es que TCP agrega chequeos de integridad de los paquetes enviados**, por lo tanto sumando cierto overhead. Por esta razón UDP es mayormente utilizado cuando se requiere transmitir grandes volúmenes de datos y no es importante si se tiene algún tipo de pérdida de paquetes.

A continuación veremos un ejemplo de cómo crear un simple servidor TCP:
```js
var net = require('net');
var server = net.createServer(function(socket) { //'connection' listener
  console.log('Conexión recibida');
  socket.on('end', function() {
    console.log('Socket desconectado');
  });
  socket.write('hola que tal\r\n');
});
server.listen(8888, function() { 
  console.log('server TCP escuchando.');
});
```

Y un cliente que se conecte:
```js
var net = require('net');
var client = net.connect({port: 8888},
    function() { 
  console.log('El cliente se conectó');
  client.write('hola server TCP\r\n');
});
client.on('data', function(data) {
  console.log(data.toString());
  client.end();
});
client.on('end', function() {
  console.log('El cliente se desconectó');
});
```