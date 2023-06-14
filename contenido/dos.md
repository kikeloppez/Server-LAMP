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

Ejecutamos las siguientes lineas con los datos que queremos ponerle.
![12]()

Una vez realizado, volvemos al navegador e intentamos logearnos con el usuario creado.
![13]()
![14]()

### Instalar certificado SSL (HTTPS)

Instalamos el paquete UFW para permitir el acceso de Apache con el puerto 80 y 443.
```
apt install ufw
```
Ejecutamos el siguiente comando.
```
ufw allow "Apache Full"
```
![15]()

Activamos el servicio SSL con el siguiente comando.
```
a2enmod ssl
```
Y reiniciamos el servicio apache
```
systemclt restart apache2
```
![16]()

Creamos el certificado SSL personal.
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/clave-kike.key -out /etc/ssl/certs/clave-kike.crt
```
![17]()

Para activar el redireccionamiento creamos un archivo en la siguiente ruta.
```
nano /etc/apache2/sites-available/192.168.1.35.conf
```
Añadimos el siguiente contenido.
```
<VirtualHost *:443>
   ServerName 192.168.1.35
   DocumentRoot /var/www/192.168.1.35

   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/clave-kike.crt
   SSLCertificateKeyFile /etc/ssl/private/clave-kike.key
</VirtualHost>
```
Creamos el directorio de nuestro servidor y un fichero index.html
```
mkdir /var/www/192.168.1.35
```
Dentro del index podemos poner lo que queramos, ya que será reemplazado en el futuro.
```
nano /var/www/192.168.1.35/index.html
```
![19]()

Activamos los ficheros de configuración.
![21]()

Comprobamos el funcionamiento añadiendo "https://" en nuestro navegador.
![20]()

Finalmente para redirigir "http" a "https" sin tener que añadirlo hago lo siguiente.

Modifico el siguiente fichero.
```
nano /etc/apache2/sites-available/192.168.1.35.conf
```
Añado las siguientes lineas al final del documento.
```
<VirtualHost *:80>
	ServerName 192.168.1.35
	Redirect / https://192.168.1.35/
</VirtualHost>
```
Ejecutamos los siguientes comandos para activar la configuración.
```
apachectl configtest
```
```
systemctl reload apache2
```
Finalmente volvemos a probar accediendo desde "http://192.168.1.35" y vemos como nos redirige a "https://"
