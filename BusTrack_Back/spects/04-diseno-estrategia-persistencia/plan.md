# plan.md — Etapa 04: Diseño de la estrategia de persistencia

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Depende de la Etapa 03 (DEC-001)  
**Última actualización:** 2026-10-29  
**Etapa:** 04  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa diseña la persistencia. No autoriza implementar repositorios ni crear recursos en Azure.

---

## 1. Objetivo

Diseñar el modelo de datos NoSQL y la estrategia de acceso a datos para el dominio de BusTrack.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 02 aprobada; Etapa 03 completada (DEC-001 resuelta); especificaciones funcionales parciales |
| Decisión bloqueante | DEC-001 — Proveedor NoSQL |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Diseñar el modelo de documentos NoSQL para las entidades del dominio.
2. Definir la estrategia de particionado según el proveedor seleccionado.
3. Definir la estrategia de indexado.
4. Diseñar las interfaces de repositorio del dominio.
5. Documentar los patrones de acceso a datos esperados.
6. Obtener aprobación del diseño de persistencia.

## 4. Entregables esperados

- Diseño del modelo de documentos NoSQL.
- Interfaces de repositorio del dominio diseñadas y aprobadas.
- Estrategia de particionado e indexado documentada.

## 5. Criterios de salida

- El modelo de datos es coherente con el proveedor seleccionado.
- Las interfaces de repositorio están definidas para las entidades principales del dominio.
- El diseño ha sido revisado y aprobado.
- Las interfaces no exponen tipos ni conceptos específicos del proveedor.

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 4 |
| Tareas | `TAREA-008`, `TAREA-009` |
| Decisiones relacionadas | DEC-001 |
| Criterios de aceptación | AC-ARCH-09 |

---

*El diseño de persistencia no puede iniciarse mientras DEC-001 permanezca pendiente.*
