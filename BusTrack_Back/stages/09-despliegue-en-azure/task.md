# task.md — Etapa 09: Preparación del despliegue en Azure

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 09  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-020 | Primer despliegue de la API base en Azure | BLOQUEADA |

---

### TAREA-020

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-020 |
| **Título** | Primer despliegue de la API base en Azure |
| **Etapa** | 09 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-019 completada y DEC-007 resuelta |
| **Referencia** | `plan.md` Fase 9 |

**Descripción:**  
Configurar el despliegue en Azure y realizar el primer despliegue de la API base en el entorno de desarrollo o staging. Verificar el funcionamiento del endpoint `/health` en el entorno desplegado.

**Objetivo:**  
Validar que el backend puede desplegarse correctamente en Azure.

**Dependencias:**  
- TAREA-019 completada.
- DEC-007 resuelta.
- Suscripción y recursos de Azure disponibles.

**Criterios de aceptación:**
- [ ] La API está desplegada en Azure.
- [ ] `GET /health` retorna 200 en el entorno de Azure.
- [ ] Los secretos se gestionan mediante el servicio seleccionado.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
