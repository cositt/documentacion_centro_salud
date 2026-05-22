# Guía de usuario — cs_patient_followup_forms: Motor de evaluaciones y formularios dinámicos

## ¿Para qué sirve este módulo?

`cs_patient_followup_forms` es un motor de formularios dinámicos para registrar evaluaciones clínicas de pacientes. Permite crear **plantillas** con secciones y campos de diferentes tipos (texto, escala, sí/no, fecha, imagen…), y luego instanciarlas como **evaluaciones** sobre un paciente concreto. Cada evaluación puede rellenarse campo a campo mediante un asistente guiado o directamente en el formulario, y puede exportarse a PDF.

Uso habitual en Equilibrium: escalas de valoración psiquiátrica, evaluaciones de evolución, cuestionarios de seguimiento familiar, inventarios de síntomas.

---

## Acceso al módulo

> Menú principal → **Followup Pacientes**

Submenús:

| Submenú | Contenido |
|---------|-----------|
| **Plantillas** | Crear y gestionar plantillas de formulario |
| **Evaluaciones** | Instancias completadas o en curso por paciente |

---

## Arquitectura del módulo

```
Plantilla (cs.followup.template)
├── Sección 1 (cs.followup.template.section)
│   ├── Campo A (cs.followup.template.field)
│   └── Campo B
└── Sección 2
    └── Campo C

         ↓  Se instancia como

Evaluación (cs.followup.assessment)  [vinculada a un paciente]
├── Respuesta A (cs.followup.assessment.answer)
├── Respuesta B
└── Respuesta C
```

Una plantilla puede generar **múltiples evaluaciones** (una por paciente, una por fecha de valoración). Las evaluaciones heredan la estructura de la plantilla en el momento de creación; cambios posteriores en la plantilla no afectan evaluaciones ya creadas.

---

## Parte 1 — Crear una plantilla

### Paso 1: Cabecera

1. **Followup Pacientes** → **Plantillas** → **Nuevo**.
2. Rellenar:

| Campo | Descripción |
|-------|-------------|
| **Nombre** | Nombre identificativo (p. ej. "Escala GAF de funcionamiento global") |
| **Descripción** | Explicación del propósito de la plantilla |
| **Versión** | Número de versión; incrementar al hacer cambios significativos |
| **Estado** | `Borrador` → `Publicada` → `Archivada` |

### Paso 2: Añadir secciones

En la pestaña **Secciones**, añadir grupos temáticos:
- Cada sección tiene un **Título** y un **Orden** (número que determina la posición).
- Dentro de cada sección se añaden los campos.

### Paso 3: Añadir campos

Por cada campo en una sección:

| Campo del campo | Tipo | Descripción |
|----------------|------|-------------|
| **Etiqueta** | Texto | El texto de la pregunta o ítem |
| **Tipo** | Selección | Ver tabla de tipos abajo |
| **Código técnico** | Texto | Identificador interno (opcional, para integraciones) |
| **Ayuda** | Texto | Texto explicativo que se muestra al rellenar |
| **Obligatorio** | Booleano | Si la evaluación no se puede completar sin este campo |
| **Opciones** | Texto | Solo para tipo `Selección`: una opción por línea |
| **Valor mínimo / máximo** | Número | Para validaciones en tipos numéricos |

### Tipos de campo disponibles

| Tipo | Uso |
|------|-----|
| **Escala 1-10** | Valoraciones numéricas (intensidad, frecuencia, nivel) |
| **Sí/No** | Presencia/ausencia de síntomas, confirmaciones |
| **Texto corto** | Respuestas breves (nombre, diagnóstico puntual) |
| **Texto largo** | Observaciones, narrativas, descripciones extendidas |
| **Fecha** | Fechas de eventos (debut, recaída, última revisión) |
| **Selección** | Opciones predefinidas (p. ej. "Leve / Moderado / Grave") |
| **Imagen** | Fotografías, capturas, documentos escaneados |

### Paso 4: Publicar la plantilla

- Solo se pueden usar plantillas en estado **Publicada**.
- Pulsar **Publicar** (requiere al menos un campo; si no hay campos el sistema lo impide).
- Para editar una plantilla publicada: volver a **Borrador** → editar → **Publicar** de nuevo. Esto no afecta evaluaciones ya creadas.
- **Archivar** para ocultar plantillas que ya no se usan sin borrarlas.

> [SCREENSHOT: formulario de plantilla con dos secciones y varios campos de distintos tipos]

---

## Parte 2 — Crear una evaluación

1. **Followup Pacientes** → **Evaluaciones** → **Nuevo**.
2. Campos de cabecera:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Plantilla** | Sí | Solo plantillas en estado `Publicada` son seleccionables |
| **Paciente** | Sí | Contacto (res.partner) al que pertenece la evaluación |
| **Profesional** | Sí | Usuario que realiza la evaluación (por defecto: usuario actual) |
| **Fecha** | Sí | Fecha de la evaluación (por defecto: hoy) |

3. Al seleccionar la plantilla, las **Respuestas** se crean automáticamente — una por cada campo de la plantilla, en el mismo orden y agrupación por sección.
4. La **Referencia** se genera automáticamente: `[Paciente] - [Plantilla] ([Fecha])`.

> [SCREENSHOT: evaluación recién creada con respuestas pre-generadas pero vacías]

---

## Parte 3 — Rellenar una evaluación

### Modo directo (en el formulario)

En la pestaña **Respuestas**, cada fila muestra:
- El campo/pregunta de la plantilla
- El campo de respuesta apropiado según el tipo

Editar directamente cada respuesta en la tabla. Guardar con el botón habitual de Odoo.

### Modo guiado (pregunta a pregunta)

Para evaluaciones largas o cuando se quiere evitar errores, usar el **asistente guiado**:

1. En la evaluación, pulsar **Rellenado guiado**.
2. Se abre un diálogo que muestra **una pregunta a la vez**:
   - Título de la pregunta y texto de ayuda (si está configurado).
   - Indicador de progreso: `N de M` (p. ej. "3 de 12").
   - Campo de respuesta adaptado al tipo (texto, escala, casilla, fecha…).
   - Botones **Anterior** / **Siguiente** para navegar.
3. Al llegar a la última pregunta: botón **Guardar y cerrar** — las respuestas quedan guardadas en la evaluación.

> El asistente guarda la respuesta actual antes de avanzar a la siguiente. Si se cierra el diálogo antes de terminar, las respuestas ya respondidas quedan guardadas; las no respondidas quedan en blanco.

### Completar la evaluación

1. Rellenar todas las respuestas obligatorias.
2. Pulsar **Marcar como completada**.
   - El sistema valida que todos los campos obligatorios estén rellenos y que los tipos sean correctos (escala 1–10 dentro de rango, campos de selección con opción elegida, etc.).
   - Si falta alguno: error con el nombre del campo que falta.
3. Estado → **Completada**. La evaluación queda bloqueada para edición.

Para corregir una evaluación completada: pulsar **Volver a borrador** → editar → **Marcar como completada** de nuevo.

---

## Parte 4 — Exportar a PDF

Con la evaluación abierta (cualquier estado):

1. Pulsar **Descargar PDF**.
2. El sistema genera un informe con: datos del paciente, profesional, fecha, plantilla, versión y todas las respuestas agrupadas por sección.
3. El PDF se descarga automáticamente o se abre en el visor del navegador.

> [SCREENSHOT: PDF de evaluación con secciones y respuestas]

---

## Parte 5 — Estados de una evaluación

```
Borrador ──► Completada
    │             │
    │◄────────────┘  (Volver a borrador)
    │
    └──► Cancelada
```

| Estado | Significado |
|--------|-------------|
| **Borrador** | En proceso, totalmente editable |
| **Completada** | Cerrada y validada, solo lectura |
| **Cancelada** | Descartada (no se puede completar) |

---

## Flujo completo con ejemplo real

**Contexto:** Psicóloga María Sánchez realiza la Escala GAF mensual de Ana López.

1. La psicóloga va a **Followup Pacientes** → **Evaluaciones** → **Nuevo**.
2. Plantilla: `Escala GAF — Valoración mensual`. Paciente: `Ana López`. Fecha: `21/05/2026`. Profesional: `María Sánchez`.
3. Pulsar **Rellenado guiado**:
   - Pregunta 1/8: "Nivel de funcionamiento global (1-10)" → introduce `6`.
   - Pregunta 2/8: "¿Ha habido episodios disociativos esta semana?" → `No`.
   - (…continúa pregunta a pregunta…)
   - Última pregunta: pulsa **Guardar y cerrar**.
4. De vuelta en la evaluación: revisar respuestas → **Marcar como completada**.
5. Pulsar **Descargar PDF** → adjuntar el PDF a la historia clínica en cs_medical_care.

---

## Casos de uso frecuentes

### Crear una escala tipo Likert (1-5)
- Tipo de campo: `Escala 1-10` con `Valor mínimo: 1` y `Valor máximo: 5`.
- El sistema valida que la respuesta esté en el rango al completar.

### Añadir un campo de selección con opciones
- Tipo: `Selección`.
- En **Opciones**: escribir una opción por línea:
  ```
  Nunca
  A veces
  Con frecuencia
  Siempre
  ```

### Crear nueva versión de una plantilla
- Volver la plantilla a **Borrador** → editar campos → incrementar **Versión** → **Publicar**.
- Las evaluaciones existentes mantienen la versión con la que fueron creadas (campo `Version plantilla` en la evaluación).

### Ver todas las evaluaciones de un paciente
- **Evaluaciones** → búsqueda por **Paciente** → ver historial cronológico.

### Evaluación accesible desde la ficha del contacto
- El módulo añade una pestaña o smart button en la ficha del contacto (res.partner) que muestra las evaluaciones vinculadas.

---

## Errores y avisos comunes

| Mensaje | Causa | Solución |
|---------|-------|----------|
| `No puedes publicar una plantilla sin campos` | La plantilla no tiene ningún campo en sus secciones | Añadir al menos un campo en al menos una sección |
| `El campo 'X' es de tipo Seleccion y debe tener opciones` | Campo de selección sin opciones definidas | Añadir las opciones en el campo **Opciones** del campo (una por línea) |
| `Debe informar una opcion para respuestas de tipo seleccion` | Al completar la evaluación, un campo de selección está sin respuesta | Volver a borrador → rellenar el campo → marcar como completada de nuevo |
| `La escala debe estar entre 1 y 10` | Valor numérico fuera del rango de la escala | Introducir un valor entre 1 y 10 inclusive |
| La plantilla no aparece al crear evaluación | La plantilla está en estado `Borrador` o `Archivada` | Publicar la plantilla antes de usarla |
| `Esta evaluacion no tiene campos para rellenar` | La plantilla asociada no tiene campos en ninguna sección | Revisar la plantilla: añadir secciones y campos |
| `No puede responder dos veces el mismo campo` | Error interno si se modifica la plantilla mientras una evaluación está en curso | No cambiar la plantilla mientras hay evaluaciones en borrador que la usen |
