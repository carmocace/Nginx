---
# **Casos Prácticos**

<p align="center">
  <img src="/Imagenes/NGINX6.jpg" alt="Descripción de la imagen" width="600"/>
</p> 

---
## **A) Versión de *Nginx* instalado.**

- Ejecutamos *nginx -v* para saber la versión de Nginx que hemos instalado.

````bash
sudo nginx -v
````

<p align="center">
  <img src="/Imagenes/1.png" alt="Descripción de la imagen" width="300"/>
</p> 

---
## **B) Servicio asociado.**

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

. **Los ficheros más importantes son:**

•	Archivo de configuración global: */etc/nginx/nginx.conf* 

````bash
sudo nano /etc/nginx/nginx.conf
````

<p align="center">
  <img src="/Imagenes/25.png" alt="Descripción de la imagen" width="500"/>
</p> 

•	Archivos específicos de cada sitio web: 

*/etc/nginx/sites-available/* 

````bash
sudo cd /etc/nginx/sites-available/ | ls -l
````

- En este directorio tendremos los archivos disponibles para publicar. 

*/etc/nginx/sites-enabled/* 

````bash
sudo cd /etc/nginx/sites-enabled/ | ls -l
````

- En este directorio tendremos los archivos que queramos que se publiquen.


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

Modifica la página web que lanza por defecto y personalízala.
“Bienvenidos a Mi servidor web Tu Nombre:”

- Editamos con **Nano** el archivo */var/www/html/index.html*

````bash
sudo nano /var/www/html/index.html
````

<p align="center">
  <img src="/Imagenes/27.png" alt="Descripción de la imagen" width="600"/>
</p> 

---
## **E) Virtual Hosting:**

Queremos que nuestro servidor web ofrezca dos sitios web, teniendo en cuenta lo siguiente:

Cada sitio web tendrá nombres distintos.

Cada sitio web compartirán la misma dirección **IP** y el mismo **Puerto (80)**.

Los dos sitios web tendrán las siguientes características:

El nombre de dominio del primero será www.web1.org, su directorio base será /var/www/web1 y contendrá una página llamada index.html, donde sólo se verá una bienvenida a la página web1.

El nombre de dominio del primero será www.web2.org, su directorio base será /var/www/web2 y contendrá una página llamada index.html, donde sólo se verá una bienvenida a la página web2.



#### **Comprobación:** 

Configura la resolución estática en los clientes y muestra el acceso a cada una de las páginas.

---
## **F) Autentificación, Autorización y Control de acceso**

www.web1.org se puede acceder desde la red externa y la red interna.

www.web2.org sólo se puede acceder desde la red interna.

#### **Comprobación:** 

Cliente-red interna: Accede a www.web1.org y www.web2.org

Cliente-red externa: Accede a www.web1.org y NO a www.web2.org

---
## **G) Autentificación, Autorización y Control de acceso.**

www.web1.org contiene un directorio llamado privado.

Configura una autentificación básica. Sólo pueden acceder **usuarios válidos**.

#### **Comprobación:** 

Cliente-red interna o externa: Accede a www.web1.org/privado y pide credenciales para entrar.

---
## **H) Autentificación, Autorización y Control de acceso.**

www.web1.org contiene un directorio llamado privado.

Desde la red externa pide autorización y desde la red interna **NO**.

#### **Comprobación:** 

Cliente-red interna: Accede a www.web1.org/privado **NO** pide credenciales para entrar.

Cliente-red-externa: Accede a www.web1.org/privado **Sí** pide credenciales para entrar.

---
## **I) Seguridad.**

---
<p align="center">
  <img src="/Imagenes/NGNIX-SERVER-SSL.png" alt="Descripción de la imagen" width="500"/>
</p> 

Configura el sitio virtual www.web1.org para que el acceso sea seguro.

#### **Comprobación:** 
Cliente-red interna o externa: Accede a https://www.web1.org/

---

- Para realizar este Trabajo hemos buscado información en internet, para su consulta, o para ampliar información, esta disponible en estas [**Direcciones Web**](Referencias.md)

---
<p align="center">
  <img src="/Imagenes/AC.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
