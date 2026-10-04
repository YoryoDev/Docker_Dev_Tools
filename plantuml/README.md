# PlantUML Server

Servidor para crear diagramas UML a partir de texto, disponible en
http://localhost:8082.

```bash
docker compose up -d
```

Para usar otro puerto:

```bash
PLANTUML_PORT=9002 docker compose up -d
```

## MCP para OpenCode

El servidor comunitario `plantuml-mcp-server` está configurado globalmente en
OpenCode y apunta a `http://127.0.0.1:8082`. Se ejecuta con Node.js 26 mediante
`mise` y permite generar, validar, codificar y decodificar diagramas PlantUML.

Inicia este contenedor antes de solicitar el renderizado de un diagrama.
