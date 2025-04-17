# Configuración de GitHub Sync para Obsidian en Windows

Esta guía te ayudará a configurar el plugin GitHub Sync para Obsidian en Windows, permitiéndote sincronizar tu bóveda entre diferentes dispositivos.

## Requisitos previos
- Cuenta de GitHub
- Obsidian instalado
- Git para Windows

## Paso 1: Instalar Git para Windows

1. Descarga Git para Windows desde [git-scm.com](https://git-scm.com/download/win)
2. Ejecuta el instalador y sigue las instrucciones:
   - En las opciones, asegúrate de seleccionar "Git from the command line and also from 3rd-party software"
   - Para el editor predeterminado, puedes elegir el que prefieras (Notepad++ o Visual Studio Code son buenas opciones)
   - Para la rama predeterminada, mantén "main"
   - Para PATH, selecciona "Git from the command line and also from 3rd-party software"
   - Para SSH, selecciona "Use OpenSSH"
   - Para HTTPS, selecciona "Use the OpenSSL library"
   - Para conversión de fin de línea, selecciona "Checkout Windows-style, commit Unix-style"
   - Para el emulador de terminal, selecciona "Use MinTTY"
   - Para git pull, selecciona "Default"
   - Para credenciales, selecciona "Git Credential Manager"
   - Habilita la caché de sistema de archivos

## Paso 2: Generar una clave SSH

1. Abre Git Bash (busca en el menú inicio o haz clic derecho en cualquier carpeta y selecciona "Git Bash Here")
2. Ejecuta el siguiente comando para generar una clave SSH (reemplaza con tu email de GitHub):
   ```
   ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
   ```
3. Cuando te pida la ubicación para guardar la clave, puedes presionar Enter para usar la ubicación predeterminada o especificar una ruta personalizada
4. Establece una contraseña para tu clave SSH (opcional pero recomendado)
5. Verifica que la clave se haya generado:
   ```
   ls -la ~/.ssh
   ```

## Paso 3: Agregar la clave SSH a GitHub

1. Copia tu clave pública al portapapeles:
   ```
   cat ~/.ssh/id_ed25519.pub | clip
   ```
   (Si usaste un nombre de archivo personalizado, ajusta el comando)
2. Abre [GitHub](https://github.com) en tu navegador e inicia sesión
3. Haz clic en tu foto de perfil → Settings
4. En la barra lateral izquierda, haz clic en "SSH and GPG keys"
5. Haz clic en "New SSH key"
6. Proporciona un título descriptivo (por ejemplo, "Windows Laptop")
7. Pega la clave en el campo "Key"
8. Haz clic en "Add SSH key"

## Paso 4: Configurar Git

1. Configura tu identidad de Git:
   ```
   git config --global user.name "Tu Nombre"
   git config --global user.email "tu_email@ejemplo.com"
   ```

## Paso 5: Instalar el plugin GitHub Sync en Obsidian

1. Abre Obsidian
2. Haz clic en el icono de configuración (⚙️) en la barra lateral izquierda
3. Ve a "Plugins de la comunidad"
4. Haz clic en "Examinar" y busca "GitHub Sync"
5. Haz clic en "Instalar"
6. Después de la instalación, habilita el plugin

## Paso 6: Clonar tu repositorio existente

Si ya tienes una bóveda sincronizada en GitHub y quieres clonarla en Windows:

1. Abre Git Bash
2. Navega a la ubicación donde quieres crear tu bóveda:
   ```
   cd "C:/Users/TuUsuario/Documents"
   ```
3. Clona el repositorio:
   ```
   git clone git@github.com:tu-usuario/nombre-repositorio.git
   ```
4. Abre Obsidian y selecciona "Abrir carpeta como bóveda"
5. Navega hasta la carpeta clonada y selecciónala

## Paso 7: Configurar el plugin GitHub Sync

1. En Obsidian, ve a Configuración → Plugins de la comunidad → GitHub Sync → Opciones
2. En "Remote URL", introduce la URL SSH de tu repositorio:
   ```
   git@github.com:tu-usuario/nombre-repositorio.git
   ```
3. Si Git no está en tu PATH, especifica la ruta al ejecutable Git (por ejemplo: `C:/Program Files/Git/bin/`)

## Paso 8: Probar la sincronización

1. Realiza algún cambio en tu bóveda (crea una nueva nota o modifica una existente)
2. Haz clic en el icono "Sync with Remote" en la barra lateral de Obsidian
3. Si aparece algún mensaje de autenticación, introduce tu contraseña de la clave SSH si la configuraste

## Solución de problemas comunes

### Error de autenticación
Si encuentras problemas de autenticación, asegúrate de que:
- Tu clave SSH está correctamente añadida a GitHub
- El agente SSH está en ejecución:
  ```
  eval $(ssh-agent -s)
  ssh-add ~/.ssh/id_ed25519
  ```
- Prueba la conexión SSH:
  ```
  ssh -T git@github.com
  ```

### Path de Git no encontrado
Si Obsidian no puede encontrar Git:
1. Localiza dónde está instalado Git (normalmente en `C:\Program Files\Git\bin\git.exe`)
2. En la configuración del plugin, especifica la ruta a la carpeta que contiene `git.exe`

### Conflictos de fusión
Si hay conflictos durante la sincronización:
1. El plugin abrirá los archivos con conflictos
2. Edita los archivos para resolver los conflictos
3. Haz clic nuevamente en "Sync with Remote"