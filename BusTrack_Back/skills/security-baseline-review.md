# security-baseline-review.md — Skill: Revisión de Seguridad Base

**Tipo:** Procedimiento reutilizable de revisión  
**Versión:** 1.0.0  
**Estado:** Vigente  
**Referencia normativa:** [`constitution.md`](../constitution.md) | [`spec.md`](../spec.md)

> **Aviso:** Este archivo describe un procedimiento de revisión de seguridad reutilizable. No es un script ejecutable. Este procedimiento evalúa principios de seguridad a nivel documental y de diseño; no realiza análisis de vulnerabilidades de código ni pruebas de penetración.

---

## 1. Objetivo

Verificar que una propuesta de diseño, especificación funcional o configuración cumple los principios de seguridad y privacidad establecidos en `constitution.md` y `spec.md`.

---

## 2. Cuándo utilizarlo

- Antes de aprobar una especificación funcional que involucre autenticación o autorización.
- Antes de aprobar el diseño de cualquier endpoint que maneje datos sensibles.
- Antes de aprobar la configuración de infraestructura o despliegue.
- Antes de enviar cambios a revisión externa.
- Cuando se sospeche que una propuesta podría comprometer la seguridad o la privacidad.

---

## 3. Información de entrada

| Entrada | Descripción | Obligatoria |
|---------|-------------|-------------|
| `constitution.md` | Principios de seguridad (secciones 7 y 8) | Sí |
| `spec.md` | Restricciones de seguridad (secciones 11 y 12) | Sí |
| `memoria.md` | Estado de DEC-002 y DEC-003 | Sí |
| Propuesta bajo revisión | Documento o diseño que se desea revisar | Sí |

---

## 4. Procedimiento paso a paso

### Paso 1: Verificar la ausencia de secretos y datos sensibles

Buscar en todos los archivos de la propuesta:

- [ ] Contraseñas o frases de paso.
- [ ] Cadenas de conexión con credenciales embebidas.
- [ ] Tokens de acceso o tokens de refresco.
- [ ] Claves de API de servicios externos.
- [ ] Identificadores de suscripción, tenant o recursos de Azure.
- [ ] Datos personales de usuarios o personas reales.

**Si se encuentra alguno de los anteriores:** Reportar inmediatamente como hallazgo crítico sin reproducir el valor sensible en el informe.

### Paso 2: Verificar los principios de autenticación

1. Verificar que todos los endpoints diseñados requieren autenticación.
2. Verificar que los endpoints públicos están explícitamente marcados como tales y justificados.
3. Verificar que no se ha seleccionado un mecanismo de autenticación específico sin que DEC-002 esté resuelta.
4. Si DEC-002 está resuelta, verificar que el mecanismo adoptado es coherente con la decisión aprobada.

### Paso 3: Verificar los principios de autorización

1. Verificar que el diseño contempla control de acceso basado en roles o políticas.
2. Verificar que los roles o políticas están definidos (o marcados como pendientes de especificación funcional).
3. Verificar que operaciones sensibles tienen control de acceso más restrictivo.

### Paso 4: Verificar la seguridad del transporte

1. Verificar que el diseño especifica HTTPS para todos los entornos no locales.
2. Verificar que la redirección de HTTP a HTTPS está contemplada.
3. Verificar que no se contempla comunicación sin cifrar con servicios externos.

### Paso 5: Verificar la validación de entradas

1. Verificar que el diseño contempla validación de todas las entradas del cliente.
2. Verificar que la validación de formato se realiza en la capa API.
3. Verificar que la validación de reglas de negocio se realiza en las capas de dominio o aplicación.
4. Verificar que no se asume que las entradas del cliente son confiables.

### Paso 6: Verificar la protección de datos y privacidad

1. Verificar que los logs no incluyen datos personales identificables.
2. Verificar que las respuestas de error no revelan detalles internos (rutas, nombres de tablas, stack traces).
3. Verificar que los datos personales se manejan con principio de mínima exposición.
4. Verificar que no se transmiten datos sensibles en parámetros de URL (query strings).

### Paso 7: Verificar el principio de mínimo privilegio

1. Verificar que las cuentas de servicio propuestas tienen solo los permisos necesarios.
2. Verificar que los recursos de Azure propuestos tienen políticas de acceso restrictivas.
3. Verificar que la aplicación no requiere permisos de administrador en producción.

### Paso 8: Verificar la gestión de secretos

1. Verificar que no hay secretos en el repositorio ni en archivos de configuración versionados.
2. Verificar que la propuesta contempla el uso de variables de entorno o del servicio de gestión de secretos.
3. Si DEC-003 está resuelta, verificar que la propuesta es coherente con el servicio seleccionado.

---

## 5. Criterios de aceptación

La revisión resulta en estado **SEGURIDAD CONFORME** cuando:

- No se encuentran secretos ni datos sensibles en ningún archivo de la propuesta.
- Todos los endpoints diseñados tienen autenticación (o están explícitamente justificados como públicos).
- El diseño contempla autorización basada en roles o políticas.
- HTTPS está especificado para entornos no locales.
- La validación de entradas está contemplada en el diseño.
- Los logs no incluyen datos personales.
- Las respuestas de error no revelan detalles internos.
- La gestión de secretos es coherente con los principios de la constitución.

---

## 6. Errores que debe evitar

| Error | Descripción |
|-------|-------------|
| Reproducir secretos en el informe | Nunca copiar valores sensibles, ni siquiera para reportarlos |
| Seleccionar un mecanismo de autenticación sin aprobación | DEC-002 debe estar resuelta primero |
| Marcar como conforme sin verificar todos los pasos | Cada paso es obligatorio |
| Confundir validación de formato con validación de negocio | Son responsabilidades de capas distintas |
| Ignorar endpoints marcados como públicos sin justificación | Todo endpoint público debe estar explícitamente justificado |

---

## 7. Formato esperado del resultado

```markdown
# Resultado de Revisión de Seguridad Base

**Fecha:** YYYY-MM-DD
**Propuesta revisada:** [nombre o descripción]
**Revisado por:** [agente o colaborador]

## Resumen

Estado: SEGURIDAD CONFORME / NO CONFORME / CONFORME CON OBSERVACIONES

## Verificación por paso

### Paso 1: Ausencia de secretos y datos sensibles
[resultado: CONFORME / HALLAZGO CRÍTICO / NO APLICA]

### Paso 2: Autenticación
[resultado]

### Paso 3: Autorización
[resultado]

### Paso 4: Seguridad del transporte
[resultado]

### Paso 5: Validación de entradas
[resultado]

### Paso 6: Protección de datos y privacidad
[resultado]

### Paso 7: Mínimo privilegio
[resultado]

### Paso 8: Gestión de secretos
[resultado]

## Hallazgos

| ID | Severidad | Paso | Descripción | Recomendación |
|----|-----------|------|-------------|---------------|
| SEG-001 | CRÍTICA/ALTA/MEDIA/BAJA | [paso] | [descripción sin reproducir valores sensibles] | [recomendación] |

## Próximos pasos recomendados

[Acciones a tomar antes de considerar la revisión superada]
```

---

*Este procedimiento puede actualizarse siguiendo el proceso de control de cambios de `constitution.md`.*
