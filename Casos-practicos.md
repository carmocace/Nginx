# **Casos Prácticos**

---
a) Versión de Nginx instalado.

b) Servicio asociado.

c) Ficheros de configuración.

d) Página web por defecto:
Modifica la página web que lanza por defecto y personalízala.
“Bienvenidos a Mi servidor web Tu Nombre:”

e) Virtual Hosting:

Queremos que nuestro servidor web ofrezca dos sitios web, teniendo en cuenta lo siguiente:

Cada sitio web tendrá nombres distintos.

Cada sitio web compartirán la misma dirección IP y el mismo puerto (80).

Los dos sitios web tendrán las siguientes características:

El nombre de dominio del primero será www.web1.org, su directorio base será /var/www/web1 y contendrá una página llamada index.html, donde sólo se verá una bienvenida a la página web1.

El nombre de dominio del primero será www.web2.org, su directorio base será /var/www/web2 y contendrá una página llamada index.html, donde sólo se verá una bienvenida a la página web2.

Comprobación: 
Configura la resolución estática en los clientes y muestra el acceso a cada una de las páginas.

f) Autentificación, Autorización y Control de acceso
www.web1.org se puede acceder desde la red externa y la red interna.
www.web2.org sólo se puede acceder desde la red interna.

Comprobación: 
Cliente-red interna: Accede a www.web1.org y www.web2.org
Cliente-red externa: Accede a www.web1.org y NO a www.web2.org

g) Autentificación, Autorización y Control de acceso
www.web1.org contiene un directorio llamado privado.
Configura una autentificación básica. Sólo puede acceder usuarios válidos.

Comprobación: 
Cliente-red interna o externa: Accede a www.web1.org/privado y pide credenciales para entrar.

h) Autentificación, Autorización y Control de acceso
www.web1.org contiene un directorio llamado privado.
Desde la red externa pide autorización y desde la red interna NO.

Comprobación: 
Cliente-red interna: Accede a www.web1.org/privado NO pide credenciales para entrar.
Cliente-red-externa: Accede a www.web1.org/privado Sí pide credenciales para entrar.


i)Seguridad
Configura el sitio virtual www.web1.org para que el acceso sea seguro.

Comprobación: 
Cliente-red interna o externa: Accede a https://www.web1.org/
