# backend-architecture-review.md — Skill: Revisión de Arquitectura del Backend

**Tipo:** Procedimiento reutilizable de revisión  
**Versión:** 1.0.0  
**Estado:** Vigente  
**Referencia normativa:** [`constitution.md`](../constitution.md) | [`spec.md`](../spec.md)

> **Aviso:** Este archivo describe un procedimiento de revisión reutilizable. No es un script ejecutable ni depende de ninguna plataforma específica.

---

## 1. Objetivo

Verificar que una propuesta de diseño o implementación del backend de BusTrack es coherente con la arquitectura base definida en `spec.md` y con los principios del monolito modular establecidos en `constitution.md`.

---

## 2. Cuándo utilizarlo

- Antes de aprobar la estructura de proyectos .NET propuesta en la Fase 2.
- Antes de iniciar la implementación de cualquier capa o módulo.
- Cuando se propone agregar una dependencia externa nueva.
- Cuando se propone modificar la organización de capas.
- Cuando se detecta una posible violación de los principios de separación de responsabilidades.

---

## 3. Información de entrada

| Entrada | Descripción | Obligatoria |
|---------|-------------|-------------|
| `spec.md` | Especificación de arquitectura base (secciones 4, 5, 6) | Sí |
| `constitution.md` | Principios obligatorios (secciones 4 y 5) | Sí |
| `memoria.md` | Decisiones confirmadas | Sí |
| Propuesta bajo revisión | Documento, diagrama o descripción de la estructura propuesta | Sí |

---

## 4. Procedimiento paso a paso

### Paso 1: Verificar el patrón arquitectónico

1. Confirmar que la propuesta adopta el patrón **monolito modular**.
2. Verificar que no introduce conceptos de microservicios (servicios desplegados independientemente, comunicación por red entre módulos del mismo sistema, etc.).
3. Verificar que la propuesta contempla un único proceso desplegable.

### Paso 2: Verificar la separación de capas

Para cada capa propuesta (API, Application, Domain, Infrastructure o equivalentes aprobados):

1. Verificar que la responsabilidad de la capa está claramente definida.
2. Verificar que la capa solo contiene los tipos de componentes que le corresponden.
3. Verificar que no existe lógica de negocio en la capa API.
4. Verificar que no existe acceso directo a datos desde la capa API.

### Paso 3: Verificar las dependencias entre capas

1. Confirmar que la capa Domain **no** depende de Application, Infrastructure ni API.
2. Confirmar que la capa Application **no** depende directamente de implementaciones de Infrastructure.
3. Confirmar que Application **no** depende de la capa API.
4. Confirmar que Infrastructure implementa interfaces definidas en Domain.
5. Si la propuesta incluye un diagrama de dependencias, verificar que no hay ciclos.

### Paso 4: Verificar el desacoplamiento de persistencia

1. Verificar que las interfaces de repositorio están definidas en la capa Domain.
2. Verificar que las interfaces no exponen tipos específicos del proveedor NoSQL.
3. Verificar que la propuesta no asume un proveedor NoSQL específico (DEC-001 pendiente).
4. Verificar que la capa Application usa las interfaces, no las implementaciones.

### Paso 5: Verificar la inyección de dependencias

1. Verificar que el diseño utiliza inyección de dependencias para conectar implementaciones con interfaces.
2. Verificar que la configuración de la inyección de dependencias está en la capa API o en el punto de entrada.
3. Verificar que no hay dependencias hardcodeadas entre capas.

### Paso 6: Verificar las convenciones de API

1. Verificar que los endpoints propuestos usan sustantivos en plural y minúsculas.
2. Verificar que el prefijo `/api/v1/` está presente.
3. Verificar que los métodos HTTP son semánticamente correctos.
4. Verificar que los códigos de respuesta HTTP son apropiados.
5. Verificar que las respuestas de error siguen la estructura definida (o la propuesta aprobada).

---

## 5. Criterios de aceptación

La revisión resulta en estado **ARQUITECTURA CONFORME** cuando:

- El patrón de monolito modular se mantiene.
- Las responsabilidades de cada capa están claramente delimitadas.
- Las reglas de dependencia entre capas se respetan.
- La persistencia está desacoplada mediante interfaces en el dominio.
- No se adopta un proveedor NoSQL específico sin aprobación (DEC-001).
- Las convenciones de API son coherentes con `spec.md`.

---

## 6. Errores que debe evitar

| Error | Descripción |
|-------|-------------|
| Aprobar dependencias de Domain hacia Infrastructure | Viola la inversión de dependencias; es un error crítico |
| Aprobar lógica de negocio en controladores | Viola la separación de responsabilidades |
| Asumir que DEC-001 está resuelta | El proveedor NoSQL no está seleccionado |
| Aprobar interfaces de repositorio con tipos de SDK específicos | Rompe el desacoplamiento |
| Confundir modularización con microservicios | El sistema es un monolito modular; un solo proceso desplegable |

---

## 7. Formato esperado del resultado

```markdown
# Resultado de Revisión de Arquitectura del Backend

**Fecha:** YYYY-MM-DD
**Propuesta revisada:** [nombre o descripción]
**Revisado por:** [agente o colaborador]

## Resumen

Estado: ARQUITECTURA CONFORME / NO CONFORME / CONFORME CON OBSERVACIONES

## Verificación por paso

### Paso 1: Patrón arquitectónico
[resultado]

### Paso 2: Separación de capas
[resultado]

### Paso 3: Dependencias entre capas
[resultado]

### Paso 4: Desacoplamiento de persistencia
[resultado]

### Paso 5: Inyección de dependencias
[resultado]

### Paso 6: Convenciones de API
[resultado]

## Observaciones

[Lista de observaciones con referencia al componente afectado]

## Recomendaciones

[Acciones sugeridas para resolver las no conformidades]
```

---

*Este procedimiento puede actualizarse siguiendo el proceso de control de cambios de `constitution.md`.*
