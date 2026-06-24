# AAY1108 - Evaluación Parcial 3
## Sistemas y Servicios en Cloud — Duoc UC

**Estudiante:** Vicente Salazar

Este repositorio contiene la evidencia fotográfica del despliegue de dos servidores en AWS (AWS Academy Learner Lab), correspondiente a la Evaluación Parcial 3.

---

## Paso a Paso Completo del Despliegue (36 Pasos)



### Paso 2: Configuración del Security Group permitiendo tráfico SSH y HTTP


### Paso 3: Creación del par de claves (key pair) para acceso seguro
![Paso 1](./01_image13.png)
![Paso 2](./02_image10.png)
![Paso 3](./03_image35.png)

### Paso 4: Conexión remota a la instancia mediante PuTTY (SSH)
![Paso 4](./04_image3.png)

### Paso 5: Instalación del servidor web Apache (`httpd`)
![Paso 5](./05_image15.png)

### Paso 6: Verificación del estado del servicio e inicio del mismo (`systemctl status/start httpd`)
![Paso 6](./06_image32.png)

### Paso 7: Descarga del logo de Duoc UC y alojamiento en el servidor (`/var/www/html/`)
![Paso 7](./08_image27.png)

### Paso 8: Modificación de la página de bienvenida (`index.html`) con nombre del estudiante y logo institucional
![Paso 8](./09_image6.png)

### Paso 9: Verificación del sitio web desde el navegador (Servidor Linux)
![Paso 9](./11_image4.png)

### Paso 10: Detención de la instancia Linux
![Paso 10](./12_image20.png)

### Paso 11: Creación de la instancia EC2 con Windows Server 2019 Base
![Paso 11](./13_image2.png)

### Paso 12: Configuración del Security Group permitiendo tráfico RDP, HTTP y FTP
![Paso 12](./14_image7.png)

### Paso 13: Creación del par de claves para desencriptar la contraseña de administrador
![Paso 13](./15_image33.png)

### Paso 14: Conexión remota mediante Escritorio Remoto (RDP)
![Paso 14](./16_image9.png)

### Paso 15: Acceso al Administrador del servidor (Server Manager)
![Paso 15](./17_image30.png)

### Paso 16: Instalación del rol "Servidor web (IIS)"
![Paso 16](./18_image12.png)

### Paso 17: Configuración de IIS y habilitación de características HTTP
![Paso 17](./19_image16.png)

### Paso 18: Instalación del servicio FTP (FTP Server)
![Paso 18](./20_image18.png)

### Paso 19: Configuración del servicio FTP en IIS
![Paso 19](./21_image1.png)

### Paso 20: Verificación de los servicios IIS y FTP en estado "En ejecución"
![Paso 20](./22_image22.png)

### Paso 21: Descarga del logo de Duoc UC en Windows
![Paso 21](./23_image8.png)

### Paso 22: Navegación a la carpeta raíz del sitio web IIS (`C:\inetpub\wwwroot\`)
![Paso 22](./24_image29.png)

### Paso 23: Colocación del logo de Duoc UC en la carpeta raíz del sitio
![Paso 23](./25_image31.png)

### Paso 24: Creación de la página de bienvenida (`index.html`) con nombre del estudiante
![Paso 24](./26_image19.png)

### Paso 25: Edición del contenido HTML con nombre e información del estudiante
![Paso 25](./27_image11.png)

### Paso 26: Inserción del logo en la página HTML
![Paso 26](./28_image26.png)

### Paso 27: Guardado de la página `index.html` en `C:\inetpub\wwwroot\`
![Paso 27](./29_image36.png)

### Paso 28: Verificación del sitio web desde el navegador (Servidor Windows)
![Paso 28](./30_image21.png)

### Paso 29: Configuración de permisos FTP para usuarios
![Paso 29](./31_image5.png)

### Paso 30: Creación de cuenta de usuario para acceso FTP
![Paso 30](./32_image24.png)

### Paso 31: Asignación de permisos FTP al usuario creado
![Paso 31](./33_image14.png)

### Paso 32: Verificación de conectividad al servidor FTP mediante cliente FTP
![Paso 32](./34_image25.png)

### Paso 33: Descarga de archivos a través del servidor FTP
![Paso 33](./35_image28.png)

### Paso 34: Prueba de carga de archivos mediante FTP
![Paso 34](./36_image17.png)

### Paso 35: Verificación de los archivos subidos en el servidor web
![Paso 35](./10_image34.png)

### Paso 36: Confirmación final del despliegue de ambos servidores (Linux y Windows)
![Paso 36](./10_image34.png)

---

## Resumen de Configuraciones

### Ítem 1 — Servidor Linux (RHEL 9)

**Configuración:**
- Instancia EC2: Red Hat Enterprise Linux 9
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Security Group: SSH (puerto 22) y HTTP (puerto 80) abiertos, origen 0.0.0.0/0

**Servicios instalados:**
- Servidor web Apache (httpd)
- Página de bienvenida con nombre del estudiante y logo de Duoc UC

**Pasos realizados (Pasos 1-10):**
1. Creación de la instancia EC2 con RHEL 9
2. Configuración del Security Group permitiendo tráfico SSH y HTTP
3. Creación del par de claves (key pair) para acceso seguro
4. Conexión remota a la instancia mediante PuTTY (SSH)
5. Instalación del servidor web Apache (httpd)
6. Verificación del estado del servicio e inicio del mismo (systemctl status/start httpd)
7. Descarga del logo de Duoc UC y alojamiento en el servidor (/var/www/html/)
8. Modificación de la página de bienvenida (index.html) con nombre del estudiante y logo institucional
9. Verificación del sitio web desde el navegador
10. Detención de la instancia

---

### Ítem 2 — Servidor Windows Server 2019

**Configuración:**
- Instancia EC2: Microsoft Windows Server 2019 Datacenter (con GUI)
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Security Group: RDP (puerto 3389), HTTP (puerto 80) y FTP (puerto 21) abiertos, origen 0.0.0.0/0

**Servicios instalados:**
- Servidor web IIS (Internet Information Services)
- Servidor FTP
- Página de bienvenida con nombre del estudiante y logo de Duoc UC

**Pasos realizados (Pasos 11-36):**
11. Creación de la instancia EC2 con Windows Server 2019 Base
12. Configuración del Security Group permitiendo tráfico RDP, HTTP y FTP
13. Creación del par de claves para desencriptar la contraseña de administrador
14. Conexión remota mediante Escritorio Remoto (RDP)
15. Acceso al Administrador del servidor (Server Manager)
16. Instalación del rol "Servidor web (IIS)"
17. Configuración de IIS y habilitación de características HTTP
18. Instalación del servicio FTP (FTP Server)
19. Configuración del servicio FTP en IIS
20. Verificación de los servicios IIS y FTP en estado "En ejecución"
21. Descarga del logo de Duoc UC en Windows
22. Navegación a la carpeta raíz del sitio web IIS (C:\inetpub\wwwroot\)
23. Colocación del logo de Duoc UC en la carpeta raíz del sitio
24. Creación de la página de bienvenida (index.html) con nombre del estudiante
25. Edición del contenido HTML con nombre e información del estudiante
26. Inserción del logo en la página HTML
27. Guardado de la página index.html en C:\inetpub\wwwroot\
28. Verificación del sitio web desde el navegador (Servidor Windows)
29. Configuración de permisos FTP para usuarios
30. Creación de cuenta de usuario para acceso FTP
31. Asignación de permisos FTP al usuario creado
32. Verificación de conectividad al servidor FTP mediante cliente FTP
33. Descarga de archivos a través del servidor FTP
34. Prueba de carga de archivos mediante FTP
35. Verificación de los archivos subidos en el servidor web
36. Confirmación final del despliegue de ambos servidores (Linux y Windows)

---

## Evidencias

Todas las capturas de pantalla del proceso (36 imágenes en total) se encuentran en este repositorio, numeradas del 01 al 36 en el orden secuencial en que se realizaron los pasos. Cada paso incluye su correspondiente evidencia fotográfica del despliegue.

---

## Notas

- Ambos servidores fueron desplegados en la región `us-east-1` (Norte de Virginia) utilizando AWS Academy Learner Lab.
- Las contraseñas y claves privadas utilizadas durante el proceso no se incluyen en este repositorio por motivos de seguridad.
- La sección de Windows Server comprende los pasos 11-36, incluyendo la instalación y configuración completa de IIS, FTP, y la página de bienvenida.
