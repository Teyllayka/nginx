# Nginx Instalācijas Instrukcija

## Sistēmas prasības

- **Operētājsistēma:** Linux
- **Procesors:** 1 GHz vai ātrāks
- **Atmiņa:** Vismaz 512 MB RAM
- **Disku vieta:** Vismaz 1 GB brīvas vietas
- **Tīkls:** Piekļuve internetam

### 1. Nginx Instalēšana

```
sudo apt install nginx -y
```

### 2. Nginx Statusa Pārbaude

```
sudo systemctl status nginx

```

### 3. Ugunsmūra Konfigurēšana

```
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

### 4. Nginx Darbības Pārbaude

```
sudo lsof -i -P -n | grep LISTEN | grep nginx
```

### 5. Vietnes Konfigurācijas Pievienošana

```
sudo nano /etc/nginx/sites-available/example.com
```

```
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/example.com/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Logging
    access_log /var/log/nginx/example.com.access.log;
    error_log /var/log/nginx/example.com.error.log;

    # Additional configuration
    # Uncomment these lines if SSL/TLS is set up
    # listen 443 ssl;
    # ssl_certificate /etc/ssl/certs/example.com.pem;
    # ssl_certificate_key /etc/ssl/private/example.com.key;
}
```

### 6. Aktivizē Vietni

```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```

### 7. Vietnes Kataloga Izveide

```
sudo mkdir -p /var/www/example.com/html
sudo nano /var/www/example.com/html/index.html

```

```
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to example.com!</title>
</head>
<body>
    <h1>Veiksmi ar Nginx!</h1>
</body>
</html>
```

### 8. Nginx Pārbaude un Restartēšana

```
sudo nginx -t
sudo systemctl restart nginx
```

### 9. DONE!

Atveriet pārlūkprogrammu un ievadiet sava servera IP adresi. Jūs redzēsiet vietni, kuru esat pievienojis konfigurācijā.
