# Instalación Wordpress

Eliseo Muñoz Hernández | 2 CFGM de SMX (vesprada)

AWE

Fecha: 22-10-26
## 1. Compruebo el punto de partida.

Compruebo que LAMP funciona, y además apunto qué sitios tengo. Ejecuto:

``` bash
systemctl is-active apache2 mariadb
```

``` bash
php-v
```

``` bash
ls /etc/apache2/sites-enabled/
```

``` bash
grep Listen /etc/apache2/ports.conf
```

![Respuesta de los comandos:](Aplicaciones-Web-Prácticas/Práctica01-HTML-básico/img/Wordpress/AWE_CAP1.png)

## 2. Creo la base de datos y el usuario.

## 3. Descargo Wordpress y lo coloco en su carpeta.

## 4. Propietario y permisos.

## 5. Creo el VirtualHost de Wordpress.

## 6. Instalación desde el navegador.
