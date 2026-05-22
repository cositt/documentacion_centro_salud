# Guía de Usuario — cs_psychology
## Psicología y Llamadas Familiares

**Módulo:** `cs_psychology` v1.1.0  
**Perfil:** Psicólogos, coordinadores  
**Menú principal:** `Psicología`

---

## ¿Para qué sirve?

Gestiona toda la actividad psicológica del residente:
- **Evaluación psicológica inicial** al ingreso (hipótesis, antecedentes, riesgos, plan)
- **Sesiones de psicología** individuales, familiares, grupales o de coordinación — sincronizadas automáticamente con el calendario de Odoo
- **Llamadas y contactos familiares** visibles desde la ficha del residente
- **Calendario** con todas las citas psicológicas del centro en vista mensual/semanal/diaria

---

## Acceso al módulo

```
Menú superior → Psicología
```

| Submenú | Descripción |
|---------|-------------|
| `Citas (calendario)` | Vista calendario de todas las sesiones |
| `Sesiones` | Lista de sesiones psicológicas |
| `Evaluación inicial` | Evaluaciones iniciales al ingreso |
| `Contactos familia` | Registro de llamadas y contactos familiares |

---

## Parte 1 — Evaluación psicológica inicial

### ¿Qué es?
Documento de primer contacto clínico psicológico. Se crea durante la admisión (Paso 4) o de forma independiente. Recoge hipótesis diagnóstica, antecedentes, riesgo y plan inicial.

### 1.1 Crear una evaluación inicial

**Ruta:** `Psicología > Evaluación inicial > Nuevo`

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Residente | ✓ | Paciente evaluado |
| Fecha | ✓ | Fecha de la evaluación |
| Psicólogo/a | — | Solo acepta trabajadores con puesto "Psicólogo" |
| Motivo de derivación / demanda | — | Por qué llega al centro y qué pide |
| Antecedentes relevantes | — | Historia psicopatológica, consumos, traumas... |
| Hipótesis / impresión inicial | — | Formulación clínica provisional |
| Riesgo / alertas | — | Riesgo suicida, heteroagresividad, autolesiones... |
| Recomendaciones / plan inicial | — | Objetivos, frecuencia de sesiones, derivaciones |

**Vincular un formulario de evaluación estandarizado:**
1. Selecciona una **Plantilla** (solo plantillas publicadas del módulo `cs_patient_followup_forms`)
2. Se crea automáticamente una evaluación vinculada
3. Rellena las escalas o ítems del formulario desde ese vínculo
4. El formulario puede generarse en PDF

**Adjuntos:** sube informes psicológicos previos, test proyectivos escaneados, documentación clínica.

### 1.2 Estados

| Estado | Descripción |
|--------|-------------|
| `Borrador` | En elaboración |
| `Cerrada` | Evaluación finalizada y firmada |

Haz clic en **"Cerrar evaluación"** para pasar a estado Cerrada.  
Haz clic en **"Reabrir"** si necesitas editarla de nuevo.

[SCREENSHOT: Evaluación inicial con hipótesis y riesgo rellenos]

---

## Parte 2 — Sesiones de psicología

### ¿Qué es una sesión?
Registro de cada encuentro terapéutico. Al crear o modificar una sesión, el sistema **sincroniza automáticamente** una cita en el calendario de Odoo.

### 2.1 Crear una sesión

**Ruta:** `Psicología > Sesiones > Nuevo`

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Residente | ✓ | Paciente |
| Fecha y hora | ✓ | Inicio de la sesión |
| Duración (min) | — | Por defecto 50 minutos |
| Psicólogo/a | — | Trabajador con puesto "Psicólogo" |
| Tipo de sesión | — | Individual / Familiar / Grupal / Coordinación |
| Resumen / objetivos | — | Qué se trabajó o qué se pretende |
| Notas clínicas | — | Registro clínico de la sesión (confidencial) |

**Vincular formulario de evaluación:** igual que en la evaluación inicial — selecciona plantilla y se crea la evaluación vinculada.

**Adjuntos:** materiales terapéuticos, informes, test aplicados.

### 2.2 Sincronización automática con el calendario

Al guardar la sesión, el sistema crea o actualiza automáticamente una **cita en el calendario de Odoo** con:
- Título: `Psicología — [Nombre residente] ([Tipo])`
- Inicio y fin calculado con la duración
- Participantes: residente + psicólogo
- Ubicación: residencia y habitación del residente
- Privacidad: confidencial
- Estado: ocupado

> Si modificas la fecha/hora en el **calendario**, la sesión se actualiza automáticamente también. La sincronización es bidireccional.

Para abrir la cita en el calendario desde la ficha de la sesión: botón **"Ver cita en calendario"**.

### 2.3 Estados de la sesión

```
[Planificada] → [Realizada]
             ↘ [Cancelada] → [Planificada]
```

- **"Marcar como realizada"** — registra que la sesión se celebró
- **"Cancelar"** — la sesión no tuvo lugar (el evento de calendario se archiva)
- **"Reabrir"** — vuelve a estado planificada

### 2.4 Ver sesiones desde la ficha del residente

En la ficha del residente (`Centro Sanitario > Residentes`), el contador **"Sesiones Psicología (N)"** en la cabecera abre directamente la lista de todas las sesiones de ese residente.

[SCREENSHOT: Lista de sesiones con tipos y estados]

---

## Parte 3 — Citas en el calendario

**Ruta:** `Psicología > Citas (calendario)`

Vista filtrada del calendario de Odoo que muestra **solo las citas de psicología** del centro.

### Vistas disponibles:
- **Mes** — visión general del mes
- **Semana** — planificación semanal
- **Día** — agenda del día
- **Lista** — listado cronológico

### Crear una sesión desde el calendario:
1. Haz clic en un hueco del calendario
2. Se crea un evento marcado como visita psicológica
3. Rellena residente y psicólogo
4. Al guardar, se crea automáticamente la sesión (`cs.psychology.session`) vinculada

### Campos adicionales en la cita (visibles en el formulario del evento):
| Campo | Descripción |
|-------|-------------|
| Residente | Paciente — al seleccionarlo autocompleta residencia y habitación |
| Residencia | Centro |
| Habitación | Habitación del residente |
| Psicólogo/a | Profesional asignado |
| Tipo de visita | Individual / Familiar / Grupal / Coordinación / Otro |

> Cambiar fecha/hora arrastrando la cita en el calendario actualiza automáticamente la fecha de la sesión vinculada.

---

## Parte 4 — Llamadas y contactos familiares

### ¿Qué es un contacto familiar?
Registro de cada comunicación con la familia del residente — llamadas, videollamadas, visitas presenciales. Visible tanto desde el menú de psicología como desde el bloque **"Psicología — Llamadas y contactos familiares"** en la ficha del residente.

### 4.1 Registrar una llamada familiar

**Ruta:** `Psicología > Contactos familia > Nuevo`  
O desde la ficha del residente → bloque "Llamadas y contactos familiares" → **"Añadir una línea"**

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Residente | ✓ | Paciente sobre quien se comunica |
| Fecha y hora | ✓ | Momento del contacto |
| Persona contactada | ✓ | Nombre (texto libre o desde familiar vinculado) |
| Familiar vinculado | — | Sub-contacto del residente en Odoo (autocompleta el nombre) |
| Relación con el residente | — | Madre, padre, hermano, tutor... |
| Canal | — | Teléfono / Videollamada / Presencial / Otro |
| Duración (min) | — | Minutos de la comunicación |
| Resultado | — | Información / Coordinación / Incidencia / Apoyo emocional / Otro |
| Notas | — | Contenido del contacto |
| Profesional | — | Persona del centro que realizó el contacto |

**Familiar vinculado vs. nombre libre:**
- Si el familiar ya es sub-contacto del residente en Odoo: selecciónalo en "Familiar vinculado" — el nombre se autocompleta
- Si no está en el sistema: deja vacío "Familiar vinculado" y escribe el nombre directamente en "Persona contactada"

### 4.2 Ver todas las llamadas de un residente desde su ficha

En la ficha del residente (`Centro Sanitario > Residentes`), al final del formulario aparece el bloque:

**"Psicología — Llamadas y contactos familiares"**

Muestra la lista de todos los contactos familiares registrados para ese residente con fecha, persona, canal y resultado. Puedes añadir nuevos directamente desde ahí.

[SCREENSHOT: Bloque llamadas familiares en ficha residente]

---

## Flujo típico completo

### Escenario: Seguimiento semanal de un residente

**Lunes — Planificar sesiones de la semana:**
1. `Psicología > Citas (calendario)` → vista semanal
2. Haz clic en el miércoles a las 10:00 → crea cita para el residente
3. La sesión queda planificada con evento en el calendario

**Miércoles — Realizar la sesión:**
1. `Psicología > Sesiones` → abre la sesión planificada
2. Rellena "Notas clínicas" con lo trabajado
3. Si se aplicó algún test: selecciona plantilla, rellena la evaluación
4. Haz clic en **"Marcar como realizada"**

**Jueves — Llamada a la familia:**
1. `Psicología > Contactos familia > Nuevo`
2. Residente + fecha/hora + Familiar vinculado (o nombre libre)
3. Canal: Teléfono — Resultado: Coordinación
4. Notas: resumen de lo comunicado

**Viernes — Revisar evaluación inicial si es residente nuevo:**
1. `Psicología > Evaluación inicial` → abre la evaluación del residente
2. Actualiza hipótesis o plan si ha cambiado
3. Cierra la evaluación

---

## Casos de uso frecuentes

### "El psicólogo nuevo no aparece en el campo Psicólogo/a"
El puesto del trabajador debe ser exactamente `psicólogo` (en minúsculas). Revisa en `Centro Sanitario > Trabajadores > [trabajador] > Puesto de Trabajo`.

### "Quiero ver todas las sesiones del mes de un residente"
1. `Psicología > Sesiones`
2. Busca por nombre del residente
3. Agrupa por fecha o filtra por mes desde la barra de búsqueda

### "Una sesión fue cancelada pero sigue en el calendario"
Al cancelar la sesión, el evento de calendario se archiva (no se borra, queda inactivo). Para verlo: en el calendario de Odoo, activa los filtros de eventos archivados.

### "Quiero registrar una visita familiar presencial"
1. `Psicología > Contactos familia > Nuevo`
2. Canal: `Presencial`
3. Resultado: según el contenido de la visita
4. Anota en "Notas" lo relevante clínicamente

### "La sesión se creó en el calendario sin el residente como participante"
Ocurre si el residente no tiene contacto (`partner_id`) vinculado. Verifica en la ficha del residente que el campo "Contacto (Paciente)" no está vacío.

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| El psicólogo no aparece en el campo | Puesto no es "psicólogo" exacto | Revisa el puesto en `Centro Sanitario > Trabajadores` |
| La sesión no crea evento en calendario | El módulo `calendar` no está activo | Verifica en Ajustes > Aplicaciones que el módulo Calendario está instalado |
| "Persona contactada" es obligatorio | Falta nombre al registrar llamada | Selecciona familiar vinculado (autocompleta) o escribe el nombre manualmente |
| El bloque de llamadas no aparece en la ficha del residente | Módulo `cs_psychology` no instalado | Instala el módulo |
| Cambio de hora en calendario no actualiza la sesión | Solo se sincronizan cambios en `start`/`stop`/`duration` | Otros campos (notas, tipo) se editan desde `Psicología > Sesiones` |
