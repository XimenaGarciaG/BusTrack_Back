# charts.md — Etapa 01: Validación de la documentación SDD

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 01  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de la etapa. Son ilustrativos y no sustituyen los criterios de aceptación de `spec.md`.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 01"] --> B["TAREA-001<br/>Revisión de coherencia interna"]
    B --> C{"¿Contradicciones<br/>detectadas?"}
    C -- "Sí" --> D["Registrar en memoria.md<br/>como conflicto pendiente"]
    D --> E["Resolver o documentar<br/>el bloqueo"]
    E --> B
    C -- "No" --> F["TAREA-002<br/>Revisión del responsable"]
    F --> G{"¿Aprobación<br/>formal de spec.md?"}
    G -- "No" --> H["Incorporar observaciones"]
    H --> B
    G -- "Sí" --> I["TAREA-003<br/>Resolver DEC-005"]
    I --> J["Registrar aprobación<br/>en memoria.md"]
    J --> K["Fin · habilitar Etapa 02"]
```

## 2. Documentos revisados

```mermaid
flowchart LR
    C["constitution.md"]
    A["AGENTS.md"]
    M["memoria.md"]
    S["spec.md"]
    P["plan.md"]
    T["task.md"]
    R["Resultado:<br/>documentación coherente"]

    C --> R
    A --> R
    M --> R
    S --> R
    P --> R
    T --> R
```

## 3. Dependencias con otras etapas

```mermaid
flowchart LR
    E01["01 · Validación documental"]
    E02["02 · Diseño .NET"]
    E03["03 · Selección NoSQL"]

    E01 -- "habilita" --> E02
    E01 -- "habilita" --> E03
```

## 4. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> PENDIENTE
    PENDIENTE --> EN_PROGRESO: inicia revisión
    EN_PROGRESO --> BLOQUEADA: depende de decisión externa
    BLOQUEADA --> EN_PROGRESO: bloqueo resuelto
    EN_PROGRESO --> COMPLETADA: evidencia + aprobación
    COMPLETADA --> [*]
```

## 5. Mapa de criterios de salida

| Criterio de salida | Tarea asociada | Evidencia |
|--------------------|----------------|-----------|
| Coherencia documental | TAREA-001 | Registro de revisión |
| Aprobación de `spec.md` | TAREA-002 | Aprobación en `memoria.md` |
| DEC-005 resuelta | TAREA-003 | Decisión confirmada en `memoria.md` |
