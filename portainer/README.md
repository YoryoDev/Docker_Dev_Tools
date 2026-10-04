# Portainer Community Edition

Interfaz web para ver y gestionar los contenedores, imágenes, redes y volúmenes
del Docker local, disponible en https://localhost:9443.

## Iniciar

```bash
docker compose up -d
```

Portainer usa un certificado autofirmado, por lo que el navegador mostrará un
aviso de seguridad la primera vez. Crea el usuario administrador en la pantalla
inicial y selecciona el entorno Docker local.

La configuración de Portainer se conserva en un volumen Docker. Para eliminar
también esa configuración:

```bash
docker compose down -v
```

## Configuración opcional

Para usar otro puerto:

```bash
PORTAINER_PORT=9444 docker compose up -d
```

> Portainer tiene acceso al socket de Docker para poder administrar el motor.
> Esto equivale, en la práctica, a permisos administrativos sobre el equipo.
> Por seguridad, el puerto solo se publica en `127.0.0.1`; no lo expongas a una
> red sin configurar antes autenticación, HTTPS y controles de acceso adecuados.
