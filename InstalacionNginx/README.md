# Inslatación de Nginx en Linux

![logo](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/logo.png)

## Índice

- <a href="#1">1. Requisitos previos</a>
- <a href="#2">2. Instalar Nginx</a>
- <a href="#3">3. Aplicar ajustes al firewall</a>
- <a href="#4">4. Comprobar estado del servidor web</a>
- <a href="#5">5. Configurar bloques de servidor</a>

<a name="1"></a>

### 1. Requisitos previos
Para esta práctica necesitamos tener una máquina con Ubuntu 20.04 con un usuario normal con privilegios root.

<a name="2"></a>

### 2. Instalar Nginx
Antes de empezar, como siempre, tendremos que actualizar los repositorios de Ubuntu. Con los comandos <b>sudo apt update y sudo apt upgrade</b>.

![1](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/1.png)

![2](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/2.png)

Después de actualizar los repositorios, procedemos a instalar <b>Nginx</b> con el comando <b>sudo apt install nginx</b>.

![3](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/3.PNG)

<a name="3"></a>

### 3. Aplicar ajustes al firewall
Antes de empezar a usar Nginx, tenemos que aplicar unos cambios en el firewall para permitir el acceso al servicio de Nginx. Para ello usaremos el comando <b>sudo ufw app list</b>, para ver la lista de todos los perfiles de las aplicaciones instaladas.

![4](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/4.PNG)

Para habilitar el perfíl de Nginx tendremos que hacer el siguiente comando: <b>sudo ufw allow ‘Nginx HTTP’</b>. Después de activarlo podemos comprobarlo con el comando <b>sudo ufw status</b>, para ver todos los perfiles que están activos.

![5](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/5.PNG)

<a name="4"></a>

### 4. Comprobar estado del servidor web
Cuando acabemos la instalación y configuración de Nginx, el servicio debería de estar activo para comprobarlo usaremos el comando <b>systemctl status nginx</b>.

![6](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/6.PNG)

Para comprobarlo mediante web, tendremos que poner en la url la ip del servidor, en nuestro caso será localhost, más el puerto al que está asociado Nginx que sería el 8080, la url quedaría tal que así: <b>localhost:8080</b>.

![16](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/16.png)

<a name="5"></a>

### 5. Configurar bloques de servidor
Nginx viene por defecto con un bloque de servidor por defecto, que estará en la ruta <b>/var/www/html</b>, pero nosotros crearemos nuestro propio dominio en la siguiente ruta: <b>/var/www/your_domain/html</b>. Con el comando <b>sudo mkdir -p your_domain/html</b>.

![7](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/7.PNG)

Después de crear el directorio, asignaremos la propiedad del directorio con la variable de entorno: usando el comando <b>sudo chown -R $USER:$USER /var/www/your_domain/html</b>.

![8](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/8.PNG)

Le daremos todos los permisos al propietario para que pueda leer, escribir y ejecutar archivos, con el comando <b>sudo chmod -R 755 /var/www/your_domain/</b>. Luego crearemos un fichero .html con el nombre <b>index.html</b> con el código que se muestra en pantalla.

![9](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/9.PNG)

Para que Nginx muestre el contenido anterior debemos de crear un archivo nuevo de configuración predeterminado. Lo crearemos en el siguiente directorio: <b>/etc/nginx/sites-available/your_domain</b>, con el siguiente código. Después de crearlo, haremos un enlace simbólico a la ruta: <b>/etc/nginx/sites-enabled/your_domain</b>.

![11](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/11.PNG)

![10](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/10.png)

Para evitar problemas de memoria, tendremos que ir al fichero <b>/etc/nginx/nginx.conf</b> y buscar la línea comentada <b>“#server_names_hash_bucket_size 64;”</b> y la descomentamos. Guardamos el fichero y salimos.

![12](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/12.PNG)

Para comprobar que no haya errores de sintaxis en el fichero de configuración usamos el comando <b>sudo nginx -t</b> que nos dirá si todo está correcto o no.

![13](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/13.PNG)

Para que funcione correctamente el dominio tenemos que agregarlo en el fichero <b>/etc/hosts</b> con la siguiente línea:
<b>127.0.1.1        your_domain your_domain.com www.your_domain.com</b>

![14](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/14.png)

Antes de probar si funciona en un navegador tendremos que reiniciar el servicio de Nginx. Una vez hecho abrimos un navegador poniendo directamente: <b>your_domain:8085</b>.

![15](https://github.com/Regnierd/Nginx/blob/main/InstalacionNginx/img/15.png)