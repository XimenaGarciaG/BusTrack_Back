# charts.md — Etapa 10: Incorporación de especificaciones funcionales

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 10  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas del ciclo SDD por funcionalidad. No representan funcionalidades aprobadas.

---

## 1. Ciclo por funcionalidad

```mermaid
flowchart TD
    A["Requisito funcional"] --> B["Especificación<br/>spec-{módulo}.md"]
    B --> C["Actualizar memoria.md"]
    C --> D{"¿Especificación<br/>aprobada?"}
    D -- "No" --> E["Incorporar observaciones"]
    E --> B
    D -- "Sí" --> F["Crear tareas<br/>en task.md"]
    F --> G["Implementar"]
    G --> H["Pruebas automatizadas"]
    H --> I{"¿Criterios de<br/>aceptación cumplidos?"}
    I -- "No" --> G
    I -- "Sí" --> J["Actualizar documentación"]
    J --> K["Fin de la funcionalidad"]
```

## 2. Secuencia de etapas previas

```mermaid
flowchart LR
    E01["01 · Validación"]
    E02["02 · Diseño .NET"]
    E03["03 · NoSQL"]
    E04["04 · Persistencia"]
    E05["05 · Base API"]
    E06["06 · Seguridad"]
    E07["07 · Pruebas"]
    E08["08 · CI"]
    E09["09 · Despliegue"]
    E10["10 · Funcionalidades"]

    E01 --> E02 --> E05
    E01 --> E03 --> E04
    E05 --> E06
    E05 --> E07 --> E08 --> E09
    E04 --> E10
    E06 --> E10
    E09 --> E10
```

## 3. Estados del ciclo funcional

```mermaid
stateDiagram-v2
    [*] --> ESPECIFICACION
    ESPECIFICACION --> APROBACION: propuesta
    APROBACION --> ESPECIFICACION: observaciones
    APROBACION --> IMPLEMENTACION: aprobada
    IMPLEMENTACION --> PRUEBAS
    PRUEBAS --> IMPLEMENTACION: falla
    PRUEBAS --> DOCUMENTACION: criterios cumplidos
    DOCUMENTACION --> [*]
```

## 4. Mapa de trazabilidad

| Artefacto | Documento |
|-----------|-----------|
| Requisito | Por definir |
| Especificación | `spec-{módulo}.md` |
| Decisiones | `memoria.md` |
| Tareas | `task.md` / `stages/10-.../task.md` |
| Pruebas | Proyectos de prueba |
| Evidencia | Pipeline de CI |
