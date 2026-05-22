# Guía de Usuario — cs_medical_care
## Atención Médica

**Módulo:** `cs_medical_care` v1.1.0  
**Perfil:** Médicos, enfermería, monitoras (PRN)  
**Menú principal:** `Centro Sanitario > Atención Médica`

---

## ¿Para qué sirve?

Centraliza toda la actividad clínica del residente en un único módulo:
- Consultas médicas con diagnóstico y codificación CIE-10
- Prescripciones farmacológicas (pauta de medicación)
- Tratamientos (heridas, fisioterapia, rehabilitación...)
- Analgesia y control del dolor
- Rescates asistenciales (crisis, caídas, urgencias)
- Rescates PRN farmacológicos (administración puntual por monitoras)
- Tests y pruebas clínicas (laboratorio, imagen, ECG...)
- Seguimientos planificados
- Historia clínica de texto libre
- **Hoja de emergencias** imprimible con toda la información crítica

Todo queda vinculado a la ficha del residente y accesible desde contadores (smart buttons) en su ficha.

---

## Acceso al módulo

```
Menú superior → Centro Sanitario → Atención Médica
```

Submenús disponibles:
| Submenú | Modelo | Perfil |
|---------|--------|--------|
| Consultas Médicas | `cs.medical.consultation` | Médico / Enfermero |
| Prescripciones | `cs.prescription` | Médico |
| Rescates | `cs.medical.rescue` | Médico / Enfermero / Cuidador |
| Analgesia | `cs.medical.analgesia` | Médico / Enfermero |
| Tratamientos | `cs.medical.treatment` | Médico / Enfermero / Fisioterapeuta |
| Tests / pruebas | `cs.medical.clinic.test` | Médico / Enfermero |
| Seguimiento | `cs.medical.followup` | Médico / Enfermero |
| Historia clínica (básica) | `cs.medical.history` | Todos los sanitarios |
| Rescates PRN (monitoras) | `cs.medical.prn.rescue` | Monitoras / Enfermería |

---

## Acceso desde la ficha del residente

Todos los registros médicos están también accesibles directamente desde `Centro Sanitario > Residentes > [residente]` mediante **contadores en la cabecera** (smart buttons):

| Contador | Qué abre |
|----------|----------|
| Prescripciones activas / Total | Lista de prescripciones del residente |
| Consultas (N) | Lista de consultas médicas |
| Historial (N) | Historia clínica básica |
| Rescates (N) | Rescates asistenciales |
| Analgesia (N) | Registros de analgesia |
| Tests (N) | Pruebas clínicas |
| Tratamientos (N) | Tratamientos activos y planificados |
| Seguimientos pendientes (N) | Revisiones pendientes |

> Los contadores se actualizan en tiempo real. Un número en rojo indica elementos que requieren atención.

---

## Parte 1 — Consultas Médicas

### ¿Qué es una consulta médica?
Registro de cada visita o acto médico. Es el punto de entrada habitual — desde una consulta puedes generar prescripciones, tratamientos, tests y seguimientos vinculados.

### 1.1 Crear una consulta médica

**Ruta:** `Centro Sanitario > Atención Médica > Consultas Médicas > Nuevo`

**Campos obligatorios:**
| Campo | Descripción |
|-------|-------------|
| Residente | Paciente atendido |
| Profesional Médico | Médico o enfermero que realiza la consulta (filtrado por puesto) |
| Fecha y Hora | Se pre-rellena con el momento actual |

**Tipo de consulta:**
- `General` — consulta rutinaria
- `Seguimiento` — revisión de problema anterior
- `Urgencia` — atención urgente
- `Especializada` — interconsulta o especialista externo

**Campos clínicos:**
| Campo | Descripción |
|-------|-------------|
| Motivo de Consulta | Síntomas o razón de la visita |
| Diagnóstico | Texto libre del diagnóstico |
| Código CIE-10 | Código estandarizado (ej: `F10.2`) |
| Diagnóstico CIE-10 | Nombre del diagnóstico CIE-10 |
| Observaciones Clínicas | Notas adicionales |

**Vincular un formulario de evaluación:**
Si el módulo `cs_patient_followup_forms` está activo, puedes seleccionar una **Plantilla de Evaluación**. Al seleccionarla, el sistema crea automáticamente una evaluación vinculada a la consulta que se puede rellenar y generar en PDF.

### 1.2 Flujo de estados de una consulta

```
[Programada] → [En Curso] → [Completada]
                           ↘ [Cancelada]
```

- Haz clic en **"En curso"** cuando empieces la consulta
- Haz clic en **"Completada"** al terminar — si hay evaluación vinculada, también la marca como completada
- Usa **"Cancelar"** si la consulta no se celebró

[SCREENSHOT: Consulta médica con diagnóstico, CIE-10 y estado completada]

---

## Parte 2 — Prescripciones

### ¿Qué es una prescripción?
Documento de pauta farmacológica. Contiene uno o más medicamentos con dosis, frecuencia y vía de administración. Si tienes el módulo `cs_cima` instalado, los medicamentos pueden vincularse al catálogo oficial AEMPS.

### 2.1 Crear una prescripción

**Ruta:** `Centro Sanitario > Atención Médica > Prescripciones > Nuevo`

**Campos obligatorios:**
| Campo | Descripción |
|-------|-------------|
| Residente | Paciente |
| Médico Prescriptor | Solo acepta trabajadores con puesto "Médico" |
| Fecha Prescripción | Fecha de inicio de la pauta |

**Vincular a consulta:** (opcional) selecciona la consulta que genera esta prescripción para tener trazabilidad completa.

### 2.2 Añadir medicamentos (líneas de prescripción)

En el bloque **"Medicamentos"**, haz clic en **"Añadir una línea"** por cada fármaco:

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Nombre del Medicamento | ✓ | Nombre del fármaco |
| Dosis | ✓ | Ej: `500 mg`, `2 comprimidos`, `1 ampolla` |
| Frecuencia | ✓ | Cada 8h, una vez al día, según necesidad... |
| Vía | — | Oral (defecto), IM, IV, SC, tópica, inhalada |
| Duración (días) | — | Número de días del tratamiento |
| Notas | — | Instrucciones específicas para esta línea |

**Frecuencias disponibles:**
`Cada hora / 2h / 4h / 6h / 8h / 12h / Una vez al día / Dos veces / Tres veces / Cuatro veces / Según sea necesario`

### 2.3 Estados de la prescripción

```
[Borrador] → [Activa] → [Pausada] → [Activa]
                      ↘ [Finalizada]
                      ↘ [Cancelada]
```

| Estado | Uso |
|--------|-----|
| `Borrador` | En preparación, no aplicada aún |
| `Activa` | Pauta en vigor — aparece en la hoja de emergencias |
| `Pausada` | Suspensión temporal (ej: ingreso hospitalario) |
| `Finalizada` | Ciclo de tratamiento completado |
| `Cancelada` | Prescripción anulada |

> Solo las prescripciones en estado **Activa** aparecen en la **Hoja de Emergencias**.

**Instrucciones especiales:** campo libre al final para indicaciones globales de la prescripción (ej: "Tomar con comida", "No partir el comprimido").

[SCREENSHOT: Prescripción con 3 líneas de medicamento, estado activa]

---

## Parte 3 — Tratamientos

### ¿Qué es un tratamiento?
Protocolo de actuación no ligado línea a línea a la medicación diaria. Útil para curas de heridas, planes de fisioterapia, pautas nutricionales, etc.

### 3.1 Crear un tratamiento

**Ruta:** `Centro Sanitario > Atención Médica > Tratamientos > Nuevo`

**Campos obligatorios:**
| Campo | Descripción |
|-------|-------------|
| Residente | Paciente |
| Título tratamiento | Nombre descriptivo (ej: `Cura úlcera presión talón derecho`) |
| Tipo | Farmacológico / Heridas / Fisioterapia / Respiratorio / Nutrición / Otro |
| Inicio | Fecha de inicio |

**Ítems del tratamiento:** añade las acciones concretas con descripción, dosis/cantidad, pauta/frecuencia y vía.

**Estados:** `Planificado → Activo → Completado / Suspendido`

---

## Parte 4 — Analgesia

### ¿Qué es un registro de analgesia?
Documenta cada administración de medicación analgésica o medida de control del dolor, con escala EVA antes y después.

### 4.1 Registrar analgesia

**Ruta:** `Centro Sanitario > Atención Médica > Analgesia > Nuevo`

| Campo | Descripción |
|-------|-------------|
| Residente | Paciente |
| Fecha y hora administración | Momento exacto |
| EVA antes (0–10) | Escala de dolor antes de la intervención |
| Medicación / medida | Fármaco o medida no farmacológica |
| Dosis | Cantidad administrada |
| Vía | Oral, IM, IV, SC, tópica, inhalada, otra |
| Profesional | Médico o enfermero que administra |
| EVA después (0–10) | Dolor tras la intervención (rellena más tarde si es necesario) |
| Observaciones | Notas adicionales |

Puede vincularse a una **consulta** y/o a una **prescripción** para trazabilidad.

> Las escalas EVA deben ser valores entre 0 y 10. El sistema lo valida al guardar.

---

## Parte 5 — Rescates asistenciales

### ¿Qué es un rescate asistencial?
Registro de una intervención urgente ante una situación de riesgo físico o psíquico del residente (caída, convulsión, crisis de agitación, dolor torácico, etc.).

> **Distinción importante:** El rescate asistencial es para **intervenciones de emergencia**. Para administración puntual de medicación "según necesidad" por monitoras, usa los [Rescates PRN](#parte-7--rescates-prn-monitoras).

### 5.1 Registrar un rescate asistencial

**Ruta:** `Centro Sanitario > Atención Médica > Rescates > Nuevo`

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Residente | ✓ | Paciente |
| Fecha y hora | ✓ | Momento de la intervención |
| Tipo de situación | ✓ | Ver tabla abajo |
| Lugar | — | Habitación, sala, jardín... |
| Hallazgos / circunstancias | — | Qué pasó exactamente |
| Actuación realizada | — | Protocolo aplicado, primeros auxilios... |
| Desenlace | — | Resuelto en centro / Observación / Traslado a hospital / Otro |
| Notas del desenlace | — | Detalles del desenlace |
| Profesional que registra | — | Filtrado por puestos sanitarios/dirección |
| Consulta relacionada | — | Consulta médica generada por este rescate |
| Adjuntos | — | Informes, fotos clínicas autorizadas |

**Tipos de situación:**
| Código | Descripción |
|--------|-------------|
| `Caída` | Caída con o sin lesión |
| `Convulsión / crisis` | Crisis epiléptica u otro tipo |
| `Atragantamiento` | Obstrucción de vía aérea |
| `Alteración de consciencia` | Síncope, confusión aguda... |
| `Dolor torácico` | Posible evento cardíaco |
| `Hemorragia relevante` | Sangrado que requiere atención |
| `Agitación / comportamiento de riesgo` | Crisis conductual con riesgo |
| `Otro` | Cualquier otra urgencia |

[SCREENSHOT: Rescate asistencial de caída con hallazgos y desenlace rellenos]

---

## Parte 6 — Tests y pruebas clínicas

### ¿Qué es un test clínico?
Registro de una prueba diagnóstica (análisis de sangre, radiografía, ECG, prueba cognitiva...) con sus resultados.

### 6.1 Registrar un test clínico

**Ruta:** `Centro Sanitario > Atención Médica > Tests / pruebas > Nuevo`

| Campo | Descripción |
|-------|-------------|
| Residente | Paciente |
| Fecha | Fecha de la prueba o de recepción de resultados |
| Tipo | Laboratorio / Imagen / Funcional / Cognitivo / ECG / Otra |
| Nombre / estudio | Denominación (ej: `Hemograma completo`, `Radiografía tórax`) |
| Resultado / conclusiones | Texto libre con los resultados |
| Solicitado por | Médico o enfermero que pidió la prueba |
| Informes adjuntos | PDFs, imágenes del resultado |

---

## Parte 7 — Rescates PRN (monitoras)

### ¿Qué es un rescate PRN?
Registro de la administración de medicación **puntual por protocolo** ("pro re nata" = según necesidad) realizada por una monitora o enfermera. Diferente del rescate asistencial: aquí no hay emergencia física, sino una medicación de rescate prevista en el plan terapéutico del paciente.

Ejemplos: ansiolítico de rescate nocturno, antihistamínico por reacción leve, paracetamol puntual.

> Si el módulo `cs_cima` está instalado, el campo medicamento puede vincularse al catálogo oficial AEMPS (la extensión `cs_cima` añade este campo).

### 7.1 Registrar un rescate PRN

**Ruta:** `Centro Sanitario > Atención Médica > Rescates PRN (monitoras) > Nuevo`

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Residente | ✓ | Paciente |
| Fecha y hora | ✓ | Momento de la administración |
| Medicamento | ✓ | Nombre del fármaco (texto libre) |
| Dosis | ✓ | Cantidad administrada |
| Vía de administración | ✓ | Oral (defecto), Sublingual, IM, IV, SC, Tópica, Inhalada, Otro |
| Motivo PRN | ✓ | Por qué se administró (síntoma concreto) |
| Administrado por | — | Monitora o profesional |
| Efecto observado | — | Cómo respondió el paciente |

### 7.2 Confirmar el registro PRN

Los registros se crean en estado **Borrador**. Una vez revisados:
1. Abre el registro
2. Haz clic en **"Confirmar"**
3. El estado cambia a `Registrado`

> Los PRN en borrador son visibles para enfermería, que puede revisar y confirmar al final del turno.

---

## Parte 8 — Seguimiento médico

### ¿Qué es un seguimiento?
Recordatorio planificado de una revisión o control futuro. Permite que el médico programe "revisar tensión en 15 días" o "cita de seguimiento postalta".

### 8.1 Crear un seguimiento

**Ruta:** `Centro Sanitario > Atención Médica > Seguimiento > Nuevo`

| Campo | Descripción |
|-------|-------------|
| Residente | Paciente |
| Motivo / tema | Qué se va a revisar |
| Próxima fecha revisión | Cuándo |
| Indicaciones | Qué vigilar, qué preparar |
| Coordinador | Médico o enfermero responsable |
| Consulta origen | Consulta que genera este seguimiento |

**Estados:** `Pendiente → Realizado / Cancelado`

Al marcar como **Realizado**: rellena la "Fecha realización".

> El contador "Seguimientos pendientes" en la ficha del residente solo cuenta los que están en estado `Pendiente` — ideal para ver a quién hay que llamar esta semana.

---

## Parte 9 — Historia clínica (básica)

### ¿Qué es la historia clínica básica?
Registro de texto libre para cualquier evento clínico que no encaje en los formularios específicos. También permite registrar constantes vitales puntuales.

### 9.1 Añadir una entrada al historial

**Ruta:** `Centro Sanitario > Atención Médica > Historia clínica (básica) > Nuevo`

**Tipo de registro:**
`Consulta Médica / Diagnóstico / Medicación / Procedimiento / Resultados Laboratorio / Nota de Enfermería / Otro`

**Constantes vitales (opcionales):**
| Campo | Descripción |
|-------|-------------|
| Temperatura (°C) | |
| Presión Arterial (mmHg) | Texto libre (ej: `120/80`) |
| Frecuencia Cardíaca (bpm) | |
| Frecuencia Respiratoria (rpm) | |
| Saturación O2 (%) | |
| Peso (kg) | |
| Altura (cm) | |

**Marcar como confidencial:** el campo "Información Confidencial" oculta el registro a usuarios sin permisos específicos.

---

## Parte 10 — Hoja de Emergencias

### ¿Qué es la hoja de emergencias?
Documento PDF imprimible con toda la información médica crítica del residente en una sola hoja. Diseñada para ser entregada a servicios de emergencias o en traslados hospitalarios.

### Contenido de la hoja:
- Datos personales del residente
- Alergias conocidas (obtenidas de la admisión o del PIAI)
- Prescripciones **activas** con dosis, frecuencia y vía
- Tratamientos activos y planificados
- Últimos 5 diagnósticos médicos con código CIE-10
- Últimos 5 rescates asistenciales
- Últimos 5 rescates PRN farmacológicos
- Evaluación psicológica más reciente
- Últimas 10 entradas de historia clínica

### Imprimir la hoja de emergencias:

1. Ve a `Centro Sanitario > Residentes` y abre la ficha del residente
2. Busca el botón **"Imprimir hoja de emergencias"** (en la barra de acciones o smart buttons)
3. Se genera un PDF descargable con toda la información crítica actualizada

> La hoja siempre refleja el estado actual del sistema — imprímela justo antes de un traslado para que sea la más reciente.

---

## Flujo típico completo

### Escenario: Consulta de seguimiento semanal

1. `Atención Médica > Consultas Médicas > Nuevo`
   - Residente + Médico + Tipo: "Seguimiento"
   - Motivo: "Control tensión arterial. Refiere cefalea matutina."
   - Diagnóstico: "HTA no controlada"
   - CIE-10: `I10` / "Hipertensión esencial"
   - → Marcar "En curso" → atender → "Completada"

2. Desde la misma consulta, **nueva prescripción:**
   - `Atención Médica > Prescripciones > Nuevo`
   - Médico + Residente + vincular a consulta anterior
   - Línea: Enalapril 10mg / Una vez al día / Oral
   - → Activar prescripción

3. **Crear seguimiento para dentro de 2 semanas:**
   - `Atención Médica > Seguimiento > Nuevo`
   - Motivo: "Control TA tras ajuste de Enalapril"
   - Fecha: 2 semanas desde hoy
   - Consulta origen: la consulta de hoy

4. **Imprimir hoja de emergencias** actualizada para el expediente físico del residente.

---

## Casos de uso frecuentes

### "El residente se ha caído en el baño"
1. `Atención Médica > Rescates > Nuevo`
2. Tipo: `Caída` — Lugar: "Baño habitación 104"
3. Hallazgos: descripción de la caída y lesiones observadas
4. Actuación: protocolo aplicado
5. Desenlace: `Resuelto en centro` o `Traslado a hospital`
6. Si precisa consulta médica: créala y vincúlala al rescate

### "Una monitora administra un ansiolítico de rescate a las 2am"
1. `Atención Médica > Rescates PRN (monitoras) > Nuevo`
2. Residente + fecha/hora + Medicamento: "Lorazepam 1mg" + Dosis + Vía: Oral
3. Motivo PRN: "Agitación nocturna intensa, no cede con medidas no farmacológicas"
4. Efecto observado: rellenar al rato ("Se tranquilizó en 30 min")
5. La mañana siguiente, enfermería lo revisa y → **Confirmar**

### "Quiero ver todas las prescripciones activas de un residente"
1. Abre la ficha del residente
2. Haz clic en el contador **"Prescripciones activas"** en la cabecera
3. Se filtra automáticamente por ese residente y estado activo

### "El médico quiere saber cuántos rescates ha tenido un residente este mes"
1. `Atención Médica > Rescates`
2. Busca por nombre de residente
3. Filtra por fecha: "Desde: 01/05/2026"
4. El contador inferior muestra el total

### "Hay que entregar un resumen médico al hospital"
1. Abre la ficha del residente
2. Haz clic en **"Imprimir hoja de emergencias"**
3. Descarga el PDF — contiene toda la información crítica actualizada

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| No aparece el médico en "Profesional Médico" | El trabajador no tiene puesto "Médico" o "Enfermero" | Revisa la ficha del trabajador en `Centro Sanitario > Trabajadores` |
| No aparece en "Médico Prescriptor" | El trabajador no tiene puesto exactamente "Médico" (las prescripciones filtran solo médicos) | El puesto debe ser "Médico" en la ficha del trabajador |
| "Las escalas de dolor deben estar entre 0 y 10" | Valor de EVA fuera de rango | Introduce un número entre 0 y 10 |
| La hoja de emergencias no muestra alergias | No se registraron en la admisión ni en el PIAI | Añade las alergias en el campo "Alergias conocidas" de la ficha del residente (campo herencia de admisión) |
| Prescripción no aparece en hoja de emergencias | Estado no es "Activa" | Asegúrate de activar la prescripción con el botón "Activa" |
| El contador de seguimientos pendientes no baja | El seguimiento no está marcado como "Realizado" | Abre el seguimiento y cambia el estado a "Realizado" |
