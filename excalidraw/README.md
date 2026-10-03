# Excalidraw con MCP

Pizarra local compatible con MCP, disponible en http://localhost:8081. Incluye
sincronización en tiempo real y persistencia SQLite.

Esta instalación usa el proyecto comunitario
[`mcp-excalidraw-local`](https://github.com/sanjibdevnathlabs/mcp-excalidraw-local),
basado en Excalidraw. No es el contenedor oficial de Excalidraw.

## Iniciar el lienzo

```bash
docker compose up -d
```

Para usar otro puerto:

```bash
EXCALIDRAW_PORT=9001 docker compose up -d
```

Puedes cambiar el puerto web sin modificar el MCP, porque este se comunica con
el lienzo mediante la red interna de Docker.

## Usar el MCP desde OpenCode

El archivo [`../opencode.jsonc`](../opencode.jsonc) configura un servidor MCP
local llamado `excalidraw`. OpenCode lanza el proceso MCP en un contenedor
temporal y lo conecta al lienzo mediante la red de Docker Compose.

1. Inicia el lienzo:

   ```bash
   docker compose -f excalidraw/compose.yaml up -d
   ```

2. Reinicia OpenCode desde la raíz de este repositorio.
3. Comprueba la conexión:

   ```bash
   opencode mcp list
   ```

El servicio debe aparecer como `excalidraw` y conectado. El MCP ofrece
herramientas para crear, consultar, modificar, ordenar, importar y exportar
elementos.

## Persistencia

Los lienzos se guardan en el volumen Docker `excalidraw-data` y sobreviven a
`docker compose down`. Para eliminar definitivamente la base de datos:

```bash
docker compose down -v
```

## Compatibilidad con excalidraw.com

El MCP permite:

- Exportar escenas como archivos `.excalidraw` que puedes abrir en
  https://excalidraw.com/.
- Importar al lienzo local archivos creados en `excalidraw.com`.
- Usar `export_to_excalidraw_url` para generar un enlace compartible cifrado.

No existe sincronización automática con una pestaña o cuenta de
`excalidraw.com`. La interoperabilidad se realiza mediante archivos o enlaces
compartibles.

## Detener

```bash
docker compose -f excalidraw/compose.yaml down
```
