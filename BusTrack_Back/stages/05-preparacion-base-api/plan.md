# plan.md — Etapa 05: Preparación de la base de la API

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Depende de las Etapas 02 y 03 y de DEC-010  
**Última actualización:** 2026-10-29  
**Etapa:** 05  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa inicia la implementación técnica de la arquitectura base. Requiere aprobación explícita de las etapas previas.

---

## 1. Objetivo

Implementar la estructura base del proyecto .NET con las capas, la configuración de la API, el manejo de errores y los mecanismos base de observabilidad.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 02 (estructura aprobada); Etapa 03; DEC-005; DEC-010; DEC-004 o solución provisional |
| Bloqueos | DEC-010 (formato de errores), DEC-004 (logging) |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Crear la estructura de proyectos .NET aprobada en la Etapa 02.
2. Configurar el enrutamiento con versionado `/api/v1/`.
3. Implementar el middleware centralizado de manejo de errores.
4. Implementar el endpoint `/health` de verificación de salud.
5. Configurar el registro estructurado con `ILogger`.
6. Configurar OpenAPI para la documentación de la API.
7. Implementar la inyección de dependencias base.
8. Ejecutar las pruebas de los criterios de aceptación AC-ARCH-01 al AC-ARCH-12.

## 4. Entregables esperados

- Estructura de proyectos .NET creada.
- API base ejecutable con endpoint `/health` funcional.
- Middleware de errores implementado.
- Registro estructurado configurado.
- Pruebas de los criterios de aceptación de arquitectura base.

## 5. Criterios de salida

- Todos los criterios de aceptación AC-ARCH-01 al AC-ARCH-12 pasan.
- La API base compila y se ejecuta sin errores en el entorno de desarrollo.
- Los controladores no contienen lógica de negocio.

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 5 |
| Tareas | `TAREA-010` a `TAREA-014` |
| Decisiones relacionadas | DEC-005, DEC-010, DEC-004 |
| Criterios de aceptación | AC-ARCH-01 a AC-ARCH-12 |

---

*Esta etapa no autoriza desplegar en Azure ni implementar funcionalidades de negocio.*
