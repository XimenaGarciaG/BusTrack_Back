# plan.md — Etapa 02: Diseño de la estructura de la solución .NET

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Etapa 01 y resolución de DEC-005  
**Última actualización:** 2026-10-29  
**Etapa:** 02  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa es de diseño documental. No autoriza crear proyectos ni archivos de código.

---

## 1. Objetivo

Definir y aprobar la organización de proyectos, namespaces y capas del monolito modular antes de escribir código.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 01 aprobada; DEC-005 resuelta |
| Decisión bloqueante para avanzar | DEC-001 — Selección del proveedor NoSQL (para el diseño de infraestructura) |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Proponer la estructura de proyectos .NET (nombres de proyectos y referencias entre proyectos).
2. Definir las convenciones de namespaces y organización de carpetas.
3. Proponer las interfaces clave del dominio (repositorios, servicios).
4. Definir los modelos de configuración (_options pattern_).
5. Documentar la estructura propuesta en un documento de diseño.
6. Obtener aprobación de la estructura antes de crear archivos.

## 4. Entregables esperados

- Documento de diseño de la estructura de la solución .NET.
- Diagrama de dependencias entre proyectos.
- Convenciones de nomenclatura aprobadas.

## 5. Criterios de salida

- La estructura de proyectos ha sido aprobada.
- No existen dependencias circulares entre capas en el diseño.
- Las convenciones de nomenclatura están documentadas.
- El diseño respeta la inversión de dependencias (`Domain` no depende de `Infrastructure`).

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 2 |
| Tareas | `TAREA-004`, `TAREA-005` |
| Decisiones relacionadas | DEC-005, DEC-001 |
| Criterios de aceptación | AC-ARCH-01, AC-ARCH-02, AC-ARCH-09 |

---

*Esta etapa no autoriza el inicio de la Etapa 05 ni la creación de archivos de código.*
