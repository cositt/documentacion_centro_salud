# Guía de usuario — cs_piai: Plan Individualizado de Atención Integral

## ¿Para qué sirve este módulo?

El **PIAI** (Plan Individualizado de Atención Integral) es el documento clínico central del proceso terapéutico de cada residente. Agrupa en un único expediente:

- La **valoración inicial** multidisciplinar por áreas (psicológica, sanitaria, social, familiar, etc.)
- El **diagnóstico y formulación** del caso
- Los **objetivos terapéuticos** por área con indicadores de seguimiento
- Las **intervenciones** planificadas (tipo, frecuencia, responsable)
- Los **riesgos y alertas clínicas** (autolítico, fuga, recaída…)
- El **plan familiar y de restricciones**
- Las **revisiones periódicas** (ordinarias y extraordinarias)
- Las **notas de evolución** cotidianas
- El **plan de prevención de recaídas**
- El **plan de alta y continuidad**
- Las **firmas y validaciones** del equipo

Además, el PIAI integra automáticamente registros de otros módulos del sistema: consultas médicas, prescripciones, rescates asistenciales, sesiones de psicología y llamadas familiares del residente.

---

## Acceso al módulo

> Menú principal → **PIAI**

Submenús según el perfil del usuario:

| Submenú | Visible para | Contenido |
|---------|-------------|-----------|
| **Todos los PIAIs** | Dirección, Psicología, Social, Médico, Admisión | Lista completa de PIAIs del centro |
| **Residentes** | Monitoras | Vista simplificada con información de restricciones por residente |

---

## Parte 1 — Ciclo de vida del PIAI

```
Borrador ──► Pendiente de Validación ──► Activo
               (equipo completa el plan)       │
                                               ▼
                                          En Revisión
                                               │
                              ┌────────────────┤
                              ▼                │
                       Cerrado — Alta          │
                       Terapéutica             │
                       Alta Voluntaria    ◄────┘
                       Derivado
                       Expulsión
```

| Estado | Significado |
|--------|-------------|
| **Borrador** | PIAI creado, en proceso de elaboración |
| **Pendiente de Validación** | Plan completo, esperando revisión y firma del equipo |
| **Activo** | PIAI vigente — el residente está en tratamiento activo |
| **En Revisión** | Proceso de revisión periódica o extraordinaria en curso |
| **Cerrado — Alta Terapéutica** | Residente ha completado el programa satisfactoriamente |
| **Cerrado — Alta Voluntaria** | Residente abandona por decisión propia |
| **Cerrado — Derivado** | Residente trasladado a otro recurso |
| **Cerrado — Expulsión** | Alta disciplinaria |

> **Restricción crítica:** Solo puede haber **un PIAI activo** por residente. Para activar un nuevo PIAI hay que cerrar el anterior.

---

## Parte 2 — Crear un PIAI

### Creación automática desde admisión

El PIAI se crea automáticamente al completar el proceso de admisión (cs_admission). En ese momento queda en estado **Borrador** con el residente vinculado.

### Creación manual

1. **PIAI** → **Todos los PIAIs** → **Nuevo**.
2. Campos de cabecera:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Residente** | Sí | El residente al que pertenece el plan |
| **Fase Terapéutica** | Sí | Fase actual del proceso (ver tabla abajo) |
| **Profesional Referente** | Sí (para activar) | Trabajador responsable del seguimiento del PIAI |
| **Fecha de Elaboración** | Sí | Fecha de inicio de la elaboración del plan |
| **Fecha Próxima Revisión** | Sí (para activar) | Cuándo se hará la primera revisión ordinaria |
| **Observaciones Generales** | No | Texto libre de contexto general |
| **Consentimiento LOPD firmado** | No | Marca si el residente ha firmado el consentimiento de protección de datos |

### Fases terapéuticas disponibles

| Fase | Momento típico |
|------|---------------|
| Acogida / Admisión | Primeros días del internamiento |
| Evaluación | Período inicial de valoración |
| Desintoxicación | Proceso de desintoxicación activa |
| Deshabituación | Trabajo de deshabituación y craving |
| Rehabilitación | Fase central del proceso terapéutico |
| Reinserción Social | Preparación para la vida en comunidad |
| Preparación al Alta | Últimas semanas antes del alta |
| Seguimiento Post-Alta | Seguimiento externo tras el alta |

---

## Parte 3 — Valoraciones Iniciales

Las valoraciones iniciales son la radiografía de partida del residente al ingresar: qué necesidades tiene en cada área, qué riesgos presenta y cuál es la prioridad de intervención.

**Acceso:** En el PIAI, pestaña **Valoraciones Iniciales** → añadir una fila por área valorada.

| Campo | Descripción |
|-------|-------------|
| **Área** | Área de valoración (ver lista abajo) |
| **Fecha de Valoración** | Fecha en que se realizó la valoración |
| **Profesional Valorador** | Quién realizó la valoración |
| **Prioridad** | Baja / Media / Alta / Crítica |
| **Riesgos Detectados** | Riesgos identificados en esta área |
| **Necesidades Detectadas** | Necesidades específicas a abordar |

Según el **Área** seleccionada, aparecen campos adicionales específicos:

| Área | Campos adicionales destacados |
|------|------------------------------|
| **Psicológica** | Sustancia principal, edad inicio, motivación al cambio, craving, riesgo autolítico/heteroagresivo, impulsividad |
| **Sanitaria/Médica** | Antecedentes médicos, patologías activas, alergias, medicación al ingreso, signos de abstinencia |
| **Psiquiátrica** | Diagnóstico psiquiátrico previo, patología dual, estabilidad psiquiátrica |
| **Social** | Situación familiar, red de apoyo, situación económica, habitacional y laboral |
| **Familiar** | Personas implicadas, dinámica familiar, autorización de información, contacto de emergencia |
| **Educativa** | Nivel educativo, habilidades sociales, autonomía personal |

> **Recomendación:** Completar al menos las áreas Psicológica, Sanitaria y Social al inicio. Las demás áreas pueden completarse en los primeros días del internamiento.

---

## Parte 4 — Diagnóstico / Formulación

Pestaña **Diagnóstico / Formulación**: descripción narrativa del caso con los diagnósticos clínicos (CIE-10 si aplica) y la formulación psicológica del problema.

---

## Parte 5 — Objetivos Terapéuticos

Los objetivos son los resultados concretos que se quieren conseguir con el residente en cada área.

**Acceso:** En el PIAI, pestaña **Objetivos**.

| Campo | Descripción |
|-------|-------------|
| **Objetivo** | Descripción del objetivo (redactado en positivo y observable) |
| **Área** | A qué área terapéutica pertenece |
| **Estado** | No iniciado → En progreso → Conseguido / Parcialmente / No conseguido / Suspendido / Reformulado |
| **Responsable** | Profesional que lidera este objetivo |
| **Indicador de Seguimiento** | Cómo se medirá si el objetivo se ha conseguido |
| **Fecha de Inicio / Prevista / Real** | Seguimiento temporal del objetivo |

**Áreas disponibles para objetivos:** Adicciones, Psicológica, Psiquiátrica, Médica/Sanitaria, Social, Educativa, Familiar, Laboral, Ocio y Tiempo Libre, Convivencial, Judicial/Legal, Actividad física, Prevención de recaídas, Alta / Reinserción, Espiritual/Cultural, Otro.

> Para **activar** el PIAI se requiere al menos un objetivo en estado no suspendido.

---

## Parte 6 — Intervenciones

Las intervenciones son las acciones terapéuticas planificadas para conseguir los objetivos.

**Acceso:** En el PIAI, pestaña **Intervenciones**.

| Campo | Descripción |
|-------|-------------|
| **Área** | Área de la intervención |
| **Tipo de Intervención** | (ver lista abajo) |
| **Objetivos Asociados** | Qué objetivos persigue esta intervención |
| **Descripción** | Detalle de cómo se implementará |
| **Frecuencia** | Diaria / Semanal / Quincenal / Mensual / Según necesidad |
| **Responsable** | Profesional que la ejecuta |
| **Fechas** | Inicio y fin planificados |
| **Estado** | Activa / Suspendida / Finalizada |

Tipos de intervención disponibles (selección): Psicoterapia Individual, Psicoterapia Grupal, Entrevista Motivacional, Prevención de Recaídas, Terapia Cognitivo-Conductual, Terapia Familiar, Habilidades Sociales, Terapia Ocupacional, Trabajo Social, Cuidados de Enfermería, Seguimiento Psiquiátrico, Seguimiento Médico, Psicoeducación, Control Toxicológico, Actividad Deportiva, Talleres, Asamblea, Derivación a Recurso Externo, Mindfulness, entre otros.

---

## Parte 7 — Riesgos y Alertas Clínicas

Los riesgos identifican situaciones que requieren vigilancia especial y tienen protocolo de actuación definido.

**Acceso:** En el PIAI, pestaña **Riesgos y Alertas**.

| Campo | Descripción |
|-------|-------------|
| **Tipo de Riesgo** | Autolítico/Suicida, Heteroagresivo, Fuga/Abandono, Recaída, Intoxicación Aguda, Abstinencia, Médico/Físico, Psiquiátrico, Judicial, Familiar, Convivencial, Otro |
| **Nivel de Riesgo** | Bajo / Moderado / Alto / Crítico |
| **Descripción del Riesgo** | Qué factores concretos generan este riesgo |
| **Medidas Preventivas** | Acciones para prevenir que se materialice |
| **Plan de Actuación** | Qué hacer si el riesgo se materializa |
| **Responsable** | Quien monitoriza este riesgo |
| **Fechas** | Identificación, revisión prevista, última revisión |
| **Estado** | Activo / Resuelto / En seguimiento |

### Alertas automáticas del sistema (cron diario)

El sistema genera actividades automáticas (tareas en el chatter) cuando:

| Situación | Alerta |
|-----------|--------|
| Riesgo **Crítico** sin revisión en **48 horas** | Actividad urgente en el PIAI |
| Riesgo **Alto** sin revisión en **7 días** | Actividad de aviso |
| PIAI en **Borrador** más de **7 días** | Recordatorio de completar |
| **Revisión periódica vencida** | Actividad en el PIAI |
| **Objetivo vencido** (fecha prevista pasada, en progreso) | Actividad de aviso |
| PIAI **Activo** sin **firma de validación inicial** | Actividad para completar firma |
| Revisión próxima en **30 días** sin plan de alta | Recordatorio de elaborar plan de alta |

---

## Parte 8 — Plan Familiar y Restricciones

El plan familiar registra la implicación de la familia en el tratamiento y las restricciones acordadas.

**Acceso:** En el PIAI, pestaña **Plan Familiar y Social**.

Incluye: restricciones de llamadas, visitas, salidas, objetos y medicación. Estas restricciones son visibles para las monitoras en su vista simplificada del PIAI.

---

## Parte 9 — Revisiones del PIAI

Las revisiones son reuniones periódicas del equipo para evaluar la evolución del plan.

**Acceso:** Botón **Nueva Revisión** en el PIAI, o pestaña **Revisiones**.

| Campo | Descripción |
|-------|-------------|
| **Fecha de Revisión** | Cuándo se realizó la revisión |
| **Tipo de Revisión** | Ordinaria (mensual) / Extraordinaria |
| **Motivo** | Si es extraordinaria, por qué se convocó |
| **Participantes** | Trabajadores del equipo presentes |
| **Evolución Global** | Muy favorable / Favorable / Estable / Irregular / Desfavorable |
| **Cambios Realizados** | Modificaciones al PIAI acordadas en la revisión |
| **Acuerdos** | Decisiones adoptadas |
| **Participa el Residente** | Sí/No |
| **Información Trasladada al Residente** | Sí/No |
| **Próxima Revisión Prevista** | Fecha de la siguiente revisión |
| **Validado por / Fecha** | Firma y fecha de validación |

> El cron mensual genera automáticamente una actividad de recordatorio para PIAI activos sin revisión en los últimos 30 días.

---

## Parte 10 — Notas de Evolución

Las notas de evolución son el diario clínico del residente durante su estancia.

**Acceso:** Botón **Nueva Nota de Evolución** en el PIAI, o pestaña **Notas de Evolución**.

Registro rápido de observaciones cotidianas por cualquier miembro del equipo: incidencias, avances, retrocesos, observaciones de conducta.

---

## Parte 11 — Plan de Prevención de Recaídas

**Acceso:** Pestaña **Prevención de Recaídas**.

Recoge los factores de riesgo personales, señales de alarma, situaciones de alto riesgo identificadas y estrategias de afrontamiento para prevenir una recaída una vez salga del centro.

---

## Parte 12 — Plan de Alta

El plan de alta se crea cuando el residente se aproxima al final de su estancia. Solo puede haber un plan de alta por PIAI.

**Acceso:** Campo **Plan de Alta** en la cabecera del PIAI → crear desde ahí.

| Campo | Descripción |
|-------|-------------|
| **Tipo de Alta** | Alta Terapéutica / Voluntaria / Disciplinaria / Derivación / Traslado / Abandono / Expulsión / Exitus |
| **Fecha Prevista de Alta** | Cuándo se prevé el alta |
| **Objetivos Conseguidos / Pendientes** | Resumen del logro del plan |
| **Recurso de Derivación** | Si se deriva a otro centro, nombre y contacto |
| **Plan de Tratamiento de Continuidad** | Qué seguimiento clínico tendrá tras el alta |
| **Plan de Seguimiento Post-Alta** | Citas programadas, contactos de seguimiento |
| **Recomendaciones** | Indicaciones al residente y familia |
| **Medicación al Alta** | Fármacos que continúa al salir |
| **Familia Informada / Residente Firma** | Confirmación documental |

---

## Parte 13 — Firmas y Validaciones

**Acceso:** Pestaña **Firmas y Validaciones**.

Registro de las firmas del equipo y del residente en los hitos del PIAI: validación inicial, revisiones, alta. Incluye: tipo de firma, profesional firmante, fecha, estado de validación.

---

## Parte 14 — Registros integrados de otros módulos

El PIAI muestra automáticamente (sin necesidad de introducir datos) los registros clínicos del residente procedentes de otros módulos, accesibles mediante smart buttons en la cabecera:

| Smart button | Módulo origen | Contenido |
|-------------|---------------|-----------|
| **Consultas Médicas** | cs_medical_care | Todas las consultas del residente |
| **Prescripciones** | cs_medical_care | Medicación prescrita |
| **Rescates** | cs_medical_care | Intervenciones de rescate asistencial |
| **Sesiones Psicología** | cs_psychology | Sesiones del psicólogo |
| **Llamadas Familiares** | cs_psychology | Llamadas registradas con familiares |

---

## Parte 15 — Informes PDF

Pulsar **Imprimir PIAI** (wizard de impresión) para generar informes:

| Informe | Contenido |
|---------|-----------|
| **Informe Completo** | Todo el PIAI: valoraciones, objetivos, intervenciones, riesgos, plan familiar, revisiones, plan de alta |
| **Resumen Ejecutivo** | Versión condensada para reuniones de equipo |
| **Informe de Alta** | Sección de alta + medicación + plan de continuidad |
| **Informe Mensual** | Evolución del mes + revisión + notas |
| **Informe de Auditoría** | Registro de cambios de estado para auditoría interna |

---

## Flujo completo con ejemplo real

**Contexto:** Ingresa Carlos Ruiz, 34 años, consumo de cocaína y alcohol, patología dual. Admisión el 21/05/2026.

**Día 1 — Admisión:**
- El módulo cs_admission crea automáticamente el PIAI en estado **Borrador**.
- Referente asignado: psicóloga María Sánchez.

**Días 1-3 — Valoraciones iniciales:**
- Psicóloga añade valoración Área Psicológica: sustancia principal `Cocaína + Alcohol`, motivación al cambio `Contemplación`, craving `Alto`, riesgo autolítico `Bajo`.
- Médico añade valoración Área Sanitaria: antecedentes `HTA`, signos abstinencia `Leves`, medicación al ingreso.
- Trabajadora social añade valoración Área Social: situación familiar `vive solo`, sin red de apoyo laboral.

**Día 3 — Completar el plan:**
1. Añadir **Objetivos**: "Abstinencia de cocaína en 30 días" (Área Adicciones, responsable psicóloga), "Estabilidad psiquiátrica" (Área Psiquiátrica, responsable psiquiatra).
2. Añadir **Intervenciones**: Psicoterapia Individual (semanal, psicóloga), Seguimiento Psiquiátrico (quincenal, psiquiatra), Trabajo Social (mensual, trabajadora social).
3. Añadir **Riesgos**: Tipo `Recaída`, Nivel `Alto`. Medidas preventivas: control toxicológico 2x/semana.
4. Plan Familiar: restricciones de visitas (solo familiares aprobados por dirección).
5. Fecha próxima revisión: `21/06/2026`.

**Día 4 — Activar:**
- Pulsar **Pendiente de Validación** → equipo revisa → pulsar **Activar**.
- El sistema valida: ✓ fecha elaboración, ✓ referente, ✓ fase terapéutica, ✓ valoración inicial, ✓ objetivos activos, ✓ intervenciones, ✓ próxima revisión.
- Estado → **Activo**.

**21/06/2026 — Primera revisión ordinaria:**
- Botón **Nueva Revisión**. Tipo `Ordinaria`. Participantes: psicóloga, médico, monitora coordinadora.
- Evolución Global: `Favorable`. Carlos ha reducido craving. Cambio en objetivo: fecha prevista aplazada 2 semanas.
- Próxima revisión: 21/07/2026.

---

## Vista de Monitoras (menú Residentes)

Las monitoras tienen acceso a una vista simplificada que muestra, por cada residente con PIAI activo:
- Nombre, foto, residencia y habitación
- **Restricciones vigentes**: llamadas, visitas, salidas, objetos, medicación
- Fase terapéutica actual
- Riesgos activos (nivel y tipo)

No tienen acceso a la historia clínica completa ni a los objetivos/intervenciones.

---

## Errores y avisos comunes

| Mensaje / Situación | Causa | Solución |
|--------------------|-------|----------|
| `El residente X ya tiene un PIAI activo` | Se intenta activar un segundo PIAI | Cerrar el PIAI activo actual antes de activar el nuevo |
| `Falta el profesional referente` al activar | El campo Profesional Referente está vacío | Asignar un profesional en la cabecera del PIAI |
| `Debe existir al menos una valoración inicial` | No hay ninguna fila en la pestaña Valoraciones | Añadir al menos una valoración por cualquier área |
| `Debe existir al menos un objetivo activo` | No hay objetivos o todos están suspendidos | Añadir al menos un objetivo en estado no suspendido |
| `Debe existir al menos una intervención` | Pestaña Intervenciones vacía | Añadir al menos una intervención |
| `Falta la fecha de próxima revisión` | El campo de próxima revisión está vacío | Introducir una fecha de revisión |
| Actividad de alerta `Riesgo crítico sin revisión` | El cron detecta un riesgo crítico sin revisar en 48h | Actualizar el campo `Última Revisión` en la línea del riesgo |
| El PIAI no aparece en el menú de la monitora | El PIAI no está en estado `Activo` | Activar el PIAI o verificar que la monitora tiene el rol correcto |
| Registros integrados (consultas, sesiones) no aparecen | El residente no tiene registros en esos módulos aún | Normal — se irán mostrando a medida que se creen desde cs_medical_care y cs_psychology |
