# Excalidraw

Pizarra para crear diagramas, disponible en http://localhost:8081.

```bash
docker compose up -d
```

Para usar otro puerto:

```bash
EXCALIDRAW_PORT=9001 docker compose up -d
```

Esta configuración ejecuta el frontend de Excalidraw. No incluye servidor de
colaboración en tiempo real ni almacenamiento en servidor.
