# AAY1108 - Evaluación Parcial 3
## Sistemas y Servicios en Cloud — Duoc UC




# 🐧 SERVIDOR LINUX (RHEL 9)

## Descripción General
Implementación de un servidor web Apache en Red Hat Enterprise Linux 9 en una instancia EC2 t3.medium de AWS, con página de bienvenida personalizada.

**Especificaciones:**
- **AMI:** Red Hat Enterprise Linux 9
- **Tipo:** t3.medium (2 vCPU, 4 GB RAM)
- **Almacenamiento:** 30 GB EBS gp3
- **Región:** us-east-1 (N. Virginia)
- **Puertos Abiertos:** 22 (SSH), 80 (HTTP)
- **Acceso:** SSH + PuTTY

---

## Paso 1: Lanzamiento de la instancia EC2 (RHEL 9)

*Se configura la instancia inicial con Red Hat Enterprise Linux 9, seleccionando el tipo de instancia t3.medium para garantizar suficientes recursos computacionales (2 vCPU y 4 GB de RAM).*

![Paso 1](./10_image34.png)

**Acciones realizadas:**
- Selección de AMI: Red Hat Enterprise Linux 9
- Tipo de instancia: t3.medium
- Configuración de almacenamiento: 30 GB EBS gp3
- Red: VPC por defecto, asignación de IP pública automática

---

## Paso 2: Configuración del Security Group (SSH y HTTP)

*Se configuran las reglas del Security Group para permitir conexiones entrantes en puerto 22 (SSH) y puerto 80 (HTTP) desde cualquier dirección IP (0.0.0.0/0) para facilitar acceso remoto y consultas web.*

![Paso 2 - Security Group SSH](./02_image10.png)
![Paso 2 - Security Group HTTP](./03_image35.png)

**Reglas configuradas:**
- **Inbound SSH:** Protocolo TCP, Puerto 22, Origen 0.0.0.0/0
- **Inbound HTTP:** Protocolo TCP, Puerto 80, Origen 0.0.0.0/0
- **Outbound:** Tráfico saliente permitido a todos los destinos

---

## Paso 3: Creación del par de claves (Key Pair)

*Se genera un par de claves RSA que permite autenticación segura sin contraseña en la instancia Linux. La clave privada se descarga en formato .pem para uso posterior en herramientas SSH como PuTTY.*

![Paso 3](./01_image13.png)

**Proceso:**
- Generación de par de claves RSA de 2048 bits
- Descarga de clave privada: formato .pem
- Nombre de clave: AAY1108-Linux-Key
- Almacenamiento seguro en equipo local

---

## Paso 4: Conexión remota vía SSH (PuTTY)

*Se establece sesión SSH remota utilizando PuTTY, convertiendo la clave .pem al formato .ppk requerido por la herramienta. Se accede a la terminal del servidor Linux con permisos de usuario estándar.*

![Paso 4](./04_image3.png)

**Configuración PuTTY:**
- Host: IP pública de la instancia
- Puerto: 22 (SSH)
- Usuario: ec2-user (usuario por defecto RHEL)
- Autenticación: Clave privada en formato .ppk
- Terminal: xterm (256 colores)

---

## Paso 5: Instalación del servidor Apache (httpd)

*Se ejecutan comandos de terminal para instalar Apache HTTP Server utilizando el gestor de paquetes DNF (Dandified Yum) disponible en RHEL 9. Apache es el servidor web más ampliamente utilizado en entornos Linux de producción.*

![Paso 5](./05_image15.png)

**Comandos ejecutados:**
```bash
$ sudo dnf update -y
$ sudo dnf install httpd -y
```

**Detalles:**
- Versión: Apache httpd 2.4+
- Ubicación: `/usr/sbin/httpd`
- Configuración: `/etc/httpd/conf/httpd.conf`
- Directorio raíz: `/var/www/html/`

---

## Paso 6: Inicio y verificación del servicio Apache

*Se verifica que el servicio Apache esté correctamente instalado utilizando `systemctl status httpd` y se inicia el servicio con `systemctl start httpd`. Se habilita el inicio automático con `systemctl enable httpd`.*

![Paso 6](./06_image32.png)

**Comandos ejecutados:**
```bash
$ sudo systemctl start httpd
$ sudo systemctl enable httpd
$ sudo systemctl status httpd
```

**Estado esperado:**
- Estado: Active (running)
- Inicio automático: enabled
- Escucha en: 0.0.0.0:80

---

## Paso 7: Descarga del logo de Duoc UC

*Se descarga el logo institucional de Duoc UC en la instancia Linux y se coloca en el directorio raíz `/var/www/html/`. Este será el directorio donde se almacenarán todos los archivos servidos por HTTP.*

![Paso 7](./08_image27.png)

**Acciones realizadas:**
- Descarga: `curl -O [URL-logo-duoc]` o `wget [URL-logo-duoc]`
- Destino: `/var/www/html/duoc-logo.png`
- Permisos: 644 (lectura para todos, escritura solo propietario)
- Verificación: `ls -la /var/www/html/`

---

## Paso 8: Creación de página index.html personalizada

*Se crea un archivo `index.html` personalizado en `/var/www/html/` que incluye el nombre del estudiante (Vicente Salazar) y una referencia al logo institucional mediante etiqueta `<img>`. Este será el archivo que se sirva por defecto.*

![Paso 8](./09_image6.png)

**Archivo creado:**
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bienvenida - AAY1108</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
        img { max-width: 200px; margin: 20px 0; }
    </style>
</head>
<body>
    <h1>Bienvenido a Duoc UC</h1>
    <h2>Estudiante: Vicente Salazar</h2>
    <img src="duoc-logo.png" alt="Logo Duoc UC">
    <p>Evaluación Parcial 3 - Sistemas y Servicios en Cloud</p>
</body>
</html>
```

**Ubicación:** `/var/www/html/index.html`

---

## Paso 9: Verificación del sitio web desde navegador

*Se accede mediante navegador web a la dirección IP pública de la instancia EC2 (ej: http://IP-pública) para verificar que Apache está sirviendo correctamente la página index.html con el nombre del estudiante y el logo.*

![Paso 9](./11_image4.png)

**Pruebas realizadas:**
- URL: `http://[IP-pública-ec2]/`
- Verificación: Página carga correctamente
- Elementos visibles: Título, nombre Vicente Salazar, logo Duoc UC
- Código HTTP: 200 OK

---

## Paso 10: Detención de la instancia Linux

*Se detiene (stop) la instancia EC2 de Linux para liberar recursos mientras se procede con la configuración del servidor Windows Server. La instancia no se elimina, permitiendo reactivarla posteriormente si es necesario.*

![Paso 10](./12_image20.png)

**Acción realizada:**
- Comando AWS: `Stop Instance`
- Estado: stopped (detiene sin terminar)
- Recursos: EBS persiste, IP pública puede cambiar
- Costo: Se sigue cobrando almacenamiento

---

# 🪟 SERVIDOR WINDOWS SERVER 2019

## Descripción General
Implementación de un servidor web IIS con servicio FTP en Windows Server 2019 en una instancia EC2 t3.medium de AWS, incluyendo página de bienvenida personalizada y acceso seguro por FTP.

**Especificaciones:**
- **AMI:** Windows Server 2019 Datacenter
- **Tipo:** t3.medium (2 vCPU, 4 GB RAM)
- **Almacenamiento:** 30 GB EBS gp3
- **Región:** us-east-1 (N. Virginia)
- **Puertos Abiertos:** 3389 (RDP), 80 (HTTP), 21 (FTP)
- **Acceso:** RDP + Escritorio Remoto

---

## Paso 11: Lanzamiento de instancia Windows Server 2019

*Se lanza una nueva instancia EC2 utilizando la AMI de Windows Server 2019 Datacenter con interfaz gráfica. Se selecciona el mismo tipo de instancia (t3.medium) y región (us-east-1) para mantener consistencia.*

![Paso 11](./13_image2.png)

**Configuración:**
- AMI: Windows Server 2019 Datacenter (con GUI)
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Almacenamiento: 30 GB EBS gp3
- Asignación de IP pública: Automática
- IAM Role: Por defecto (EC2InstanceProfileRole)

---

## Paso 12: Configuración del Security Group (RDP, HTTP, FTP)

*Se configuran las reglas de firewall del Security Group para permitir acceso en Puerto 3389 (RDP), Puerto 80 (HTTP) y Puerto 21 (FTP), todas desde origen 0.0.0.0/0.*

![Paso 12](./14_image7.png)

**Reglas configuradas:**
- **RDP:** Protocolo TCP, Puerto 3389, Origen 0.0.0.0/0
- **HTTP:** Protocolo TCP, Puerto 80, Origen 0.0.0.0/0
- **FTP:** Protocolo TCP, Puerto 21, Origen 0.0.0.0/0
- **Outbound:** Tráfico saliente permitido a todos

---

## Paso 13: Creación del par de claves para desencriptación

*Se genera un nuevo par de claves para Windows Server. La clave pública se encripta en el servidor y la clave privada se descarga en formato .pem, permitiendo desencriptar la contraseña de administrador.*

![Paso 13](./15_image33.png)

**Proceso:**
- Generación de par RSA 2048 bits
- Descarga de clave privada: formato .pem
- Encriptación de contraseña: algoritmo DPAPI de Windows
- Desencriptación: Usando EC2 Instance Connect o herramienta local

---

## Paso 14: Conexión remota vía RDP (Escritorio Remoto)

*Se establece conexión remota a la instancia Windows Server 2019 utilizando el protocolo RDP mediante la herramienta Escritorio Remoto de Windows. Se usa la IP pública y contraseña de administrador desencriptada.*

![Paso 14](./16_image9.png)

**Conexión RDP:**
- Protocolo: Remote Desktop Protocol (RDP)
- Puerto: 3389/tcp
- Usuario: Administrator
- Autenticación: Contraseña desencriptada
- Resolución: 1024x768 (adaptable)

---

## Paso 15: Acceso al Server Manager

*Se abre la consola Server Manager en Windows Server, que proporciona una interfaz centralizada para administrar roles, características y servicios. Este es el punto de partida para instalar IIS y otros componentes.*

![Paso 15](./17_image30.png)

**Acciones:**
- Ruta: `Server Manager` (automático al iniciar sesión)
- Sección: "Manage" → "Add Roles and Features"
- Vista: Información general del servidor y servicios

---

## Paso 16: Instalación del rol "Servidor web (IIS)"

*Se utiliza Server Manager para instalar el rol "Web Server (IIS)" que incluye Internet Information Services 10. Se seleccionan componentes predeterminados necesarios para un servidor web funcional.*

![Paso 16](./18_image12.png)

**Instalación:**
- Rol: Web Server (IIS) - v10
- Componentes incluidos:
  - Web Server Core
  - HTTP Activation
  - Common HTTP Features
  - Default Document
  - Static Content
- Ruta de instalación: `C:\Windows\System32\inetsrv\`

---

## Paso 17: Configuración de características HTTP en IIS

*Se configuran características específicas de IIS tales como módulos CGI, compresión, y seguridad. Se verifica que el servicio World Wide Web Publishing Service esté iniciado.*

![Paso 17](./19_image16.png)

**Configuración realizadas:**
- Compresión estática: Habilitada
- Autenticación anónima: Habilitada
- Módulo FastCGI: Habilitado
- Seguridad: Configurada por defecto
- Servicio: World Wide Web Publishing Service → Iniciado

---

## Paso 18: Instalación del servicio FTP (FTP Server)

*Se añade el rol "FTP Server" a través de Server Manager como característica complementaria de IIS. Esto instala el servicio FTP que permite transferencia bidireccional de archivos controlada por credenciales.*

![Paso 18](./20_image18.png)

**Instalación:**
- Característica: FTP Server (versión 7.5+)
- Ubicación: Dentro de Server Manager → Add Role
- Dependencias: IIS debe estar instalado primero
- Servicio: FTP Publishing Service

---

## Paso 19: Configuración del servicio FTP en IIS

*Se configura el servicio FTP en IIS mediante IIS Manager, estableciendo puerto 21, habilitando SSL/TLS, y definiendo la ruta raíz como `C:\inetpub\wwwroot\`. Se configuran reglas de firewall implícitas.*

![Paso 19](./21_image1.png)

**Configuración FTP:**
- Puerto: 21 (TCP)
- SSL/TLS: Recomendado pero opcional
- Directorio raíz: `C:\inetpub\wwwroot\`
- Aislamiento de usuarios: Deshabilitado
- Límites de conexión: 10 conexiones simultáneas

---

## Paso 20: Verificación de servicios IIS y FTP en ejecución

*Se verifica en Services (servicios.msc) que tanto "World Wide Web Publishing Service" (IIS) como "FTP Publishing Service" están en estado "Started". Se confirma inicio automático.*

![Paso 20](./22_image22.png)

**Verificación:**
- Abrir: `services.msc`
- Servicios a verificar:
  - World Wide Web Publishing Service → Started
  - FTP Publishing Service → Started
- Tipo de inicio: Automatic
- Marca de verificación: ✓ En ejecución

---

## Paso 21: Descarga del logo de Duoc UC

*Se descarga el logo institucional de Duoc UC en Windows Server 2019 a través de navegador web o PowerShell. El archivo se guarda temporalmente en carpeta de descargas del administrador.*

![Paso 21](./23_image8.png)

**Proceso:**
- Método: Microsoft Edge (navegador)
- Descarga: Logo Duoc UC (PNG o JPG)
- Ubicación temporal: `C:\Users\Administrator\Downloads\`
- Nombre de archivo: duoc-logo.png

---

## Paso 22: Navegación a C:\inetpub\wwwroot\

*Se abre el Explorador de archivos de Windows y se navega a `C:\inetpub\wwwroot\`, que es el directorio raíz del servidor IIS donde se almacenan todos los archivos servidos por HTTP.*

![Paso 22](./24_image29.png)

**Ruta de acceso:**
- Ruta completa: `C:\inetpub\wwwroot\`
- Permisos: NETWORK SERVICE (leer), Administrators (escribir)
- Archivos por defecto: iisstart.htm, pjsdebug.js

---

## Paso 23: Colocación del logo en wwwroot

*Se copia el archivo del logo de Duoc UC desde descargas a `C:\inetpub\wwwroot\` utilizando Explorador de archivos. Se verifica la correcta ubicación para referencia en HTML.*

![Paso 23](./25_image31.png)

**Acciones:**
- Origen: `C:\Users\Administrator\Downloads\duoc-logo.png`
- Destino: `C:\inetpub\wwwroot\duoc-logo.png`
- Método: Copiar/Pegar en Explorador
- Verificación: Logo visible en directorio

---

## Paso 24: Creación de index.html personalizado

*Se crea un archivo `index.html` nuevo en `C:\inetpub\wwwroot\` utilizando Notepad o editor de texto. Este será la página predeterminada que IIS sirva cuando se acceda a la raíz del servidor.*

![Paso 24](./26_image19.png)

**Creación del archivo:**
- Herramienta: Notepad (Bloc de notas)
- Ubicación: `C:\inetpub\wwwroot\index.html`
- Codificación: UTF-8
- Contenido: HTML personalizado

---

## Paso 25: Edición del contenido HTML

*Se edita el contenido del archivo `index.html` agregando estructura HTML con título, encabezado, párrafos conteniendo el nombre del estudiante (Vicente Salazar) e información de Duoc UC.*

![Paso 25](./27_image11.png)

**Contenido HTML:**
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Windows Server - Duoc UC</title>
    <style>
        body { font-family: Segoe UI, sans-serif; text-align: center; margin-top: 60px; }
        h1 { color: #003f7f; }
        img { max-width: 250px; margin: 30px 0; }
        footer { margin-top: 40px; color: #666; }
    </style>
</head>
<body>
    <h1>Servidor Web - Windows Server 2019</h1>
    <h2>Bienvenido a Duoc UC</h2>
    <img src="duoc-logo.png" alt="Logo Duoc UC">
    <h3>Estudiante: Vicente Salazar</h3>
    <p>AAY1108 - Evaluación Parcial 3</p>
    <p>Sistemas y Servicios en Cloud</p>
    <footer><p>&copy; 2026 Duoc UC - Todos los derechos reservados</p></footer>
</body>
</html>
```

---

## Paso 26: Inserción del logo en HTML

*Se añade una etiqueta `<img>` al código HTML que referencia el archivo del logo ubicado en `C:\inetpub\wwwroot\`. Se configura el atributo `src` con la ruta relativa.*

![Paso 26](./28_image26.png)

**Código agregado:**
```html
<img src="duoc-logo.png" alt="Logo Duoc UC" width="250px">
```

**Atributos:**
- `src`: Ruta relativa del logo
- `alt`: Texto alternativo si falla la carga
- `width`: Ancho de imagen en píxeles

---

## Paso 27: Guardado de index.html

*Se guarda el archivo `index.html` con el contenido personalizado en `C:\inetpub\wwwroot\`. Se verifica que los permisos NTFS permiten que el servicio IIS lea el archivo.*

![Paso 27](./29_image36.png)

**Guardado:**
- Ruta: `C:\inetpub\wwwroot\index.html`
- Codificación: UTF-8
- Permisos: Leer para NETWORK SERVICE
- Verificación: Archivo guardado correctamente

---

## Paso 28: Verificación del sitio web desde navegador

*Se abre navegador web en Windows Server y se accede a `http://localhost` para verificar que IIS está sirviendo correctamente la página index.html personalizada con el nombre del estudiante y logo.*

![Paso 28](./30_image21.png)

**Prueba:**
- URL: `http://localhost/` o `http://127.0.0.1/`
- Resultado esperado: Página carga con nombre Vicente Salazar y logo Duoc UC
- Código HTTP: 200 OK
- Elemento: Favicon de IIS (predeterminado)

---

## Paso 29: Configuración de permisos FTP para usuarios

*Se accede a IIS Manager y se navega a la configuración FTP. Se establecen permisos de lectura (Read) y escritura (Write) para usuarios específicos, limitando acceso por credenciales.*

![Paso 29](./31_image5.png)

**Configuración:**
- Herramienta: IIS Manager → FTP Site
- Permisos: Read + Write
- Usuarios: Seleccionados específicos
- Autenticación: Basic Auth con SSL

---

## Paso 30: Creación de usuario para acceso FTP

*Se crea una nueva cuenta de usuario local en Windows (Administración de usuarios y grupos locales) para acceso FTP exclusivo. Se asigna contraseña segura con limitación a directorio `C:\inetpub\wwwroot\`.*

![Paso 30](./32_image24.png)

**Usuario creado:**
- Nombre: ftpuser
- Contraseña: Fuerte (mayúsc, minúsc, números, caracteres especiales)
- Grupo: Usuarios
- Directorio home: `C:\inetpub\wwwroot\`
- Descripción: Usuario FTP - AAY1108

---

## Paso 31: Asignación de permisos NTFS al usuario FTP

*Se asignan permisos NTFS al usuario FTP creado en el directorio `C:\inetpub\wwwroot\`, permitiendo lectura (Read) y modificación (Modify). Se verifica acceso limitado a este directorio.*

![Paso 31](./33_image14.png)

**Permisos NTFS:**
- Recurso: `C:\inetpub\wwwroot\`
- Usuario: ftpuser
- Permisos: 
  - Read (Lectura): ✓
  - Modify (Modificar): ✓
  - Write (Escribir): ✓
  - Delete (Eliminar): ✗ (no permitido)

---

## Paso 32: Prueba de conectividad FTP

*Se utiliza un cliente FTP (ej: FileZilla, WinSCP o comando `ftp`) desde máquina remota para conectarse a `ftp://IP-pública` con credenciales del usuario ftpuser. Se confirma conexión exitosa.*

![Paso 32](./34_image25.png)

**Conexión FTP:**
- Host: IP pública EC2
- Puerto: 21 (FTP estándar)
- Usuario: ftpuser
- Contraseña: [contraseña segura]
- Modo pasivo: Habilitado
- Resultado: Conexión exitosa ✓

---

## Paso 33: Descarga de archivos vía FTP

*Se descargan (GET/download) archivos existentes en `C:\inetpub\wwwroot\` a través de la conexión FTP establecida. Se verifica que los archivos llegan correctamente al cliente local sin corrupción.*

![Paso 33](./35_image28.png)

**Descarga realizada:**
- Archivos: index.html, duoc-logo.png
- Método: Download en cliente FTP
- Destino local: Carpeta de usuario
- Verificación: Archivos íntegros y funcionales

---

## Paso 34: Prueba de carga de archivos vía FTP

*Se suben (PUT/upload) archivos de prueba desde cliente local al servidor FTP en `C:\inetpub\wwwroot\`. Se verifica que archivos se escriben correctamente, permisos se aplican, y archivos son accesibles vía HTTP.*

![Paso 34](./36_image17.png)

**Carga realizada:**
- Archivo: test.txt (archivo de prueba)
- Método: Upload en cliente FTP
- Destino servidor: `C:\inetpub\wwwroot\test.txt`
- Verificación HTTP: `http://IP-pública/test.txt` → 200 OK

---


## Resumen de Configuraciones

### Servidor Linux (RHEL 9) - Pasos 1-10
- **Instancia EC2 - RHEL 9**
- **Servidor:** Apache httpd
- **Puertos:** 22 (SSH), 80 (HTTP)
- **Autenticación:** Key Pair SSH
- **Página web:** index.html personalizado con nombre estudiante y logo Duoc UC

### Servidor Windows Server 2019 - Pasos 11-34
- **Instancia EC2 - Windows Server 2019**
- **Servidor web:** IIS 10
- **Servidor FTP:** FTP Publishing Service
- **Puertos:** 3389 (RDP), 80 (HTTP), 21 (FTP)
- **Autenticación:** RDP + usuario FTP
- **Página web:** index.html personalizado con nombre estudiante y logo Duoc UC
- **Acceso FTP:** Usuario ftpuser con permisos NTFS limitados

---


**Fecha de realización:** 2026-06-24  
**Estudiante:** Vicente Salazar  / sebastian  serpa /victor   painen
**Institución:** Duoc UC  
**Curso:** AAY1108 - Sistemas y Servicios en Cloud  
**Evaluación:** Parcial 3
