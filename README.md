# ORAMA MCP · API REST v1 (OpenAPI 3.1)

Especificación de la API de ORAMA MCP (Bitcopper Tech SpA): `openapi.json`.

## Qué es y qué no es

- **Se genera desde el código**, no se escribe a mano: `npm run openapi` recorre `app/api/v1`. Cada `route.js` es una ruta y cada método exportado es una operación. El comentario que acompaña a la función en el código es la descripción.
- **La prueba `tests/openapi.test.mjs` falla si el archivo no coincide con el código.** Así la especificación publicada no queda desactualizada.
- **Los cuerpos y las respuestas se describen en texto** (la descripción de cada operación), no con esquemas tipados. Lo único tipado es:
  - la forma común de los errores: `{ "error": { "codigo", "mensaje", "campos"? } }`;
  - los parámetros de ruta.

  Los esquemas no se inventan: cuando se tipen, saldrán del código de validación (`shared/*.js`).
- Algunas operaciones no tienen comentario en el código, así que salen sin descripción. Se identifican porque les falta `description`; el campo `x-archivo` dice qué archivo documentar.

## Autenticación

- `sesion`: `Authorization: Bearer <token de sesión de Supabase>`. Es el mismo token que usa el panel y lo tienen casi todas las rutas.
- `clave`: `Authorization: Bearer <clave de dispositivo>`. Lo usan `/api/v1/flota/ingesta` y `/api/v1/seguridad/eventos`; la clave se crea en el panel.

El servidor MCP (`/api/mcp`) no está en esta especificación: usa el protocolo MCP con OAuth 2.1, no REST.

## Servidor

`https://mcp-business-agent.vercel.app`

## Licencia

© Bitcopper Tech SpA. Esta especificación se publica bajo la licencia [Creative Commons Atribución 4.0 Internacional (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/): se puede usar, copiar y adaptar, también con fines comerciales, citando a Bitcopper Tech SpA. El texto legal completo está en `LICENSE`. La licencia cubre este documento, no el código de ORAMA MCP, que no es público, ni ninguna patente.
