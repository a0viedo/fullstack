# Sistemas Operativos

## Permisos
Los sistemas operativos actualmente utilizan un enfoque de restricción de privilegios basado en *anillos* que se pueden clasificar en dos partes: user y *kernel*. Básicamente, cualquier proceso/aplicación en el cual no se aclare que se ejecute con privilegios de *kernel* se ejecutará con priviligios de usuario.

## System calls
Cada sistema operativo se encarga de exponer una interfaz por la cual las aplicaciones realizarán pedidos de interrupciones, memoria, escalación de privilegios, etc. La interfaz consiste en una lista de *system calls* (o más comunmente syscalls) las cuales varían dependiendo del sistema operativo.

![Figura 1.](https://andrewharvey4.files.wordpress.com/2010/07/os.png) 

Si hacemos un zoom a lo que vendría a representar "OS" en la Figura 1, podremos ver que se puede desglosar en más partes.

![Figura 2.](http://docs.oracle.com/cd/E19683-01/806-5222/images/kernelovr.arch.epsi.gif)

La Figura 2 representa a un diagrama del kernel del sistema operativo [Solaris](http://es.wikipedia.org/wiki/Solaris_(sistema_operativo)). Describamos brevemente los bloques más importantes:
- Process management: se encarga de exponer métodos para trabajar con procesos, cómo por ejemplo para su creación, destrucción e identificación.
- Device control: se encarga del manejo de los dispositivos de I/O.
- Networking: encargado del control de las interfaces utilizadas para la conectividad. Por ejemplo eth0, wlan1, etc.
- Virtual memory: se encarga del mapeo de páginas virtuales a páginas físicas. Las aplicaciones accederán únicamente a páginas de memoria virtuales.
- File system: encargado de la interfaz utilizada para guardar/leer información de dispositivos de almacenamiento. El concepto de directorios (carpetas) es sólo una abstracción del file system, en el fondo lo único que se guarda son ceros y unos.




