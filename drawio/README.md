# Draw.io / diagrams.net

Editor de diagramas técnicos, flujos y arquitecturas, disponible en
http://localhost:8083.

```bash
docker compose up -d
```

Para usar otro puerto:

```bash
DRAWIO_PORT=9003 docker compose up -d
```

Los diagramas pueden guardarse como archivos locales desde la propia
aplicación. La configuración no habilita integraciones externas ni HTTPS.

## MCP para OpenCode

El servidor MCP oficial `@drawio/mcp` está configurado globalmente en OpenCode
y usa esta instancia mediante `DRAWIO_BASE_URL=http://127.0.0.1:8083/`. Se
ejecuta con Node.js 26 a través de `mise` y permite crear diagramas XML, CSV o
Mermaid, buscar formas y editar páginas de archivos `.drawio`.

Inicia este contenedor antes de abrir los enlaces generados por el MCP.
