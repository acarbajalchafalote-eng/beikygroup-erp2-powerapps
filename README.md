# BEIKYGROUP ERP 2.0 — Proyecto para Codex Web

Este repositorio **privado** contiene el punto de partida autorizado: un `.msapp` original, su código fuente `*.pa.yaml` de solo referencia, una maqueta HTML **no productiva**, el logotipo oficial y especificaciones de negocio.

**ATENCIÓN**: no es un `.msapp` nuevo listo para abrir. El objetivo de Codex es construir una versión validable por Power Apps Studio, sin modificar la app original ni datos reales. **No subir el repositorio a una cuenta pública**.

1. Leer `AGENTS.md` y `docs/ESPECIFICACION_FUNCIONAL.md`.
2. Ejecutar `python tests/verificar_base.py`.
3. Analizar el paquete original, sus conectores y los `*.pa.yaml`.
4. Utilizar herramientas **oficiales** de Power Platform donde estén disponibles. Crear un *candidato* `.msapp` en `dist/` sin tocar `base/`.
5. No declarar finalizado sin importar y probar en Power Apps Studio; si careces de permisos de Microsoft, informa el bloqueo concreto y qué autorización se necesita.

El archivo HTML `referencia/Prototipo_UX_CRM_V10_NO_PRODUCTIVO.html` es exclusivamente una **referencia de navegación y UX**, sin acceso real a SUNAT, Microsoft ni SharePoint.

## Documentos

- `AGENTS.md`: reglas de trabajo para Codex.
- `docs/ESPECIFICACION_FUNCIONAL.md`: decisiones confirmadas con el usuario.
- `docs/INTEGRACION_SHAREPOINT_FLUJOS.md`: conexiones, datos y disparadores.
- `docs/PLAN_DE_VALIDACION.md`: pruebas y criterios de aceptación.
- `docs/INSTRUCCION_PARA_CODEX_WEB.md`: tarea lista para copiar.

## Documentación oficial

- https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/power-apps-yaml
- https://learn.microsoft.com/en-us/power-platform/developer/cli/reference/canvas
- https://learn.microsoft.com/en-us/power-platform/developer/howto/install-cli-net-tool
- https://learn.microsoft.com/en-us/power-platform/alm/git-integration/canvas-apps-git-integration
