# Publicando una aplicación

A la hora de la puesta en marcha de una aplicación, muchos factores entran en juego. Detalles cómo elegir un tipo de servidor, un sistema operativo, configuración de permisos de usuario, configuración de puertos, entre muchos otros.<br>
Muchas veces resulta útil optar por una solución que nos brinde la posibilidad de obviar todas las configuraciones mencionadas anteriormente y que, mediante una serie de pasos sencillos, pueda publicar mi aplicación. <br>
A estas soluciones, se las llama [Platform as a service](http://en.wikipedia.org/wiki/Platform_as_a_service) (o PaaS). Algunas de ellas son:

- [Heroku](https://www.heroku.com/)
- [Modulus](https://modulus.io/)
- [DigitalOcean](https://www.digitalocean.com/)
- [OpenShift](http://openshift.redhat.com/)

La mayoría de estas opciones ofrecen cuentas gratuitas en las que uno puede crear (un número acotado de) aplicaciones. A continuación explicaremos los pasos para crear una aplicación en OpenShift.

## Openshift
Pasos a seguir:

1. [Crear un nuevo repositorio git](https://github.com/new)
2. [Subir cambios deseados al repositorio del punto 1](#subir-cambios-deseados-a-un-repositorio)
3. [Crear una cuenta en OpenShift](https://www.openshift.com/app/account/new)
4. [Crear una aplicación en OpenShift](#crear-una-aplicación-en-openshift)
5. (Opcional) [Realizar cambios y actualizar la aplicación creada en el paso 3](#realizar-cambios-a-una-aplicación-existente)

## Subir cambios deseados a un repositorio
Con el repositorio git creado, debemos ubicarnos en el directorio correspondiente (luego de haber hecho `git clone urlDelRepositorio`) y ejecutar los comandos para agregar todos los archivos nuevos y subirlos.
```
git add .
git commit -m "primera version de archivos"
git push
```

## Crear una aplicación en OpenShift
Una vez creada nuestra cuenta, deberíamos estar en condiciones de acceder a nuestra [lista de aplicaciones](https://openshift.redhat.com/app/console/applications). Debemos seleccionar "Add application" para luego seleccionar el tipo "Node.js 0.10":
![Node.js](http://imgur.com/V16fcI0.png)
En la siguiente pantalla, dentro del campo "Public URL" debemos ingresar la URL pública por la cual nosotros quisieramos acceder a nuestra aplicación.
En el campo "Source Code" ingresaremos la URL al repositorio de Git que creamos en el paso 1.

## Realizar cambios a una aplicación existente
Para autenticarte contra los servidores de OpenShift es necesario contar con keys SSH. Podés leer más sobre cómo generarlas [acá](https://developers.openshift.com/en/managing-remote-connection.html#keys). <br>
A continuación, deberás ingresar a la [lista de aplicaciones](https://openshift.redhat.com/app/console/applications) y hacer click en la aplicación en cuestión. Dentro de la configuración de dicha aplicación, deberás copiar el campo `Source Code`.
![source code](http://i.imgur.com/8b1uW9O.png)
Con ese texto se tendrá que ejecutar el comando `git clone source-code` para crear una carpeta del repositorio que contiene el código fuente de la aplicación.<br>
A continuación, se deberán realizar cambios en el repositorio git, y subir los mismos cómo en cualquier otro repositorio. Una vez que se ejecute `git push` OpenShift se encargará de reiniciar la aplicación para que tome los nuevos cambios.
