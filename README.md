# AAY1108 - Evaluación Parcial 3
## Sistemas y Servicios en Cloud — Duoc UC


Evidencia del despliegue de dos servidores en AWS (AWS Academy Learner Lab): uno Linux (RHEL 9) y uno Windows Server 2019, cada uno con su servidor web configurado y una página de bienvenida personalizada.

---

# 🐧 Ítem 1 — Servidor Linux (RHEL 9)

**Configuración:**
- AMI: Red Hat Enterprise Linux 9
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Security Group: SSH (puerto 22) y HTTP (puerto 80), origen 0.0.0.0/0
- Acceso remoto: SSH mediante PuTTY

## Paso 1: Creación de la instancia EC2 (RHEL 9)

Se lanza la instancia con AMI Red Hat Enterprise Linux 9 y tipo de instancia t3.medium.

![Instancia Linux creada](./10_image34.png)

## Paso 2: Configuración del Security Group (SSH y HTTP)

Se configuran las reglas de entrada permitiendo tráfico SSH (puerto 22) y HTTP (puerto 80) desde cualquier origen.

![Security Group SSH](./02_image10.png)
![Security Group HTTP](./03_image35.png)

## Paso 3: Creación del par de claves (Key Pair)

Se genera un par de claves RSA y se descarga la clave privada en formato `.pem`.

![Key pair creado](./01_image13.png)

## Paso 4: Conexión remota vía SSH (PuTTY)

Se convierte la clave `.pem` a `.ppk` con PuTTYgen y se establece la conexión SSH usando PuTTY, con usuario `ec2-user`.

![Conexión SSH con PuTTY](./04_image3.png)

## Paso 5: Instalación del servidor Apache (httpd)

Se instala Apache mediante el gestor de paquetes `dnf`.

```bash
sudo dnf install httpd -y
```

![Instalación de httpd](./05_image15.png)

## Paso 6: Inicio y verificación del servicio Apache

Se inicia el servicio y se verifica su estado, confirmando "active (running)".

```bash
sudo systemctl start httpd
sudo systemctl status httpd
```

![Servicio httpd activo](./06_image32.png)

## Paso 7: Descarga del logo de Duoc UC

Se descarga el logo institucional directamente en el servidor, alojado en `/var/www/html/`.

```bash
sudo curl -L -o /var/www/html/duoc-logo.png "https://upload.wikimedia.org/wikipedia/commons/thumb/a/aa/Logo_DuocUC.svg/960px-Logo_DuocUC.svg.png"
```

![Logo descargado en el servidor](./08_image27.png)

## Paso 8: Creación de la página de bienvenida (index.html)

Se crea el archivo `index.html` en `/var/www/html/` con el nombre del estudiante y el logo institucional.

![Creación de index.html](./09_image6.png)

## Paso 9: Verificación del sitio web desde el navegador

Se accede a la IP pública de la instancia desde el navegador, confirmando que se muestra la página personalizada.

![Sitio web Linux funcionando](./11_image4.png)

## Paso 10: Detención de la instancia

Se detiene la instancia Linux una vez completadas las verificaciones.

![Instancia Linux detenida](./12_image20.png)

---

# 🪟 Ítem 2 — Servidor Windows Server 2019

**Configuración:**
- AMI: Microsoft Windows Server 2019 Datacenter (con GUI)
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Security Group: RDP (puerto 3389), HTTP (puerto 80) y FTP (puerto 21), origen 0.0.0.0/0
- Acceso remoto: Escritorio Remoto (RDP)

## Paso 11: Creación de la instancia EC2 (Windows Server 2019)

Se lanza la instancia con AMI Microsoft Windows Server 2019 Base y tipo de instancia t3.medium.

![Instancia Windows creada](./13_image2.png)

## Paso 12: Configuración del Security Group (RDP, HTTP y FTP)

Se configuran las reglas de entrada permitiendo tráfico RDP (3389), HTTP (80) y FTP (21).

![Security Group RDP/HTTP/FTP](./14_image7.png)

## Paso 13: Creación del par de claves

Se genera un nuevo par de claves para desencriptar la contraseña de administrador de la instancia Windows.

![Key pair Windows creado](./15_image33.png)

## Paso 14: Conexión remota vía RDP

Se obtiene la contraseña de Administrator desencriptada con la clave `.pem` y se establece la conexión por Escritorio Remoto.

![Conexión RDP exitosa](./16_image9.png)

## Paso 15: Acceso al Server Manager

Se accede al Server Manager de Windows, punto de partida para instalar roles y características.

![Server Manager](./17_image30.png)

## Paso 16: Instalación del rol "Servidor web (IIS)"

Se utiliza el asistente "Add Roles and Features" para instalar el rol Web Server (IIS).

![Instalación rol IIS](./18_image12.png)

## Paso 17: Selección de Role Services de IIS

Se confirman los servicios de rol HTTP por defecto (Common HTTP Features, Default Document, etc.).

![Role Services IIS](./19_image16.png)

## Paso 18: Instalación del servicio FTP Server

Dentro del mismo asistente de roles, se marca "FTP Server" (incluyendo FTP Service y FTP Extensibility).

![Instalación FTP Server](./20_image18.png)

## Paso 19: Confirmación e instalación

Se confirma la selección de roles y servicios, y se ejecuta la instalación.

![Instalación completada](./21_image1.png)

## Paso 20: Verificación del rol IIS instalado

Se verifica en el Server Manager que el rol IIS aparece correctamente instalado y el servidor está "Online".

![IIS instalado y verificado](./22_image22.png)

## Paso 21: Apertura del IIS Manager

Se abre "Internet Information Services (IIS) Manager" y se navega hasta "Default Web Site".

![IIS Manager](./23_image8.png)

## Paso 22: Exploración de la carpeta wwwroot

Se navega a la carpeta `C:\inetpub\wwwroot\`, directorio raíz del sitio web por defecto de IIS.

![Carpeta wwwroot](./24_image29.png)

## Paso 23: Descarga del logo de Duoc UC en el servidor

Se descarga el logo institucional desde el navegador del escritorio remoto y se guarda directamente en `C:\inetpub\wwwroot\`.

![Logo Duoc UC en wwwroot](./25_image31.png)

## Paso 24: Creación del archivo index.html

Se crea un nuevo archivo `index.html` en `C:\inetpub\wwwroot\` usando el Bloc de notas.

![Creación de index.html en Windows](./26_image19.png)

## Paso 25: Edición del contenido HTML

Se edita el archivo con el HTML que incluye el nombre del estudiante y la referencia a la imagen del logo.

![Edición del HTML](./27_image11.png)

## Paso 26: Guardado del archivo

Se guarda `index.html`, que IIS sirve automáticamente como página de inicio.

![Archivo guardado](./28_image26.png)

## Paso 27: Verificación del sitio web desde el navegador

Se accede a la IP pública de la instancia, confirmando que se muestra el nombre del estudiante y el logo de Duoc UC.

![Sitio web Windows funcionando](./29_image36.png)

## Paso 28: Creación del sitio FTP en IIS

Se agrega un nuevo sitio FTP desde IIS Manager ("Add FTP Site"), apuntando a la misma carpeta `C:\inetpub\wwwroot\`, puerto 21, sin SSL.

![Creación sitio FTP](./30_image21.png)

## Paso 29: Configuración de autenticación y autorización FTP

Se habilita autenticación anónima con acceso de solo lectura ("Read") para todos los usuarios.

![Configuración autenticación FTP](./31_image5.png)

## Paso 30: Sitio FTP creado y en ejecución

Se confirma en IIS Manager que el sitio FTP quedó en estado "Started", escuchando en el puerto 21.

![Sitio FTP iniciado](./32_image24.png)

## Paso 31: Apertura del puerto 21 en el Security Group

Se agrega la regla TCP personalizado (puerto 21) en el Security Group de AWS, con descripción del nombre del estudiante.

![Regla FTP en Security Group](./33_image14.png)

## Paso 32: Verificación del sitio web desde el navegador externo

Se confirma nuevamente, desde fuera de la instancia, que el sitio web responde correctamente con el contenido personalizado.

![Verificación final HTTP](./34_image25.png)

## Paso 33: Verificación del servicio FTP desde el navegador

Se accede mediante `ftp://IP-publica` desde el navegador para confirmar que el servicio FTP responde y lista el contenido de `wwwroot`.

![Verificación FTP](./35_image28.png)

## Paso 34: Detención de la instancia Windows

Se detiene la instancia Windows Server 2019 una vez finalizadas todas las verificaciones.

![Instancia Windows detenida](./36_image17.png)

---

## Resumen

| | Ítem 1 — Linux | Ítem 2 — Windows |
|---|---|---|
| AMI | Red Hat Enterprise Linux 9 | Windows Server 2019 Datacenter |
| Instancia | t3.medium | t3.medium |
| Acceso remoto | SSH (PuTTY) | RDP (Escritorio Remoto) |
| Servidor web | Apache (httpd) | IIS 10 |
| Puertos abiertos | 22, 80 | 3389, 80, 21 |
| Servicio adicional | — | FTP Server |

---

## Notas

- Ambos servidores se desplegaron en la región `us-east-1` (Norte de Virginia) utilizando AWS Academy Learner Lab.
- El acceso FTP se configuró con autenticación anónima de solo lectura, exclusivamente para fines de verificación de la evaluación.
- Las contraseñas y claves privadas utilizadas durante el proceso no se incluyen ni son visibles en las capturas de este repositorio.

**Fecha de realización:** 24-06-2026
**Estudiante:** Sebasthian Serpa Vicente Salazar
**Institución:** Duoc UC
**Curso:** AAY1108 - Sistemas y Servicios en Cloud
**Evaluación:** Parcial 3
