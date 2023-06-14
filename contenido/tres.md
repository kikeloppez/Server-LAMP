# Instalar certificado SSL (HTTPS)

Instalamos el paquete UFW para permitir el acceso de Apache con el puerto 80 y 443.
```
apt install ufw
```
Ejecutamos el siguiente comando.
```
ufw allow "Apache Full"
```
![15](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/15.png)

Activamos el servicio SSL con el siguiente comando.
```
a2enmod ssl
```
Y reiniciamos el servicio apache
```
systemclt restart apache2
```
![16](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/16.png)

Creamos el certificado SSL personal.
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/clave-kike.key -out /etc/ssl/certs/clave-kike.crt
```
![17](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/17.png)

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
![19](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/19.png)

Activamos los ficheros de configuración.
![21](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/21.png)

Comprobamos el funcionamiento añadiendo "https://" en nuestro navegador.
![20](https://github.com/kikeloppez/Server-LAMP/blob/main/contenido/uno/20.png)

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
