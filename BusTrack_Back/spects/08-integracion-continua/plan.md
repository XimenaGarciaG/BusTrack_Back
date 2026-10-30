# plan.md — Etapa 08: Integración continua

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Depende de la Etapa 07 y de DEC-006  
**Última actualización:** 2026-10-29  
**Etapa:** 08  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa configura automatización. No autoriza desplegar en Azure.

---

## 1. Objetivo

Configurar el pipeline de CI/CD para la ejecución automática de pruebas y la validación de la calidad del código.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 07 completada; DEC-006; repositorio configurado (`.gitignore`, protección de ramas) |
| Bloqueo | DEC-006 — Herramienta de CI/CD |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Seleccionar la herramienta de CI/CD (DEC-006).
2. Crear el pipeline de integración continua.
3. Configurar la ejecución automática de pruebas en cada commit o pull request.
4. Configurar análisis de calidad de código (opcional en esta etapa).
5. Documentar el pipeline y su configuración.

## 4. Entregables esperados

- Pipeline de CI configurado y funcionando.
- Ejecución automática de pruebas verificada.
- Documentación del pipeline.

## 5. Criterios de salida

- El pipeline ejecuta las pruebas automáticamente y falla si alguna prueba no pasa.
- Ningún artefacto se genera si las pruebas fallan.
- La configuración no contiene secretos versionados.

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 8 |
| Tareas | `TAREA-019` |
| Decisiones relacionadas | DEC-006 |
| Criterios de aceptación | `spec.md` sección 14 |

---

*No se asume ninguna plataforma de CI/CD hasta que DEC-006 esté confirmada.*
