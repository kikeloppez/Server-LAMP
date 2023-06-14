# Instalar Wordpress en Servidor LAMP

Para instalar wordpress primero tenemos que crear una base de datos y un usuario con privilegios para la BD.

Para ello entramos en mysql.
```
mysql -u root -p
```
Ejecutamos los siguientes comandos.
![1]()

Instalamos los siguientes paquetes.
```
apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
```
Reiniciamos el servicio de Apache
```
sudo systemctl restart apache2
```
Entramos en el directorio de configuración de apache.
```
cd /etc/apache2/sites-available
```
En este directorio creo un fichero llamado wordpress.conf
```
nano wordpress.conf
```
Añado las siguientes lineas.
```
<Directory /var/www/wordpress/>
	AllowOverride All
</Directory>
```
Ejecuto  el siguiente comando.
```
a2enmod rewrite
```
Reinicio el servicio de apache.
```
systemctl restart apache2
```
Compruebo la configuración.
```
apache2ctl configtest
```
Me dirijo al directorio principal para descargar el paquete de Wordpress
```
cd /home/usuario
```
```
curl -O https://wordpress.org/latest.tar.gz
```
Descomprimimos el archivo.
```
tar xzvf latest.tar.gz
```
Añadimos un archivo para Wordpress.
```
touch wordpress/.htaccess
```
