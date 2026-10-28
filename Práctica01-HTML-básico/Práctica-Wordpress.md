# Instalación Wordpress

Eliseo Muñoz Hernández | 2 CFGM de SMX (vesprada)

AWE

Fecha: 22-10-26

# Índice

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

![Respuesta de los comandos:](img/AWE_CAP1.png)

Podemos ver que tanto apache2 como mariadb están activos. Por otra parte, no tenía el puerto 8080 desde antes, lo habilité antes de que se pidiera en la guía. Por último, comprobamos la versión de PHP. Además, en la imagen se puede apreciar que no tengo ningún sitio activado.

### 1.1 ¿Qué sitios tienes habilitados y en qué puertos escucha Apache? ¿Qué puerto vas a usar para WordPress y por qué no el 80?

No tengo ni un solo sitio habilitado, y apache escucha por los puertos:

1. Puerto 80.
2. Puerto 9999.
3. Puerto 8080.

Además del 443 de HTTPS.

Voy a usar el 8080 para Wordpress... en realidad, porque así lo pedía la guía. No tengo ningún sitio habilitado, por tanto el puerto 80 está libre y podría hacer uso del mismo.

## 2. Creo la base de datos y el usuario.

Para crear la base de datos que usará Wordpress, y también un usuario con permiso SOLO sobre ella... primero tenemos que entrar en mariadb.

```bash
sudo mariadb
```

### 2.1 Creo la base de datos.

```sql
CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Creamos una base de datos llamada `wordpress`, donde WordPress guardará todas sus tablas. Es mejor que tenga la suya propia que compartirla con otras aplicaciones, porque así sus datos quedan separados y es más fácil hacer copias de seguridad.

### 2.2 Creo el usuario.

```sql
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY '********';
```

Creamos el usuario `wp_user`, con el que WordPress se conectará a MariaDB. El `@'localhost'` hace que solo pueda conectarse desde la propia máquina, y WordPress y MariaDB están en el mismo servidor, así que no necesita más. La contraseña no la escribo aquí por seguridad.
### 2.3 Darle permiso solo sobre su base de datos.

```sql
GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
```

### 2.4 Aplico los cambios y salgo.

```sql
FLUSH PRIVILEGES;
```

```sql
EXIT;
```

### 2.5 Compruebo que el usuario funciona.

Antes de seguir, comprobamos que el usuario se ha creado bien y puede entrar.

```bash
mariadb -u wp_user -p wordpress
```

Una vez dentro:

```sql
SHOW TABLES;
```

Debe responder `Empty set`. Eso significa que el usuario puede entrar y ver su base de datos, pero todavía no tiene tablas.

![Comprobación del usuario wp_user:](img/AWE_CAP2.png)

### 2.6 ¿Por qué creamos wp_user en lugar de usar root?

Porque root tiene control total sobre todo MariaDB. Si WordPress se viera comprometido, el atacante tendría ese poder.

### 2.7 ¿Qué significa wordpress.* en la orden GRANT?

Indica a qué se aplican los permisos: wordpress es la base de datos y * significa “todas sus tablas”. Así wp_user tiene todos los permisos solo dentro de la base wordpress y ninguno sobre las demás.

## 3. Descargo Wordpress y lo coloco en su carpeta.

## 4. Propietario y permisos.

## 5. Creo el VirtualHost de Wordpress.

## 6. Instalación desde el navegador.
