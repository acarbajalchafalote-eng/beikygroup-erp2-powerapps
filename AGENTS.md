# INSTRUCCIONES PARA CODEX — BEIKYGROUP ERP

## Prioridad y seguridad
- Trabaja con una **copia** de `base/ERP_BEIKYGROUP_ORIGINAL.msapp`; prohíbido sobrescribirlo.
- No uses `BEIKYGROUP_ERP_POWERAPPS_V11_CANDIDATO.msapp` ni ningún paquete modificado manualmente: Microsoft lo rechazó.
- No introduzcas contraseñas, API keys ni tokens en el repositorio. No solicites al usuario que los pegue en el chat; usa autenticación OAuth o mecanismos Microsoft autorizados.
- No hacer cambios reales en SharePoint ni ejecutar flujos hasta autorización explícita del usuario. No enviar correos de prueba a la organización.
- No modificar listas/columnas, esquema SUNAT ni numeración SOLPED durante esta iteración.
- Nunca generes un msapp manipulando `Controls/*.json`, `Header.json`, `References/*.json` con ZIP manual. Usa el flujo soportado en el momento por Microsoft (Studio / ALM / pac). Los comandos `pac canvas pack/unpack` están marcados deprecated; úsalos solamente si la versión actual y el modo SourceCode aceptan el original, y valida el resultado en Studio.
- La sola validez del ZIP no equivale a un `.msapp` importable.

## Obligaciones
1. Analiza las 6 pantallas de origen: Inicio, CRM, Ventas, Gastos, Facturación, Cobranzas, y conserva los componentes funcionales.
2. Crear portal responsivo en web/iPad/celular con siete tarjetas; no incluir Proyectos/Operaciones. Solo Comercial y CRM habilitado.
3. Crear/ajustar Clientes B2B, Contactos, Nueva oportunidad, Listado de oportunidades y SOLPED. B2C marcado en UI como pendiente sin listas.
4. El cliente B2B se registra introduciendo solo RUC; búsqueda de duplicado por RUC; la información SUNAT llega asíncronamente por flujo existente después del alta de lista.
5. No crea SOLPED desde la aplicación: cambia Estado a Ganado y el flujo existente se encarga del código y la notificación. No inventar nuevos endpoints, listas o flujos.
6. Cada cliente admite múltiples contactos y oportunidades, identificados por sus propios IDs.
7. Todos ven todas las oportunidades; solo el responsable asignado puede editar abiertas, administrador puede editar todas las abiertas; Ganada/Perdida son solo lectura. Una validación UI NO sustituye permisos de SharePoint; no afirmar que sea seguro antes de imponerlos en fuente.
8. Nuevo lead: Cliente, Contacto, Responsable vacíos al inicio; tras guardar/editar con éxito, limpiar esos campos y los demás sin perder registros.
9. Diseñar combobox con búsqueda en la **misma casilla** para clientes y servicios. El tipo de servicio procede del Lookup `Tipo_Servicio_BeikyGroup` (44 tipos observados, no lista plana fija).
10. Manejar correctamente opciones Choice / Lookup / Person / fechas, tipos internos, delegación y Refresh.
11. Obtener confirmación del usuario antes de cualquier cambio que afecte datos o publicación general.
12. Ejecutar pruebas con usuarios/identidades de prueba y registrar evidencia real de aceptación Studio/importación.

## Entrega honesta
- Entregar ruta del archivo fuente y del paquete de importación SOLAMENTE si Power Apps Studio lo abrió correctamente.
- Enumerar pruebas pasadas, fallidas y no ejecutadas, sin presentarlas como completadas.
- Si no tienes sesión Microsoft, no inventar URL de app publicada ni afirmar que funciona: dejar un PR y el bloqueo exacto.
