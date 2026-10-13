### Instalación MariaDB

## 1. Instalación del sistema

Empezamos actualizando la lista de paquetes.

`sudo apt update`

Comprobamos que apache está activo.

`systemctl is-active apache2`

## 2. Instalación de MariaDB

Ejecutamos el siguiente comando para instalarlo:

`sudo apt install mariadb-server -y`

Y ahora comprobamos la versión que tenemos de mariadb con:

`mariadb --version`

### ¿Qué diferencia hay entre el paquete mariadb-server y el paquete mariadb-client? ¿Cuál de los dos ha instalado?

## 3. Comprobamos que mariadb esté en funcionamiento

`sudo systemctl status mariadb`

`systemctl is-enabled mariadb`

### ¿Qué diferencia hay entre active (running) y enabled? ¿Qué pasaría con la web de WordPress si MariaDB estuviera active pero no enabled y se reiniciara el servidor?

## 4. ¿Qué pasa si MariaDB está parado?

Vamos a comprobarlo, deteniendo a propósito el servicio.

`systemctl stop mariadb`

Para detenerlo.Y:

`systemctl is-active mariadb`

Para comprobar que se ha detenido.

Desactivado MariaDB, intentamos entrar:

`mariadb`

Y debería responderte algo parecido a:

**ERROR 2002 (HY000): Can't connect to local server through socket '/run/mysqld/mysqld.sock' (2)**

Volvemos a arrancarlo, y comprobamos que funciona.

`sudo systemctl start mariadb`

`systemctl is-active mariadb`
