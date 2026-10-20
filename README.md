# Loyal_Pass — Caso de estudio

Sistema de tarjetas de lealtad digitales para múltiples negocios.

**Estado:** versión 1.4.0 en desarrollo. Este caso de estudio describe el proyecto a partir de su código y documentación; no acredita una operación en producción.

**Actualización documental:** 19 de octubre de 2026.

## Problema y enfoque

El proyecto aborda el registro de clientes y el seguimiento de programas de lealtad. La estructura separa negocios, sucursales y empleados, y vincula cada tarjeta a un negocio.

El flujo contempla registro, identificación por QR o código manual, acumulación de visitas y gestión de recompensas. La versión 1.4.0 incorpora administración centralizada e historial de operaciones por negocio.

## Avances de la versión 1.4.0

- **Administración global:** panel para crear y configurar negocios y administrar empleados locales desde una identidad independiente de los roles de cada negocio.
- **Gestión de empleados:** creación, cambios de permisos, activación/desactivación y restablecimiento de PIN, conservando el historial de operaciones.
- **Historial por negocio:** consulta de visitas y canjes con cliente, encargado, sucursal y fecha/hora comercial; filtros por fecha, encargado y tipo de operación, con paginación de 25 registros.
- **Permisos por rol:** empleados registran visitas; encargados y administradores locales pueden además canjear y consultar el historial. La administración global conserva las reglas de negocio y el aislamiento de datos.
- **Auditoría administrativa:** registro transaccional de cambios en negocios y empleados. Es independiente del historial de visitas y canjes y se consulta desde la base de datos.

El proyecto conserva las rutas y reglas existentes de edad mínima, consentimientos, duplicados, límite diario y canje.

## Tecnologías del proyecto

| Capa | Tecnologías |
| --- | --- |
| Interfaz | HTML, CSS y JavaScript |
| API | TypeScript y funciones serverless para Vercel |
| Base de datos | Supabase/PostgreSQL y migraciones SQL |
| Pruebas | Vitest |
| Herramientas | Node.js y Vercel CLI |

## Estructura

- `public/`: interfaces de clientes, empleados y administración global.
- `api/`: endpoints de registro, consulta, visitas, recompensas, recuperación, historial y administración.
- `lib/`: validación, autenticación, acceso a datos y utilidades.
- `supabase/migrations/`: estructura de datos y evolución de reglas.
- `tests/`: pruebas de lógica y contratos.

## Decisiones observables

- Separación de información mediante `business_id`.
- Validación de entradas en la API.
- Credenciales de servicio utilizadas desde el backend.
- Migraciones SQL para conservar la evolución del esquema.
- Reglas de vigencia y visitas basadas en el calendario del negocio.
- Autorización comprobada en el servidor para el historial y las operaciones administrativas.
- Validación de filtros y rechazo de fechas futuras en el historial.
- Identidad global separada de empleados y administradores locales.
- Registro de cambios administrativos sin guardar PIN en texto plano en la auditoría.

## Validación y límites

La documentación de v1.4.0 reporta funcionamiento local del panel y los permisos confirmado por el usuario, y escenarios aislados de canje y repetición. Esta revisión comprobó los archivos del repositorio; no verificó un despliegue ni una base de datos en producción.

El repositorio incluye pruebas de validación administrativa, autorización de API, identidad global e historial, además de las pruebas existentes. Algunas verificaciones usan dependencias simuladas o inspeccionan contratos SQL; no equivalen a una prueba integral contra Supabase.

Comandos documentados para pruebas y compilación:

```powershell
npm test -- --maxWorkers=1
npm run build
```

Las pruebas no se ejecutaron como parte de la preparación de este caso de estudio. Su presencia no confirma que estén pasando actualmente.

Siguen pendientes la prueba real del reinicio por vencimiento, el procesamiento de notificaciones, la validación de Wallet en dispositivos y las comprobaciones de integración y seguridad antes de producción. El acceso global por PIN no incorpora MFA; la documentación recomienda añadirlo junto con sesiones de administración dedicadas antes de operar con datos reales en producción.

## Disponibilidad

El código permanece en un repositorio privado. Este documento presenta el alcance técnico sin publicar credenciales, registros de clientes ni configuraciones específicas de negocios.
