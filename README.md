# Linux
## 1. Logs del Sistema
* Introducción a syslog
* Configuraciones avanzadas de syslog
* Rotación de logs
* Herramientas de logs
## 2. Administrar Usuarios y Grupos
* Comandos para gestionar cuentas de usuarios, grupos y contraseña
* Archivos de usuarios y grupos
* Herramientas de usuarios y grupos y delegación de privilegios
* Auditoría y límites de usuarios y grupos
## 3. Administrar Tareas Programadas y Configuración Regional
* Tareas programadas en Linux con cron
* Tareas programadas con anacron y con at
* Zonas horarias y fechas
* Configuración Regional
## 4. Mantener el Reloj del Sistema e Impresión
* Administrando la hora del equipo
* El daemon NTP en Linux
* Introducción a CUPS
* Trabajando con impresoras desde CUPS
## 5. X Windows System
* Instalación y configuración de X
* Configurar un administrador de pantalla
* Configurar el administrador de pantalla para ser usado con estaciones-X.
* Accesibilidad
## 6. Cifrado con GPG y Compilación
* Cifrar y firmar con GPG
* Cifrar archivos
* El kernel Linux
* Compilación del kernel
* Instalación de programas a partir del código fuente
## 7. Linux Servicios
* Familia de protocolos TCP-IP.
* Configuración de HW de red.
* Acceso a redes : PPP.
* Configuración de una LAN.
* Demonios y el superservidor de internet (inetd, xinetd).
* Servicios de acceso : Telnet / SSH.
* Servicios de transferencia de ficheros : FTP /SFTP/ SCP.
* Servicio de resolución de nombres : DNS.
* Servicios de compartición de ficheros e impresoras: NFS, Samba.
* Servicio de correo : SMTP.
* Servicios web : HTTP (Apache).
* Servicio de news.
* Servicio de IRC.
* Instalación de colas de trabajo : NQS.

#Creatubers
Publicado el 30 ene. 2017
En este tutorial te enseño a instalar un certificado SSL en tu servidor web usando Certbot y Let's Encrypt. ¿Quieres aprender a configurar un servidor VPS para montar tu página web? Mira este tutorial:

##Comandos y líneas de código:
```bash
deb http://ftp.debian.org/debian jessie-backports main
apt-get update && apt-get upgrade -y
apt-get install certbot -t jessie-backports
certbot certonly --webroot -w /var/www/html -d tudominio.com -d www.tudominio.com 
server {
 listen       443 ssl default;
    root /var/www/html;
    index index.php index.html index.htm;
    server_name tudominio.com www.tudominio.com;
 ssl_certificate /etc/letsencrypt/live/tudominio.com/fullchain.pem;
 ssl_certificate_key /etc/letsencrypt/live/tudominio.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
 location ~ /.well-known {
                allow all;
        }
  

    location / {
  # First attempt to serve request as file, then
  # as directory, then fall back to displaying a 404.
  #try_files $uri $uri/ =404;
  try_files $uri $uri/ /index.php?q=$uri&$args;
 }
 
 

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
 
 location ~ \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 365d;
    }

    location ~ \.(pdf)$ {
        expires 30d;
}
}

server {
 listen 80 default_server;
 listen [::]:80 default_server;
 server_name tudominio.com www.tudominio.com;
 return 301 https://$host$request_uri;
}

service nginx restart
crontab -e
@daily certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
```

Equipo utilizado:

-Cámara: Panasonic Lumix GH4R
-Objetivo: Panasonic Lumix 25mm f/1.7
-Micrófono: Sony ECMCS3
-Grabadora de sonido: Zoom H1
-Iluminación: antorcha LED Yongnuo YN160 III 


#Ejemplos de codigo
bash sh zsh shell Jekyll console apache
html js python perl haskell gawk awk 

```{r, engine='bash', count_lines.code_block_name}
apt-get remove --purge apache2*
wget https://www.dotdeb.org/dotdeb.gpg
apt-key add dotdeb.gpg
apt-get update && apt-get upgrade
apt-get dist-upgrade
apt-get install nginx
nginx -v
```

#Servidor

Texto a añadir en **/etc/apt/sources.list**
```sh
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all
```
Borrar apache2 e instalar nginx
```bash
apt-get remove --purge apache2*
wget https://www.dotdeb.org/dotdeb.gpg
apt-key add dotdeb.gpg
apt-get update && apt-get upgrade
apt-get dist-upgrade
apt-get install nginx
nginx -v
```

Instalaciónde php7
```console
apt-get install php7.0 php7.0-mysql php7.0-xmlrpc php7.0-cgi php7.0-curl php7.0-gd php7.0-fpm php7.0-apc php7.0-dev php7.0-mcrypt
service nginx restart
service php7.0-fpm restart
```
Texto a añadir en **/etc/nginx/nginx.conf**:
```apache
user www-data;
worker_processes 4;
pid /run/nginx.pid;
events {
    worker_connections 768;
    # multi_accept on;
}
http {
    ##
    # Basic Settings
    ##
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    # server_tokens off;
    client_max_body_size 50m;
    # server_names_hash_bucket_size 64;
    # server_name_in_redirect off;
    include /etc/nginx/mime.types;
    default_type application/octet-stream;
    ##
    # SSL Settings
    ##
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
    ssl_prefer_server_ciphers on;
    ##
    # Logging Settings
    ##
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    ##
    # Gzip Settings
    ##
    gzip on;
    gzip_disable "msie6";
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_buffers 16 8k;
    gzip_http_version 1.1;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    ##
    # Virtual Host Configs
    ##
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}
```
Texto a añadir en **/etc/nginx/sites-available/default**:
```apache
server {
    listen 80 default;
    root /var/www/html;
    index index.php index.html index.htm;
    server_name nombre.com www.nombre.com;
    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        #try_files $uri $uri/ =404;
        try_files $uri $uri/ /index.php?q=$uri&$args;
    }
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
