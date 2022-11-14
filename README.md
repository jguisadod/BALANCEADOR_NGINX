# BALANCEADOR CON NGINX
## Scripts de aprovisionamiento de todas las maquinas
### Scrip de aprovisionamiento para Mysql
![](images/scriptmysql.jpg)
### Scrip de aprovisionamiento para Nginx
![](images/scriptnginx.jpg)
### Scrip de aprovisionamiento para el Balanceador
![](images/scriptbal.jpg)
## CONFIGURACIÓN MYSQL
### Lo primero será acceder al directorio **/etc/mysql/mariadb.conf.d** y editar el fichero de configuración **50-server.cnf**
![](images/sq1.jpg)
### En el fichero de configuración cambiamos la *bind-address* por la ip de la máquina Mysql
![](images/sq2.jpg)
### Tras esto utilizamos el comando *mysql_secure_installation* para asignarle una contraseña al root
![](images/sq3.jpg)
### Iniciamos sesión como root en mysql y creamos el usuario *lamp_user*
![](images/sq4.jpg)
### Con el comando **sudo git clone** clonamos el repositorio en nuestra máquina
![](images/sq5.jpg)
### Nos vamos a la ruta *iaw-practica-lamp/db* y cargamos la base de datos
![](images/sq6.jpg)
### Una vez cargada la base de datos volvemos a iniciar sesión como root y le damos todos los privilegios al usuario anteriormente creado. Tras esto recargamos los privilegios
![](images/sq7.jpg)
## CONFIGURACIÓN NGINX
### Primero vamos a la ruta */var/www* y creamos una carpeta. Cambiamos el propietario de dicha carpeta a **www-data**
![](images/ng1.jpg)
### Dentro de la carpeta clonamos el repositorio remoto
![](images/ng2.jpg)
### Nos vamos a la ruta *iaw-practica-lamp/src* y movemos todos los archivos de ese directorio a la carpeta creada anteriormente
![](images/ng3.jpg)
### Editamos el fichero *config.php* y añadimos la ip de la máquina de Mysql
![](images/ng4.jpg)
### Lo siguiente es ir a la ruta **/etc/php/7.4/fpm/pool.d** y editamos el archivo *www.conf*
![](images/ng5.jpg)
### En este archivo buscamos la línea donde pone *listen* y la cambiamos
![](images/ng6.jpg)
### Restauramos el servicio. Nos vamos a **/etc/nginx/sites-available** y hacemos una copia del archivo *default*
![](images/ng7.jpg)
### Editamos la copia añadiendo la ruta de la carpet anteriormente creada a la línea *root*, añadimos *index.php* para que pueda detectarlo y descomentamos varias líneas
![](images/ng8.jpg)
### Creamos un enlace de la copia hacia **sites-enabled** y borramos el archivo *default*
![](images/ng9.jpg)
### Con el comando *sudo nginx -t* comprobamos que todo está correcto
![](images/ng10.jpg)
### Ya solo queda restaurar nginx y hacer todo lo anterior de nuevo en otra máquina Nginx
## CONFIGURACIÓN BALANCEADOR
### Vamos a **/etc/nginx/sites-enabled** y borramos el archivo *default*
![](images/ba1.jpg)
### Con el comando **sudo nano /etc/nginx/conf.d/balanceador.conf** creamos el archivo *balanceador.conf* y lo rellenamos con estas líneas, donde declaramos las ip de las máquinas conectadas al balanceador, el nombre del servidor, el puerto, etc...
![](images/ba2.jpg)