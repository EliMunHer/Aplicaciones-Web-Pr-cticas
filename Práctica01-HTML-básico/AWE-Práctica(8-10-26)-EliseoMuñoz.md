# 1. Instalar Ubuntu Server.
## 1. Algunos detalles del SO escogido.
Ubuntu Server es una distribución de Linux, diseñada para servidores. 
Suele utilizarse para alojar páginas web, bases de datos, aplicaciones y servicios en red. No incluye ninguna gráfica por defecto, por lo que se administra directamente desde la terminal. 
Es gratuito, seguro, estable y de código abierto. 
## 2. Montaje de la máquina virtual en VirtualBox.
Para montar la máquina virtual con el SO Ubuntu Server, el proceso fue muy sencillo. Dentro de la interfaz gráfica de Oracle VirtualBox, se pulsa "Nova", "New" o "Nueva". Ahí es donde se ajustan los parámetros de la máquina virtual que quieres montar.
Yo, primero, puse el nombre: "UbuntuServer_AWE", y el siguiente paso fue escoger el archivo ISO que la máquina utilizaría para instalar el sistema operativo, en mi caso, "Ubuntu Server 24.10".
Entonces ajusté los parámetros del hardware que usará la máquina virtual, de modo que quedó así:
`Memoria base:` 2048 MB.
`Procesadores:` 2.
`Disco duro:` 25 GB.
Luego configuré 2 adaptadores de red.
1. El primero en modo NAT, para que pueda salir a Internet desde el router.
2. El segundo en modo Red solo anfitrión, para comunicarse con el ordenador anfitrión y otras máquinas virtuales, sin exponerlas directamente a Internet.
(Tuve que crear una red solo anfitrión en la interfaz de Oracle VirtualBox, y escoger la dirección IP que tendría. Le puse el nombre "vboxnet0".
Y ya estaría finalizada, lista para el:
## 3. Proceso de instalación.
Seleccioné la opción de instalar/actualizar Ubuntu Server, elegí el idioma y el teclado y actualicé el instalador. Después, mantuve la configuración predeterminada del servidor y de red, seleccioné Use an entire disk para el almacenamiento y confirmé el formateo. Configuré el usuario y la contraseña, omití Ubuntu Pro e instalé OpenSSH Server. Finalmente, completé la instalación, reinicié la máquina virtual y, tras el arranque, inicié sesión con las credenciales configuradas
