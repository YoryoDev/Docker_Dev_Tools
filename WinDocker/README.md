# WinDocker

Máquina virtual Windows 11 Pro ejecutada con KVM mediante
[`dockurr/windows`](https://github.com/dockur/windows). La interfaz web está
disponible en http://localhost:8006 y RDP en `localhost:3389`.

## Requisitos

- Linux (recomendado) o Windows con WSL2 y virtualización anidada. macOS no es
  compatible porque no ofrece KVM.
- Linux con virtualización Intel VT-x o AMD-V habilitada.
- Docker Engine con acceso a `/dev/kvm` y `/dev/net/tun`.
- Al menos 6 GB de RAM disponibles.
- Espacio suficiente para la descarga de Windows y un disco virtual de hasta
  100 GB.
- Una licencia válida de Windows para activarlo.

Puedes comprobar KVM con:

```bash
test -e /dev/kvm && echo "KVM disponible"
```

## Configurar e iniciar

Crea el archivo local de credenciales y edítalo antes del primer inicio:

```bash
cp .env.example .env
```

Después inicia la máquina:

```bash
docker compose up -d
```

El primer arranque descarga e instala Windows automáticamente y puede tardar
bastante. Las credenciales de `.env` se utilizan para Windows y para proteger
la interfaz web. El archivo está excluido de Git.

Los datos persistentes se guardan por defecto en `./storage` (junto a este
`compose.yaml`), mientras que `./shared` se monta con acceso de lectura y
escritura como la unidad compartida `Z:`. Ambas rutas son relativas para
funcionar en cualquier sistema; define `WINDOCKER_STORAGE` y `WINDOCKER_SHARED`
en `.env` para usar otras (por ejemplo, para conservar una instalación previa).

## Detener

```bash
docker compose down
```

No borres el directorio de almacenamiento si quieres conservar la instalación.
Los puertos y las rutas pueden personalizarse con las variables opcionales que
aparecen en `.env.example`.

> Los puertos solo se publican en `127.0.0.1`. El contenedor recibe acceso a KVM,
> TUN y `NET_ADMIN`, y Windows puede modificar los archivos de la carpeta
> compartida.
