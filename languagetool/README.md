# LanguageTool

Corrector de gramática, ortografía y estilo en más de 25 idiomas (incluido
español), autoalojado. Los textos no salen de tu equipo. API disponible en
http://localhost:8088/v2.

```bash
docker compose up -d
```

Para usar otro puerto:

```bash
LANGUAGETOOL_PORT=9008 docker compose up -d
```

## Probar la API

```bash
curl -d "language=es" -d "text=Ayer fuimos a la playa y se nos olvido la toalla." \
  http://localhost:8088/v2/check
```

Lista de idiomas soportados: `http://localhost:8088/v2/languages`.

## Memoria

Por defecto la JVM usa entre 256 MB y 1 GB (`LANGUAGETOOL_JAVA_XMS` y
`LANGUAGETOOL_JAVA_XMX`). Sin n-gramas es suficiente para español; la
detección de palabras confundibles es algo menos precisa, pero se evita la
descarga de unos 16 GB de datos.

## Uso con IA

El servidor encaja con un MCP como
[mcp-grammar-checker](https://glama.ai/mcp/servers/olga1988olga/mcp-grammar-checker/tree),
que por defecto usa la API pública (con límite de uso). Apúntalo a
`http://localhost:8088` para revisar sin límites y sin enviar el contenido a
terceros.
