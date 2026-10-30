# charts.md — Etapa 02: Diseño de la estructura de la solución .NET

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 02  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de diseño propuestos. La estructura definitiva depende de DEC-005 y de la aprobación de esta etapa.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 02"] --> B["TAREA-004<br/>Propuesta de proyectos .NET"]
    B --> C["Diagrama de dependencias"]
    C --> D{"¿Existen ciclos<br/>o violaciones de capas?"}
    D -- "Sí" --> E["Corregir diseño"]
    E --> C
    D -- "No" --> F["TAREA-005<br/>Convenciones de nomenclatura"]
    F --> G["Aprobación de la estructura"]
    G --> H["Registrar DEC-005<br/>en memoria.md"]
    H --> I["Fin · habilitar Etapa 05"]
```

## 2. Dependencias entre proyectos (propuesta)

```mermaid
flowchart TB
    API["BusTrack.Api"]
    APP["BusTrack.Application"]
    DOM["BusTrack.Domain"]
    INF["BusTrack.Infrastructure"]

    API --> APP
    API -.-> DOM
    APP --> DOM
    INF --> DOM
    INF -.-> APP
```

> La dependencia `Infrastructure → Application` solo es válida a través de interfaces declaradas en `Domain`. Cualquier dependencia directa está prohibida por `spec.md` sección 6.

## 3. Dependencias con otras etapas

```mermaid
flowchart LR
    E01["01 · Validación"]
    E02["02 · Diseño .NET"]
    E05["05 · Base API"]

    E01 --> E02
    E02 --> E05
```

## 4. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: Etapa 01 aprobada y DEC-005 resuelta
    PENDIENTE --> EN_PROGRESO: inicia diseño
    EN_PROGRESO --> COMPLETADA: diseño aprobado
    COMPLETADA --> [*]
```

## 5. Mapa de criterios de salida

| Criterio de salida | Tarea asociada | Evidencia |
|--------------------|----------------|-----------|
| Estructura de proyectos definida | TAREA-004 | Documento de diseño |
| Sin ciclos de dependencia | TAREA-004 | Diagrama de dependencias |
| Convenciones documentadas | TAREA-005 | Documento de convenciones |
