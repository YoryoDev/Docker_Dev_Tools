# Penpot con MCP local

Herramienta profesional de diseño y prototipado disponible en
http://localhost:8087. Permite crear wireframes de baja fidelidad y evolucionar
los mismos archivos hasta interfaces de alta fidelidad con componentes, estilos,
tokens, layouts, recursos e interacciones.

La integración utiliza el MCP oficial de Penpot en modo local. El diseño y el
servidor MCP permanecen en el equipo.

## Configurar e iniciar

```bash
cp .env.example .env
```

Completa `PENPOT_SECRET_KEY` y `PENPOT_DB_PASSWORD` siguiendo los comandos
indicados en el ejemplo. Después inicia todos los servicios:

```bash
docker compose up -d
```

El primer arranque descarga varias imágenes y puede tardar. Crea una cuenta
local en http://localhost:8087 y abre o crea un archivo de diseño.

Cuando el servicio ya esté activo, abre `/mcps` en OpenCode y reconecta
`penpot` si el primer intento ocurrió antes de que terminara de arrancar.

## Conectar el MCP

1. En Penpot abre **Plugins → Load from URL**.
2. Introduce `http://localhost:4400/manifest.json`.
3. Ejecuta el plugin y pulsa **Connect to MCP server**.
4. Mantén abiertas la ventana del plugin y la pestaña de Penpot.
5. Pide primero al agente una operación de lectura, por ejemplo: “resume la
   estructura de la página actual”.

OpenCode se conecta localmente a `http://127.0.0.1:4401/mcp`. El MCP actúa sobre
la página enfocada en la pestaña que tenga conectado el plugin.

## Archivos y seguridad

El MCP puede ejecutar operaciones de escritura en el diseño. También tiene
acceso limitado a [`files/`](./files/) como `/workspace` dentro del contenedor
para importar y exportar recursos. No se monta el resto del repositorio ni el
directorio personal.

Conviene pedir al agente que describa los cambios antes de aplicarlos y trabajar
en pasos pequeños. Los diseños y recursos persistentes se guardan en volúmenes
Docker. Para eliminarlos definitivamente:

```bash
docker compose down -v
```

> La versión de Penpot y `@penpot/mcp` está fijada a `2.15.4` porque el proyecto
> oficial exige que ambas coincidan. Actualiza las dos juntas.
