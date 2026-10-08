# Virtualhost por nombre con dos puertos (80 y 9999) y una intranet con contraseña
## 1. Crear las carpetas y las páginas.
Primero creé las carpetas necesarias para almacenar las páginas web. Utilicé el siguiente comando:

sudo mkdir -p /var/www/smr/web /var/www/smr/intranet

Después creé la página principal de la web pública:

`echo "<h1>Bienvenidos a SMR</h1>" | sudo tee /var/www/smr/web/index.html`

Y creé la página de la intranet:

`echo "<h1>Intranet de SMR</h1>" | sudo tee /var/www/smr/intranet/intranet.html`

De esta forma, quedaron creadas dos carpetas:

    `/var/www/smr/web, que contiene la página pública index.html.`
    `/var/www/smr/intranet, que contiene la página de la intranet intranet.html.`

La página pública utiliza el nombre index.html, que es el nombre que Apache busca normalmente como página principal.

En cambio, la intranet utiliza intranet.html, por lo que posteriormente será necesario indicarle a Apache que esta es su página principal.

## 2. Crear el usuario de la intranet
Para poder proteger la intranet mediante usuario y contraseña instalé el paquete apache2-utils:

`sudo apt install apache2-utils -y`

Después creé el usuario alumno utilizando htpasswd:

sudo htpasswd -c /etc/apache2/.htpasswd alumno

El sistema me pidió introducir la contraseña dos veces para confirmar que era correcta.

El fichero /etc/apache2/.htpasswd contiene las credenciales necesarias para acceder a la intranet.

La opción -c se utiliza para crear el fichero desde cero. Si el fichero ya existiera y tuviera otros usuarios, no habría que utilizar esta opción porque se podrían eliminar los usuarios existentes.
## 3. Configurar el puerto 9999
A continuación modifiqué la configuración de puertos de Apache:

`sudo nano /etc/apache2/ports.conf`

Añadí el puerto 9999 debajo del puerto 80:

`Listen 80`
`Listen 9999`

De esta manera, Apache queda preparado para recibir conexiones tanto por el puerto 80 como por el puerto 9999.

Para guardar los cambios en Nano utilicé Ctrl+O, pulsé Enter y finalmente Ctrl+X para salir.
## 4. Crear el VirtualHost
Después creé el fichero de configuración del sitio:

`sudo nano /etc/apache2/sites-available/smr.conf`

Dentro del fichero configuré dos VirtualHost. El primero corresponde a la página pública y utiliza el puerto 80.

## 5. Activar el sitio y reiniciar Apache
Una vez creada la configuración, activé el sitio con:

`sudo a2ensite smr.conf`

Después desactivé el sitio que viene activado por defecto:

`sudo a2dissite 000-default.conf`

Antes de reiniciar Apache comprobé que la configuración no tuviera errores:

`sudo apachectl configtest`

El resultado correcto es:

`Syntax OK`

Finalmente reinicié el servicio Apache:

`sudo systemctl restart apache2`

Con esto Apache quedó funcionando con la nueva configuración.
