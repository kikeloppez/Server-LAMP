# Dos

En mi caso voy a usar una maquina virtual en VirtualBox para hacer el simulacro.

Las caracteristicas de la maquina son:
- 50Gb
- 4 Gb RAM
- 2 nucleos/cores
- Adaptador puente
- IP Estática

Antes de instalar ningun programa vamos a actualizar el equipo usando los siguientes comandos.
```
apt update & apt upgrade -y
```
Una vez actualizado, instalamos los siguientes paquetes.
```
apt install apache2 php php-mysql mysql-server
```
```
 apt install libapache2-mod-php phpmyadmin
```
Configuramos la contraseña para el servicio de PhpMyAdmin.
![5]()
![6]()
