---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos previos (antes de atacar Born2BeRoot)

### 📌 Objetivo:

Tener **todas las herramientas técnicas y conceptuales** necesarias para configurar y asegurar una máquina virtual Debian **con confianza**, evitando errores comunes y entendiendo **lo que estás haciendo y por qué**.

---

### 🛠️ Creación y configuración de la máquina virtual

#### ✅ Descarga de ISO de Debian e instalación de VirtualBox

1. **Descarga de ISO de Debian**: Click aquí
2. **Descarga de VirtualBox**: Click aquí

#### 🔧 Creación de la máquina virtual

1. Abrir VirtualBox y crear una nueva máquina virtual.
2. Configurar la máquina virtual en el directorio **sgoinfre**.
3. Seleccionar la cantidad de memoria RAM.
4. Crear un disco duro virtual (VDI) reservado dinámicamente.
5. Seleccionar la ISO de Debian y comenzar la instalación.

---

### 🧱 Instalación de Debian en la VM

1. Selección de idioma, zona horaria y país.
2. Creación de un nombre de host y una contraseña para la máquina.
3. Creación de un primer usuario y su contraseña.
4. Configuración de las particiones de la máquina utilizando LVM (Logical Volume Manager).

#### 🧪 ¿Qué es LVM?

LVM permite crear, redimensionar o eliminar particiones dinámicamente desde la línea de comandos mientras el sistema está en funcionamiento, sin necesidad de reiniciar.

---

### 📦 Configuración de la máquina virtual

#### 🛠️ Gestión de paquetes

1. **aptitude**: Recuerda qué paquetes se solicitaron explícitamente y desinstala automáticamente los paquetes no necesarios.
2. **apt**: Ejecuta exactamente lo que se le indica en la línea de comandos.

#### 🔒 Seguridad

1. **APPArmor**: Sistema de seguridad que proporciona control de acceso obligatorio.
2. **SSH (Secure Shell)**: Permite administrar servidores Linux de forma segura.
3. **UFW (Uncomplicated Firewall)**: Configuración de firewall para proteger la red, dejando abierto solo el puerto 4242.
4. **Política de contraseñas**: Reglas para mejorar la seguridad de las contraseñas, incluyendo expiración cada 30 días y requisitos de complejidad.

---

### 📚 Grupos y usuarios

1. **root y sudo**: Uso de `sudo` para otorgar permisos temporales de administrador sin iniciar sesión como root.
2. **Crontab**: Uso de `cron` para ejecutar scripts automáticamente en intervalos predefinidos.

---

### 🧬 Script de monitoreo

#### ✅ Descripción del script

Un script en Bash que recoge información del sistema, como arquitectura, núcleos físicos y virtuales, uso de memoria y disco, porcentaje de uso de CPU, último reinicio, uso de LVM, conexiones TCP, usuarios conectados, dirección IP y MAC, y número de comandos ejecutados con `sudo`.

#### 🧪 Ejemplo de script

```bash
#!/bin/bash
# O.S. ARCHITECTURE
architecture=$(uname -a)
# PHYSICAL CPU identifier
cpu_phy=$(grep "physical id" /proc/cpuinfo | wc -l)
# Number of virtual processors (vCPUs)
vcpus=$(grep "processor" /proc/cpuinfo | wc -l)
# MEMORY RAM
total_memory=$(free --mega | awk '$1 == "Mem:" {print $2}')
used_memory=$(free --mega | awk '$1 == "Mem:" {print $3}')
memory_usage_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
# DISK
total_disk_space=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_t += $2} END {printf ("%.1fGb\n"), disk_t/1024}')
used_disk_space=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')
disk_usage_percent=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} {disk_t += $2} END {printf("%d"), disk_u/disk_t*100}')
# CPU load
inactive_cpu=$(vmstat 1 2 | tail -1 | awk '{printf $15}')
cpu_usage=$(expr 100 - $inactive_cpu)
formatted_cpu=$(printf "%.1f" $cpu_usage)
# LAST BOOT
last_boot=$(who -b | awk '$1 == "system" {print $3 " " $4}')
# LVM USE
lvm_use=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)
# TCP CONNECTIONS
tcp_connections=$(ss -ta | grep ESTAB | wc -l)
# USER LOG
user_log=$(users | wc -w)
# NETWORK
ip_net=$(hostname -I)
mac=$(ip link | grep "link/ether" | awk '{print $2}')
# SUDO COMMANDS
sudo_commands=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
# Wall message
wall "\t# Architecture: $architecture\n\t# CPU physical: $cpu_phy\n\t# vCPU: $vcpus\n\t# Memory Usage: $used_memory/${total_memory}MB ($memory_usage_percent%)\n\t# Disk Usage: $used_disk_space/${total_disk_space} ($disk_usage_percent%)\n\t# CPU load: $formatted_cpu%\n\t# Last boot: $last_boot\n\t# LVM use: $lvm_use\n\t# TCP Connections: $tcp_connections ESTABLISHED\n\t# User log: $user_log\n\t# Network: IP $ip_net ($mac)\n\t# Sudo: $sudo_commands cmd"
```

---

### 🧾 Crontab

#### ✅ Configuración de crontab

Publicar un mensaje cada 10 minutos utilizando `cron`.

```bash
sudo crontab -u root -e
```

Formato de Crontab:

- **m** Minuto de ejecución (0-59).
- **h** Hora de ejecución (0-23).
- **dom** Día del mes (puedes especificar un día, como 15).
- **dow** Día de la semana (0-7, donde 0 y 7 son domingo) o las primeras tres letras del día en inglés: mon, tue, wed, thu, fri, sat, sun.
- **user** Usuario que ejecuta el comando (root u otro con permisos).
- **command** Comando o ruta absoluta del script a ejecutar.

---

### 📜 Signature.txt

#### ✅ Generación de firma

Uso de `shasum` para obtener la firma de la máquina virtual y subirla al repositorio.

```bash
shasum nombremaquina.vdi
```

---

### 🧠 Evaluación

#### ✅ Preguntas de evaluación

1. **Qué es una máquina virtual?**
2. **Por qué te decantaste por Debian?**
3. **Diferencias básicas entre Rocky y Debian**
4. **Propósito de las máquinas virtuales**
5. **Diferencias entre apt y aptitude**
6. **Qué es APPArmor?**
7. **Qué es LVM?**

#### ✅ Comandos de evaluación

1. **Verificar interfaces gráficas en uso:** `ls /usr/bin/*session`
2. **Comprobar estado del servicio UFW:** `sudo ufw status`
3. **Comprobar estado del servicio SSH:** `sudo service ssh status`
4. **Verificar sistema operativo (Debian o CentOS):** `uname -v` o `uname --kernel-version`
5. **Verificar pertenencia a grupos "sudo" y "user42":** `getent group sudo` y `getent group user42`
6. **Crear nuevo usuario con política de contraseñas:** `sudo adduser name_user`
7. **Crear grupo "evaluating":** `sudo addgroup evaluating`
8. **Añadir usuario al grupo:** `sudo adduser name_user evaluating`
9. **Comprobar hostname:** `hostname`
10. **Modificar hostname:** Editar `/etc/hostname` y `/etc/hosts`
11. **Comprobar particiones:** `lsblk`
12. **Verificar si sudo está instalado:** `which sudo` o `dpkg -s sudo`
13. **Agregar nuevo usuario al grupo sudo:** `sudo adduser name_user sudo`
14. **Mostrar aplicación de reglas de sudo.**
15. **Verificar existencia de /var/log/sudo/:** Comprobar que contenga al menos un fichero de historial de comandos utilizados con sudo.
16. **Verificar instalación y estado de UFW:** `dpkg -s ufw` y `sudo service ufw status`
17. **Listar reglas activas en UFW:** `sudo ufw status numbered`
18. **Crear y eliminar regla para puerto 8080:** `sudo ufw allow 8080` y `sudo ufw delete num_rule`
19. **Comprobar estado de SSH y puerto 4242:** `which ssh` y `sudo service ssh status`
20. **Iniciar sesión con el nuevo usuario via SSH
