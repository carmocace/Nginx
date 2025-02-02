---
# Esquema de Red:

<p align="center">
  <img src="/Imagenes/nginx.jpg" alt="Descripción de la imagen" width="400"/>
</p> 

---
- Para la realizar la **Práctica** y las **Comprobaciones**, vamos a usar dos **MV's** (**Debian-carmona** y **Debian-cliente**) de **VitualBox** que se conectarán a **Internet** por **Adaptador Puente** (**Bridge**) a través de la **Interfaz Física** del **Anfitrión**, y que se comunicarán entre ellas por **Red Interna** a través de una **Interfaz Paravirtualizada**.

---
## **debian-carmona**

---
- Ejecutamos ***ip a*** para comprobar que nuestras **IP's** son, en la Red Puente **192.168.1.43**, y en la Red Interna **192.168.2.100/24**

````bash
ip a
````
<p align="center">
  <img src="/Imagenes/red-ser-ipa.png" alt="Descripción de la imagen" width="500"/>
</p> 

### **Configuración Adaptador Puente**

<p align="center">
  <img src="/Imagenes/red-serv-in1.png" alt="Descripción de la imagen" width="250"/>
</p> 

- Hacemos Ping a la MV debian-cliente en la Red del Equipo Anfitrión.

````bash
ping -c 4 192.168.1.37
````
<p align="center">
  <img src="/Imagenes/red-serv-ping3.png" alt="Descripción de la imagen" width="300"/>
</p> 

### **Configuración Red Interna**

<p align="center">
  <img src="/Imagenes/red-serv-in2.png" alt="Descripción de la imagen" width="250"/>
</p> 

-Hacemos Ping a la MV debian-cliente en la Red Interna.

````bash
ping -c 4 192.168.2.101
````

<p align="center">
  <img src="/Imagenes/red-serv-ping2.png" alt="Descripción de la imagen" width="300"/>
</p> 

-Hacemos Ping a Google para comprobar la salida a Internet.

````bash
ping -c4 8.8.8.8
````

<p align="center">
  <img src="/Imagenes/red-serv-ping1.png" alt="Descripción de la imagen" width="300"/>
</p> 

---
## **debian-cliente**

---

````bash
ip a
````

<p align="center">
  <img src="/Imagenes/red-cl-ipa.png" alt="Descripción de la imagen" width="500"/>
</p> 

---
### **Configuración Adaptador Puente**

<p align="center">
  <img src="/Imagenes/red-cl-1.png" alt="Descripción de la imagen" width="250"/>
</p> 

-Hacemos Ping a la MV debian-carmona en la Red del Equipo Anfitrión.

````bash
ping -c 4 192.168.1.43
````
<p align="center">
  <img src="/Imagenes/red-cl-ping2.png" alt="Descripción de la imagen" width="300"/>
</p> 

### **Configuración Red Interna**

<p align="center">
  <img src="/Imagenes/red-cl-2.png" alt="Descripción de la imagen" width="250"/>
</p> 

-Hacemos Ping a la MV debian-carmona en la Red Interna.

````bash
ping -c 4 192.168.2.100
````
<p align="center">
  <img src="/Imagenes/red-cl-ipa2.png" alt="Descripción de la imagen" width="300"/>
</p>

---
- Una vez configurada a red, procedemos a la [**Instalación y Configuración de Nginx**](Instalacion.md)

---
<p align="center">
  <img src="/Imagenes/NGINX (1).jpg" alt="Descripción de la imagen" width="400"/>
</p> 

---
