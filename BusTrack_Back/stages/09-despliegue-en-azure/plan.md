# plan.md — Etapa 09: Preparación del despliegue en Azure

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Depende de la Etapa 08 y de DEC-007  
**Última actualización:** 2026-10-29  
**Etapa:** 09  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa prepara el despliegue. Requiere una cuenta y suscripción de Azure disponibles, y aprobación explícita.

---

## 1. Objetivo

Preparar la configuración e infraestructura necesaria para desplegar el backend en Azure.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 08 completada; DEC-007; cuenta y suscripción de Azure |
| Bloqueo | DEC-007 — Servicio de alojamiento en Azure |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Seleccionar el servicio de alojamiento en Azure (DEC-007).
2. Definir la configuración de despliegue para cada entorno.
3. Configurar el pipeline de CD (entrega continua).
4. Verificar la correcta gestión de secretos en el entorno de Azure.
5. Realizar el primer despliegue de la API base en el entorno de desarrollo/staging.
6. Verificar el endpoint `/health` en el entorno desplegado.

## 4. Entregables esperados

- API base desplegada en Azure (entorno de desarrollo o staging).
- Pipeline de CD configurado.
- Documentación del proceso de despliegue.

## 5. Criterios de salida

- La API responde correctamente en el entorno de Azure.
- El endpoint `/health` retorna 200.
- Los secretos se gestionan mediante el servicio seleccionado (no están en el código).

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 9 |
| Tareas | `TAREA-020` |
| Decisiones relacionadas | DEC-007, DEC-003 |
| Criterios de aceptación | AC-ARCH-07, AC-ARCH-11 |

---

*No se asume ningún servicio de alojamiento hasta que DEC-007 esté confirmada.*
