# Instalación Ubuntu Server
### Crear la máquina virtual
1.  Abrimos Virtual Box.
2.  Arriba a la derecha, hacemos clic en "Nueva".
3.  Cambiamos el nombre (Por ejemplo, "UbuntuServer_Examen_AWE").
4.  En "Iso Image", introducimos el archivo ISO, adjuntándolo desde la carpeta en la que lo tenemos almacenado.
5. Desactivamos la casilla "Proceed with Unattended Instalattion", que se encuentra justo debajo de la opción "OS Version".
6. Podemos hacer clic en "Endavant".
7. A partir de ahí, ajustamos los siguientes parámetros:
  - Memoria Base = 2048 MB.
  - Procesadores = 2.
  - Disk Size = 25 GB.
8. Volvemos a pulsar en "Endavant".
9. Pulsamos en "Finish".

### Arrancar la máquina virtual

**Si da error, posiblemente debas comprobar las versiones de Oracle VirtualBox. Aunque puedes probar eliminando la máquina virtual, y haciendo otra exactamente igual.**

A partir de ahí, te da tres opciones. Alguna tiene que decir algo parecido a: "Try to install/upgrade UbuntuServer". Esa es la que pulsarás.
Acto seguido, te pedirá escoger el idioma. Busca "Español", o "Spanish".

Entonces, te saldrá algo similar a:

`Actualizar al instalador nuevo`

`Continuar sin actualizar`

`Atrás`

Puedes pulsar la primera opción, "Actualizar al instalador nuevo".

Tras actualizarse, pedirá el idioma del teclado. 

Escoge `Done`.
*Enter*

Ahora debes escoger el tipo de instalación. Te dará tres opciones:

1. ` [X] Ubuntu Server`
2. ` [ ] Ubuntu Server (minimized)`
3. ` [ ] Additional options`

Queremos la primera opción. Predeterminadamente, estará pulsada,lo sabrás por esa "X" entre los [].

Escoge `Done`.
*Enter*

**"Network Configuration"**

Escoge `Done`.
*Enter*

**"Proxy configuration"**

Puedes  dejarlos en blanco.

Escoge `Done`.
*Enter*

**"Ubuntu archive mirror configuration"**

Escoge `Done`.
*Enter*

**"Guided storage configuration"**

Comprueba que solo esté pulsada la opción:

`Use an entire disk`

Puede que se te escoja otra también, pero desmárcala. 

Escoge `Done`.
*Enter*

**"Storage configuration"**

Escoge `Done`.
*Enter*

**"Confirm destructive action"**

Escoge `Continue`
*Enter*

**"Profile configuration"**

Puedes rellenar los huecos con la siguiente información.
Eloise
`Your name:` Eliseo

`Your servers name:` ubuntu_server

`Pick a username:` eliseo07

`Choose a password:` 20072005

`Confirm your password:` 20072005

**"Upgrade to Ubuntu Pro"**

Puedes marcar la opción `Skip for now`

Escoge `Done`.
*Enter*

**"SSH configuration"**

Marca la opción `Install OpenSSH server`

Escoge `Done`.
*Enter*

**"Featured server snaps"**

Escoge `Done`.
*Enter*

Nos deja instalar "paquetes" adicionales, pero no hace falta que lo hagamos.

**"Installing system..."**

**"Updating system..."**

**"Installation complete!""**

Escoge `Reboot Now`
*Enter*

Seguramente te saldrá un error.

`[FAILED] Failed unmounting cdrom-mount - /cdrom.`

Reiniciamos la máquina.

Al encender la máquina, te pedirá nombre de usuario, y luego la contraseña.

### Configurar las interfaces de red

En Oracle VirtualBox:

Parámetros>Red>Adaptador 1

Marca la casilla "Habilitar adaptador de red", y en "Conectado a", selecciona NAT.

...

Iniciamos la máquina virtual, y entramos en nuestro usuario.

Entonces, para comprobar el fichero al que has de acceder, puedes escribir:

`ls /etc/netplan`

Te responderá algo parecido a:

`50-cloud-init.yaml`

Así que ese es el fichero que buscamos.

Escribimos:

`sudo nano /etc/netplan/50-cloud-init.yaml`

Puedes usar `TAB` para ayudarte.

### Conectarse por SSH

Abre la terminal del sistema operativo anfitrión. 

Puedes comprobar si tienes conexión con la MV haciendo un ping. Ejemplo:

`Ping 192.168.56.10`

Entonces, si todo está correcto, escribe el siguiente comando:

`ssh (usuario_MV)@(direccciónIP)`

En mi caso, por ejemplo es:

`ssh eliseo07@192.168.56.10`

Debe pedirte algo de una clave, acéptala.

Y a continuación debería pedirte la contraseña.
