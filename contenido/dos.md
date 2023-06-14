# Instalar y configurar LAMP

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
![5](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/5.png)
![6](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/6.png)

Accedemos al directorio de Apache.
```
cd /var/www/html
```
Creamos un enlace a PhpMyAdmin
```
ln -s /usr/share/phpmyadmin phpmyadmin
```
![7](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/7.png)

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
![8](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/8.png)
![9](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/9.png)

Vamos al navegador y accedemos al servidor mediante la IP.
![10](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/10.png)

Al intentar logearnos nos dará un error, por lo que debemos crear un nuevo usuario en MySQL con permisos administrador.
```
mysql -u root -p
```
![11](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/11.png)

Ejecutamos las siguientes lineas con los datos que queremos ponerle.
![12](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/12.png)

Una vez realizado, volvemos al navegador e intentamos logearnos con el usuario creado.
![13](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/13.png)
![14](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/14.png)

:arrow_left: [VOLVER](https://github.com/kikeloppez/Server-LAMP)
