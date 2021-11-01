# Inslatación de PHP en Ubuntu para Nginx

![logo]()

## Índice

- <a href="#1">1. PHP para Apache</a>
- <a href="#2">2. PHP para Nginx</a>
- <a href="#3">3. Cómo probar PHP con Nginx</a>

<a name="1"></a>

### 1. PHP para Apache 
Para instalar PHP para Apache en Ubuntu tendremos que actualizar los repositorios locales de Ubuntu. Para ello usaremos el comando sudo apt update.

![1]()

Después de actualizar hacemos el comando: sudo apt install -y php

![2]()

<a name="2"></a>

### 2. PHP para Nginx
Por otro lado, también se puede instalar para el servicio de Nginx. Usando el comando: sudo apt install -y php-fpm.

![3]()

Después de que acabe la instalación tendremos que configurar Nginx para que se pueda conectar al servicio PHP-FPM. Para ello  tendremos que ir al archivo que se encuentra en la siguiente ruta: /etc/nginx/sites-available/default y encontrar el siguiente pedazo de código comentado.

![4]()

Descomentamos las siguientes líneas y guardamos los cambios.

![5]()

<a name="3"></a>

### 3. Cómo probar PHP con Nginx
Antes de probar si funciona, tendremos que recargar la configuración de Nginx. Usando el comando sudo systemctl reload nginx.

![6]()

A continuación, creamos un fichero en la siguiente ruta: /var/www/html/info.php con el siguiente código de PHP.

![7]()

Por último, abrimos un navegador y comprobamos que funciona poniendo en la url:
localhost:8080/info.php

![8]()

