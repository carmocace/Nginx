---
# Instalación de NGINX en Debian 12

<p align="center">
  <img src="/Imagenes/nginx-and-debian.png" alt="Descripción de la imagen" width="500"/>
</p> 


---
En este apartado, explicaremos paso a paso cómo instalar y configurar NGINX en **Debian 12 "Bookworm"**.

---
## 1. Actualizar el sistema

---
Antes de instalar cualquier paquete, es recomendable actualizar la lista de paquetes del sistema:

```bash
sudo apt update && sudo apt full-upgrade
```

---
## 2. Instalar NGINX

---
Debian 12 incluye NGINX en sus repositorios oficiales, por lo que podemos instalarlo fácilmente con:

```bash
sudo apt install nginx
```

<p align="center">
  <img src="/Imagenes/20.png" alt="Descripción de la imagen" width="500"/>
</p> 

Una vez finalizada la instalación, podemos verificar la versión instalada con:

```bash
nginx -v
```

<p align="center">
  <img src="/Imagenes/1.png" alt="Descripción de la imagen" width="300"/>
</p> 

---

## 3. Verificar el estado del servicio

---
Después de la instalación, NGINX se iniciará automáticamente. Si el servicio no está activo, lo podemos iniciar manualmente con:

```bash
sudo systemctl start nginx
``` 
Para comprobar que está corriendo correctamente, usamos:

```bash
sudo systemctl status nginx
```

<p align="center">
  <img src="/Imagenes/2.png" alt="Descripción de la imagen" width="500"/>
</p> 

Para asegurarnos de que NGINX se inicie automáticamente en cada reinicio del sistema:

```bash
sudo systemctl enable nginx
```

<p align="center">
  <img src="/Imagenes/enable.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
## 4. Configurar el firewall.

---
Si el firewall UFW está activo en el sistema, debemos permitir el tráfico HTTP y HTTPS:

```bash
sudo ufw allow 'Nginx Full'
sudo ufw reload
```

Para comprobar que las reglas se han aplicado correctamente ejecutaremos:

```bash
sudo ufw status
```

Nosotros usamos **iptables** en lugar de UFW, los siguientes comandos nos permitirán el tráfico en los puertos **80 (HTTP)** y **443 (HTTPS)**:

```bash
sudo iptables -I INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 443 -j ACCEPT
```

<p align="center">
  <img src="/Imagenes/iptables.png" alt="Descripción de la imagen" width="500"/>
</p> 


---
## 5. Verificar la instalación en el navegador

Para confirmar que NGINX está funcionando, abrimos el navegador y accedemos a:

---
```
http://localhost
```

Si todo está configurado correctamente, veremos la **Página de Inicio de NGINX**.

<p align="center">
  <img src="/Imagenes/local.png" alt="Descripción de la imagen" width="500"/>
</p> 

También podemos comprobarlo desde la terminal con:

```bash
sudo curl -I http://localhost
```

Si **NGINX** está corriendo correctamente, nos responderá: **HTTP/1.1 200 OK**

<p align="center">
  <img src="/Imagenes/curl.png" alt="Descripción de la imagen" width="500"/>
</p> 

---

---
## 6. Desinstalación de NGINX (Opcional)

---
Si en algún momento deseas eliminar **NGINX** del sistema:

```bash
sudo apt remove --purge nginx -y
sudo apt autoremove -y
```

Para borrar también la configuración:

```bash
sudo rm -rf /etc/nginx
```

---
- Hemos instalado y configurado **NGINX en Debian 12** para poder realizar los [Casos Prácticos](Casos-practicos.md)

- Ahora tendremos que [Conectar las **MV's**](Esquema-de-Red.md) para crear el entorno de trabajo.

---

<p align="center">
  <img src="/Imagenes/Nginx.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
