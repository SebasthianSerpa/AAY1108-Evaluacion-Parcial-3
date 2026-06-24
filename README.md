# AAY1108 - Evaluación Parcial 3
## Sistemas y Servicios en Cloud — Duoc UC

**Estudiante:** Vicente Salazar

Este repositorio contiene la evidencia fotográfica del despliegue de dos servidores en AWS (AWS Academy Learner Lab), correspondiente a la Evaluación Parcial 3.

---

## Ítem 1 — Servidor Linux (RHEL 9)

**Configuración:**
- Instancia EC2: Red Hat Enterprise Linux 9
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Security Group: SSH (puerto 22) y HTTP (puerto 80) abiertos, origen 0.0.0.0/0

**Pasos realizados:**
1. Creación de la instancia EC2 con RHEL 9.
2. Configuración del Security Group permitiendo tráfico SSH y HTTP.
3. Creación del par de claves (key pair) para acceso seguro.
4. Conexión remota a la instancia mediante PuTTY (SSH).
5. Instalación del servidor web Apache (`httpd`).
6. Verificación del estado del servicio e inicio del mismo (`systemctl status/start httpd`).
7. Descarga del logo de Duoc UC y alojamiento en el servidor (`/var/www/html/`).
8. Modificación de la página de bienvenida (`index.html`) con nombre del estudiante y logo institucional.
9. Verificación del sitio web desde el navegador.
10. Detención de la instancia.

---

## Ítem 2 — Servidor Windows Server 2019

**Configuración:**
- Instancia EC2: Microsoft Windows Server 2019 Datacenter (con GUI)
- Tipo de instancia: t3.medium (2 vCPU, 4 GB RAM)
- Security Group: RDP (puerto 3389), HTTP (puerto 80) y FTP (puerto 21) abiertos, origen 0.0.0.0/0

**Pasos realizados:**
1. Creación de la instancia EC2 con Windows Server 2019 Base.
2. Configuración del Security Group permitiendo tráfico RDP, HTTP y FTP.
3. Creación del par de claves para desencriptar la contraseña de administrador.
4. Conexión remota mediante Escritorio Remoto (RDP).
5. Instalación del rol "Servidor web (IIS)" junto con el servicio FTP (FTP Server).
6. Verificación de la correcta instalación del rol y servicios.
7. Descarga del logo de Duoc UC y alojamiento en el servidor (`C:\inetpub\wwwroot\`).
8. Creación de una página de bienvenida (`index.html`) con nombre del estudiante y logo institucional.
9. Configuración de un sitio FTP en IIS sobre la misma carpeta de contenido.
10. Verificación del sitio web (HTTP) y del servicio FTP desde el navegador.
11. Detención de la instancia.

---

## Evidencias

Todas las capturas de pantalla del proceso se encuentran en la carpeta [`/capturas`](./capturas), numeradas en el orden en que se realizaron los pasos.

---

## Notas

- Ambos servidores fueron desplegados en la región `us-east-1` (Norte de Virginia) utilizando AWS Academy Learner Lab.
- Las contraseñas y claves privadas utilizadas durante el proceso no se incluyen en este repositorio por motivos de seguridad.
