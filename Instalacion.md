---
# Instalación de NGINX en Debian 12

---
En este apartado, explicaremos paso a paso cómo instalar y configurar NGINX en **Debian 12 "Bookworm"**.

---
## 1. Actualizar el sistema

---
Antes de instalar cualquier paquete, es recomendable actualizar la lista de paquetes del sistema:

```bash
sudo apt update && sudo apt upgrade -y
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

Para comprobar que las reglas se han aplicado correctamente:

```bash
sudo ufw status
```

Si se usa **iptables** en lugar de UFW, los siguientes comandos permiten el tráfico en los puertos 80 (HTTP) y 443 (HTTPS):

```bash
sudo iptables -I INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 443 -j ACCEPT
```

---
## 5. Verificar la instalación en el navegador

Para confirmar que NGINX está funcionando, abre un navegador y accede a:

---
```
http://localhost
```

Si todo está configurado correctamente, verás la **página de bienvenida de NGINX**.

También puedes comprobarlo desde la terminal con:

```bash
curl -I http://localhost
```

Si NGINX está corriendo correctamente, devolverá:

```
HTTP/1.1 200 OK
```

---
## 6. Ubicación de los archivos de configuración

---
Una vez instalado NGINX, es importante conocer la estructura de archivos:

- Archivo principal de configuración:
  
  ```
  /etc/nginx/nginx.conf
  ```

- Configuración de sitios disponibles:
  
  ```
  /etc/nginx/sites-available/
  ```

- Configuración de sitios habilitados (enlazados desde sites-available):
  
  ```
  /etc/nginx/sites-enabled/
  ```

Para aplicar cambios en la configuración, se debe recargar el servicio:

```bash
sudo systemctl reload nginx
```

---
## 7. Desinstalación de NGINX (Opcional)

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
## Conclusión

---
Con estos pasos, hemos instalado y configurado **NGINX en Debian 12**. Ahora podemos continuar con su configuración avanzada, como la creación de **Virtual Hosts**, la configuración de **proxy inverso** o el uso de **SSL/TLS** para mejorar la seguridad.

---
