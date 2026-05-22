# Guía de Usuario — cs_resident
## Residentes, Residencias, Habitaciones y Trabajadores

**Módulo:** `cs_resident` v1.0.5  
**Perfil:** Todos los usuarios del sistema  
**Menú principal:** `Centro Sanitario`

---

## ¿Para qué sirve?

Es el núcleo de todo el sistema. Aquí se registran y gestionan:
- Los **residentes** (pacientes internados)
- Las **residencias** (centros o unidades físicas)
- Las **habitaciones** de cada residencia
- Los **trabajadores/profesionales** del equipo

Todos los demás módulos (atención médica, psicología, monitoreo…) giran alrededor de la ficha de residente creada aquí.

---

## Acceso al módulo

```
Menú superior → Centro Sanitario
```

Submenús disponibles:
- `Centro Sanitario > Residentes`
- `Centro Sanitario > Residencias`
- `Centro Sanitario > Habitaciones`
- `Centro Sanitario > Trabajadores`

> **Nota:** Si no ves el menú "Centro Sanitario" es porque el módulo no está instalado o tu usuario no tiene acceso. Contacta con el administrador.

---

## Parte 1 — Residencias

### ¿Qué es una residencia?
Una residencia es el centro o unidad física donde viven los pacientes. Puede haber más de una. Cada residencia tiene sus propias habitaciones.

### 1.1 Crear una residencia

**Ruta:** `Centro Sanitario > Residencias > Nuevo`

**Campos obligatorios:**
| Campo | Descripción |
|-------|-------------|
| Nombre de Residencia | Nombre completo del centro |
| Código | Identificador único (ej: `EQ-01`). No puede repetirse. |

**Campos opcionales:**
| Campo | Descripción |
|-------|-------------|
| Dirección, Ciudad, C.P., Provincia, País | Ubicación física |
| Teléfono / Email | Contacto del centro |
| Capacidad Total | Número máximo de plazas |
| Notas | Observaciones internas |

**Pasos:**
1. Haz clic en **Nuevo**
2. Escribe el nombre (ej: `Equilibrium - Sede Principal`)
3. Escribe un código único (ej: `EQ-01`)
4. Rellena los datos de ubicación y contacto
5. Indica la capacidad total de plazas
6. Haz clic en **Guardar**

**Estados posibles:**
- `Activa` — en funcionamiento normal
- `Inactiva` — temporalmente cerrada
- `Mantenimiento` — en obras o reforma
- `Cerrada` — cierre definitivo

[SCREENSHOT: Vista form de residencia con datos de ejemplo rellenos]

### 1.2 Adjuntar planos y documentación a una residencia

Una vez guardada la residencia, aparece el bloque **"Planos y documentación"**.

**Pasos:**
1. Abre la ficha de la residencia
2. Haz clic en **"Abrir archivos y planos"**
3. En la ventana que se abre, haz clic en **Nuevo** o arrastra archivos
4. Sube planos, normativas o cualquier documento relacionado
5. Los archivos quedan vinculados permanentemente a esa residencia

> También puedes usar el **chatter** (panel derecho) → "Registrar una nota" → clip para adjuntar archivos de forma más rápida.

El contador **"Archivos vinculados: N"** muestra cuántos documentos tiene esa residencia.

### 1.3 Añadir habitaciones desde la ficha de residencia

En la pestaña **"Habitaciones"** dentro de la residencia puedes ver y crear habitaciones directamente.

**Pasos:**
1. Abre la ficha de la residencia
2. Baja hasta el bloque "Habitaciones"
3. Haz clic en **Añadir una línea**
4. Rellena: Número, Tipo, Planta, Capacidad y Estado
5. Guarda

---

## Parte 2 — Habitaciones

### ¿Qué es una habitación?
Unidad de alojamiento dentro de una residencia. Se controla su capacidad y ocupación en tiempo real.

### 2.1 Crear una habitación independiente

**Ruta:** `Centro Sanitario > Habitaciones > Nuevo`

**Campos obligatorios:**
| Campo | Descripción |
|-------|-------------|
| Número de Habitación | Identificador (ej: `101`, `A-03`) |
| Residencia | Residencia a la que pertenece |
| Tipo | Individual / Doble / Triple |

**Campos informativos (calculados automáticamente):**
| Campo | Descripción |
|-------|-------------|
| Capacidad | Número máximo de personas |
| Ocupados | Residentes activos asignados (automático) |
| Disponibles | Capacidad − Ocupados (automático) |

**Estados posibles:**
- `Disponible` — libre, acepta residentes
- `Ocupada` — completa
- `Mantenimiento` — no disponible temporalmente
- `Cerrada` — fuera de servicio

> **Atención:** Los campos "Ocupados" y "Disponibles" se calculan solos. No se pueden editar manualmente.

### 2.2 Ver qué residentes están en una habitación

Desde la ficha de la habitación, en el bloque **"Residentes"**, aparece la lista de residentes asignados con su nombre, DNI y estado.

[SCREENSHOT: Ficha habitación mostrando bloque Residentes]

### 2.3 Filtrar habitaciones disponibles

**Ruta:** `Centro Sanitario > Habitaciones`

En la barra de búsqueda, haz clic en el desplegable y selecciona el filtro **"Disponibles"**. El sistema mostrará solo las habitaciones con plazas libres.

---

## Parte 3 — Trabajadores

### ¿Qué es un trabajador?
Cualquier profesional del centro (médico, enfermero, psicólogo, monitor, cocinero, etc.) que debe ser asignado a residentes o residencias.

> Los trabajadores se vinculan a un **contacto** existente en Odoo (res.partner). Si el profesional ya tiene usuario en el sistema, el contacto ya existe.

### 3.1 Crear un trabajador

**Ruta:** `Centro Sanitario > Trabajadores > Nuevo`

**Pasos:**
1. Haz clic en **Nuevo**
2. En el campo **"Contacto del Trabajador"**, busca y selecciona el contacto correspondiente
   - Si no existe, puedes crearlo desde ese mismo campo (icono de creación rápida)
   - Los campos Nombre, Teléfono y Email se rellenan solos desde el contacto
3. Selecciona el **Puesto de Trabajo** en el desplegable:
   - Psicólogo/a, Enfermero/a, Médico, Fisioterapeuta, Terapeuta, Cuidador/a, Cocinero/a, Limpiador/a, Administrativo/a, Director/a, Otro
   - Si eliges "Otro", aparece un campo adicional para especificar
4. Asigna las **Residencias** donde trabaja (campo etiquetas múltiples)
5. Guarda

> **Truco:** Si el contacto ya tiene categorías (etiquetas) que coincidan con un puesto (ej: "Psicólogo"), el sistema intentará autocompletar el campo Puesto de Trabajo.

**Estados posibles:**
- `Activo` — en plantilla
- `Inactivo` — suspensión temporal
- `Baja` — ha dejado la empresa

[SCREENSHOT: Ficha trabajador con puesto y residencias asignadas]

### 3.2 Asignar residentes a un trabajador

Desde la ficha del trabajador, en el bloque **"Residentes Asignados"**, puedes ver y modificar qué residentes tiene asignados.

> También puedes asignar desde la ficha del residente (ver Parte 4).

### 3.3 Filtrar por puesto de trabajo

En `Centro Sanitario > Trabajadores`, usa los filtros rápidos:
- **Psicólogos** — solo psicólogos
- **Enfermeros** — solo enfermería
- **Médicos** — solo médicos
- **Activos / Inactivos** — por estado

---

## Parte 4 — Residentes

### ¿Qué es un residente?
La ficha central del sistema. Representa a un paciente que vive o ha vivido en el centro. Todo el historial clínico, económico y de seguimiento está vinculado a esta ficha.

### 4.1 Crear un residente nuevo

**Ruta:** `Centro Sanitario > Residentes > Nuevo`

**Dos formas de crear:**

#### Opción A — Vincular a contacto existente (recomendado si ya fue paciente antes)
1. Haz clic en **Nuevo**
2. En el campo **"Contacto (Paciente)"**, busca el contacto por nombre o DNI
3. El sistema autocompleta: Nombre, Teléfono y DNI/NIF
4. Completa los campos que falten (fecha de nacimiento, residencia, habitación)
5. Guarda

#### Opción B — Residente completamente nuevo (primera vez en el sistema)
1. Haz clic en **Nuevo**
2. Deja vacío el campo "Contacto (Paciente)"
3. Escribe el **Nombre Completo**
4. Escribe el **DNI/NIF**
5. Introduce la **Fecha de Nacimiento**
6. Al guardar, el sistema **crea automáticamente un contacto** con etiqueta "Paciente"

**Campos obligatorios:**
| Campo | Descripción |
|-------|-------------|
| Nombre Completo | Nombre y apellidos |
| DNI/NIF | Debe ser único en el sistema |
| Fecha de Nacimiento | Para calcular la edad |

**Campos de ubicación:**
| Campo | Descripción |
|-------|-------------|
| Residencia | Centro donde está ingresado |
| Habitación | Se filtra automáticamente por residencia seleccionada |

> Al seleccionar la residencia, el campo Habitación muestra solo las habitaciones de esa residencia.

**Campos opcionales:**
| Campo | Descripción |
|-------|-------------|
| Teléfono | Contacto directo del residente |
| Peso (kg) | Dato clínico básico |
| Altura (cm) | Dato clínico básico |
| Trabajadores Asignados | Profesionales responsables |
| Notas | Observaciones libres |

[SCREENSHOT: Ficha residente con todos los campos rellenos]

### 4.2 Barra de estado del residente

En la parte superior de la ficha hay una barra de estado con 4 posibles valores:

```
[Activo] → [Pausado] → [Alta] → [Baja]
```

| Estado | Significado |
|--------|-------------|
| **Activo** | Residente ingresado y activo en el centro |
| **Pausado** | Ausencia temporal (hospitalización, permiso) |
| **Alta** | Ha completado el programa y se ha ido |
| **Baja** | Ha abandonado el centro sin completar el programa |

> Cambiar el estado no borra ningún dato. El historial se conserva íntegramente.

### 4.3 Datos económicos (saldo del monedero)

Si el residente tiene un monedero activo (módulo `cs_purse_pocket`), aparece el bloque **"Datos Económicos"** con:
- **Saldo (€):** saldo actual disponible (calculado en tiempo real)

Si no tiene monedero, este bloque queda oculto.

> Para crear el monedero de un residente, ve a la guía [02 — Monedero y fondos de terceros](../02_cs_purse_pocket/guia.md).

### 4.4 Asignar trabajadores al residente

En el bloque **"Trabajadores Asignados"**:
1. Haz clic dentro del campo de etiquetas
2. Busca y selecciona el profesional
3. Puedes asignar varios profesionales de distintos perfiles
4. Guarda

### 4.5 Buscar y filtrar residentes

**Ruta:** `Centro Sanitario > Residentes`

Búsqueda por texto: nombre o DNI

Filtros rápidos disponibles:
- **Activos** — solo residentes con estado "activo"
- **Pausados** — residentes con ausencia temporal
- **Alta** — residentes que han completado el programa
- **Baja** — residentes que han abandonado

[SCREENSHOT: Vista lista de residentes con filtros aplicados]

### 4.6 Chatter y trazabilidad

Cada ficha de residente tiene un **chatter** (panel de mensajes inferior/lateral). Aquí aparece automáticamente:
- Cambios de estado con fecha y usuario
- Cambios en campos con tracking (residencia, habitación, DNI, trabajadores…)
- Mensajes y notas internas que cualquier usuario puede añadir
- Actividades programadas (recordatorios, tareas)

Para añadir una nota interna:
1. Haz clic en **"Registrar una nota"**
2. Escribe el mensaje
3. Opcionalmente adjunta un archivo (icono clip)
4. Haz clic en **"Añadir"**

---

## Flujo típico completo

### Escenario: Nuevo residente llega al centro

1. **Pre-admisión:** Si tienes el módulo OCR DNI, escanea el DNI del paciente en `Contactos` para crear el contacto base. Ver [Guía 11 — OCR DNI](../11_cs_dni_ocr/guia.md).

2. **Crear residencia** (si no existe): `Centro Sanitario > Residencias > Nuevo`

3. **Crear habitaciones** de esa residencia (si no existen): desde la ficha de residencia o `Centro Sanitario > Habitaciones > Nuevo`

4. **Crear el residente:** `Centro Sanitario > Residentes > Nuevo`
   - Vincular al contacto creado por OCR (Opción A) o crear desde cero (Opción B)
   - Asignar residencia y habitación
   - Asignar trabajadores responsables

5. **Continuar con admisión completa:** el proceso de ingreso guiado está en el módulo de admisión. Ver [Guía 3 — Admisión](../03_cs_admission/guia.md).

---

## Casos de uso frecuentes

### "El residente sale de permiso unos días"
1. Abre la ficha del residente
2. Cambia el estado a **Pausado**
3. Añade una nota en el chatter: "Permiso familiar del 15 al 20 de junio"
4. Cuando regrese, vuelve a cambiar a **Activo**

### "El residente ha sido dado de alta del programa"
1. Abre la ficha del residente
2. Cambia el estado a **Alta**
3. El residente queda en el historial pero no aparece en los filtros de activos

### "El residente cambia de habitación"
1. Abre la ficha del residente
2. Modifica el campo **Habitación**
3. Guarda — el cambio queda registrado en el chatter automáticamente

### "Quiero ver todas las habitaciones libres de una residencia"
1. Ve a `Centro Sanitario > Habitaciones`
2. Usa el filtro **"Disponibles"**
3. Opcionalmente, busca por nombre de residencia para filtrar más

### "El DNI aparece como duplicado al crear un residente"
El sistema no permite dos residentes con el mismo DNI. Busca en la lista de residentes el DNI que da error — puede que el paciente ya esté registrado (incluso en estado Alta o Baja).

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| "El DNI/NIF del residente debe ser único" | Ese DNI ya existe en el sistema | Busca el residente por DNI antes de crear uno nuevo |
| "El código de residencia debe ser único" | Ya existe una residencia con ese código | Usa un código diferente (ej: `EQ-02`) |
| Campo Habitación no muestra opciones | No se ha seleccionado Residencia primero | Selecciona la residencia antes de elegir habitación |
| Bloque "Datos Económicos" no aparece | El residente no tiene monedero creado | Crea el monedero desde el módulo `cs_purse_pocket` |
| El botón "Abrir archivos y planos" no aparece | La residencia no está guardada todavía | Guarda primero la ficha de residencia |
