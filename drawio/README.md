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
