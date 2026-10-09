# Docker Dev Tools

Colección de herramientas de desarrollo autoalojadas con Docker. Cada servicio
vive en su propia carpeta y puede iniciarse de forma independiente.

## Servicios

| Herramienta | Descripción | URL local |
| --- | --- | --- |
| [IT Tools](./it-tools/) | Utilidades para desarrolladores | http://localhost:8080 |
| [Excalidraw MCP](./excalidraw/) | Pizarra local controlable por IA | http://localhost:8081 |
| [PlantUML](./plantuml/) | Renderizado de diagramas UML | http://localhost:8082 |
| [Draw.io](./drawio/) | Creación de diagramas técnicos | http://localhost:8083 |
| [Hoppscotch](./hoppscotch/) | Desarrollo y pruebas de APIs | http://localhost:8084 |
| [CyberChef](./cyberchef/) | Conversión y análisis de datos | http://localhost:8085 |
| [ChartDB](./chartdb/) | Diseño y visualización de bases de datos | http://localhost:8086 |
| [Penpot](./penpot/) | Wireframes y prototipos de baja y alta fidelidad | http://localhost:8087 |
| [Portainer CE](./portainer/) | Gestión local de contenedores Docker | https://localhost:9443 |
| [WinDocker](./WinDocker/) | Máquina virtual Windows 11 con KVM | http://localhost:8006 |

## Requisitos

- Docker Engine o Docker Desktop
- Docker Compose v2

## Uso

Inicia una herramienta desde la raíz del repositorio:

```bash
docker compose -f it-tools/compose.yaml up -d
docker compose -f excalidraw/compose.yaml up -d
docker compose -f plantuml/compose.yaml up -d
docker compose -f drawio/compose.yaml up -d
docker compose --env-file hoppscotch/.env -f hoppscotch/compose.yaml up -d
docker compose -f cyberchef/compose.yaml up -d
docker compose -f chartdb/compose.yaml up -d
docker compose --env-file penpot/.env -f penpot/compose.yaml up -d
docker compose -f portainer/compose.yaml up -d
docker compose --env-file WinDocker/.env -f WinDocker/compose.yaml up -d
```

Para detenerla, sustituye `up -d` por `down`. Por ejemplo:

```bash
docker compose -f it-tools/compose.yaml down
```

Consulta los logs de un servicio con:

```bash
docker compose -f it-tools/compose.yaml logs -f
```

## Configuración

Cada carpeta contiene un `.env.example` con las variables disponibles. Para
personalizar un servicio, entra en su carpeta y copia el ejemplo:

```bash
cd it-tools
cp .env.example .env
docker compose up -d
```

Hoppscotch, Penpot y WinDocker requieren crear y completar su `.env` antes del
primer inicio. En los demás servicios es opcional porque existen valores por defecto.
Si ejecutas Compose desde la raíz, indica el archivo explícitamente con
`--env-file carpeta/.env`.

Los puertos se pueden cambiar mediante variables de entorno:

```bash
IT_TOOLS_PORT=9000 docker compose -f it-tools/compose.yaml up -d
EXCALIDRAW_PORT=9001 docker compose -f excalidraw/compose.yaml up -d
PLANTUML_PORT=9002 docker compose -f plantuml/compose.yaml up -d
DRAWIO_PORT=9003 docker compose -f drawio/compose.yaml up -d
HOPPSCOTCH_PORT=9004 docker compose --env-file hoppscotch/.env -f hoppscotch/compose.yaml up -d
CYBERCHEF_PORT=9005 docker compose -f cyberchef/compose.yaml up -d
CHARTDB_PORT=9006 docker compose -f chartdb/compose.yaml up -d
PENPOT_PORT=9007 docker compose --env-file penpot/.env -f penpot/compose.yaml up -d
PORTAINER_PORT=9444 docker compose -f portainer/compose.yaml up -d
WINDOCKER_WEB_PORT=8016 docker compose --env-file WinDocker/.env -f WinDocker/compose.yaml up -d
```

En PowerShell, define la variable antes de ejecutar Compose:

```powershell
$env:IT_TOOLS_PORT = "9000"
docker compose -f it-tools/compose.yaml up -d
```

> Estas aplicaciones se publican en `127.0.0.1` por defecto y solo son
> accesibles desde el equipo local. Para exponerlas en la red, cambia
> `127.0.0.1` por `0.0.0.0` en el `compose.yaml` correspondiente.

## Integración MCP (OpenCode y Claude Code)

Draw.io, PlantUML, Excalidraw, Hoppscotch y Penpot se configuran en dos archivos equivalentes.
Copia el que corresponda a la raíz de tu proyecto:

| Cliente | Archivo | Comprobar |
| --- | --- | --- |
| OpenCode | [`opencode.jsonc`](./opencode.jsonc) | `opencode mcp list` |
| Claude Code | [`.mcp.json`](./.mcp.json) | `claude mcp list` |

Requisitos: Docker (Excalidraw) y Node.js 22 o superior (Draw.io, PlantUML y
Hoppscotch). Inicia
antes los contenedores correspondientes; el MCP de Penpot lo expone su propio
`compose.yaml`. Claude Code pide aprobar los servidores de `.mcp.json` la
primera vez.

Los archivos son idénticos en Windows, macOS y Linux. Hoppscotch se lanza con
`node` y `shell: true`, que usa `npx` o `npx.cmd` según el sistema, así que no
hace falta el envoltorio `cmd /c` en Windows.

Draw.io y PlantUML usan tus contenedores locales (puertos 8083 y 8082 por
defecto); si cambias el puerto, actualiza `DRAWIO_BASE_URL` o
`PLANTUML_SERVER_URL`.
