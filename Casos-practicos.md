---
# **Casos Prácticos**

---
<p align="center">
  <img src="/Imagenes/NGINX6.jpg" alt="Descripción de la imagen" width="600"/>
</p> 

---
## **A) Versión de *Nginx* instalado.**

---
- Ejecutamos *nginx -v* para saber la versión de Nginx que hemos instalado.

````bash
sudo nginx -v
````

<p align="center">
  <img src="/Imagenes/1.png" alt="Descripción de la imagen" width="300"/>
</p> 

---
## **B) Servicio asociado.**

---
- El servicio asociado de ***Nginx*** se refiere a los procesos o componentes que trabajan junto con el servidor web ***Nginx*** para gestionar y optimizar el tráfico web, realizar balanceo de carga, manejo de solicitudes, y asegurar la correcta entrega de contenido.

- Para consultar el servicio asociado de ***Nginx***:

**1.	Verificamos el estado del servicio de *Nginx*** utilizando el comando *sudo systemctl status nginx*, y nos indica que está activo:

````bash
sudo systemctl status nginx
````

<p align="center">
  <img src="/Imagenes/2.png" alt="Descripción de la imagen" width="500"/>
</p> 

- **Active:** active (running) indica que el servicio está en ejecución.
- **Main PID:** es el identificador del proceso principal de **Nginx**.

**2.	Para consultar los procesos asociados de *Nginx***, ejecutamos *ps aux | grep nginx*, esto filtrará los procesos en ejecución, y así podremos ver el proceso principal de ***Nginx*** ***(master)*** y los procesos secundarios ***(workers)***.

````bash
sudo ps -aux | grep nginx
````

<p align="center">
  <img src="/Imagenes/5.png" alt="Descripción de la imagen" width="500"/>
</p> 

**3.	Consultar logs del servicio:** Nginx genera archivos de log donde podemos observar la actividad del servidor y sus posibles errores. 
- Log de acceso:  *cat /var/log/nginx/access.log*

````bash
sudo cat /var/log/nginx/access.log
````

<p align="center">
  <img src="/Imagenes/6.png" alt="Descripción de la imagen" width="600"/>
</p> 

- Log de errores: *cat /var/log/nginx/error.log*

````bash
sudo cat /var/log/nginx/error.log
````

<p align="center">
  <img src="/Imagenes/7.png" alt="Descripción de la imagen" width="500"/>
</p> 

**4.	Para ver qué otros servicios o procesos están interactuando con *Nginx***, como bases de datos, servicios de **caché** o servicios de **backend**, podremos examinar las configuraciones y puertos en uso ejecutando *sudo netstat -tuln | grep 80*.
Nos mostrará los puertos donde Nginx está escuchando (generalmente en el puerto **80** para **HTTP** o **443** para **HTTPS**).

````bash
sudo netstat -tuln | grep 80
````

<p align="center">
  <img src="/Imagenes/8.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
## **C) Ficheros de configuración.**

---
. **Los ficheros más importantes son:**

•	Archivo de configuración global: */etc/nginx/nginx.conf* 

````bash
sudo nano /etc/nginx/nginx.conf
````

<p align="center">
  <img src="/Imagenes/25.png" alt="Descripción de la imagen" width="500"/>
</p> 

•	Archivos específicos de cada sitio web: 

````bash
sudo cd /etc/nginx/ | ls -l
````
<p align="center">
  <img src="/Imagenes/24b.png" alt="Descripción de la imagen" width="300"/>
</p> 

*/etc/nginx/sites-available/* 

- En este directorio tendremos los archivos disponibles para publicar. Contiene un archivo **default** (por defecto) que podremos editar con **Nano**.

<p align="center">
  <img src="/Imagenes/23.png" alt="Descripción de la imagen" width="400"/>
</p> 

*/etc/nginx/sites-enabled/* 

- En este directorio tendremos los archivos que queramos que se publiquen. También contiene un archivo **default** (por defecto), que podremos editar con **Nano**.

<p align="center">
  <img src="/Imagenes/sites-enabled.png" alt="Descripción de la imagen" width="400"/>
</p> 

•	Archivos de configuración **SSL** si utilizamos **HTTPS**: Algunas ubicaciones comunes son: 

*- /etc/nginx/ssl/certificado.crt*

*- /etc/nginx/ssl/certificado.pem*

````bash
sudo cd /etc/nginx/ssl/ | ls -l
````

*- /etc/ssl/certs/certificado.crt*

````bash
sudo cd /etc/ssl/certs/ | ls -l
````

- En estos directorios podremos encontrar los **Certificados de Autentificación** que tengamos instalados, segun cual sea su formato.

---
## **D) Página web por defecto:**

---
Modifica la página web que lanza por defecto y personalízala.
“Bienvenidos a Mi servidor web Tu Nombre:”

- Editamos con **Nano** el archivo */var/www/html/index.html*

````bash
sudo nano /var/www/html/index.html
````

<p align="center">
  <img src="/Imagenes/27.png" alt="Descripción de la imagen" width="500"/>
</p> 

<p align="center">
  <img src="/Imagenes/199.png" alt="Descripción de la imagen" width="500"/>
</p> 


---
## **E) Virtual Hosting:**

---
Queremos que nuestro servidor web ofrezca dos sitios web, teniendo en cuenta lo siguiente:

Cada sitio web tendrá nombres distintos.

Cada sitio web compartirán la misma dirección **IP** y el mismo **Puerto (80)**.

Los dos sitios web tendrán las siguientes características:

El nombre de dominio del primero será www.web1.org, su directorio base será /var/www/web1 y contendrá una página llamada index.html, donde sólo se verá una bienvenida a la página web1.

El nombre de dominio del primero será www.web2.org, su directorio base será /var/www/web2 y contendrá una página llamada index.html, donde sólo se verá una bienvenida a la página web2.

### 1. Creamos los directorios y las páginas web:

````bash
sudo mkdir -p /var/www/web1 /var/www/web2
sudo chown -R www-data:www-data /var/www/web1
sudo chown -R www-data:www-data /var/www/web2
sudo chmod -R 755 /var/www/
````

<p align="center">
  <img src="/Imagenes/105.png" alt="Descripción de la imagen" width="500"/>
</p> 

````bash
echo "<h1>Bienvenido a Web1</h1>" | sudo tee /var/www/web1/index.html
echo "<h1>Bienvenido a Web2</h1>" | sudo tee /var/www/web2/index.html
````

<p align="center">
  <img src="/Imagenes/200.png" alt="Descripción de la imagen" width="500"/>
</p> 

### 2. Configuramos los archivos de sitio en /etc/nginx/sites-available/:

- **Web1.org**

````bash
sudo nano /etc/nginx/sites-available/web1.conf
````
<p align="center">
  <img src="/Imagenes/201.png" alt="Descripción de la imagen" width="500"/>
</p> 

- **Web2.org**

````bash
sudo nano /etc/nginx/sites-available/web2.conf
````
<p align="center">
  <img src="/Imagenes/202.png" alt="Descripción de la imagen" width="500"/>
</p> 

### 3.- Habilitamos los Sitios:

````bash
sudo ln -s /etc/nginx/sites-available/web1.conf /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/web2.conf /etc/nginx/sites-enabled/

````
<p align="center">
  <img src="/Imagenes/203.png" alt="Descripción de la imagen" width="500"/>
</p> 

- **Recargamos Nginx**:

````bash
sudo systemctl reload nginx
````

<p align="center">
  <img src="/Imagenes/204.png" alt="Descripción de la imagen" width="500"/>
</p> 

#### **Comprobación:** 

Configura la resolución estática en los clientes y muestra el acceso a cada una de las páginas.

- Editamos en **debian-cliente** el archivo /etc/hosts y le añadimos las Entradas.

 ````bash
sudo nano /etc/hosts
````

<p align="center">
  <img src="/Imagenes/205.png" alt="Descripción de la imagen" width="500"/>
</p>

•	Abrimos un navegador y accedemos a **http://www.web1.org** y a **http://www.web2.org**.

<p align="center">
  <img src="/Imagenes/206.png" alt="Descripción de la imagen" width="500"/>
</p>

<p align="center">
  <img src="/Imagenes/207.png" alt="Descripción de la imagen" width="500"/>
</p>

---
## **F) Autentificación, Autorización y Control de acceso**

---
www.web1.org se puede acceder desde la red externa y la red interna.

www.web2.org sólo se puede acceder desde la red interna.

1.	**Acceso desde redes externas e internas para www.web1.org:**
- Editamos el archivo de configuración de web1.conf y nos aseguramos de que no haya restricciones.

 ````bash
sudo nano /etc/nginx/sites-available/web1.conf
````

<p align="center">
  <img src="/Imagenes/210.png" alt="Descripción de la imagen" width="500"/>
</p>

2. **Acceso solo desde red interna para www.web2.org:**
- Editamos el archivo de configuración de web2.conf y agregamos una restricción basada en IP:

````bash
sudo nano /etc/nginx/sites-available/web2.conf
````

<p align="center">
  <img src="/Imagenes/211.png" alt="Descripción de la imagen" width="500"/>
</p>

3. **Recargamos Nginx:**

````bash
sudo systemctl reload nginx
````

#### **Comprobación:** 

Cliente-red interna: Accede a www.web1.org y www.web2.org

<p align="center">
  <img src="/Imagenes/220.png" alt="Descripción de la imagen" width="500"/>
</p>

<p align="center">
  <img src="/Imagenes/221.png" alt="Descripción de la imagen" width="500"/>
</p>

Cliente-red externa: Accede a www.web1.org y NO a www.web2.org

<p align="center">
  <img src="/Imagenes/222.png" alt="Descripción de la imagen" width="500"/>
</p>

<p align="center">
  <img src="/Imagenes/223.png" alt="Descripción de la imagen" width="500"/>
</p>

---
## **G) Autentificación, Autorización y Control de acceso.**

---
www.web1.org contiene un directorio llamado privado.

Configura una autentificación básica. Sólo pueden acceder **usuarios válidos**.

- **Autentificación básica**

1. Creamos un archivo .htpasswd para almacenar credenciales:

````bash
sudo htpasswd -c /etc/nginx/.htpasswd usuario
````

<p align="center">
  <img src="/Imagenes/260.png" alt="Descripción de la imagen" width="500"/>
</p>

- Comprobamos que se ha creado correctamente:

````bash
sudo cat /etc/nginx/.htpasswd
````

<p align="center">
  <img src="/Imagenes/226.png" alt="Descripción de la imagen" width="500"/>
</p>

2. Configuramos la autenticación básica para proteger el directorio **/privado**:

````bash
sudo nano /etc/nginx/sites-available/web1.conf
````

<p align="center">
  <img src="/Imagenes/261.png" alt="Descripción de la imagen" width="400"/>
</p>

````bash
sudo systemctl reload nginx
````

<p align="center">
  <img src="/Imagenes/228.png" alt="Descripción de la imagen" width="400"/>
</p>

3. Creamos el directorio **/privado**:

- Dentro crearemos un archivo **index.html**

````bash
sudo mkdir -p /var/www/web1/privado
sudo nano /var/www/web1/privado/index.html
````

<p align="center">
  <img src="/Imagenes/229.png" alt="Descripción de la imagen" width="400"/>
</p>

<p align="center">
  <img src="/Imagenes/230.png" alt="Descripción de la imagen" width="400"/>
</p>

#### **Comprobación:** 

Cliente-red interna o externa: Accede a www.web1.org/privado y pide credenciales para entrar.

<p align="center">
  <img src="/Imagenes/262.png" alt="Descripción de la imagen" width="400"/>
</p>

---
## **H) Autentificación, Autorización y Control de acceso.**

---
www.web1.org contiene un directorio llamado privado.

Desde la red externa pide autorización y desde la red interna **NO**.

#### **Comprobación:** 

Cliente-red interna: Accede a www.web1.org/privado **NO** pide credenciales para entrar.

<p align="center">
  <img src="/Imagenes/270.png" alt="Descripción de la imagen" width="400"/>
</p>


Cliente-red-externa: Accede a www.web1.org/privado **Sí** pide credenciales para entrar.

<p align="center">
  <img src="/Imagenes/280.png" alt="Descripción de la imagen" width="400"/>
</p>


---
## **I) Seguridad.**

---
<p align="center">
  <img src="/Imagenes/NGNIX-SERVER-SSL.png" alt="Descripción de la imagen" width="300"/>
</p>

---
Configuración del sitio virtual www.web1.org para que el acceso sea seguro.

- Generamos un **certificado autofirmado** 

````bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/selfsigned.key -out /etc/ssl/certs/selfsigned.crt
````
---
<p align="center">
  <img src="/Imagenes/290.png" alt="Descripción de la imagen" width="300"/>
</p>

---
- Editamos el archivo /etc/nginx/sites-avalaible/web1

````bash
nano /etc/nginx/sites-avalaible/web1
````

<p align="center">
  <img src="/Imagenes/291.png" alt="Descripción de la imagen" width="300"/>
</p>

---
#### **Comprobación:** 
Cliente-red interna o externa: Accede a https://www.web1.org/

<p align="center">
  <img src="/Imagenes/292.png" alt="Descripción de la imagen" width="300"/>
</p>

---
<p align="center">
  <img src="/Imagenes/AC.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
- Para realizar este Trabajo hemos investigado en internet. Para consultar o ampliar la información, la hemos obtenido de las siguientes [**Direcciones Webs**](Referencias.md).
---
