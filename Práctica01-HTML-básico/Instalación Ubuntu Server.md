# Instalación de Ubuntu Server 24.04 en VirtualBox

## Índice

1. [Objetivo](#1-objetivo)
2. [Crear la red Host-only](#2-crear-la-red-host-only)
3. [Crear y configurar la máquina virtual](#3-crear-y-configurar-la-máquina-virtual)
4. [Instalar Ubuntu Server](#4-instalar-ubuntu-server)
5. [Comprobar las interfaces de red](#5-comprobar-las-interfaces-de-red)
6. [Configurar una IP fija con Netplan](#6-configurar-una-ip-fija-con-netplan)
7. [Conectarse mediante SSH](#7-conectarse-mediante-ssh)
8. [Comprobación final](#8-comprobación-final)
9. [Problemas frecuentes](#9-problemas-frecuentes)

## 1. Objetivo

Crear una máquina virtual con Ubuntu Server 24.04 LTS para realizar las prácticas del módulo de Aplicaciones Web. La máquina tendrá dos adaptadores de red:

- **NAT:** permite acceder a Internet para actualizar el sistema e instalar programas.
- **Host-only:** crea una red privada entre la máquina virtual y el equipo anfitrión para conectarse mediante SSH.

## 2. Crear la red Host-only

Desde VirtualBox, accedemos a **Archivo → Herramientas de red del anfitrión**.

1. Pulsamos **Crear** para generar un adaptador, normalmente llamado `vboxnet0`.
2. Comprobamos que su dirección IPv4 sea `192.168.56.1` y su máscara `255.255.255.0`.
3. Desactivamos el servidor DHCP, ya que configuraremos la IP de la máquina virtual manualmente.

Esta configuración se realiza una sola vez y permite establecer una conexión privada entre ambos equipos.

## 3. Crear y configurar la máquina virtual

En VirtualBox, pulsamos **Nueva** y configuramos:

- **Nombre:** `SMR-AplicacionesWeb`.
- **Tipo:** Linux, Ubuntu (64-bit).
- **Memoria RAM:** mínimo 2048 MB.
- **Disco duro:** VDI, reservado dinámicamente, de 20-25 GB.
- **Procesador:** 1 o 2 CPU, según los recursos disponibles.

Con la máquina apagada, entramos en **Configuración → Red** y habilitamos los dos adaptadores:

| Adaptador | Modo | Función |
|---|---|---|
| 1 | NAT | Acceso a Internet |
| 2 | Solo-anfitrión (`vboxnet0`) | Conexión privada por SSH |

## 4. Instalar Ubuntu Server

En **Configuración → Almacenamiento**, seleccionamos la unidad óptica y cargamos la ISO de Ubuntu Server 24.04 descargada desde la web oficial de Ubuntu.

Iniciamos la máquina virtual y seguimos el instalador:

1. Elegimos el idioma y la distribución del teclado.
2. Seleccionamos Ubuntu Server, sin la versión minimizada.
3. Dejamos las interfaces de red con DHCP temporalmente.
4. Dejamos el proxy y el mirror con sus valores predeterminados.
5. Seleccionamos el disco virtual completo para instalar Ubuntu.
6. Creamos el usuario, la contraseña y el nombre del servidor (*hostname*).
7. En **SSH Setup**, marcamos `Install OpenSSH server`.
8. No seleccionamos aplicaciones adicionales.
9. Terminamos la instalación y reiniciamos la máquina.

**Importante:** hay que recordar el usuario y la contraseña, y activar OpenSSH durante la instalación para poder conectarnos desde el equipo anfitrión.

## 5. Comprobar las interfaces de red

Tras iniciar sesión en Ubuntu, ejecutamos:

```bash
ip a
```

Este comando muestra las interfaces de red y sus direcciones IP. Normalmente:

- La interfaz NAT tiene una IP del rango `10.0.2.x`.
- La interfaz Host-only tendrá una IP del rango `192.168.56.x` o todavía no tendrá ninguna.

Comprobamos que hay conexión a Internet:

```bash
ping -c 3 archive.ubuntu.com
```

Si recibimos respuestas, la conexión funciona. Si no, debemos revisar la configuración de red.

## 6. Configurar una IP fija con Netplan

Netplan permite configurar las interfaces de red en Ubuntu Server.

Primero, localizamos el archivo de configuración:

```bash
ls /etc/netplan/
```

Editamos el archivo `.yaml` que aparezca, sustituyendo el nombre por el correcto:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

Configuramos las interfaces con sus nombres reales, obtenidos mediante `ip a`. Por ejemplo:

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      dhcp4: false
      addresses:
        - 192.168.56.10/24
```

En este ejemplo, `enp0s3` utiliza DHCP para la conexión NAT, mientras que `enp0s8` tiene una IP fija para Host-only.

**Nota:** la indentación de YAML es importante. Se deben utilizar espacios, nunca tabuladores.

Guardamos el archivo en Nano con `Ctrl + O`, pulsamos `Enter` y salimos con `Ctrl + X`.

Aplicamos la configuración:

```bash
sudo netplan apply
```

Comprobamos el resultado:

```bash
ip a
```

La interfaz Host-only debe mostrar la dirección `192.168.56.10/24`. Cada alumno debe utilizar una IP que no esté asignada a otra máquina.

## 7. Conectarse mediante SSH

Desde una terminal del equipo anfitrión, ejecutamos:

```bash
ssh tu_usuario@192.168.56.10
```

Sustituimos `tu_usuario` por el usuario creado durante la instalación.

La primera vez, aceptamos la huella del servidor escribiendo `yes` y después introducimos la contraseña.

Si la conexión funciona, podremos administrar Ubuntu Server desde la terminal del equipo anfitrión sin tener que utilizar directamente la ventana de VirtualBox.

## 8. Comprobación final

Antes de comenzar las prácticas de Aplicaciones Web, verificamos que:

- [ ] La máquina virtual tiene los dos adaptadores habilitados: NAT y Host-only.
- [ ] Ubuntu Server 24.04 está instalado.
- [ ] OpenSSH Server está instalado y funciona.
- [ ] `ip a` muestra las interfaces y sus direcciones IP.
- [ ] El comando `ping -c 3 archive.ubuntu.com` comprueba el acceso a Internet.
- [ ] La IP Host-only está configurada de forma fija mediante Netplan.
- [ ] Podemos conectarnos desde el equipo anfitrión mediante SSH.

## 9. Problemas frecuentes

| Problema | Posible solución |
|---|---|
| No aparece la interfaz Host-only | Comprobar que el adaptador 2 esté habilitado y conectado a `vboxnet0`. |
| No hay conexión a Internet | Revisar que el adapt
