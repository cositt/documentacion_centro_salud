# Guía de usuario — cs_monitoring: Monitorización diaria

## ¿Para qué sirve este módulo?

`cs_monitoring` agrupa cuatro registros operativos que las monitoras cumplimentan cada día:

1. **Checklists diarios** — verificaciones de bienestar del residente (estado general, higiene, ingestas, medicación, etc.)
2. **Temperaturas corporales** — toma y registro de temperatura de los residentes
3. **Temperaturas de alimentos (HACCP)** — control de temperatura en recepción y reconstitución de bandejas, exigido por normativa sanitaria
4. **Guardias de monitoras** — registro de inicio/fin de turno, incidencias y relevo

---

## Acceso al módulo

> Menú principal → **Monitoreo**

Submenús disponibles:

| Submenú | Contenido |
|---------|-----------|
| Temperaturas | Registros de temperatura corporal de residentes |
| Checklists diarios | Formularios de seguimiento diario |
| Plantillas de checklist | Configuración de ítems reutilizables |
| Temperaturas de alimentos | Control HACCP de comidas |
| Guardias de monitoras | Registro de turnos y relevos |

---

## Parte 1 — Checklists diarios

### ¿Para qué sirve?

Cada jornada, la monitora crea un checklist por residente (o por residencia, si es global) para verificar que se han atendido todos los aspectos de cuidado: constantes, higiene, comida, medicación, movilización y comportamiento.

### Crear un checklist

1. **Monitoreo** → **Checklists diarios** → **Nuevo**.
2. Rellenar campos principales:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Fecha** | Sí | Por defecto hoy |
| **Residencia** | Sí | Se rellena automáticamente al seleccionar el residente |
| **Residente (opcional)** | No | Si es específico de un residente; si es global de la residencia, dejar vacío |
| **Monitora / responsable** | No | Quién ejecuta el checklist |
| **Plantilla** | No | Carga ítems predefinidos automáticamente |

3. Cargar ítems:
   - **Opción A — Plantilla:** Seleccionar plantilla en el campo correspondiente; los ítems se cargan solos. Pulsar **Aplicar plantilla** si no se cargaron automáticamente.
   - **Opción B — Estándar:** Pulsar **Cargar ítems estándar** para añadir los 6 ítems por defecto del sistema.
   - **Opción C — Manual:** Añadir ítems directamente en la tabla.

4. Ítems por defecto (botón **Cargar ítems estándar**):
   - Constantes y estado general
   - Higiene y confort
   - Ingestas (dieta / hidratación)
   - Medicación según pauta
   - Movilización y cambios posturales
   - Participación / comportamiento

5. Para cada ítem: marcar la casilla **OK** si se ha completado correctamente. Añadir **Observaciones** si hay algo a destacar.
6. Añadir **Notas generales** al final si hay incidencias globales.
7. Pulsar **Marcar como hecho** para cerrar el checklist. (Se puede reabrir con **Volver a borrador**.)

### Estados

| Estado | Significado |
|--------|-------------|
| **Borrador** | En proceso, editable |
| **Hecho** | Completado y cerrado |

> [SCREENSHOT: formulario de checklist con ítems marcados]

---

## Parte 2 — Plantillas de checklist

Las plantillas permiten tener conjuntos de ítems predefinidos para reutilizar en cada turno sin tener que escribirlos de nuevo.

### Crear una plantilla

1. **Monitoreo** → **Plantillas de checklist** → **Nuevo**.
2. Dar nombre a la plantilla (p. ej. "Turno mañana - planta 1").
3. Añadir ítems en la tabla con su texto y orden.
4. Guardar.

La plantilla ya está disponible en el campo **Plantilla** de cualquier checklist nuevo.

> **Nota:** Al seleccionar una plantilla en un checklist, los ítems se añaden sin duplicar los que ya existían.

---

## Parte 3 — Temperaturas corporales

### ¿Para qué sirve?

Registro de cada toma de temperatura de un residente: valor, vía de medición, fecha/hora y quién la tomó. Permite hacer seguimiento de fiebres y detectar tendencias.

### Crear un registro

1. **Monitoreo** → **Temperaturas** → **Nuevo**.
2. Campos:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Residente** | Sí | Al seleccionarlo, residencia y habitación se rellenan automáticamente |
| **Fecha y hora** | Sí | Por defecto ahora |
| **Temperatura (°C)** | Sí | Rango válido: 30,0 °C – 45,0 °C. Fuera de rango: error de validación |
| **Vía de medición** | No | Oral, Axilar, Timpánica, Rectal, Otro (por defecto: Axilar) |
| **Registrado por** | No | Monitora o profesional que tomó el dato |
| **Observaciones** | No | Notas adicionales (síntomas, contexto) |

3. Guardar. La referencia se genera automáticamente.

> **Validación importante:** El sistema rechaza temperaturas inferiores a 30,0 °C o superiores a 45,0 °C — probablemente error de escritura.

### Consultar el histórico de un residente

- En la lista: filtrar por **Residente** o buscar por nombre.
- Ordenación: más reciente primero.

> [SCREENSHOT: lista de temperaturas con varios residentes ordenadas por fecha]

---

## Parte 4 — Temperaturas de alimentos (HACCP)

### ¿Para qué sirve?

Control de temperatura obligatorio en dos momentos del ciclo de alimentación:
- **Recepción de comida:** al llegar el catering o suministro
- **Reconstitución de bandeja:** al servir/calentar antes de dar al residente

Cada registro verifica automáticamente si la temperatura medida está dentro del rango definido. Los registros fuera de rango quedan marcados como incidencia.

### Crear un registro de temperatura de alimentos

1. **Monitoreo** → **Temperaturas de alimentos** → **Nuevo**.
2. Campos:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Residencia** | Sí | Residencia donde se realiza el control |
| **Tipo de registro** | Sí | `Recepción de comida` o `Reconstitución de bandeja` |
| **Alimento** | Sí | Nombre del alimento o preparación (p. ej. "Ensalada mixta", "Pollo guisado") |
| **Temperatura medida (°C)** | Sí | Temperatura real medida con el termómetro |
| **Temperatura mínima (°C)** | Sí | Límite inferior del rango aceptable (por defecto: 0,0 °C) |
| **Temperatura máxima (°C)** | Sí | Límite superior del rango aceptable (por defecto: 8,0 °C) |
| **Fecha y hora** | Sí | Por defecto ahora |
| **Monitora / Responsable** | No | Quién realiza el control |
| **Observaciones** | No | Incidencias, proveedor, lote, acciones correctoras |

3. El campo **Dentro del rango** se calcula automáticamente: `Sí` si `temp_min ≤ temp_medida ≤ temp_max`.
4. Guardar.

### Rangos habituales por tipo de alimento

| Tipo de alimento | Rango recomendado |
|-----------------|-------------------|
| Fríos (ensaladas, lácteos) | 0 °C – 8 °C |
| Calientes (guisos, sopas) | 65 °C – 100 °C |
| Congelados | -18 °C – -10 °C |

> **Ajustar los rangos** según el protocolo APPCC del centro — los valores por defecto (0–8 °C) son solo un ejemplo para alimentos fríos.

---

## Parte 5 — Guardias de monitoras

### ¿Para qué sirve?

Registro formal de cada turno de guardia: quién está de guardia, en qué residencia, cuándo empieza y termina, qué turno es y si hubo incidencias. También permite registrar el relevo (de qué guardia anterior recibe el turno).

### Crear una guardia

1. **Monitoreo** → **Guardias de monitoras** → **Nuevo**.
2. Campos:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Monitora** | Sí | Trabajadora que realiza la guardia |
| **Residencia** | Sí | Residencia asignada |
| **Inicio de guardia** | Sí | Fecha y hora de inicio (por defecto: ahora) |
| **Fin de guardia** | No | Se rellena al terminar el turno |
| **Turno** | Sí | Mañana / Tarde / Noche / Fin de semana |
| **Relevo recibido de** | No | Enlace a la guardia del turno anterior (quién entregó) |
| **Incidencias** | No | Texto libre con cualquier incidencia durante el turno |

3. Al terminar el turno: abrir la guardia y rellenar **Fin de guardia** + **Incidencias** si las hubo.

> **Validación:** El sistema no permite que la fecha de fin sea anterior al inicio.

> [SCREENSHOT: formulario de guardia con turno de noche e incidencias registradas]

---

## Flujo completo con ejemplo real

**Turno de mañana — monitora Ana Pérez — Residencia Equilibrium 1**

1. **Al llegar (8:00):**
   - Crear guardia: Monitora `Ana Pérez`, Residencia `Equilibrium 1`, Turno `Mañana`, Inicio `08:00`.
   - Relevo recibido de: seleccionar la guardia de noche anterior.

2. **Al recibir el catering (9:30):**
   - **Temperaturas de alimentos** → **Nuevo**. Tipo: `Recepción de comida`.
   - Alimento: `Ensalada César`. Temp. medida: `6,2 °C`. Rango: `0–8 °C`. Dentro del rango: ✓.
   - Alimento: `Pollo al horno`. Temp. medida: `72 °C`. Rango: `65–100 °C`. Dentro del rango: ✓.

3. **Ronda de 10:00 — toma de temperatura a un residente:**
   - **Temperaturas** → **Nuevo**. Residente: `María García`. Temperatura: `37,8 °C`. Vía: `Axilar`. Observaciones: `Ligera febrícula, se comunica a enfermería`.

4. **Checklist de 11:00:**
   - **Checklists diarios** → **Nuevo**. Residente: `María García`. Fecha: hoy.
   - Cargar plantilla `Turno mañana`. Marcar ítems completados. Observación en `Ingestas`: `Desayuno reducido por malestar`.
   - **Marcar como hecho**.

5. **Al terminar el turno (14:00):**
   - Abrir la guardia creada al llegar. Rellenar **Fin de guardia**: `14:00`.
   - Incidencias: `María García con febrícula 37,8°C — informado a enfermería. Sin otros incidentes`.

---

## Casos de uso frecuentes

### Registro HACCP de bandeja caliente fuera de rango
- Si temp. medida < 65 °C en reconstitución: campo **Dentro del rango** → `No`.
- Añadir en **Observaciones** la acción correctora (recalentar, desechar, notificar a cocina).
- Este registro queda como evidencia documental para inspecciones sanitarias.

### Residente con fiebre recurrente
- Buscar en **Temperaturas** filtrando por residente → ver todas las tomas ordenadas cronológicamente.
- Si la tendencia supera 38 °C varios días: añadir observación en cada registro y comunicar al médico.

### Checklist global de residencia (no por residente)
- Crear checklist sin seleccionar **Residente** — solo con **Residencia**.
- Útil para verificaciones de instalaciones, material, limpieza de zonas comunes.

### Guardia de fin de semana con varias monitoras
- Crear una guardia por cada monitora con turno `Fin de semana` y sus horarios propios.
- No es necesario un registro conjunto; la vista de lista permite ver todas las guardias del fin de semana filtradas por residencia.

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| `La temperatura debe estar entre 30,0 °C y 45,0 °C` | Temperatura corporal fuera del rango biológico posible | Verificar la lectura del termómetro antes de guardar; probablemente es error de escritura |
| `La temperatura mínima debe ser menor que la máxima` | En temperatura de alimentos se puso mín > máx | Invertir los valores del rango |
| `El fin de guardia no puede ser anterior al inicio` | Error de fecha en la guardia | Corregir la hora de fin |
| `La residencia del checklist debe coincidir con la del residente` | El residente pertenece a una residencia diferente | Verificar la residencia asignada al residente en su ficha |
| Plantilla no carga ítems automáticamente | El campo plantilla se puso después de guardar | Usar el botón **Aplicar plantilla** para forzar la carga |
| No aparece el submenú **Monitoreo** | El módulo no está instalado | Pedir al administrador que instale `cs_monitoring` |
