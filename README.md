# 🎬 Pelis Latam - Tizen Smart TV App

Este repositorio contiene el código fuente y la automatización para compilar una **Hosted Web App** para Smart TVs de Samsung (Tizen OS). La aplicación funciona como un contenedor en pantalla completa que carga directamente una plataforma web de películas y series en español latino.

La compilación y el empaquetado del archivo `.wgt` firmado se realizan de forma 100% automática en la nube a través de **GitHub Actions**.

---

## 📁 Estructura del Proyecto

```text
├── .github/
│   └── workflows/
│       └── tizen-build.yml       # Script de automatización (GitHub Actions)
├── config.xml                  # Configuración de la App de Tizen
├── icon.png                    # Icono de la aplicación (512x512 px)
└── README.md                   # Documentación del proyecto
```

---

## 🚀 Configuración Inicial en GitHub (Obligatorio)

Para que el servidor de GitHub pueda firmar digitalmente la aplicación, debes registrar tus credenciales de seguridad. Ve a **Settings > Secrets and variables > Actions** en este repositorio y añade los siguientes **Repository secrets**:

1. **`TIZEN_CERTIFICATE_BASE64`**: El archivo de tu certificado (`author.p12`) convertido a texto plano Base64.
   * *Comando para generarlo en Windows (PowerShell):*
     ```powershell
     [Convert]::ToBase64String([IO.File]::ReadAllBytes("RUTA\A\TU\author.p12"))
     ```
2. **`TIZEN_CERTIFICATE_PASSWORD`**: La contraseña privada que le asignaste a tu certificado `.p12`.

---

## 🛠️ Cómo Compilar

¡No necesitas instalar nada en tu computadora!
1. Realiza cualquier cambio en el archivo `config.xml` (como actualizar la URL en `<content src="..." />`).
2. Sube los cambios a la rama principal (`git push origin main`).
3. Ve a la pestaña **Actions** en la parte superior de este repositorio en GitHub.
4. Verás el flujo de trabajo ejecutándose. Al finalizar (2-3 minutos), haz clic en la compilación exitosa y descarga el archivo **`tizen-widget`** de la sección de **Artifacts** (abajo del todo).

---

---

## 📺 Instalación en el Smart TV Samsung (Método Fácil con Apps2Samsung)

Este método te permite enviar el archivo `.wgt` compilado desde tu computadora al televisor usando una interfaz gráfica, sin necesidad de escribir comandos en la terminal.

### 1. Requisitos Previos
* Descarga el archivo **`.wgt`** final desde la pestaña **Actions** de este repositorio.
* Descarga la herramienta **Apps2Samsung** en tu computadora.
* **Importante:** Tu PC y tu Smart TV deben estar conectados a la **misma red Wi-Fi o cable LAN**.

### 2. Activar el Modo Desarrollador en el TV
1. En el televisor, ve a la sección de **Apps** (o Smart Hub).
2. Con el control remoto físico del TV, presiona la secuencia: **`1` ➔ `2` ➔ `3` ➔ `4` ➔ `5`**.
3. En la ventana emergente cambia el interruptor a **`ON`**.
4. En el campo **Host IP**, introduce la dirección IP local de tu computadora.
5. Selecciona **OK** y reinicia el televisor (mantén presionado el botón de encendido del control hasta que el televisor se apague y vuelva a encender solo).

### 3. Enviar la App al Televisor
1. Abre el programa **Apps2Samsung** en tu computadora.
2. En el campo **TV IP**, escribe la dirección IP de tu Smart TV.  
   *(La encuentras en tu TV en: Configuración > General > Red > Estado de red > Ajustes de IP)*.
3. Haz clic en **Select File** (o *Load WGT*) y selecciona el archivo `.wgt` que descargaste de GitHub.
4. Haz clic en el botón **Install** (o *Send to TV*).
5. En unos segundos, la aplicación **Pelis Latam** se instalará y se abrirá automáticamente en la pantalla de tu televisor.
