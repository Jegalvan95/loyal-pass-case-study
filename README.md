# Loyal_Pass — Caso de estudio

Sistema de tarjetas de lealtad digitales para múltiples negocios.

**Estado:** versión 1.3.0 en desarrollo. Este caso de estudio describe el proyecto a partir de su código y documentación; no acredita una operación en producción.

## Problema y enfoque

El proyecto aborda el registro de clientes y el seguimiento de programas de lealtad. La estructura separa negocios, sucursales y empleados, y vincula cada tarjeta a un negocio.

El flujo contempla registro, identificación por QR o código manual, acumulación de visitas y gestión de recompensas.

## Tecnologías del proyecto

| Capa | Tecnologías |
| --- | --- |
| Interfaz | HTML, CSS y JavaScript |
| API | TypeScript y funciones serverless para Vercel |
| Base de datos | Supabase/PostgreSQL y migraciones SQL |
| Pruebas | Vitest |
| Herramientas | Node.js y Vercel CLI |

## Estructura

- `public/`: interfaz de clientes y empleados.
- `api/`: endpoints de registro, consulta, visitas, recompensas y recuperación.
- `lib/`: validación, autenticación, acceso a datos y utilidades.
- `supabase/migrations/`: estructura de datos y evolución de reglas.
- `tests/`: pruebas de lógica y contratos.

## Decisiones observables

- Separación de información mediante `business_id`.
- Validación de entradas en la API.
- Credenciales de servicio utilizadas desde el backend.
- Migraciones SQL para conservar la evolución del esquema.
- Reglas de vigencia y visitas basadas en el calendario del negocio.

## Validación y límites

La documentación del proyecto reporta conexión y flujos básicos comprobados en Supabase. Contiene comandos para pruebas y compilación:

```powershell
npm test -- --maxWorkers=1
npm run build
```

Las pruebas no se ejecutaron como parte de la preparación de este caso de estudio. Su presencia no confirma que estén pasando actualmente.

El README mantiene pendientes de validación real de canje, repetición y vencimiento; procesamiento de notificaciones; integración Wallet; y comprobaciones antes de producción.

## Disponibilidad

El código permanece en un repositorio privado. Este documento presenta el alcance técnico sin publicar credenciales, registros de clientes ni configuraciones específicas de negocios.
