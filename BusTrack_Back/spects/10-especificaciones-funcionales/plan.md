# plan.md — Etapa 10: Incorporación de especificaciones funcionales

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Requiere las Etapas 01 a 09 completadas  
**Última actualización:** 2026-10-29  
**Etapa:** 10  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa agrupa las funcionalidades de negocio. Cada funcionalidad requiere su propia especificación aprobada antes de implementarse.

---

## 1. Objetivo

Diseñar, especificar e implementar las funcionalidades del sistema en iteraciones, siguiendo la metodología SDD.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapas 01 a 09 completadas; especificaciones funcionales aprobadas |
| Bloqueo | Requisitos funcionales no recibidos ni aprobados |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas (por cada funcionalidad)

1. Recibir y revisar el requisito funcional.
2. Crear o actualizar la especificación funcional en un `spec-{módulo}.md`.
3. Actualizar `memoria.md` con las decisiones de diseño.
4. Obtener aprobación de la especificación.
5. Crear o actualizar las tareas en `task.md`.
6. Implementar la funcionalidad siguiendo la especificación aprobada.
7. Crear pruebas automatizadas.
8. Verificar contra los criterios de aceptación.
9. Actualizar la documentación.

## 4. Entregables esperados

- Especificaciones funcionales por módulo.
- Implementación de funcionalidades según las especificaciones aprobadas.
- Pruebas automatizadas para cada funcionalidad.

## 5. Criterios de salida

- La funcionalidad implementada cumple todos los criterios de aceptación de su especificación.
- Las pruebas pasan en el pipeline de CI.
- La documentación está actualizada.

## 6. Funcionalidades fuera del alcance actual

Según `memoria.md` sección 6 y `constitution.md` sección 12, las siguientes funcionalidades solo pueden abordarse en esta etapa mediante especificaciones aprobadas:

- Registro, autenticación y recuperación de contraseña.
- Consulta y búsqueda de rutas, paradas, destinos y horarios.
- Cálculo y consulta de tarifas.
- Gestión de calificaciones y comentarios.
- Recomendaciones mediante inteligencia artificial.
- Detección de paradas mediante acelerómetro.
- Operaciones administrativas específicas.
- Integraciones con proveedores externos.

> El seguimiento GPS en tiempo real está fuera del alcance del sistema y no se especificará en esta etapa.

## 7. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 10 |
| Tareas | Aún no creadas (se definirán por funcionalidad) |
| Decisiones relacionadas | DEC-011 (paginación y filtrado) |
| Criterios de aceptación | Por funcionalidad |

---

*Las tareas de esta etapa se crearán cuando se reciban y aprueben los requisitos funcionales específicos.*
