# Criterios de aceptación y evidencia

## Etapa 0: base y seguridad
- [ ] `base/ERP_BEIKYGROUP_ORIGINAL.msapp` permanece SHA256 idéntico al manifiesto.
- [ ] El `.msapp` original abre en Studio.
- [ ] Existe aplicación aparte llamada `BEIKYGROUP ERP 2.0 - DESARROLLO`, no modifica producción.
- [ ] Ninguna contraseña o API key se almacena en repositorio.

## Etapa 1: UI
- [ ] Portal con 7 módulos y solo CRM habilitado.
- [ ] Logotipo correcto, colores y Montserrat.
- [ ] Sin scroll horizontal en 390px, 820px y 1440px; navegación y formularios visibles.
- [ ] Los módulos inactivos no producen pantallas de error.

## Etapa 2: CRM y registros
- [ ] RUC 11 dígitos, se evita duplicidad y el flujo recupera datos después de guardar.
- [ ] Contacto asociado a cliente, al guardar se queda en Contactos.
- [ ] Múltiples oportunidades por cliente; lookups referencian IDs correctos.
- [ ] Clientes/servicios con filtro dentro del mismo combo.
- [ ] Listado de todos visible a 2 ejecutivos distintos.
- [ ] Solo oportunidades propias abiertas editables, salvo administrador; cerradas nunca editables.
- [ ] Nuevo/Editar limpia campos solo cuando Save retorna éxito.
- [ ] Cambio Ganado: flujo SOLPED existente ejecuta una vez y almacena código; avisos sin duplicidad.

## Etapa 3: publicación
- [ ] Compilación/paquete por herramientas Microsoft sin editar JSON internos.
- [ ] Importación real a Power Apps Studio; registrar fecha y evidencia.
- [ ] Pruebas de lectura y escritura en un entorno aprobado. No pruebas de producción sin autorización.
- [ ] Informe de errores, dependencia de licencias y estado de seguridad por datos.
- [ ] Solo considerar completado cuando la aplicación se abre y usa desde Microsoft, no porque pase un parser ZIP.
