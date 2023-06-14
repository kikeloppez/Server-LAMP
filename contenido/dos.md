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

Accedemos al directorio de Apache.
```
cd /var/www/html
```
Creamos un enlace a PhpMyAdmin
```
ln -s /usr/share/phpmyadmin phpmyadmin
```
![7]()

Reiniciamos el servicio de apache.
```
systemctl restart apache2
```
Creamos un fichero en el directorio de apache.
```
nano info.php
```
Le añadimos la siguiente linea.
```
<?php phpinfo(); ?>
```
![8]()
![9]()

Vamos al navegador y accedemos al servidor mediante la IP.
![10]()

Al intentar logearnos nos dará un error, por lo que debemos crear un nuevo usuario en MySQL con permisos administrador.
```
mysql -u root -p
```
![11]()
### Instalar certificado SSL (HTTPS)

Instalamos el paquete UFW para permitir el acceso de Apache con el puerto 80 y 443.
```
apt install ufw
```
Ejecutamos el siguiente comando.
```
ufw allow "Apache Full"
```
![]
