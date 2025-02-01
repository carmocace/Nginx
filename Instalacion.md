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
sudo apt install nginx -y
```

Una vez finalizada la instalación, podemos verificar la versión instalada con:

```bash
nginx -v
```

---

## 3. Verificar el estado del servicio

---
Después de la instalación, NGINX se iniciará automáticamente. Para comprobar que está corriendo correctamente, usamos:

```bash
sudo systemctl status nginx
```

Si el servicio no está activo, lo podemos iniciar manualmente con:

```bash
sudo systemctl start nginx
```

Para asegurarnos de que NGINX se inicie automáticamente en cada reinicio del sistema:

```bash
sudo systemctl enable nginx
```

---
## 4. Configurar el firewall (si está activado)

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

Si usamos **iptables** en lugar de UFW, los siguientes comandos permitirán el tráfico en los puertos 80 (HTTP) y 443 (HTTPS):

```bash
sudo iptables -I INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 443 -j ACCEPT
```

---
## 5. Verificar la instalación en el navegador

Para confirmar que NGINX está funcionando, abrimos el navegador y accedemos a:

---
```
http://localhost
```

Si todo está configurado correctamente, veremos la **página de bienvenida de NGINX**.

También podemos comprobarlo desde la terminal con:

```bash
curl -I http://localhost
```

Si NGINX está corriendo correctamente, nos responderá:

```
HTTP/1.1 200 OK
```

---

---
## 6. Desinstalación de NGINX (Opcional)

---
Si en algún momento deseas eliminar NGINX del sistema:

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

---

<p align="center">
  <img src="/Imagenes/Nginx.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
