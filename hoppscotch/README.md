# Hoppscotch Community Edition

Cliente para desarrollar y probar APIs REST, GraphQL y WebSocket, disponible en
http://localhost:8084.

## Iniciar

```bash
docker compose up -d
```

El primer inicio crea la base de datos y ejecuta sus migraciones. PostgreSQL se
guarda en un volumen Docker para conservar la configuración, usuarios y
colecciones entre ejecuciones.

La administración está disponible en http://localhost:8084/admin.

## Configuración opcional

El puerto, la contraseña de PostgreSQL y la clave de cifrado se pueden cambiar
mediante variables de entorno:

```bash
HOPPSCOTCH_PORT=9004 \
HOPPSCOTCH_DB_PASSWORD=otra-clave \
HOPPSCOTCH_ENCRYPTION_KEY=0123456789abcdef0123456789abcdef \
docker compose up -d
```

`HOPPSCOTCH_ENCRYPTION_KEY` debe tener exactamente 32 caracteres. Conviene
cambiar ambos secretos antes del primer inicio si se almacenarán datos reales.

> Si cambias el puerto después del primer inicio, inicia nuevamente todo el
> proyecto con la misma variable para que las URLs internas coincidan.

Para eliminar también todos los datos almacenados:

```bash
docker compose down -v
```
