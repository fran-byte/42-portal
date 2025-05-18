

# 🔐 Born2beroot — Guía para Enfrentar el Proyecto con Garantías

## 🔹 1. Fundamentos Previos (Antes de Empezar)

### 📌 Objetivo:

Tener una comprensión clara de **cómo funciona un sistema Linux**, sus configuraciones de seguridad básicas, y cómo documentar y defender tu trabajo durante el examen.

---

### 🧰 Herramientas esenciales

#### ✅ VirtualBox o UTM

* **Crea una máquina virtual** con Debian (o Rocky Linux).
* Asegúrate de usar las **configuraciones oficiales** (RAM, CPU, disco).

#### ✅ Debian (recomendado)

* Familiarízate con comandos como: `apt`, `sudo`, `adduser`, `passwd`, `ufw`, `hostname`, `crontab`, `systemctl`, `auditd`.

#### ✅ Markdown y Word

* Tendrás que **documentar todo** en un archivo `.md` o `.pdf`.
* Debes explicar **qué hiciste y por qué** (¡muy importante para la defensa!).

---

## 🔹 2. Checklist de requisitos del proyecto

### 🖥️ 1. Configuración de la VM

* Debian o Rocky Linux (según lo permitido en tu campus).
* El nombre del host debe seguir este patrón: `login42`.
* Usuario: `login` y grupo `sudo` correctamente configurados.

---

### 🔒 2. Seguridad de contraseñas

* Las contraseñas deben tener:

  * Mínimo 10 caracteres
  * 1 mayúscula, 1 minúscula, 1 número
* Política de caducidad (máximo 30 días)
* 3 intentos fallidos → bloqueo temporal

Se logra configurando:

* `/etc/login.defs`
* `/etc/pam.d/common-password` (usando `pam_pwquality.so`)
* Comando `chage`

---

### 🧑‍💻 3. Sudo

* Debes instalar y configurar `sudo`.
* Solo miembros del grupo `sudo` pueden usarlo.
* Debes **auditar cada uso de `sudo`**.

---

### 🧾 4. Cron jobs

* Crear un **cron job** para:

  * Enviar cada 10 minutos un informe de uso de disco a un archivo en `/var/log/`
* Usar `crontab -e` o `/etc/crontab`.

---

### 📜 5. Hostname y UFW

* Cambiar el nombre del host: `hostnamectl set-hostname login42`
* Configurar **UFW** (firewall) para aceptar solo puertos SSH (22) y HTTP (80 si lo configuras).

---

### 🧠 6. Scripts personalizados

* Crear un script llamado `monitoring.sh`:

  * Muestra: uso de disco, memoria, CPU, número de usuarios, direcciones IP, etc.
  * Ejecutado al inicio del sistema usando un cronjob o systemd.

---

### 📦 7. Servicios activos

* `ssh` debe estar activo y funcionando.
* Otros servicios deben ser **mínimos y controlados** (`systemctl` y `ss` ayudan a revisar esto).

---

## 🔹 3. Plan de ataque paso a paso

### Paso 1: Instalar la VM correctamente

* Elige el SO permitido por tu campus
* Asigna la RAM y disco pedidos
* Configura el usuario y la contraseña correctamente

### Paso 2: Aplicar políticas de seguridad

* Usa `passwd`, `chage`, `login.defs`, `pam` para endurecer el acceso
* Prueba las contraseñas incorrectas y observa cómo se bloquea

### Paso 3: Instalar y configurar `sudo`

* Asegúrate de que solo tu usuario tenga permisos
* Verifica logs en `/var/log/auth.log`

### Paso 4: Crear y probar el cron job de monitorización

* Asegúrate de que el script se ejecuta y los logs se guardan correctamente

### Paso 5: Documentar todo

* Usa Markdown o Word
* Por cada paso: **explica el qué, el cómo y el por qué**
* Añade capturas de pantalla si es posible

---

## 🔹 4. Tips para la defensa

* El evaluador puede pedirte que expliques **cómo configuraste cada parte**.
* Puede romper o modificar algo para ver si sabes solucionarlo.
* Te pueden pedir que:

  * Añadas un nuevo usuario con políticas de seguridad
  * Muestres logs de `sudo`
  * Edite cronjobs en vivo

---

## 🧠 Consejos extra

* **Haz snapshots** de tu VM antes de hacer cambios grandes.
* **Prueba todo desde cero** al menos una vez antes de entregar.
* Practica usando `man`, `vim`, y `grep`.
* Usa `bash -x script.sh` para depurar tus scripts.

---
