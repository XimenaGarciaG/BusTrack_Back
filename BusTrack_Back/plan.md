# plan.md — Plan de Implementación del Backend de BusTrack

**Versión:** 1.0.0  
**Estado:** Borrador — Pendiente de revisión y aprobación  
**Última actualización:** 2026-10-28  
**Referencia normativa:** [`constitution.md`](./constitution.md) | [`spec.md`](./spec.md)

> **Importante:** Este documento describe las fases de implementación previstas. Ninguna actividad descrita aquí ha sido ejecutada. Este plan no autoriza el inicio de ninguna fase. Cada fase debe ser aprobada antes de comenzarse.

---

## Convenciones del plan

| Símbolo | Significado |
|---------|-------------|
| 🔴 BLOQUEADA | No puede iniciarse; depende de una decisión pendiente |
| 🟡 PENDIENTE | Puede iniciarse una vez aprobada la fase anterior |
| 🟢 ACTIVA | En curso (ninguna fase está activa actualmente) |
| ✅ COMPLETADA | Finalizada con evidencia |

---

## Fase 1 — Validación de la documentación SDD

**Objetivo:** Garantizar que la documentación SDD generada es coherente, completa y aprobada antes de iniciar cualquier implementación.

**Estado:** 🟡 PENDIENTE de revisión y aprobación

### Actividades previstas

1. Revisión de coherencia interna entre `constitution.md`, `AGENTS.md`, `memoria.md`, `spec.md`, `plan.md` y `task.md`.
2. Revisión de coherencia por parte del responsable del proyecto (profesor).
3. Identificación y resolución de contradicciones o vacíos en la documentación.
4. Aprobación formal de la especificación arquitectónica (`spec.md`).
5. Actualización de `memoria.md` con el resultado de la revisión.

### Dependencias

- Ninguna (esta es la primera fase).

### Entregables esperados

- Documentos SDD revisados y aprobados.
- Registro de decisiones actualizado en `memoria.md`.
- Lista de elementos pendientes de resolución antes de la Fase 2.

### Criterios de salida

- Los documentos `constitution.md`, `spec.md`, `plan.md` y `task.md` han sido revisados y no contienen contradicciones detectadas.
- La especificación (`spec.md`) ha sido aprobada formalmente.
- Todas las decisiones críticas para la Fase 2 están resueltas o documentadas como bloqueos aceptados.

### Decisiones que bloquean el avance a la Fase 2

- DEC-005: Estructura definitiva de capas de la solución .NET.

---

## Fase 2 — Diseño de la estructura de la solución .NET

**Objetivo:** Definir y aprobar la organización de proyectos, namespaces y capas del monolito modular antes de escribir código.

**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Fase 1 y resolución de DEC-005.

### Actividades previstas

1. Proponer la estructura de proyectos .NET (nombres de proyectos, referencias entre proyectos).
2. Definir las convenciones de namespaces y organización de carpetas.
3. Proponer las interfaces clave del dominio (repositorios, servicios).
4. Definir los modelos de configuración (options pattern).
5. Documentar la estructura propuesta en un documento de diseño.
6. Obtener aprobación de la estructura antes de crear archivos.

### Dependencias

- Fase 1 completada y aprobada.
- DEC-005: Estructura definitiva de capas.

### Entregables esperados

- Documento de diseño de la estructura de la solución .NET.
- Diagrama de dependencias entre proyectos.
- Convenciones de nomenclatura aprobadas.

### Criterios de salida

- La estructura de proyectos ha sido aprobada.
- No existen dependencias circulares entre capas en el diseño.
- Las convenciones de nomenclatura están documentadas.

### Decisiones que bloquean el avance a la Fase 3

- DEC-001: Selección del proveedor NoSQL (para el diseño de la capa de infraestructura).

---

## Fase 3 — Selección y aprobación del servicio NoSQL de Azure

**Objetivo:** Evaluar, seleccionar y documentar el proveedor de base de datos NoSQL en Azure.

**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Fase 1 y es una decisión que debe tomarse antes de la Fase 4.

### Actividades previstas

1. Evaluar los candidatos de base de datos NoSQL en Azure usando los criterios CRIT-DB-01 a CRIT-DB-11 definidos en `spec.md` y `memoria.md`.
2. Documentar la evaluación comparativa de candidatos.
3. Proponer un proveedor con justificación técnica.
4. Obtener aprobación formal de la selección.
5. Registrar la decisión en `memoria.md` como confirmada.

### Dependencias

- Fase 1 completada.
- Acceso a información suficiente sobre los candidatos.

### Entregables esperados

- Documento de evaluación comparativa de proveedores NoSQL.
- Proveedor seleccionado y aprobado (DEC-001 resuelta).
- Registro actualizado en `memoria.md`.

### Criterios de salida

- DEC-001 marcada como confirmada en `memoria.md`.
- La selección tiene justificación documentada para cada criterio de evaluación.
- El proveedor seleccionado tiene SDK oficial para .NET disponible.

### Decisiones que bloquean el avance a la Fase 4

- DEC-001 debe estar resuelta para diseñar la persistencia.

---

## Fase 4 — Diseño de la estrategia de persistencia

**Objetivo:** Diseñar el modelo de datos NoSQL y la estrategia de acceso a datos para el dominio de BusTrack.

**Estado:** 🔴 BLOQUEADA — Depende de DEC-001 (Fase 3).

### Actividades previstas

1. Diseñar el modelo de documentos NoSQL para las entidades del dominio.
2. Definir la estrategia de particionado según el proveedor seleccionado.
3. Definir la estrategia de indexado.
4. Diseñar las interfaces de repositorio del dominio.
5. Documentar los patrones de acceso a datos esperados.
6. Obtener aprobación del diseño de persistencia.

### Dependencias

- Fase 3 completada (DEC-001 resuelta).
- Fase 2 completada (estructura de capas aprobada).
- Especificaciones funcionales de dominio (parcialmente disponibles; se diseñará para las entidades conocidas).

### Entregables esperados

- Diseño del modelo de documentos NoSQL.
- Interfaces de repositorio del dominio diseñadas y aprobadas.
- Estrategia de particionado e indexado documentada.

### Criterios de salida

- El modelo de datos es coherente con el proveedor seleccionado.
- Las interfaces de repositorio están definidas para las entidades principales del dominio.
- El diseño ha sido revisado y aprobado.

---

## Fase 5 — Preparación de la base de la API

**Objetivo:** Implementar la estructura base del proyecto .NET con las capas, la configuración de la API, el manejo de errores y los mecanismos base de observabilidad.

**Estado:** 🔴 BLOQUEADA — Depende de Fases 2, 3 y resolución de DEC-005 y DEC-010.

### Actividades previstas

1. Crear la estructura de proyectos .NET aprobada en la Fase 2.
2. Configurar el enrutamiento con versionado `/api/v1/`.
3. Implementar el middleware centralizado de manejo de errores.
4. Implementar el endpoint `/health` de verificación de salud.
5. Configurar el registro estructurado con `ILogger`.
6. Configurar OpenAPI para la documentación de la API.
7. Implementar la inyección de dependencias base.
8. Ejecutar las pruebas de los criterios de aceptación AC-ARCH-01 al AC-ARCH-12.

### Dependencias

- Fase 2 completada (estructura de proyectos aprobada).
- DEC-010 resuelta (formato de respuestas de error).
- DEC-004 resuelta o adoptada una solución provisional (logging).

### Entregables esperados

- Estructura de proyectos .NET creada.
- API base ejecutable con endpoint `/health` funcional.
- Middleware de errores implementado.
- Registro estructurado configurado.
- Pruebas de los criterios de aceptación de arquitectura base.

### Criterios de salida

- Todos los criterios de aceptación AC-ARCH-01 al AC-ARCH-12 pasan.
- La API base compila y se ejecuta sin errores en el entorno de desarrollo.

---

## Fase 6 — Configuración y seguridad

**Objetivo:** Establecer la gestión de configuración por entorno, la gestión de secretos y el mecanismo base de autenticación y autorización.

**Estado:** 🔴 BLOQUEADA — Depende de DEC-002 y DEC-003.

### Actividades previstas

1. Configurar la jerarquía de configuración por entorno (`appsettings.json`, variables de entorno, gestión de secretos).
2. Integrar el servicio de gestión de secretos seleccionado en DEC-003.
3. Implementar el mecanismo de autenticación seleccionado en DEC-002.
4. Configurar la autorización base.
5. Verificar que ningún secreto se almacene en el repositorio.
6. Configurar HTTPS y redirección.

### Dependencias

- Fase 5 completada.
- DEC-002 resuelta (mecanismo de autenticación).
- DEC-003 resuelta (gestión de secretos en Azure).

### Entregables esperados

- Configuración por entorno implementada y probada.
- Secretos gestionados fuera del repositorio.
- Autenticación y autorización base funcionando.

### Criterios de salida

- Ningún endpoint devuelve datos sin autenticación (salvo endpoints públicos explícitos).
- Los secretos se leen de variables de entorno o del servicio de secretos.
- HTTPS está configurado y funciona.

---

## Fase 7 — Estrategia de pruebas

**Objetivo:** Establecer la infraestructura de pruebas y crear las pruebas iniciales de la arquitectura base.

**Estado:** 🔴 BLOQUEADA — Depende de Fase 5 y resolución de DEC-008 y DEC-009.

### Actividades previstas

1. Seleccionar las herramientas de prueba (DEC-009).
2. Crear los proyectos de prueba correspondientes.
3. Implementar pruebas unitarias para la lógica de dominio y aplicación.
4. Implementar pruebas de integración para los endpoints de la API base.
5. Validar que las pruebas se ejecutan correctamente en el entorno local.
6. Documentar la estrategia de pruebas adoptada.

### Dependencias

- Fase 5 completada.
- DEC-008 resuelta (umbral de cobertura).
- DEC-009 resuelta (herramientas de prueba).

### Entregables esperados

- Proyectos de prueba creados.
- Pruebas unitarias e integración de la arquitectura base.
- Documentación de la estrategia de pruebas adoptada.

### Criterios de salida

- Las pruebas unitarias de dominio y aplicación pasan sin infraestructura real.
- Las pruebas de integración validan los criterios de aceptación de arquitectura.
- El umbral de cobertura definido en DEC-008 se cumple.

---

## Fase 8 — Integración continua

**Objetivo:** Configurar el pipeline de CI/CD para la ejecución automática de pruebas y validación de la calidad del código.

**Estado:** 🔴 BLOQUEADA — Depende de Fase 7 y resolución de DEC-006.

### Actividades previstas

1. Seleccionar la herramienta de CI/CD (DEC-006).
2. Crear el pipeline de integración continua.
3. Configurar la ejecución automática de pruebas en cada commit o pull request.
4. Configurar análisis de calidad de código (opcional en esta fase).
5. Documentar el pipeline y su configuración.

### Dependencias

- Fase 7 completada.
- DEC-006 resuelta (herramienta de CI/CD).
- Repositorio configurado adecuadamente (`.gitignore`, protección de ramas).

### Entregables esperados

- Pipeline de CI configurado y funcionando.
- Ejecución automática de pruebas verificada.

### Criterios de salida

- El pipeline ejecuta las pruebas automáticamente y falla si alguna prueba no pasa.
- Ningún artefacto se genera si las pruebas fallan.

---

## Fase 9 — Preparación del despliegue en Azure

**Objetivo:** Preparar la configuración e infraestructura necesaria para desplegar el backend en Azure.

**Estado:** 🔴 BLOQUEADA — Depende de Fase 8 y resolución de DEC-007.

### Actividades previstas

1. Seleccionar el servicio de alojamiento en Azure (DEC-007).
2. Definir la configuración de despliegue para cada entorno.
3. Configurar el pipeline de CD (entrega continua).
4. Verificar la correcta gestión de secretos en el entorno de Azure.
5. Realizar el primer despliegue de la API base en el entorno de desarrollo/staging.
6. Verificar el endpoint `/health` en el entorno desplegado.

### Dependencias

- Fase 8 completada.
- DEC-007 resuelta (servicio de alojamiento en Azure).
- Cuenta y suscripción de Azure disponibles.

### Entregables esperados

- API base desplegada en Azure (entorno de desarrollo o staging).
- Pipeline de CD configurado.
- Documentación del proceso de despliegue.

### Criterios de salida

- La API responde correctamente en el entorno de Azure.
- El endpoint `/health` retorna 200.
- Los secretos se gestionan mediante el servicio seleccionado (no están en el código).

---

## Fase 10 — Incorporación de especificaciones funcionales

**Objetivo:** Diseñar, especificar e implementar las funcionalidades del sistema en iteraciones, siguiendo la metodología SDD.

**Estado:** 🔴 BLOQUEADA — Requiere que las Fases 1 a 9 estén completadas y que se disponga de especificaciones funcionales aprobadas.

### Actividades previstas (por cada funcionalidad)

1. Recibir y revisar el requisito funcional.
2. Crear o actualizar la especificación funcional en un `spec-{módulo}.md`.
3. Actualizar `memoria.md` con las decisiones de diseño.
4. Obtener aprobación de la especificación.
5. Crear o actualizar las tareas en `task.md`.
6. Implementar la funcionalidad siguiendo la especificación aprobada.
7. Crear pruebas automatizadas.
8. Verificar contra los criterios de aceptación.
9. Actualizar la documentación.

### Dependencias

- Fases 1 a 9 completadas.
- Especificaciones funcionales aprobadas por el responsable del proyecto.

### Entregables esperados

- Especificaciones funcionales por módulo.
- Implementación de funcionalidades según las especificaciones aprobadas.
- Pruebas automatizadas para cada funcionalidad.

### Criterios de salida

- La funcionalidad implementada cumple todos los criterios de aceptación de su especificación.
- Las pruebas pasan en el pipeline de CI.
- La documentación está actualizada.

---

## Resumen de dependencias entre fases

```
Fase 1 (Validación documental)
  └── Fase 2 (Diseño .NET) + Fase 3 (Selección NoSQL) [pueden iniciarse en paralelo tras Fase 1]
        ├── Fase 4 (Persistencia) [requiere Fase 3]
        └── Fase 5 (Base API) [requiere Fase 2]
              ├── Fase 6 (Configuración/Seguridad) [requiere Fase 5]
              └── Fase 7 (Pruebas) [requiere Fase 5]
                    └── Fase 8 (CI/CD) [requiere Fase 7]
                          └── Fase 9 (Despliegue) [requiere Fase 8]
                                └── Fase 10 (Funcionalidades) [requiere Fases 1-9]
```

---

*Este plan no tiene fechas asignadas. Las duraciones y el calendario deben acordarse cuando cada fase sea aprobada para iniciarse.*
