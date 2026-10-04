# ChartDB

Editor visual de diagramas de bases de datos, disponible en
http://localhost:8086. Permite importar un esquema mediante la consulta que
genera la propia aplicación, sin entregar a ChartDB las credenciales de la
base de datos.

## Iniciar

```bash
docker compose up -d
```

Los diagramas se guardan en el almacenamiento local del navegador. Exporta una
copia desde la aplicación si necesitas conservarlos fuera de ese navegador.

## Configuración opcional

Para usar otro puerto:

```bash
CHARTDB_PORT=9006 docker compose up -d
```

Las funciones de IA requieren una clave de OpenAI:

```bash
CHARTDB_OPENAI_API_KEY=tu-clave docker compose up -d
```

La telemetría está desactivada por defecto. Se puede habilitar iniciando el
servicio con `CHARTDB_DISABLE_ANALYTICS=false`.
