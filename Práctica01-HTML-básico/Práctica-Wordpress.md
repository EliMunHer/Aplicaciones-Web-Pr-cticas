# Instalación WordPress

## 1. Comprobar el punto de partida.

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

![Respuesta de los comandos:](/Aplicaciones-Web-Pr-cticas/Práctica01-HTML-básico/AWE_CAP1.png)
