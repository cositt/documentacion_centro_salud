# Guía de Usuario — cs_admission
## Proceso de Admisión Guiado

**Módulo:** `cs_admission` v1.0.0  
**Perfil:** Recepción, dirección, coordinación clínica  
**Menú principal:** `Centro Sanitario > Admisiones`

---

## ¿Para qué sirve?

Guía paso a paso el ingreso de un nuevo residente al centro. En lugar de tener que crear manualmente el residente, la consulta médica, la evaluación psicológica y el monedero en módulos separados, el proceso de admisión los coordina todos en un único flujo ordenado de **7 pasos**.

Al completar la admisión, el sistema automáticamente:
- Crea el residente y su contacto
- Le asigna residencia y habitación
- Vincula la consulta médica y evaluación psicológica de ingreso
- Crea el monedero del paciente
- Genera un borrador de PIAI (si el módulo `cs_piai` está instalado)

---

## Acceso al módulo

```
Menú superior → Centro Sanitario → Admisiones
```

> La vista lista muestra por defecto solo las admisiones **en curso** (filtro "En curso" activo). Para ver las cerradas, elimina el filtro o usa el filtro "Cerradas".

---

## Los 7 pasos del proceso

```
[1 · Identificación] → [2 · Ubicación] → [3 · Médico] → [4 · Psicología]
                    → [5 · Enfermería] → [6 · Documentación] → [7 · Economía] → ✓ Cerrado
```

Cada paso tiene sus campos. Los campos de un paso pasado quedan **bloqueados** (solo lectura) una vez avanzas — asegúrate de revisar antes de pulsar "Siguiente paso".

Puedes **retroceder pasos** (botón "← Paso anterior") en cualquier momento, excepto si la admisión ya está cerrada.

---

## Iniciar una nueva admisión

**Ruta:** `Centro Sanitario > Admisiones > Nuevo`

1. Haz clic en **Nuevo**
2. Se crea automáticamente con referencia `ADM/XXXX/NNNNN` y estado `Identificación`
3. La fecha de ingreso se pre-rellena con hoy (editable)
4. Empieza a rellenar el **Paso 1 — Identificación**

---

## Paso 1 — Identificación

**Objetivo:** Recoger los datos básicos del paciente y su tutor/familiar responsable.

### Campos del paciente:
| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Nombre completo | ✓ | Nombre y apellidos |
| DNI / NIF | ✓ | Debe ser único en el sistema |
| Fecha de nacimiento | — | Para calcular la edad |
| Teléfono | — | Contacto directo del paciente |
| Email | — | Email del paciente |

### Campos del tutor/familiar responsable:
| Campo | Descripción |
|-------|-------------|
| Tutor legal / Familiar responsable | Nombre del tutor o familiar |
| Teléfono tutor | Contacto del tutor |
| Email tutor | Email del tutor |

> El tutor se crea automáticamente como **sub-contacto** del paciente en Odoo, lo que permite vincularlo como familiar pagador en el monedero.

### Notas de identificación:
Campo libre para anotar cualquier observación del proceso de llegada.

### Al pulsar "Siguiente paso →":
- El sistema valida que **Nombre completo** y **DNI** estén rellenos
- Crea automáticamente:
  - Un contacto (`res.partner`) con etiqueta "Paciente"
  - Un residente (`cs.resident`) vinculado al contacto
  - El sub-contacto del tutor/familiar (si se rellenó)
- Aparece un aviso verde: "Residente creado: [Nombre]"
- Avanza al paso 2

> Una vez creado el residente, los campos de identificación quedan bloqueados. Para corregir datos del residente, usa el botón de acceso rápido (icono de persona) en la cabecera o ve directamente a `Centro Sanitario > Residentes`.

[SCREENSHOT: Paso 1 con datos rellenos y aviso azul antes de avanzar]

---

## Paso 2 — Ubicación

**Objetivo:** Asignar al residente una residencia y habitación.

| Campo | Descripción |
|-------|-------------|
| Residencia | Centro o unidad donde se ubica |
| Habitación | Solo muestra habitaciones disponibles de la residencia seleccionada |

> El filtro de habitaciones muestra **solo las que tienen estado "Disponible"**. Si no aparece ninguna, es porque todas están ocupadas o en mantenimiento — revisa `Centro Sanitario > Habitaciones`.

### Al pulsar "Siguiente paso →":
- Valida que se haya seleccionado una residencia (obligatorio)
- Escribe la residencia y habitación en la ficha del residente automáticamente
- Avanza al paso 3

---

## Paso 3 — Médico (opcional)

**Objetivo:** Registrar la consulta médica de ingreso.

Este paso es **opcional** — puedes avanzar sin crear la consulta.

### Crear una nueva consulta de ingreso:
1. Haz clic en el botón **"Nueva consulta de ingreso"**
2. Se abre un formulario de consulta médica pre-relleno con el residente
3. Rellena la consulta (diagnóstico, observaciones, tratamiento inicial...)
4. Guarda la consulta
5. Vuelve a la admisión — el campo "Consulta médica de ingreso" queda vinculado

> Para consultar la consulta de ingreso desde cualquier pantalla, usa el botón de acceso rápido con icono de estetoscopio en la cabecera de la admisión.

---

## Paso 4 — Psicología

**Objetivo:** Crear la evaluación psicológica inicial del residente.

1. Haz clic en **"Crear evaluación psicológica inicial"**
2. Se crea una evaluación inicial (`cs.initial.assessment`) vinculada al residente
3. Se abre el formulario de evaluación en ventana nueva
4. Rellena los campos clínicos psicológicos (historia, antecedentes, objetivos iniciales...)
5. Guarda la evaluación
6. Vuelve a la admisión — el campo queda vinculado

Si ya existe una evaluación inicial para ese residente, el botón cambia a **"Abrir evaluación"**.

> El botón de acceso rápido (icono de corazón/pulso) en la cabecera abre la evaluación directamente.

---

## Paso 5 — Enfermería

**Objetivo:** Registrar el estado clínico del paciente al ingreso.

### Condición al ingreso:
| Campo | Descripción |
|-------|-------------|
| Alergias conocidas | Lista de alergias o "Ninguna conocida" |
| Medicación actual al ingreso | Fármacos que toma en este momento |

### Tests al ingreso:
| Campo | Descripción |
|-------|-------------|
| Test alcohol realizado | Marca si se realizó test de alcoholemia |
| Resultado alcohol | Valor o resultado del test (aparece al marcar el checkbox) |
| Test multidrogas realizado | Marca si se realizó test de drogas |
| Resultado multidrogas | Valor o resultado (aparece al marcar el checkbox) |

### Notas de enfermería:
Campo libre para constantes vitales, estado general, observaciones clínicas al ingreso.

> Los datos de enfermería se transfieren automáticamente a la ficha del residente al cerrar la admisión.

---

## Paso 6 — Documentación

**Objetivo:** Verificar que la documentación reglamentaria está en orden y adjuntar archivos.

### Checklist de documentos:
| Documento | Descripción |
|-----------|-------------|
| DNI / pasaporte entregado | El paciente ha entregado su documento de identidad |
| Contrato de ingreso firmado | El contrato de estancia está firmado |
| Informe médico previo entregado | Se ha entregado informe médico previo |
| Consentimiento informado firmado | El paciente o tutor ha firmado el consentimiento |

Marca cada casilla cuando el documento esté en mano.

### Adjuntar documentos digitales:
En el bloque "Archivos adjuntos" puedes subir los documentos escaneados:
1. Haz clic en el área de adjuntos o arrastra el archivo
2. Los documentos quedan vinculados a esta admisión
3. Puedes subir tantos archivos como necesites (PDF, JPG, PNG, etc.)

> Si no tienes los documentos digitalizados en el momento del ingreso, puedes avanzar y adjuntarlos más adelante. La admisión no bloquea el avance por documentación faltante.

---

## Paso 7 — Economía

**Objetivo:** Crear o vincular el monedero del paciente para gestionar sus gastos personales.

### Crear el monedero:
1. Haz clic en **"Crear monedero"**
2. Se crea automáticamente una cuenta monedero (`patient.wallet.account`) para el paciente
3. Se abre el formulario del monedero en ventana nueva
4. Configura:
   - **Umbral alerta saldo bajo** (por defecto 50 €)
   - **Activar alerta saldo bajo** (activo por defecto)
   - **Extracto semanal automático** (activo por defecto)
5. Guarda el monedero
6. Vuelve a la admisión — el campo queda vinculado

Si ya existe un monedero para ese paciente (ingreso previo), el sistema lo detecta y lo vincula automáticamente. El botón cambia a **"Abrir monedero"**.

> Para la configuración completa del monedero (categorías, vínculos familiares, recargas), consulta la [Guía 2 — Monedero](../02_cs_purse_pocket/guia.md).

---

## Completar la admisión

Una vez en el paso 7 (Economía), aparece el botón **"✓ Completar Admisión"** (verde).

Al pulsar:
1. El estado cambia a **Cerrado**
2. Se registra la fecha de cierre
3. Los datos de enfermería se escriben en la ficha del residente
4. Se añade un mensaje en el chatter: "Admisión completada. Residente activado en el sistema."
5. Si el módulo `cs_piai` está instalado: se crea automáticamente un **PIAI en borrador** con fase terapéutica "Acogida" — siempre que no exista ya un PIAI activo para ese residente

### Vista de cierre (Paso 8 — Cierre):
Muestra un resumen completo de la admisión:
- Residente, residencia, habitación, fecha de cierre
- Consulta médica vinculada (si se creó)
- Evaluación psicológica vinculada (si se creó)
- Monedero vinculado (si se creó)

---

## Accesos rápidos (smart buttons)

En la cabecera del formulario de admisión aparecen botones de acceso directo a los registros creados durante el proceso:

| Botón | Icono | Se muestra cuando... |
|-------|-------|----------------------|
| Residente | 👤 persona | El residente ya fue creado (paso 1 completado) |
| Consulta Médica | 🩺 estetoscopio | Se vinculó una consulta médica |
| Evaluación Psic. | ❤️ pulso | Se creó la evaluación psicológica |
| Monedero | 💳 tarjeta | Se creó o vinculó el monedero |

---

## Flujo típico completo

### Escenario: Paciente nuevo llega al centro

1. `Centro Sanitario > Admisiones > Nuevo`

2. **Paso 1 — Identificación:**
   - Nombre: "Juan García López"
   - DNI: "12345678A"
   - Fecha nacimiento: 15/03/1985
   - Teléfono: "666 111 222"
   - Tutor: "María López" (madre) — teléfono y email
   - → Siguiente paso (se crea residente y contactos)

3. **Paso 2 — Ubicación:**
   - Residencia: "Equilibrium - Sede Principal"
   - Habitación: "104" (individual, disponible)
   - → Siguiente paso (se asigna al residente)

4. **Paso 3 — Médico:**
   - Clic "Nueva consulta de ingreso" → rellena y guarda
   - → Siguiente paso

5. **Paso 4 — Psicología:**
   - Clic "Crear evaluación psicológica inicial" → rellena y guarda
   - → Siguiente paso

6. **Paso 5 — Enfermería:**
   - Alergias: "Penicilina"
   - Medicación: "Diazepam 5mg / 24h"
   - Test alcohol: marcado — Resultado: "0.8 g/L"
   - Test drogas: marcado — Resultado: "Positivo cannabis"
   - → Siguiente paso

7. **Paso 6 — Documentación:**
   - Marcar: DNI entregado ✓, Contrato firmado ✓, Consentimiento firmado ✓
   - Adjuntar: escáner del DNI, PDF del contrato
   - → Siguiente paso

8. **Paso 7 — Economía:**
   - Clic "Crear monedero" → configura umbral 30 €, extracto semanal activo, guarda
   - Clic **"✓ Completar Admisión"**

9. **Resultado:**
   - Residente activo en el sistema
   - PIAI borrador creado automáticamente con fase "Acogida"
   - La madre (María López) queda como sub-contacto del paciente
   - Todo el equipo puede ver el residente en `Centro Sanitario > Residentes`

---

## Casos de uso frecuentes

### "El paciente ya estuvo en el centro antes"
Si existe un residente con el mismo DNI, el sistema lo detectará al crear e impedirá duplicados. En ese caso:
1. No uses el wizard de admisión para crear — el residente ya existe
2. Ve a `Centro Sanitario > Residentes`, abre la ficha del residente
3. Cambia su estado a "Activo" y asigna nueva residencia/habitación
4. O bien, crea la admisión y en el Paso 1 verás el error de DNI duplicado — cancela y actualiza directamente la ficha

### "Necesito corregir el DNI tras completar el Paso 1"
Una vez avanzado el paso de identificación, los campos quedan bloqueados. Para corregir:
1. Usa el smart button de "Residente" en la cabecera
2. Edita directamente la ficha del residente (DNI, nombre, fecha nacimiento...)

### "El médico no estaba disponible en el momento del ingreso"
El paso médico es opcional. Avanza sin crear la consulta. Cuando el médico esté disponible:
1. Abre la admisión desde `Centro Sanitario > Admisiones`
2. Si la admisión ya está cerrada, ve directamente a `Atención Médica > Consultas Médicas > Nueva`

### "Quiero ver todas las admisiones en curso"
El filtro por defecto ya muestra solo las que no están cerradas. Si las ves todas:
1. Usa el filtro **"En curso"** de la barra de búsqueda
2. O agrupa por **"Paso"** para ver cuántas hay en cada etapa

### "El PIAI no se creó al cerrar la admisión"
Puede ocurrir si:
- El módulo `cs_piai` no está instalado — instálalo desde Ajustes > Aplicaciones
- Ya existía un PIAI activo para ese residente — el sistema evita duplicados

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| "Nombre completo y DNI son obligatorios" | Falta uno de los dos en el Paso 1 | Rellena ambos campos antes de avanzar |
| "Debe seleccionar una residencia antes de continuar" | Paso 2 sin residencia | Selecciona residencia (habitación es opcional) |
| "Cree primero el residente completando el paso de Identificación" | Intentas crear consulta/evaluación/monedero antes de completar el Paso 1 | Vuelve al Paso 1 y avanza |
| "No se puede reabrir una admisión ya cerrada" | Intentas retroceder desde el estado "Cerrado" | La admisión cerrada es definitiva — actúa directamente sobre los registros vinculados |
| "Solo se puede completar la admisión desde el paso Economía" | Usas el botón "Completar" desde un paso diferente | Avanza hasta el Paso 7 (Economía) |
| No aparecen habitaciones disponibles | Todas las habitaciones están ocupadas o en mantenimiento | Ve a `Centro Sanitario > Habitaciones` y verifica disponibilidad |
