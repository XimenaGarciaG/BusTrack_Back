# charts.md — Etapa 06: Configuración y seguridad

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 06  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de configuración y seguridad. Las opciones concretas dependen de DEC-002 y DEC-003.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 06"] --> B["TAREA-015<br/>Jerarquía de configuración"]
    B --> C["TAREA-016<br/>Integrar servicio de secretos"]
    B --> D["TAREA-017<br/>Autenticación y autorización"]
    C --> E["Verificar ausencia de secretos"]
    D --> E
    E --> F{"¿Secretos solo en<br/>entorno / Key Vault?"}
    F -- "No" --> B
    F -- "Sí" --> G["Configurar HTTPS"]
    G --> H["Fin · habilitar Etapa 10"]
```

## 2. Jerarquía de configuración

```mermaid
flowchart BT
    A["appsettings.json"]
    B["appsettings.{Environment}.json"]
    C["Variables de entorno"]
    D["Servicio de secretos"]
    E["User secrets (solo dev)"]

    A --> B --> C --> D
    E -.-> C
```

> De menor a mayor prioridad según `spec.md` sección 9.

## 3. Flujo de autenticación

```mermaid
sequenceDiagram
    participant C as Cliente
    participant API as API
    participant AUTH as Proveedor de identidad
    participant APP as Application

    C->>API: Solicitud
    API->>AUTH: Validar credencial / token
    AUTH-->>API: Identidad y roles
    alt Autenticado y autorizado
        API->>APP: Ejecutar caso de uso
        APP-->>API: Resultado
        API-->>C: 200
    else Sin autenticación
        API-->>C: 401
    else Sin permiso
        API-->>C: 403
    end
```

## 4. Dependencias con otras etapas

```mermaid
flowchart LR
    E05["05 · Base API"]
    E06["06 · Configuración y seguridad"]
    E10["10 · Funcionalidades"]

    E05 --> E06
    E06 --> E10
```

## 5. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: DEC-002 y DEC-003 resueltas
    PENDIENTE --> EN_PROGRESO: inicia configuración
    EN_PROGRESO --> COMPLETADA: criterios verificados
    COMPLETADA --> [*]
```
