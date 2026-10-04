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
`HOPPSCOTCH_DB_PASSWORD_URL` debe contener la misma contraseña que
`HOPPSCOTCH_DB_PASSWORD`, pero con los caracteres reservados codificados para
URL.

> Si cambias el puerto después del primer inicio, inicia nuevamente todo el
> proyecto con la misma variable para que las URLs internas coincidan.

Para eliminar también todos los datos almacenados:

```bash
docker compose down -v
```

## MCP para OpenCode

El servidor MCP oficial `@hoppscotch/mcp-server` está configurado únicamente
para este proyecto y apunta a `http://127.0.0.1:8084`. Se ejecuta con Node.js 26
mediante `mise` y usa el perfil `core`, que expone las operaciones habituales
sin habilitar toda la administración avanzada.

Después de iniciar Hoppscotch, la primera operación MCP abrirá el navegador para
iniciar sesión. La sesión se guarda en `~/.config/hoppscotch-mcp/`. La Community
Edition puede solicitar un nuevo inicio de sesión cuando expire el token.
