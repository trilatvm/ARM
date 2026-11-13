# !!! GENERADO CON IA !!!

## ⚠️ Descargo de responsabilidad (Disclaimer)

Este kernel ha sido compilado de forma independiente y personalizada para hardware basado en **Rockchip RK322x** ejecutando **Void Linux (ARMv7l)**. 

* **Uso bajo tu propio riesgo:** La instalación y modificación del kernel de Linux, del *initramfs* o de los árboles de dispositivos (*Device Trees*) implica riesgos inherentes. El autor no se hace responsable por posibles fallos de arranque (*soft-brick*), pérdida de datos, inestabilidad del sistema o daños en el hardware (*hard-brick*) derivados del uso de estos archivos.
* **Sin garantías:** Este software se proporciona *"tal cual"* (*"as is"*), sin garantías expresas ni implícitas de ningún tipo, incluyendo compatibilidad total con todas las variantes de placas o periféricos (Wi-Fi, Bluetooth, control remoto, etc.).
* **Respaldo obligatorio:** Antes de modificar tu carpeta `/boot` o actualizar enlaces simbólicos, asegurate de tener una copia de seguridad de tus archivos actuales y un medio de arranque externo (tarjeta SD o USB) para poder recuperar el sistema en caso de emergencia.

# Linux Kernel 6.18.63 para Rockchip RK322x (ARMv7l)

Kernel Linux **6.18.63** compilado nativamente en **Void Linux (armv7l)** para TV Boxes basadas en SoC **Rockchip RK322x** (`rk3228` / `rk3229` con `rk322x-box.dtb`) que utilizan el esquema de arranque U-Boot de Armbian.

## Contenido del paquete (`Release`)

El archivo `kernel-6.18.63-rockchip-custom-armv7l.tar.xz` (~46 MB) incluye:
* **`/boot/vmlinuz-6.18.63-rockchip-custom`**: Imagen comprimida del kernel (`zImage`).
* **`/boot/uInitrd-6.18.63-rockchip-custom`**: Ramdisk inicial preparado para U-Boot (generado con `dracut` + `mkimage`, soporte `ext4`).
* **`/boot/System.map-6.18.63-rockchip-custom`**: Tabla de símbolos del kernel.
* **`/boot/config-6.18.63-rockchip-custom`**: Archivo `.config` utilizado durante la compilación.
* **`/boot/dtb-6.18.63-rockchip-custom/`**: Árboles de dispositivos (incluyendo `rk322x-box.dtb` y `overlay/`).
* **`/lib/modules/6.18.63-rockchip-custom/`**: Todos los módulos del kernel compilados y listos para cargar.

---

## Instalación rápida en tu placa

> **Nota de seguridad:** Esta instalación no borra tu kernel anterior, por lo que podés revertir los enlaces simbólicos en `/boot` si necesitás volver atrás.

### 1. Descargar y verificar el paquete
```bash
wget https://github.com
wget https://github.com.sha256

sha256sum -c kernel-6.18.63-rockchip-custom-armv7l.tar.xz.sha256
```

### 2. Extraer los archivos en el sistema
```bash
sudo tar -xJvf kernel-6.18.63-rockchip-custom-armv7l.tar.xz -C /
sudo depmod -a 6.18.63-rockchip-custom
```

### 3. Regenerar el `initrd` para tu UUID raíz (Recomendado)
Como el `uInitrd` incluido tiene embebido el UUID de la partición raíz donde fue compilado, se recomienda regenerarlo localmente para tu propio disco:
```bash
sudo dracut --force --omit "zfs" /boot/initrd.img-6.18.63-rockchip-custom 6.18.63-rockchip-custom
sudo mkimage -A arm -O linux -T ramdisk -C none -n uInitrd -d /boot/initrd.img-6.18.63-rockchip-custom /boot/uInitrd-6.18.63-rockchip-custom
```

### 4. Actualizar enlaces simbólicos en `/boot` y reiniciar
```bash
sudo ln -sf vmlinuz-6.18.63-rockchip-custom /boot/zImage
sudo ln -sf uInitrd-6.18.63-rockchip-custom /boot/uInitrd
sudo ln -sfn dtb-6.18.63-rockchip-custom /boot/dtb

sudo sync
sudo reboot
```

Al iniciar, verificá la versión ejecutando:
```bash
uname -a
```
