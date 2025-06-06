# Trabajo Práctico - Computación Aplicada
**Ingeniería en Inteligencia Artificial - 1º Año**  
**Universidad de Palermo**

## Descripción General
Este trabajo práctico tiene como objetivo la configuración de un servidor GNU/Linux Debian en una máquina virtual, realizando diversas tareas de administración del sistema, configuración de servicios y automatización mediante scripts. Se trabajó sobre una VM preconfigurada provista por la universidad, utilizando UTM como entorno de virtualización.

---

## 1. Configuración del Entorno

- La VM fue importada desde archivos `.rar`, descomprimidos y ensamblados con WinRAR.
- Se blanqueó la contraseña de root utilizando el modo de recuperación de GRUB.
- La nueva contraseña de root fue establecida como: `palermo`
- Se configuró el hostname del sistema como: `TPServer`

---

## 2. Servicios Configurados

### SSH
- Instalación de `openssh-server`.
- Configuración del acceso mediante clave pública/privada.
- Se habilitó el acceso del usuario root vía SSH.

### Servidor Web (Apache + PHP)
- Instalación de Apache y PHP (v7.3+).
- Configuración del DocumentRoot para servir `index.php` y `logo.png`.
- Apache apunta ahora a `/www_dir`.

### Base de Datos (MariaDB)
- Instalación y configuración de MariaDB.
- Importación del archivo `db.sql` provisto.
---

## 3. Configuración de Red

- Se estableció una IP estática dentro del mismo rango que la máquina física.
- Archivo de configuración incluye:
  - `ADDRESS`
  - `NETMASK`
  - `GATEWAY`
- Pruebas exitosas de conectividad desde una segunda máquina en red local.

---

## 4. Almacenamiento

- Se agregó un disco de 10 GB a la VM.
- Se crearon dos particiones (tipo 83):
  - `/www_dir`: 3 GB
  - `/backup_dir`: 6 GB
- Ambas particiones se montan automáticamente al iniciar el sistema (`/etc/fstab`).
- Apache fue reconfigurado para usar `/www_dir` como raíz.
- Se creó el archivo `/proc/particion` con redirección del contenido de `/proc/partitions`.

---

## 5. Automatización de Backups

### Script: `/opt/scripts/backup_full.sh`

- Acepta argumentos: origen y destino.
- Genera archivos `.tar.gz` con fecha en formato ANSI.
- Valida accesibilidad de sistemas de archivos antes de ejecutar.
- Implementa opción `-help` para mostrar un manual simple al usuario.

### Cron Jobs:

- `Todos los días a las 00:00`: Backupea `/var/log`
- `Lunes, miércoles y viernes a las 23:00`: Backupea `/www_dir`

---

## 6. Entregables Subidos al Repositorio

- Archivos comprimidos `.tar.gz` de:
  - `/root`
  - `/etc`
  - `/opt`
  - `/proc`
  - `/www_dir`
  - `/backup_dir`

- Directorio `/var` spliteado en partes comprimidas para su correcta subida.

---

## 7. Diagrama de Infraestructura


![Diagrama Topológico](https://raw.githubusercontent.com/AbrilSantiso/Debian/refs/heads/master/DiagramaTopologico.png)


---

**Repositorio realizado como parte del Trabajo Práctico de la materia Computación Aplicada - 2025.**
