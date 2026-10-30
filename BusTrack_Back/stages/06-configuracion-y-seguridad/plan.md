# plan.md — Etapa 06: Configuración y seguridad

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Depende de DEC-002 y DEC-003  
**Última actualización:** 2026-10-29  
**Etapa:** 06  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa no autoriza introducir secretos en el repositorio ni crear recursos en Azure.

---

## 1. Objetivo

Establecer la gestión de configuración por entorno, la gestión de secretos y el mecanismo base de autenticación y autorización.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 05 completada; DEC-002; DEC-003 |
| Bloqueos | DEC-002 (autenticación), DEC-003 (gestión de secretos) |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Configurar la jerarquía de configuración por entorno (`appsettings.json`, variables de entorno, gestión de secretos).
2. Integrar el servicio de gestión de secretos seleccionado en DEC-003.
3. Implementar el mecanismo de autenticación seleccionado en DEC-002.
4. Configurar la autorización base.
5. Verificar que ningún secreto se almacene en el repositorio.
6. Configurar HTTPS y redirección.

## 4. Entregables esperados

- Configuración por entorno implementada y probada.
- Secretos gestionados fuera del repositorio.
- Autenticación y autorización base funcionando.

## 5. Criterios de salida

- Ningún endpoint devuelve datos sin autenticación (salvo endpoints públicos explícitos).
- Los secretos se leen de variables de entorno o del servicio de secretos.
- HTTPS está configurado y funciona.
- AC-ARCH-06 y AC-ARCH-11 verificados.

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 6 |
| Tareas | `TAREA-015`, `TAREA-016`, `TAREA-017` |
| Decisiones relacionadas | DEC-002, DEC-003 |
| Criterios de aceptación | AC-ARCH-06, AC-ARCH-11 |

---

*La selección del mecanismo de autenticación y del servicio de secretos no se asume en esta etapa.*
