# Requerimientos aprobados — BeikyGroup ERP 2.0

## Identidad
Manual Corporativo 2025. Montserrat (normal, Medium, SemiBold, Bold), logo original sin cambios, colores #0090D7, #000143, #0E3192, #CCF4FF, #E5E0FF. Fondo blanco, alto contraste. Usar controles responsivos para 360–430 px (teléfono), 768–1024 px (iPad), >1200 px (desktop). **Nunca** deformar logo.

## Portal
Tarjetas: Comercial y CRM (única activa), Logística, Finanzas y Administración, Recursos Humanos, Marketing, Reportes / BI, Configuración. Proyectos y Operaciones **NO** aparece: ya existe app independiente. No agregar submódulos de otros departamentos.

## Comercial y CRM

### Clientes B2B
- Selector por razón social/RUC para clientes existentes en SharePoint, búsqueda en la casilla.
- Alta solo por RUC de 11 dígitos. Antes de guardar, validar formato y duplicados por RUC. Se crea elemento en `Clientes BeikyGroup` para que el flujo `Clientes - Autocompletar RUC` se dispare; **no duplicar consulta HTTP en Power Apps**.
- Mostrar estado de consulta y refrescar hasta datos completos o error/timeout claro. No fingir consulta completada ni guardar razón social ficticia.
- Después de guardar/validar, continuar a Contactos o volver a oportunidad.

### Contactos
- Usar `Contacto_Cliente`, vinculada a `Clientes BeikyGroup` por Lookup `ClienteLookupId`.
- Crear contacto no debe volver al portal. Permanece en Contactos mostrando confirmación y posible acción 'Crear oportunidad' con contexto.
- Arreglar valores de email/celular indefinidos y no inventar propiedades.

### Oportunidades
- Una empresa admite múltiples oportunidades, cada una por ID de CRM distinto.
- Descripción identifica la oportunidad; no pedir nombre de oportunidad duplicado.
- Cliente y Contacto Lookup; Responsable asignado sin predeterminar; Tipo de servicio Lookup; Fuente Choice; Estado Choice; monto y fecha estimada.
- Los combobox de Cliente y Servicio filtran directamente al escribir, y el contacto se filtra por cliente.
- Estado inicial Abierta si existe como opción real; reconciliar con opciones Choice de SharePoint antes de hacer Patch; no escribir valores inexistentes.
- Todos los miembros comerciales ven todas las oportunidades. Solo responsable edita abiertas; administrador edita cualquiera abierta; Ganada/Perdida se bloquean (incluido administrador).
- Al guardar crear o editar, limpiar cliente/contacto/responsable y todos los campos. Edición guardada conserva datos correctos.
- Registro nuevo activa flujo `CRM – Aviso Nuevo Lead` por SharePoint; no enviar segundo correo desde app.
- Cambio a Ganado activa `CRM - Aviso Ganado + SOLPED`, que crea y guarda el código SOLPED en el CRM; no regenerar al modificar otros campos ni crear código desde app.

### SOLPED
- Mostrar código guardado por SharePoint tras ejecución del flujo, con mensaje Pendiente/Generada/Error.
- Numeración existente `SOL-YYYY-[6 caracteres de GUID]` no cambiar sin analizar dependencias (OS/OC/SALES, histórico).

### B2C
- Ruta independiente visual, no crear datos ni lista B2C nueva hasta aprobación. Documento DNI/nombres/apellidos solo cuando el esquema y validación estén acordados.

## Usuarios
Administrador: cuenta efectiva de Ángel Carbajal (VALIDAR UPN EN MICROSOFT, pantallas de conversaciones mostraron dominios inconsistentes).
Equipo citado: Álvaro, Katherine, Lesly, Yezilu, Natalia. Validar sus identidades corporativas y los campos Persona en SharePoint con tenant/Entra antes de cualquier seguridad definitiva. No usar selector de usuario demo como seguridad productiva.
