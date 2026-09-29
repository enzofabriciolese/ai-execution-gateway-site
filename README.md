# AI Execution Gateway — sitio público y configuración OAuth

Repositorio público de información, documentación y política de privacidad para la integración OAuth de **AI Execution Gateway** con Google.

- Sitio: <https://enzofabriciolese.github.io/ai-execution-gateway-site/>
- Política de privacidad: <https://enzofabriciolese.github.io/ai-execution-gateway-site/privacy.html>
- Estado del despliegue: GitHub Pages desde la rama `main`, directorio raíz, HTTPS obligatorio.

> Este repositorio no contiene el código privado del Worker, credenciales OAuth, tokens, secretos, archivos de configuración del host ni datos del Control Plane.

## Propósito

AI Execution Gateway es una herramienta local de automatización controlada. Coordina operaciones autorizadas por el usuario y utiliza servicios de Google únicamente para las funciones configuradas.

Este repositorio existe para:

1. ofrecer una página principal pública para la pantalla de consentimiento OAuth;
2. publicar una política de privacidad específica del Gateway;
3. documentar, sin secretos, la configuración vigente de Google Auth Platform;
4. registrar el estado y los pasos pendientes de verificación.

## Arquitectura resumida

```text
Usuario
  │ autorización explícita
  ▼
Worker local de AI Execution Gateway
  ├── Google Sheets API  → plano de control autorizado
  ├── Google Drive API   → archivos creados/seleccionados para el Gateway
  └── Gmail API          → envío de notificaciones autorizadas
```

El Worker se ejecuta localmente. GitHub Pages sólo aloja documentación pública y no participa en la ejecución del Gateway.

## Google Cloud

| Propiedad | Valor |
|---|---|
| Proyecto | `ai-execution-gateway` |
| Nombre visible de la app | AI Execution Gateway |
| Tipo de usuario | Externo |
| Estado de publicación | En producción |
| Cliente OAuth existente | Aplicación de escritorio |
| Dominio autorizado | `enzofabriciolese.github.io` |
| Página principal | <https://enzofabriciolese.github.io/ai-execution-gateway-site/> |
| Política de privacidad | <https://enzofabriciolese.github.io/ai-execution-gateway-site/privacy.html> |
| Verificación de Google | Requerida; todavía no enviada |

No se creó ni reemplazó el cliente OAuth de escritorio durante esta configuración.

## APIs habilitadas

- Google Sheets API
- Google Drive API
- Gmail API

## Alcances OAuth configurados

| Alcance | Uso |
|---|---|
| `https://www.googleapis.com/auth/spreadsheets` | Leer y actualizar las hojas de cálculo autorizadas usadas como plano de control. |
| `https://www.googleapis.com/auth/drive.file` | Acceder sólo a archivos creados por la aplicación o seleccionados explícitamente por el usuario. |
| `https://www.googleapis.com/auth/gmail.send` | Enviar correos y notificaciones autorizadas; no concede lectura de la bandeja de entrada. |

Los alcances se mantienen en el mínimo necesario para las funciones actuales.

## Estado de Google Auth Platform

La información de marca ya está completa y guardada:

- nombre de aplicación configurado;
- correo de asistencia configurado en Google Cloud (no se publica en este repositorio);
- página principal pública verificada;
- política de privacidad pública verificada;
- dominio `enzofabriciolese.github.io` registrado como autorizado;
- aplicación cambiada de **Prueba** a **En producción**.

Después del cambio a producción, Google mostró el aviso:

> Tu app requiere una verificación. Cuando termines de configurar la información, envía tu app para su revisión.

La solicitud de verificación **no se ha enviado**. Ese paso requiere una fase separada de revisión y autorización.

## Estado de autenticación local

La comprobación segura del host se realizó sin enviar correos. El token local existente respondió `invalid_grant`, por lo que será necesario repetir el flujo de consentimiento OAuth después de decidir cómo gestionar la verificación de Google.

No se realizó una prueba de envío de Gmail.

## Contenido del repositorio

- `index.html`: página principal pública de AI Execution Gateway.
- `privacy.html`: política de privacidad, datos tratados, finalidades, conservación, seguridad y derechos del usuario.
- `README.md`: registro público de la configuración y el estado actual.

## Seguridad y privacidad

- Nunca se deben añadir `client_secret`, tokens de acceso, refresh tokens, cookies, contraseñas ni archivos locales de configuración.
- Los datos recibidos mediante APIs de Google se utilizan sólo para las funciones visibles y autorizadas.
- No se venden datos ni se utilizan con fines publicitarios.
- El acceso puede revocarse desde la configuración de seguridad de la cuenta de Google.
- El uso de datos de Google debe cumplir la [Política de datos de usuario de los servicios API de Google](https://developers.google.com/terms/api-services-user-data-policy), incluidos los requisitos de Uso Limitado.
- Las incidencias públicas no deben contener secretos ni información personal sensible.

## Operación y cambios

Toda modificación material de la política o de los alcances OAuth debe:

1. actualizar este README y, cuando corresponda, `privacy.html`;
2. conservar el principio de privilegio mínimo;
3. evitar publicar secretos o datos operativos privados;
4. comprobar que GitHub Pages siga disponible por HTTPS;
5. revisar si el cambio exige una nueva verificación de Google.

## Próximos pasos

1. Revisar los requisitos del Centro de verificación de Google.
2. Decidir si se enviará la aplicación para verificación con los alcances actuales.
3. Tras la decisión, renovar la autorización OAuth local para sustituir el token que devuelve `invalid_grant`.
4. Ejecutar una comprobación de autenticación sin envío.
5. Solicitar autorización separada antes de cualquier prueba real de envío de correo.

## Historial de configuración

### 28 de septiembre de 2026

- Se creó este repositorio público independiente del Worker.
- Se publicaron la página principal y la política de privacidad mediante GitHub Pages.
- Se habilitaron y verificaron las APIs de Sheets, Drive y Gmail.
- Se configuraron los alcances `spreadsheets`, `drive.file` y `gmail.send`.
- Se guardaron las URLs públicas y el dominio autorizado en Google Auth Platform.
- La aplicación pasó a estado **En producción**.
- Google indicó que la aplicación requiere verificación; la solicitud quedó pendiente y no se envió.
- La prueba local de autenticación, sin enviar correo, informó `invalid_grant`.

## Soporte

Para consultas de privacidad o solicitudes relacionadas con este sitio, abre una incidencia en [GitHub Issues](https://github.com/enzofabriciolese/ai-execution-gateway-site/issues). No publiques credenciales, tokens ni datos sensibles.

---

© 2026 AI Execution Gateway
