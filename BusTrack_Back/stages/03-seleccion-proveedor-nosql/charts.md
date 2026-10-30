# charts.md — Etapa 03: Selección y aprobación del servicio NoSQL de Azure

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 03  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de evaluación. No representan una decisión confirmada sobre el proveedor.

---

## 1. Flujo de evaluación

```mermaid
flowchart TD
    A["Inicio · Etapa 03"] --> B["TAREA-006<br/>Identificar candidatos"]
    B --> C["Evaluar CRIT-DB-01..11"]
    C --> D["Documento comparativo"]
    D --> E["TAREA-007<br/>Proponer proveedor"]
    E --> F{"¿Aprobación<br/>formal?"}
    F -- "No" --> G["Incorporar observaciones"]
    G --> E
    F -- "Sí" --> H["Registrar DEC-001<br/>como confirmada"]
    H --> I["Fin · habilitar Etapa 04"]
```

## 2. Criterios de evaluación

```mermaid
mindmap
  root((CRIT-DB))
    Compatibilidad
      CRIT-DB-01 SDK .NET
    Datos
      CRIT-DB-02 Modelo JSON
      CRIT-DB-03 Consultas
      CRIT-DB-04 Índices
      CRIT-DB-05 Particionado
      CRIT-DB-06 Consistencia
    Operación
      CRIT-DB-07 Seguridad
      CRIT-DB-08 Escalabilidad
      CRIT-DB-09 Disponibilidad
      CRIT-DB-10 Costos
      CRIT-DB-11 Operación
```

## 3. Dependencias con otras etapas

```mermaid
flowchart LR
    E01["01 · Validación"]
    E03["03 · Selección NoSQL"]
    E04["04 · Persistencia"]
    E05["05 · Base API"]

    E01 --> E03
    E03 --> E04
    E03 -.-> E05
```

## 4. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> PENDIENTE
    PENDIENTE --> EN_PROGRESO: inicia evaluación
    EN_PROGRESO --> BLOQUEADA: falta información de candidatos
    BLOQUEADA --> EN_PROGRESO: información disponible
    EN_PROGRESO --> COMPLETADA: selección aprobada
    COMPLETADA --> [*]
```

## 5. Mapa de criterios de salida

| Criterio de salida | Tarea asociada | Evidencia |
|--------------------|----------------|-----------|
| Evaluación de al menos dos candidatos | TAREA-006 | Documento comparativo |
| Evaluación de los once criterios | TAREA-006 | Matriz de evaluación |
| DEC-001 confirmada | TAREA-007 | Registro en `memoria.md` |
