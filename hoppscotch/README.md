# Hoppscotch Community Edition

Cliente para desarrollar y probar APIs REST, GraphQL y WebSocket, disponible en
http://localhost:8084.

## Iniciar

Primero crea el archivo local de configuración y completa los dos secretos que
están vacíos:

```bash
cp .env.example .env
```

`HOPPSCOTCH_DB_PASSWORD` puede generarse con `openssl rand -hex 24` y
`HOPPSCOTCH_ENCRYPTION_KEY` con `openssl rand -hex 16`. Después inicia el
servicio:

```bash
docker compose up -d
```

El primer inicio crea la base de datos y ejecuta sus migraciones. PostgreSQL se
guarda en un volumen Docker para conservar la configuración, usuarios y
colecciones entre ejecuciones.

La administración está disponible en http://localhost:8084/admin.

## Configuración

El puerto es opcional y se puede cambiar mediante una variable de entorno:

```bash
HOPPSCOTCH_PORT=9004 docker compose up -d
```

`HOPPSCOTCH_ENCRYPTION_KEY` debe tener exactamente 32 caracteres. No cambies
los secretos después del primer inicio si ya existen datos cifrados.

> Si cambias el puerto después del primer inicio, inicia nuevamente todo el
> proyecto con la misma variable para que las URLs internas coincidan.

Para eliminar también todos los datos almacenados:

```bash
docker compose down -v
```
