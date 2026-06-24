# AAY1108 - Evaluación Parcial 3
## Sistemas y Servicios en Cloud — Duoc UC

**Estudiante:** Vicente Salazar

Este repositorio contiene la evidencia fotográfica del despliegue de dos servidores en AWS (AWS Academy Learner Lab), correspondiente a la Evaluación Parcial 3.

---

## Paso a Paso Completo del Despliegue (34 Pasos)

### Paso 1: Lanzamiento de la primera instancia EC2 (RHEL 9)
*Se configura la instancia inicial con Red Hat Enterprise Linux 9, seleccionando el tipo de instancia t3.medium para garantizar suficientes recursos computacionales (2 vCPU y 4 GB de RAM).*

### Paso 2: Configuración del Security Group permitiendo tráfico SSH y HTTP
*Se configuran las reglas del Security Group para permitir conexiones entrantes en puerto 22 (SSH) y puerto 80 (HTTP) desde cualquier dirección IP (0.0.0.0/0) para facilitar acceso remoto y consultas web.*
![Paso 2](./02_image10.png)
![Paso 3](./03_image35.png)

### Paso 3: Creación del par de claves (key pair) para acceso seguro
*Se genera un par de claves RSA que permite autenticación segura sin contraseña en la instancia Linux. La clave privada se descarga en formato .pem para uso posterior en herramientas SSH como PuTTY.*
![Paso 1](./01_image13.png)

### Paso 4: Conexión remota a la instancia mediante PuTTY (SSH)
*Se establece sesión SSH remota utilizando PuTTY, convertiendo la clave .pem al formato .ppk requerido por la herramienta. Se accede a la terminal del servidor Linux con permisos de usuario estándar.*
![Paso 4](./04_image3.png)

### Paso 5: Instalación del servidor web Apache (`httpd`)
*Se ejecutan comandos de terminal para instalar Apache HTTP Server utilizando el gestor de paquetes DNF (Dandified Yum) disponible en RHEL 9. Apache es el servidor web más ampliamente utilizado en entornos Linux de producción.*
![Paso 5](./05_image15.png)

### Paso 6: Verificación del estado del servicio e inicio del mismo (`systemctl status/start httpd`)
*Se verifica que el servicio Apache esté correctamente instalado utilizando `systemctl status httpd` y se inicia el servicio con `systemctl start httpd`. Se habilita el inicio automático con `systemctl enable httpd` para que reinicie automáticamente después de reinicios del sistema.*
![Paso 6](./06_image32.png)

### Paso 7: Descarga del logo de Duoc UC y alojamiento en el servidor (`/var/www/html/`)
*Se descarga el logo institucional de Duoc UC desde un repositorio en línea (ej: curl o wget) y se coloca en el directorio raíz del sitio web Apache ubicado en `/var/www/html/`. Este será el directorio donde se almacenarán todos los archivos servidos por HTTP.*
![Paso 7](./08_image27.png)

### Paso 8: Modificación de la página de bienvenida (`index.html`) con nombre del estudiante y logo institucional
*Se crea un archivo `index.html` personalizado en `/var/www/html/` que incluye el nombre del estudiante (Vicente Salazar) y una referencia al logo institucional de Duoc UC mediante etiqueta `<img>`. Este será el archivo que se sirva por defecto cuando se acceda a la IP del servidor.*
![Paso 8](./09_image6.png)

### Paso 9: Verificación del sitio web desde el navegador (Servidor Linux)
*Se accede mediante navegador web a la dirección IP pública de la instancia EC2 (ej: http://IP-pública) para verificar que Apache está sirviendo correctamente la página index.html personalizada con el nombre del estudiante y el logo de Duoc UC.*
![Paso 9](./11_image4.png)

### Paso 10: Detención de la instancia Linux
*Se detiene (stop) la instancia EC2 de Linux para liberar recursos mientras se procede con la configuración del servidor Windows Server. La instancia no se elimina, permitiendo reactivarla posteriormente si es necesario.*
![Paso 10](./12_image20.png)

### Paso 11: Creación de la instancia EC2 con Windows Server 2019 Base
*Se lanza una nueva instancia EC2 utilizando la AMI de Windows Server 2019 Datacenter con interfaz gráfica. Se selecciona el mismo tipo de instancia (t3.medium) y región (us-east-1) para mantener consistencia con el servidor Linux.*
![Paso 11](./13_image2.png)

### Paso 12: Configuración del Security Group permitiendo tráfico RDP, HTTP y FTP
*Se configuran las reglas de firewall del Security Group para permitir: Puerto 3389 (RDP - Remote Desktop Protocol) para conexión remota gráfica, Puerto 80 (HTTP) para el servidor web IIS, y Puerto 21 (FTP) para transferencia de archivos. Todas desde origen 0.0.0.0/0.*
![Paso 12](./14_image7.png)

### Paso 13: Creación del par de claves para desencriptar la contraseña de administrador
*Se genera un nuevo par de claves para Windows Server. Esta clave pública se encripta en el servidor y la clave privada se descarga en formato .pem, permitiendo desencriptar la contraseña de administrador con herramientas como EC2 Instance Connect o PuTTYgen.*
![Paso 13](./15_image33.png)

### Paso 14: Conexión remota mediante Escritorio Remoto (RDP)
*Se establece conexión remota a la instancia Windows Server 2019 utilizando el protocolo RDP (Remote Desktop Protocol) mediante la herramienta Escritorio Remoto de Windows. Se utiliza la dirección IP pública de la instancia y la contraseña de administrador desencriptada.*
![Paso 14](./16_image9.png)

### Paso 15: Acceso al Administrador del servidor (Server Manager)
*Se abre la consola Server Manager en Windows Server, que proporciona una interfaz centralizada para administrar roles, características y servicios del servidor. Este es el punto de partida para instalar IIS y otros componentes de Windows.*
![Paso 15](./17_image30.png)

### Paso 16: Instalación del rol "Servidor web (IIS)"
*Se utiliza Server Manager para instalar el rol "Web Server (IIS)" que incluye Internet Information Services 10. Se seleccionan los componentes predeterminados necesarios para un servidor web funcional, incluyendo módulos HTTP core y características de seguridad.*
![Paso 16](./18_image12.png)

### Paso 17: Configuración de IIS y habilitación de características HTTP
*Se configuran características específicas de IIS tales como módulos CGI, compresión estática/dinámica, autenticación, y directorio seguro. Se verifica que el servicio IIS (World Wide Web Publishing Service) esté en estado "Iniciado" y habilitado para inicio automático.*
![Paso 17](./19_image16.png)

### Paso 18: Instalación del servicio FTP (FTP Server)
*Se añade el rol "FTP Server" a través de Server Manager como característica complementaria de IIS. Esto instala el servicio FTP que permite transferencia de archivos bidireccional (upload/download) de forma segura controlada por credenciales.*
![Paso 18](./20_image18.png)

### Paso 19: Configuración del servicio FTP en IIS
*Se configura el servicio FTP en IIS mediante IIS Manager, estableciendo el puerto 21, habilitando SSL/TLS para conexiones seguras, y definiendo la ruta raíz de FTP como `C:\inetpub\wwwroot\`. Se configuran reglas de firewall implícitas en Windows para permitir conexiones FTP entrantes.*
![Paso 19](./21_image1.png)

### Paso 20: Verificación de los servicios IIS y FTP en estado "En ejecución"
*Se verifica en Services (servicios.msc) que tanto "World Wide Web Publishing Service" (IIS) como "FTP Publishing Service" están en estado "Started" (Iniciado). Se confirma que ambos servicios están configurados para iniciar automáticamente al reiniciar el servidor.*
![Paso 20](./22_image22.png)

### Paso 21: Descarga del logo de Duoc UC en Windows
*Se descarga el logo institucional de Duoc UC en la instancia Windows Server 2019, generalmente a través de navegador web o PowerShell. El archivo se guarda temporalmente en la carpeta de descargas del usuario administrador.*
![Paso 21](./23_image8.png)

### Paso 22: Navegación a la carpeta raíz del sitio web IIS (`C:\inetpub\wwwroot\`)
*Se abre el Explorador de archivos de Windows y se navega a la ruta `C:\inetpub\wwwroot\`, que es el directorio raíz del servidor IIS. Este directorio contiene todos los archivos que serán servidos por HTTP a través del puerto 80.*
![Paso 22](./24_image29.png)

### Paso 23: Colocación del logo de Duoc UC en la carpeta raíz del sitio
*Se copia el archivo del logo de Duoc UC desde la carpeta de descargas a `C:\inetpub\wwwroot\` utilizando Explorador de archivos. Se verifica la correcta ubicación del archivo para su referencia posterior en HTML.*
![Paso 23](./25_image31.png)

### Paso 24: Creación de la página de bienvenida (`index.html`) con nombre del estudiante
*Se crea un archivo `index.html` nuevo en `C:\inetpub\wwwroot\` utilizando Notepad o editor de texto. Este archivo será la página predeterminada que IIS sirva cuando se acceda a la raíz del servidor web.*
![Paso 24](./26_image19.png)

### Paso 25: Edición del contenido HTML con nombre e información del estudiante
*Se edita el contenido del archivo `index.html` agregando estructura HTML básica con elementos como título, encabezado, párrafos conteniendo el nombre del estudiante (Vicente Salazar) e información de la institución Duoc UC.*
![Paso 25](./27_image11.png)

### Paso 26: Inserción del logo en la página HTML
*Se añade una etiqueta `<img>` al HTML que referencia el archivo del logo de Duoc UC ubicado en `C:\inetpub\wwwroot\`. Se configura el atributo `src` con la ruta relativa o nombre del archivo del logo.*
![Paso 26](./28_image26.png)

### Paso 27: Guardado de la página `index.html` en `C:\inetpub\wwwroot\`
*Se guarda el archivo `index.html` con el contenido personalizado en la ubicación `C:\inetpub\wwwroot\`. Se verifica que los permisos NTFS permiten que el servicio IIS (usuario NETWORK SERVICE) pueda leer el archivo.*
![Paso 27](./29_image36.png)

### Paso 28: Verificación del sitio web desde el navegador (Servidor Windows)
*Se abre un navegador web en el servidor Windows y se accede a `http://localhost` o `http://IP-pública` para verificar que IIS está sirviendo correctamente la página index.html personalizada con el nombre del estudiante Vicente Salazar y el logo de Duoc UC.*
![Paso 28](./30_image21.png)

### Paso 29: Configuración de permisos FTP para usuarios
*Se accede a IIS Manager y se navega a la configuración FTP. Se establecen permisos de lectura (Read) y escritura (Write) para usuarios específicos, limitando el acceso basado en credenciales de dominio o cuentas locales de Windows.*
![Paso 29](./31_image5.png)

### Paso 30: Creación de cuenta de usuario para acceso FTP
*Se crea una nueva cuenta de usuario local en Windows (usuarios y grupos locales) que será utilizada exclusivamente para acceso FTP. Se asigna una contraseña segura y se limitan los permisos del usuario al directorio `C:\inetpub\wwwroot\`.*
![Paso 30](./32_image24.png)

### Paso 31: Asignación de permisos FTP al usuario creado
*Se asignan permisos NTFS al usuario FTP en el directorio `C:\inetpub\wwwroot\`, permitiendo lectura (Read) y escritura (Modify). Se verifica que el usuario puede acceder solo a este directorio y no a otras áreas sensibles del sistema operativo.*
![Paso 31](./33_image14.png)

### Paso 32: Verificación de conectividad al servidor FTP mediante cliente FTP
*Se utiliza una herramienta cliente FTP (ej: FileZilla, WinSCP, o comando `ftp` en terminal) desde una máquina remota para conectarse al servidor FTP en `ftp://IP-pública` con las credenciales del usuario creado. Se confirma la conexión exitosa.*
![Paso 32](./34_image25.png)

### Paso 33: Descarga de archivos a través del servidor FTP
*Se descargan (GET/download) archivos existentes en `C:\inetpub\wwwroot\` a través de la conexión FTP establecida. Se verifica que los archivos transferidos llegan correctamente al cliente local sin corrupción.*
![Paso 33](./35_image28.png)

### Paso 34: Prueba de carga de archivos mediante FTP
*Se suben (PUT/upload) archivos de prueba desde el cliente local al servidor FTP en `C:\inetpub\wwwroot\`. Se verifica que los archivos se escriben correctamente en el servidor, que los permisos se aplican adecuadamente, y que los archivos son accesibles a través del navegador web en `http://IP-pública/nombre-archivo`.*
![Paso 34](./36_image17.png)

---

## Resumen de Configuraciones

### Ítem 1 — Servidor Linux (RHEL 9)

**Configuración Hardware:**
- Instancia EC2: Red Hat Enterprise Linux 9 (AMI)
- Tipo de instancia: t3.medium (2 vCPU Intel Xeon, 4 GB RAM)
- Almacenamiento: 30 GB EBS gp3 (SSD)
- Región: us-east-1 (N. Virginia)

**Configuración de Seguridad:**
- Security Group: SSH (22/tcp), HTTP (80/tcp) abiertos desde 0.0.0.0/0
- Autenticación: Par de claves RSA (Key Pair)
- Acceso: SSH mediante PuTTY

**Servicios instalados:**
- Apache HTTP Server (httpd) v2.4+
- Página de bienvenida personalizada con nombre del estudiante y logo de Duoc UC
- Directorios de contenido: `/var/www/html/`

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

**Configuración Hardware:**
- Instancia EC2: Windows Server 2019 Datacenter con GUI (AMI)
- Tipo de instancia: t3.medium (2 vCPU Intel Xeon, 4 GB RAM)
- Almacenamiento: 30 GB EBS gp3 (SSD)
- Región: us-east-1 (N. Virginia)

**Configuración de Seguridad:**
- Security Group: RDP (3389/tcp), HTTP (80/tcp), FTP (21/tcp) abiertos desde 0.0.0.0/0
- Autenticación: Par de claves RSA (Key Pair) para desencriptar contraseña
- Acceso: RDP mediante Escritorio Remoto

**Servicios instalados:**
- Internet Information Services (IIS) 10
- FTP Server (FTP Publishing Service)
- Página de bienvenida personalizada con nombre del estudiante y logo de Duoc UC
- Directorios de contenido: `C:\inetpub\wwwroot\`

**Pasos realizados (Pasos 11-34):**
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

---

## Evidencias

Todas las capturas de pantalla del proceso (34 imágenes en total) se encuentran en este repositorio, numeradas del 01 al 36 en el orden secuencial en que se realizaron los pasos. Cada imagen documenta un aspecto específico del despliegue e incluye evidencia visual de:

- Configuración de instancias EC2 y security groups
- Instalación y verificación de servicios
- Páginas web personalizadas con contenido del estudiante
- Configuración de protocolos FTP y permisos de acceso
- Pruebas de conectividad y funcionalidad de ambos servidores

---

## Notas Técnicas

- Ambos servidores fueron desplegados en la región `us-east-1` (Norte de Virginia) utilizando AWS Academy Learner Lab
- Las contraseñas y claves privadas utilizadas durante el proceso no se incluyen en este repositorio por motivos de seguridad
- La sección de Windows Server comprende los pasos 11-34, incluyendo la instalación y configuración completa de IIS, FTP, y la página de bienvenida
- Archivos de configuración generados: `index.html` (Linux), `index.html` (Windows), logo de Duoc UC (ambos servidores)
- Protocolos de acceso: SSH (Linux), RDP (Windows), HTTP (ambos), FTP (Windows)
- Todos los pasos fueron realizados dentro de los límites del AWS Academy Learner Lab con recursos educacionales
