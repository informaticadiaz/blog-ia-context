# Configuración de GitHub Sync para Obsidian en Linux

Esta guía te ayudará a configurar el plugin GitHub Sync para Obsidian en sistemas Linux, permitiéndote sincronizar tu bóveda entre diferentes dispositivos.

## Requisitos previos
- Cuenta de GitHub
- Obsidian instalado
- Git instalado en tu sistema

## Paso 1: Instalar Git (si aún no está instalado)

Dependiendo de tu distribución de Linux, utiliza uno de estos comandos:

**Ubuntu/Debian/Kali Linux**:
```bash
sudo apt update
sudo apt install git
```

**Fedora**:
```bash
sudo dnf install git
```

**Arch Linux**:
```bash
sudo pacman -S git
```

Verifica la instalación:
```bash
git --version
```

## Paso 2: Generar una clave SSH

1. Abre la terminal
2. Genera una nueva clave SSH:
   ```bash
   ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
   ```
   (Reemplaza con el email que usas en GitHub)
3. Cuando te pida la ubicación para guardar la clave, puedes:
   - Presionar Enter para usar la ubicación predeterminada (`~/.ssh/id_ed25519`)
   - O especificar una ruta personalizada (por ejemplo: `~/obsidian-key`)
4. Opcionalmente, establece una contraseña para la clave

## Paso 3: Configurar el agente SSH

1. Inicia el agente SSH en segundo plano:
   ```bash
   eval "$(ssh-agent -s)"
   ```

2. Añade tu clave privada al agente SSH:
   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```
   (Si usaste una ruta personalizada, ajusta el comando)

## Paso 4: Agregar la clave SSH a GitHub

1. Copia tu clave pública al portapapeles:
   ```bash
   cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard
   ```
   (Si no tienes xclip instalado: `sudo apt install xclip` en Debian/Ubuntu/Kali)

   Alternativa sin xclip:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   Y copia manualmente la salida

2. Abre [GitHub](https://github.com) en tu navegador e inicia sesión
3. Haz clic en tu foto de perfil → Settings
4. En la barra lateral izquierda, haz clic en "SSH and GPG keys"
5. Haz clic en "New SSH key"
6. Proporciona un título descriptivo (por ejemplo, "Linux Laptop")
7. Pega la clave en el campo "Key"
8. Haz clic en "Add SSH key"

## Paso 5: Configurar Git

1. Configura tu identidad de Git:
   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tu_email@ejemplo.com"
   ```

## Paso 6: Instalar Obsidian (si aún no está instalado)

**Usando el instalador AppImage**:
1. Descarga el archivo AppImage desde [la página oficial de Obsidian](https://obsidian.md/)
2. Haz el archivo ejecutable:
   ```bash
   chmod +x Obsidian-*.AppImage
   ```
3. Ejecuta la aplicación:
   ```bash
   ./Obsidian-*.AppImage
   ```

**Usando Flatpak**:
```bash
flatpak install flathub md.obsidian.Obsidian
flatpak run md.obsidian.Obsidian
```

**Usando Snap**:
```bash
sudo snap install obsidian
```

## Paso 7: Instalar el plugin GitHub Sync en Obsidian

1. Abre Obsidian
2. Haz clic en el icono de configuración (⚙️) en la barra lateral izquierda
3. Ve a "Plugins de la comunidad"
4. Haz clic en "Examinar" y busca "GitHub Sync"
5. Haz clic en "Instalar"
6. Después de la instalación, habilita el plugin

## Paso 8: Clonar tu repositorio existente

Si ya tienes una bóveda sincronizada en GitHub y quieres clonarla en tu sistema Linux:

1. Abre la terminal
2. Navega a la ubicación donde quieres crear tu bóveda:
   ```bash
   cd ~/Documentos
   ```
3. Clona el repositorio:
   ```bash
   git clone git@github.com:tu-usuario/nombre-repositorio.git
   ```
4. Abre Obsidian y selecciona "Abrir carpeta como bóveda"
5. Navega hasta la carpeta clonada y selecciónala

## Paso 9: Configurar el plugin GitHub Sync

1. En Obsidian, ve a Configuración → Plugins de la comunidad → GitHub Sync → Opciones
2. En "Remote URL", introduce la URL SSH de tu repositorio:
   ```
   git@github.com:tu-usuario/nombre-repositorio.git
   ```

## Paso 10: Probar la sincronización

1. Realiza algún cambio en tu bóveda (crea una nueva nota o modifica una existente)
2. Haz clic en el icono "Sync with Remote" en la barra lateral de Obsidian
3. Si aparece algún mensaje de autenticación, introduce tu contraseña de la clave SSH si la configuraste

## Solución de problemas comunes

### Error de permisos
Si encuentras errores de permisos:
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### Error de autenticación
Verifica que puedes conectarte a GitHub:
```bash
ssh -T git@github.com
```
Deberías recibir un mensaje como: "Hi username! You've successfully authenticated..."

### No se puede encontrar el binario Git
Si Obsidian no puede encontrar Git, puedes proporcionar la ruta completa:
```bash
which git
```
Y luego agrega esa ruta en la configuración del plugin.

### Conflictos de fusión
Si hay conflictos durante la sincronización:
1. El plugin abrirá los archivos con conflictos
2. Edita los archivos para resolver los conflictos
3. Haz clic nuevamente en "Sync with Remote"

### Error "Repository not found"
Asegúrate de que:
1. El repositorio existe en GitHub
2. Estás utilizando el nombre correcto del repositorio
3. Tu clave SSH tiene acceso al repositorio
4. Si el repositorio es privado, tu cuenta tiene permisos para acceder a él