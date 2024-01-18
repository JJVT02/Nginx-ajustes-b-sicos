# Instalacion
## Paso 1. Actualizar el sistema
Antes de comenzar la instalación, se recomienda actualizar el sistema. Para hacerlo, ejecute el siguiente comando:
```bash
sudo apt update && sudo apt upgrade
```

Paso 2. Instalar Nginx
```bash
sudo apt install nginx
```

Paso 3. Iniciar Nginx

```bash
sudo systemctl start nginx

```
Paso 4. Verificar el estado de Nginx
```bash
sudo systemctl status nginx

```

Paso 5. Configurar el firewall
```bash
sudo ufw allow 'Nginx HTTP'
sudo ufw allow 'Nginx HTTPS'
```

Paso 6. Verificar Nginx
![](/img/1.png)
Paso 7. Configurar un host virtual
```bash
sudo nano /etc/nginx/sites-available/test.friendhosting.net
```
Agregue el siguiente código al archivo:

```bash
server {
    listen 80;
    listen [::]:80;

    server_name test.friendhosting.net www.test.friendhosting.net;

    root /var/www/test.friendhosting.net/;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```


Paso 8. Activar el host virtual
```bash
sudo ln -s /etc/nginx/sites-available/test.friendhosting.net /etc/nginx/sites-enabled/

```
Luego, reinicie Nginx:


```bash
sudo systemctl restart nginx

```

Paso 9. Crear el directorio raíz del sitio web
```bash
sudo mkdir -p /var/www/test.friendhosting.net

sudo chown -R www-data:www-data /var/www/test.friendhosting.net

sudo cp /var/www/html/index.nginx-debian.html /var/www/test.friendhosting.net/index.html

sudo chown -R www-data:www-data /var/www/test.friendhosting.net/

```

#### Ahora, al ingresar http://test.friendhosting.net en la barra de direcciones del navegador, debería ver la página estándar «¡Bienvenido a nginx!».

