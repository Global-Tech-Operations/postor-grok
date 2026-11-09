# Postor para Grok Build

Conecta tu cuenta existente de Postor para buscar licitaciones públicas de México,
investigar compradores y proveedores, revisar documentos originales y organizar
proyectos, tareas y carpetas. La cobertura de contratación es México.

**Requiere una cuenta aprobada de Postor con membresía activa.** Instalar el plugin
no crea una cuenta ni abre el acceso a la plataforma privada. Las funciones dependen
del plan, rol y permisos de la empresa conectada.

## Instalación directa

```sh
grok plugin install https://github.com/VisionSocial/postor-grok.git --trust
```

Abre `/mcps`, selecciona Postor e inicia la autorización con `i`. Inicia sesión
únicamente en Postor. Autoriza solo los permisos necesarios y vuelve a Grok.
La conexión solicita solo lectura de forma predeterminada.
La conexión usa OAuth con PKCE; no pegues contraseñas, tokens ni claves en el chat.

La incorporación al catálogo oficial de xAI está pendiente de revisión.
Esta integración es para **Grok Build**, no una publicación en el chat general de grok.com.

## Permisos de escritura opcionales

Para proyectos, tareas o carpetas, solicita explícitamente los permisos necesarios
mediante la configuración nativa de Grok (`~/.grok/config.toml`), actualiza `/mcps`
y vuelve a autorizar Postor. La selección final se confirma en Postor.

```toml
[mcp_servers.postor]
url = "https://api.postor.com.mx/api/plugin/mcp"
oauth_client_id = "https://api.postor.com.mx/api/plugin/grok-client.json"
oauth_scopes = ["postor:read", "postor:write"]
```

Agrega `postor:delete` solo si necesitas eliminar carpetas. No se solicita acceso
de colaboración. Una membresía no sustituye la autorización de estos permisos.

## Ejemplos

- «Busca licitaciones vigentes de alimentos en Ciudad de México».
- «Investiga los compradores y contratos de esta empresa en Red».
- «Revisa el anexo técnico de esta licitación y cita las páginas».
- «Crea un proyecto para esta licitación y una tarea para revisar las bases».

Responde en el idioma del usuario; la documentación principal está en español.
Las 32 herramientas publicadas usan los permisos del usuario. Las escrituras y
eliminaciones requieren autorización independiente. No se realizan compras,
pagos, firmas ni presentación de propuestas ante autoridades. El análisis de
archivos depende de las capacidades del host; el plugin no inicia OCR ni trabajos
autónomos de análisis de Postor.

## Datos, red y permisos

- MCP: `https://api.postor.com.mx/api/plugin/mcp`.
- OAuth: descubrimiento y autorización en `api.postor.com.mx`; inicio de sesión y
  consentimiento en `app.postor.com.mx`; retorno local `http://127.0.0.1:<puerto>/callback`.
- Cliente público registrado: `https://api.postor.com.mx/api/plugin/grok-client.json`.
- Credenciales: solo la autorización OAuth del usuario. El paquete no incluye secretos.
- Grok guarda los tokens en su almacén local de credenciales. Los resultados
  solicitados se comparten con el proveedor de Grok según su política y tus ajustes.
- Los originales públicos pueden descargarse desde URLs temporales del almacenamiento
  de Postor devueltas por las herramientas. No se exportan archivos privados de Almacén.
- Sin scripts de instalación, hooks, telemetría ni ejecución local incluida en el paquete.

[Privacidad](https://api.postor.com.mx/api/plugin/privacy) ·
[Términos](https://postor.com.mx/terminos) ·
[Soporte](https://api.postor.com.mx/api/plugin/support) ·
[Revocar conexiones](https://app.postor.com.mx/conexiones/chatgpt)

## English

Official Postor integration for Grok Build, maintained by Global Tech Operations,
LLC. Search Mexican public tenders, research awards and companies, and manage
projects, tasks and folders. An existing approved Postor account with an active
membership is required. Installation does not grant platform access. OAuth, role,
organization, plan and scope checks apply to every operation.

## License

See [LICENSE](LICENSE). Permission covers distribution and use of this plugin
package; it does not expose or license the private Postor platform or its datasets.
