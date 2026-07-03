# Guía de Usuario — cs_social_work
## Trabajo Social

**Módulo:** `cs_social_work` v1.0.0  
**Perfil:** Trabajadoras sociales, coordinadores  
**Menú principal:** `Trabajo Social`

---

## ¿Para qué sirve?

Gestiona toda la actividad de trabajo social del residente:

- **Atenciones** individuales, familiares, grupales, de coordinación o gestión externa — sincronizadas automáticamente con el calendario de Odoo
- **Informes sociales**: valoración social inicial, seguimiento, derivación e informes para organismos oficiales
- **Gestiones y trámites**: ayudas económicas, pensiones, Ley de Dependencia, certificado de discapacidad, documentación, citas externas, recursos sociales y trámites judiciales — con fechas límite y estados
- **Contactos con familia** (registro compartido con Psicología)
- **Calendario** con todas las citas de trabajo social del centro

> **Requisito:** para asignar profesionales, el trabajador debe tener el puesto **"Trabajador/a Social"** en su ficha (`Centro Sanitario > Trabajadores`).

---

## Acceso al módulo

```
Menú superior → Trabajo Social
```

| Submenú | Descripción |
|---------|-------------|
| `Citas (calendario)` | Vista calendario de todas las atenciones |
| `Atenciones` | Lista de atenciones de trabajo social |
| `Informes sociales` | Valoraciones, seguimientos e informes oficiales |
| `Gestiones y trámites` | Trámites ante organismos con seguimiento de estado |
| `Contactos familia` | Registro de llamadas y contactos familiares |

---

## Parte 1 — Atenciones (citas)

### 1.1 Crear una atención

**Ruta:** `Trabajo Social > Atenciones > Nuevo`

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Residente | ✓ | Persona atendida |
| Fecha y hora | ✓ | Momento de la atención |
| Trabajador/a Social | — | Solo acepta trabajadores con ese puesto |
| Duración (min) | — | Por defecto 30 minutos |
| Tipo de atención | — | Individual / Familiar / Grupal / Coordinación / Gestión externa |
| Resumen / objetivos | — | Objetivo de la atención |
| Notas de la atención | — | Contenido y acuerdos |

Al guardar se crea **automáticamente una cita en el calendario** de Odoo con el residente y la profesional como asistentes. Si cambias fecha o duración en la atención, la cita se actualiza — y al mover la cita en el calendario, la atención se actualiza también (sincronización bidireccional).

**Estados:** Planificada → Realizada / Cancelada (cancelar archiva la cita del calendario).

**Formularios estandarizados:** selecciona una **Plantilla de evaluación** (módulo `cs_patient_followup_forms`) para vincular un formulario estructurado a la atención.

### 1.2 Calendario

**Ruta:** `Trabajo Social > Citas (calendario)`

Vista mensual/semanal/diaria de todas las citas marcadas como visita de trabajo social. Puedes crear citas directamente aquí: marca el check "Visita de trabajo social" y rellena residente y profesional.

---

## Parte 2 — Informes sociales

### 2.1 Tipos de informe

| Tipo | Uso |
|------|-----|
| Valoración social inicial | Historia social al ingreso |
| Informe de seguimiento | Evolución periódica |
| Informe de derivación | Traslado a otro recurso |
| Informe para organismo oficial | Dirigido a administración pública (campo "Organismo destinatario") |
| Otro | Resto de casos |

### 2.2 Crear un informe

**Ruta:** `Trabajo Social > Informes sociales > Nuevo`

Secciones de texto del informe:

- **Motivo del informe / demanda**
- **Situación socio-familiar**
- **Situación económica y laboral**
- **Vivienda y entorno**
- **Red de apoyo y recursos**
- **Valoración / diagnóstico social**
- **Plan de intervención social**

**Estados:** Borrador → Cerrado (con botón para reabrir).

Igual que en atenciones, puedes vincular una **plantilla de formulario** estandarizado y adjuntar archivos (PDF, escaneos...).

---

## Parte 3 — Gestiones y trámites

Seguimiento de trámites que la trabajadora social realiza en nombre del residente.

### 3.1 Tipos de gestión

Ayuda económica · Pensión/prestación · Ley de Dependencia · Certificado de discapacidad · Documentación (DNI, tarjeta sanitaria...) · Cita externa/acompañamiento · Recurso social/derivación · Judicial (tutela, incapacitación...) · Otro

### 3.2 Flujo de estados

```
Pendiente → En trámite → Esperando respuesta → Completada
                    ↘ Cancelada
```

| Campo | Descripción |
|-------|-------------|
| Organismo / entidad | Ante quién se tramita |
| Fecha de inicio | Cuándo se abre la gestión |
| Fecha límite | Plazo administrativo — las gestiones fuera de plazo se muestran **en rojo** en la lista |
| Fecha de finalización | Se rellena automáticamente al completar |

La lista filtra por defecto las gestiones **abiertas** y permite agrupar por tipo, estado o residente. Filtro rápido "Fuera de plazo" disponible.

---

## Parte 4 — Ficha del residente

En la ficha de cada residente aparecen 3 botones inteligentes:

- **Trabajo Social** — atenciones del residente
- **Informes sociales** — informes del residente
- **Gestiones** — trámites del residente

---

## Preguntas frecuentes

**¿Por qué no puedo seleccionar a una profesional en "Trabajador/a Social"?**  
Su ficha de trabajador debe tener el puesto "Trabajador/a Social". Edítala en `Centro Sanitario > Trabajadores`.

**¿Los contactos con familia son distintos de los de Psicología?**  
No — es el mismo registro compartido. Cualquier profesional del centro puede registrar un contacto indicando quién lo realizó.

**¿Puedo adjuntar la resolución de una ayuda?**  
Sí — cada gestión tiene su sección de archivos adjuntos.
