# plan.md — Etapa 07: Estrategia de pruebas

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Depende de la Etapa 05 y de DEC-008 y DEC-009  
**Última actualización:** 2026-10-29  
**Etapa:** 07  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa define la infraestructura de pruebas. Las herramientas y el umbral de cobertura están pendientes de decisión.

---

## 1. Objetivo

Establecer la infraestructura de pruebas y crear las pruebas iniciales de la arquitectura base.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 05 completada; DEC-008; DEC-009 |
| Bloqueos | DEC-008 (cobertura mínima), DEC-009 (herramientas de prueba) |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Seleccionar las herramientas de prueba (DEC-009).
2. Crear los proyectos de prueba correspondientes.
3. Implementar pruebas unitarias para la lógica de dominio y aplicación.
4. Implementar pruebas de integración para los endpoints de la API base.
5. Validar que las pruebas se ejecutan correctamente en el entorno local.
6. Documentar la estrategia de pruebas adoptada.

## 4. Entregables esperados

- Proyectos de prueba creados.
- Pruebas unitarias e integración de la arquitectura base.
- Documentación de la estrategia de pruebas adoptada.

## 5. Criterios de salida

- Las pruebas unitarias de dominio y aplicación pasan sin infraestructura real.
- Las pruebas de integración validan los criterios de aceptación de arquitectura.
- El umbral de cobertura definido en DEC-008 se cumple.

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 7 |
| Tareas | `TAREA-018` |
| Decisiones relacionadas | DEC-008, DEC-009 |
| Criterios de aceptación | AC-ARCH-10, AC-ARCH-04 |

---

*No se asume ninguna herramienta de prueba (xUnit, NUnit, MSTest) hasta que DEC-009 esté confirmada.*
