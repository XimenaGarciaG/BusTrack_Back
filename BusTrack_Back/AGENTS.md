# AGENTS.md — Instrucciones para Agentes y Colaboradores

**Repositorio:** `BusTrack_Back`  
**Versión:** 1.0.0  
**Estado:** Vigente

> Este archivo proporciona instrucciones operativas a cualquier agente de IA o colaborador humano que trabaje en este repositorio. Su cumplimiento es obligatorio.

---

## 1. Lectura obligatoria antes de intervenir

Antes de proponer, modificar o generar cualquier contenido en este repositorio, debes leer completamente los siguientes documentos en este orden:

1. [`constitution.md`](./constitution.md) — Norma suprema del proyecto.
2. [`memoria.md`](./memoria.md) — Contexto, decisiones confirmadas y pendientes.
3. [`spec.md`](./spec.md) — Especificación técnica de la arquitectura base (si existe y aplica a tu tarea).
4. [`plan.md`](./plan.md) — Plan de implementación por fases (si la tarea pertenece a una fase específica).
5. [`task.md`](./task.md) — Lista de tareas y su estado actual.

**Razón:** Estos documentos definen el contexto, las decisiones vigentes y el estado del proyecto. Intervenir sin leerlos puede generar contradicciones, duplicidades o retrocesos.

Si alguno de estos archivos no existe aún, regístralo como observación antes de continuar.

---

## 2. Respeto a las decisiones confirmadas

Las siguientes decisiones están confirmadas y no pueden modificarse sin seguir el proceso de control de cambios descrito en `constitution.md`:

- El backend utiliza **ASP.NET Core Web API con C#**.
- La arquitectura es un **monolito modular** (no microservicios).
- La API sigue el estilo **REST** con intercambio en **JSON**.
- El versionado de la API utilizará `/api/v1` como convención inicial.
- La base de datos es **NoSQL en Azure** (proveedor pendiente de selección).
- La persistencia debe mantenerse **desacoplada** mediante abstracciones.
- Los secretos no se almacenan en el repositorio.

Si encuentras una solicitud que contradiga alguna de estas decisiones, no la ejecutes. Documenta el conflicto en `memoria.md` y espera aprobación.

---

## 3. Prohibición de inventar requisitos o modificar decisiones pendientes

**No está permitido:**

- Asumir que una decisión pendiente tiene un valor concreto.
- Seleccionar un proveedor de base de datos (ej.: Cosmos DB, MongoDB) sin aprobación.
- Elegir un mecanismo de autenticación específico sin aprobación.
- Inventar fechas, responsables o contexto no documentado.
- Adelantar funcionalidades fuera del alcance actual.
- Modificar el estado de una decisión pendiente a confirmada sin evidencia de aprobación.

Cuando una decisión sea necesaria para avanzar pero esté pendiente, documenta el bloqueo en `task.md` y en `memoria.md`.

---

## 4. Prohibición de introducir secretos o datos sensibles

**Está estrictamente prohibido:**

- Escribir contraseñas, tokens, claves de API o cadenas de conexión en cualquier archivo del repositorio.
- Incluir información de configuración específica de entornos productivos.
- Referenciar cuentas, suscripciones, identificadores de recursos o datos de personas reales.
- Crear o modificar archivos que puedan exponer datos sensibles si se versionan.

Si necesitas ejemplificar una cadena de conexión u otro valor sensible, usa siempre un marcador de posición claramente identificado como ficticio, como:

```
"ConnectionString": "<REEMPLAZAR_CON_SECRETO_DESDE_VARIABLES_DE_ENTORNO>"
```

---

## 5. Reglas de nomenclatura, organización y documentación

### Idioma
- La documentación técnica del repositorio se escribe en **español técnico**.
- El código fuente, los nombres de clases, métodos, variables y comentarios de código se escriben en **inglés**, siguiendo las convenciones de .NET y C#.

### Nomenclatura de archivos de documentación
- Los archivos Markdown en la raíz del repositorio usan nombres en minúsculas con guión medio: `constitution.md`, `spec.md`, `plan.md`, `task.md`, `memoria.md`.
- Las excepciones son: `AGENTS.md` y `README.md` (en mayúsculas por convención universal).

### Estructura de documentos
- Todos los documentos deben comenzar con un encabezado de nivel 1 (`#`) con el nombre del documento.
- Deben incluir metadatos mínimos: versión, estado, fecha de última actualización.
- Los identificadores de tareas y requisitos deben ser estables y únicos (no reutilizar identificadores eliminados).

### Organización de directorios
```
BusTrack_Back/                        # Raíz del repositorio
├── BusTrack_Back.slnx                # Solución .NET
└── BusTrack_Back/                    # Proyecto ASP.NET Core + Documentación SDD
    ├── constitution.md               # Norma suprema
    ├── AGENTS.md                     # Este archivo
    ├── memoria.md                    # Registro de decisiones
    ├── spec.md                       # Especificación de arquitectura base
    ├── plan.md                       # Plan de implementación
    ├── task.md                       # Lista de tareas trazables
    ├── subagents/                    # Definiciones de subagentes (revisores documentales)
    ├── skills/                       # Procedimientos reutilizables de revisión
    ├── BusTrack_Back.csproj          # Proyecto .NET
    ├── Program.cs                    # Punto de entrada (plantilla inicial)
    └── Controllers/                  # Controladores (plantilla inicial)
```

---

## 6. Obligación de identificar contradicciones antes de modificar archivos

Antes de modificar cualquier archivo de documentación o código, debes verificar:

1. ¿El cambio propuesto contradice `constitution.md`?
2. ¿El cambio propuesto contradice alguna decisión confirmada en `memoria.md`?
3. ¿El cambio propuesto adelanta funcionalidades fuera del alcance actual?
4. ¿El cambio afecta a otros documentos que también deberían actualizarse?

Si la respuesta a cualquiera de las preguntas 1, 2 o 3 es "sí", no realices el cambio. Documenta el conflicto en `memoria.md` bajo la sección de conflictos pendientes.

Si la respuesta a la pregunta 4 es "sí", actualiza todos los documentos afectados en la misma intervención para mantener la coherencia.

---

## 7. Prohibición de implementar código en la etapa actual

La etapa actual del proyecto es **exclusivamente documental**.

**Está prohibido:**
- Crear archivos de código fuente (`.cs`, `.csproj`, `.sln`, etc.) más allá de la plantilla ya existente.
- Modificar los archivos de código de la plantilla actual (`Program.cs`, `WeatherForecastController.cs`, etc.).
- Agregar paquetes NuGet o dependencias.
- Ejecutar comandos de compilación, migración o despliegue.
- Crear o configurar recursos en Azure.

La plantilla `BusTrack_Back/` existe como punto de partida técnico del proyecto .NET, pero su contenido no debe modificarse hasta que la fase de diseño documental esté aprobada y se inicie la fase de implementación correspondiente.

---

## 8. Prohibición de ejecutar tareas o marcarlas como completadas sin evidencia

**Reglas sobre el estado de las tareas:**

- Una tarea no puede marcarse como `COMPLETADA` por el simple hecho de haberla escrito o de haber ejecutado pasos que se mencionan en su descripción.
- El estado `COMPLETADA` requiere evidencia verificable (artefacto generado, resultado de prueba, aprobación documentada).
- El estado `EN_PROGRESO` solo puede asignarse cuando el trabajo ha comenzado efectivamente.
- Una tarea `BLOQUEADA` debe registrar explícitamente qué la bloquea.
- No se deben crear tareas con estado `COMPLETADA` en la etapa actual, salvo las tareas de generación documental que se completen en esta misma sesión con evidencia de los archivos creados.

---

## 9. Procedimiento para proponer cambios a la constitución

Si identificas que una regla de `constitution.md` debe modificarse:

1. **No modifiques `constitution.md` directamente.**
2. Abre una entrada en `memoria.md` bajo la sección "Conflictos y propuestas de cambio".
3. Documenta:
   - La regla actual que deseas modificar (cita textual).
   - La modificación propuesta.
   - La justificación técnica.
4. Marca la propuesta como **Propuesto (pendiente de aprobación)**.
5. Espera aprobación antes de modificar `constitution.md`.

---

## 10. Registro de supuestos, riesgos y decisiones pendientes

Cuando identifiques un supuesto, un riesgo o una decisión pendiente durante tu trabajo:

1. Regístralo inmediatamente en `memoria.md` en la sección correspondiente.
2. Asígnale un identificador único (p. ej., `SUP-001`, `RIESGO-001`, `DEC-001`).
3. Describe el impacto potencial si el supuesto es incorrecto o si el riesgo se materializa.
4. No avances en ninguna tarea que dependa de ese supuesto o decisión sin que esté resuelta.

---

## 11. Herramientas y subagentes

Los archivos en el directorio `subagents/` describen los roles y restricciones de subagentes documentales. Estos archivos son **definiciones Markdown descriptivas** y no implican que ninguna plataforma de agentes esté instalada o configurada en este repositorio.

Los archivos en el directorio `skills/` describen procedimientos reutilizables de revisión.

No afirmes que un subagente o una skill está "ejecutándose" o "registrado en una plataforma" basándote únicamente en la existencia de estos archivos Markdown.

---

## 12. Verificación final antes de cerrar una intervención

Al finalizar cualquier intervención, verifica que:

- [ ] Los archivos modificados son coherentes entre sí.
- [ ] Ninguna decisión pendiente se ha convertido en confirmada sin evidencia.
- [ ] No se han introducido secretos ni datos sensibles.
- [ ] No se ha implementado código no autorizado.
- [ ] `memoria.md` refleja cualquier nueva decisión, supuesto o riesgo identificado.
- [ ] Las tareas en `task.md` tienen el estado correcto.
- [ ] Los criterios de aceptación de los documentos modificados siguen siendo verificables.

---

*Este archivo debe actualizarse si el proceso de trabajo cambia. Las actualizaciones deben seguir el proceso de control de cambios descrito en `constitution.md`.*
