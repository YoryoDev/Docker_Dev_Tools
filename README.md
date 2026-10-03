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
docker compose -f hoppscotch/compose.yaml up -d
docker compose -f cyberchef/compose.yaml up -d
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

Los puertos se pueden cambiar mediante variables de entorno:

```bash
IT_TOOLS_PORT=9000 docker compose -f it-tools/compose.yaml up -d
EXCALIDRAW_PORT=9001 docker compose -f excalidraw/compose.yaml up -d
PLANTUML_PORT=9002 docker compose -f plantuml/compose.yaml up -d
DRAWIO_PORT=9003 docker compose -f drawio/compose.yaml up -d
HOPPSCOTCH_PORT=9004 docker compose -f hoppscotch/compose.yaml up -d
CYBERCHEF_PORT=9005 docker compose -f cyberchef/compose.yaml up -d
```

En PowerShell, define la variable antes de ejecutar Compose:

```powershell
$env:IT_TOOLS_PORT = "9000"
docker compose -f it-tools/compose.yaml up -d
```

> Estas aplicaciones se publican en `127.0.0.1` por defecto y solo son
> accesibles desde el equipo local. Para exponerlas en la red, cambia
> `127.0.0.1` por `0.0.0.0` en el `compose.yaml` correspondiente.
