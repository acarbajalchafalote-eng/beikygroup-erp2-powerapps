# Fuentes reales y flujos existentes (inspección parcial, no escribir sin aprobación)

Sitio: `https://beikyperu.sharepoint.com/sites/ERPBEIKYGROUP`

| Lista | GUID observado | Función |
|---|---|---|
| CRM BeikyGroup | d6c213e2-4f5e-4fec-819f-03be30c82368 | oportunidades |
| Clientes BeikyGroup | 2305ac0b-f085-40d2-be3a-a80af28c1a47 | empresas / RUC |
| Contacto_Cliente | 3442d280-8500-4ce2-aafa-d4656fd20258 | contactos |
| Tipo_Servicio_BeikyGroup | b720c0b4-4076-4ff6-89e1-13269acf75e3 | catálogo 44 tipos / Lookup |
| SALES | 07972b12-6dfb-47ed-939e-19da13749543 | ventas, no alterar |
| SOLPED_INTERNA | 6ac5e38e-a57c-43a8-aa84-1a00943eec89 | lista distinta de SOLPED de CRM: no asumir que el flujo la escribe |

Campos observados en consultas a Graph (nombres internos/presentación según respuesta):
- CRM: `CLIENTELookupId`, `CONTACTOLookupId`, `ResponsableLookupId`, `Fuente`, `Descripcion`, `TIPO_x0020_DE_x0020_SERVICIOLookupId`, `MontoEstimado`, `Probabilidad`, `Estado`, `MotivoPerdido`, `SOLPED`, `COPIAASALES`.
- Cliente: `RUC`, `Title` (razón social), `DIRECCI_x00d3_N`, `CIUDAD`, `ESTADOSUNAT`, `CONDICIONSUNAT`, `DEPARTAMENTO`, `PROVINCIA`, `DISTRITO`.
- Contacto: `Title`, `Cargo`, `Email`, `Celular`, `ClienteLookupId`.
- Servicios: `Title` = texto del servicio; clave ID (1–44 observados).
- Fuente: valores vistos Referido, Web, WhatsApp, Llamada, Evento, Otro. Obtener Choices nativos del esquema, no asumir lista exhaustiva.
- Estado: valores vistos Perdido, Negociacion, Ganado; **el concepto de Abierta debe mapearse al estado realmente existente, sin inventarlo**.

## Flujos existentes confirmados por capturas

1. `Clientes - Autocompletar RUC`: SharePoint **al crear elemento** (lista Clientes BeikyGroup), HTTP GET, Actualizar elemento. Mapea `razonSocial`→`Title`, `nombreComercial`, `direccion`, `provincia`, `estado`, `condicion`, `departamento`, `distrito`. No interrumpir el flujo.
2. `CRM – Aviso Nuevo Lead`: existe/habilitado (definición interna no aportada). Se debe auditar su disparador antes de asumir que una actualización podría reenviar avisos.
3. `CRM - Aviso Ganado + SOLPED`: SharePoint **al crear o modificar elemento**, condición AND `Estado Value == Ganado` y `SOLPED == null` visible (hay tercera fila vacía, revisar), luego Redactar, SOLPED Final, Actualizar elemento CRM y Enviar correo.
   - Redactar visto: `concat('SOL-',formatDateTime(utcNow(),'yyyy'),'-',substring(guid(),0,6))` (captura con funciones traducidas visualmente).
   - SOLPED Final: `concat(...)` visible pero la expresión completa no fue aportada; NO afirmar conocerla.
   - Actualizar elemento también establece `Estado=Ganado`, `SOLPED=resultado` y `Probabilidad=30%` (posible inconsistencia a evaluar), preserva Descripcion y MontoEstimado.

## Reglas de escritura
- Usar `SubmitForm`/`Patch` de Power Fx desde Power Apps para CRUD, conservando los tipos SharePoint.
- Actualización por ID SharePoint y campos Lookup/Person/Choice correctos. Nunca duplicar la empresa o contacto para otra oportunidad.
- No crear una segunda SOLPED en app, y no sobreescribir el campo SOLPED por formulario al editar.
- Protección UI y lista/ítem en servidor son cosas distintas. Si no hay permisos de ítem reales, documentar expresamente el riesgo.
