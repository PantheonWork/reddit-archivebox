 Este formato incluye pasos claros y concisos para la configuración y el uso de ArchiveBox.

markdown

# ArchiveBox para Archivar Enlaces de Reddit

## Descripción
Este repositorio contiene instrucciones para configurar **ArchiveBox** y archivar el HTML de todos los enlaces que has votado en Reddit.

## Requisitos
- Docker y Docker Compose instalados en tu sistema.
- Una cuenta de Reddit.

## Pasos

### 1. Obtener el archivo de enlaces de Reddit

1. **Iniciar sesión en Reddit**: Abre tu navegador y accede a tu cuenta de Reddit.

2. **Exportar tus votos**:
   - Usa una herramienta como [Pushshift Reddit](https://pushshift.io/) para obtener un archivo con los enlaces que has votado.
   - Alternativamente, puedes usar una extensión de navegador o un script en Python para obtener el historial de tus votos y guardarlo en un archivo de texto.

3. **Guardar los enlaces**:
   - Guarda los enlaces en un archivo llamado `upvotes.txt`, con un enlace por línea.

### 2. Configurar ArchiveBox

1. **Crear el directorio para ArchiveBox**:
   ```bash
   mkdir ~/archivebox
   cd ~/archivebox

    Crear el archivo docker-compose.yml: Crea un archivo llamado docker-compose.yml con el siguiente contenido:

    yaml

    version: '3'

    services:
        archivebox:
            image: archivebox/archivebox:latest
            ports:
                - 8000:8000
            volumes:
                - ./data:/data
            environment:
                - COOKIES_FILE=/data/cookies.txt          # Archivo de cookies
                - FETCH_SINGLEFILE=True                     # Solo guardar singlefile
                - FETCH_FAVICON=False                       # Deshabilitar favicon
                - FETCH_WGET=False                          # Deshabilitar wget
                - FETCH_PDF=False                           # Deshabilitar PDF
                - FETCH_SCREENSHOT=False                    # Deshabilitar screenshots
                - FETCH_DOM=False                           # Deshabilitar DOM
                - FETCH_WARC=False                          # Deshabilitar WARC
                - FETCH_READABILITY=False                   # Deshabilitar Readability
                - FETCH_MERCURY=False                       # Deshabilitar Mercury
                - PUBLIC_ADD_VIEW=False                     # Evita que usuarios anónimos añadan enlaces

3. Agregar el archivo de cookies

    Exportar las cookies:
        Usa una extensión de navegador (como EditThisCookie) para exportar tus cookies de Reddit a un archivo llamado cookies.txt.

    Mover el archivo de cookies: Mueve el archivo cookies.txt a la carpeta data:

    bash

    mv /ruta/al/cookies.txt ~/archivebox/data/

4. Iniciar ArchiveBox

    Iniciar ArchiveBox:

    bash

docker-compose up -d

Inicializar ArchiveBox:

bash

    docker-compose run archivebox init --setup

5. Agregar enlaces

Agrega los enlaces desde el archivo upvotes.txt:

bash

docker-compose run -T archivebox add < /ruta/al/upvotes.txt

6. Acceder a la interfaz web

Accede a la interfaz web de ArchiveBox en:

arduino

http://127.0.0.1:8000
