# Guía de Usuario — cs_cima
## Catálogo de Medicamentos CIMA (AEMPS)

**Módulo:** `cs_cima` v19.0.2.1.0  
**Perfil:** Médicos, enfermería, farmacia  
**Menú principal:** `CIMA`

---

## ¿Para qué sirve?

Conecta el sistema con la base de datos oficial de medicamentos de la **AEMPS** (Agencia Española de Medicamentos y Productos Sanitarios) a través de su API pública CIMA.

Permite:
- Buscar cualquier medicamento autorizado en España por nombre
- Importar la ficha oficial al catálogo local (principios activos, forma, vía, código ATC, laboratorio)
- Vincularlo en prescripciones, analgesia y rescates PRN para autocompletar datos y tener trazabilidad
- Ver indicadores clínicos oficiales: si requiere receta, si afecta a la conducción, triángulo negro, problemas de suministro
- Consultar directamente la ficha CIMA de cada medicamento

> **Gratuito y sin API key.** Usa la API REST pública de la AEMPS — no requiere registro ni credenciales.

---

## Acceso al módulo

```
Menú superior → CIMA
```

Submenús:
| Submenú | Descripción | Acceso |
|---------|-------------|--------|
| `Catálogo de Medicamentos` | Medicamentos ya importados al sistema | Todos |
| `Importar desde CIMA` | Wizard de búsqueda e importación | Todos |
| `Registro de Uso` | Log de usos por medicamento | Solo administradores |

---

## Configuración (una sola vez)

### Activar la conexión con la API CIMA

**Ruta:** `Ajustes > (buscar "CIMA")`

En la sección **CIMA (AEMPS)** encontrarás el toggle:

- **Activar búsqueda CIMA (AEMPS):** actívalo para que el wizard de importación y los campos de búsqueda de catálogo funcionen con datos en tiempo real desde la AEMPS

> Si la opción está desactivada, los campos de catálogo siguen funcionando con los medicamentos ya importados — solo se deshabilita la búsqueda en tiempo real.

---

## Parte 1 — Importar medicamentos desde CIMA

Este es el flujo principal para añadir medicamentos al catálogo local.

### 1.1 Abrir el wizard de importación

**Ruta:** `CIMA > Importar desde CIMA`

Se abre una ventana con un campo de búsqueda.

### 1.2 Buscar un medicamento

1. Escribe al menos **2 caracteres** del nombre del medicamento en el campo **"Buscar en CIMA"**
   - Ejemplos: `lorazepam`, `diazepam`, `omeprazol`, `paracetamol`, `enalapril`
2. Haz clic en **"Buscar"**
3. Aparecen hasta 30 resultados de la AEMPS con:
   - Nombre completo del medicamento
   - Laboratorio titular
   - Estado de comercialización
   - Indicador **"Ya en catálogo"** (si ya fue importado antes)

[SCREENSHOT: Wizard de importación con resultados de búsqueda "lorazepam"]

### 1.3 Seleccionar e importar

1. Marca la casilla **"Importar"** en cada medicamento que quieras añadir
   - Puedes seleccionar varios a la vez
   - Los que ya están en el catálogo muestran el indicador — puedes reimportarlos para actualizar datos
2. Haz clic en **"Importar seleccionados"**
3. El sistema llama a la API para obtener los detalles completos de cada medicamento seleccionado
4. Se abren los registros importados en el catálogo local

> Si un medicamento da error durante la importación (API caída, timeout), el sistema informa qué medicamentos fallaron pero completa los que sí pudieron importarse.

---

## Parte 2 — Catálogo de Medicamentos

### ¿Qué es el catálogo local?
Copia local de los medicamentos importados desde CIMA. El catálogo local es más rápido que llamar a la API en cada uso y permite añadir anotaciones internas del centro.

**Ruta:** `CIMA > Catálogo de Medicamentos`

### 2.1 Información de cada medicamento

| Campo | Origen | Descripción |
|-------|--------|-------------|
| Nombre del Medicamento | CIMA | Nombre oficial |
| Principios Activos | CIMA | Sustancias activas |
| Forma Farmacéutica | CIMA | Comprimido, ampolla, jarabe... |
| Vía de Administración | CIMA | Oral, IV, IM, SC, tópica... |
| Código ATC | CIMA | Clasificación anatómica-terapéutica |
| Descripción ATC | CIMA | Texto del código ATC |
| Laboratorio | CIMA | Titular de la autorización |
| Estado | CIMA | Comercializado / Retirado-Suspendido |
| Nº Registro CIMA | CIMA | Identificador único AEMPS |
| Última Sincronización | Sistema | Fecha de última importación |

### 2.2 Indicadores clínicos

| Indicador | Significado |
|-----------|-------------|
| **Requiere Receta** | Solo se puede dispensar con prescripción médica |
| **Afecta a la Conducción** | Aviso obligatorio para pacientes que conduzcan |
| **Triángulo Negro** (▼) | Medicamento bajo monitorización adicional (autorizado recientemente o con datos limitados) |
| **Problema de Suministro** | La AEMPS ha reportado problemas de abastecimiento |

### 2.3 Enlace directo a la ficha oficial CIMA

Cada medicamento importado tiene un campo **"URL Ficha CIMA"** con enlace directo a `cima.aemps.es`. Desde ahí puedes consultar:
- Ficha técnica completa
- Prospecto para el paciente
- Condiciones de prescripción detalladas
- Alertas y comunicaciones de seguridad

### 2.4 Marcar como favorito del centro

Campo **"Favorito del Centro"** — márcalo en los medicamentos de uso más habitual para encontrarlos más rápido en los formularios de prescripción, analgesia y PRN.

### 2.5 Observaciones internas

Campo **"Observaciones Internas"** — texto libre para notas del centro sobre ese medicamento (protocolos internos, precauciones específicas, sustituciones, etc.). No se sincroniza con CIMA.

### 2.6 Ver el historial de usos de un medicamento

Desde la ficha del medicamento:
1. Mira el campo **"Usos en el Centro"** (contador calculado)
2. Haz clic en el botón **"Ver usos"** para abrir el log detallado

El log muestra cada vez que ese medicamento fue usado, en qué contexto (prescripción, analgesia, PRN) y para qué residente.

---

## Parte 3 — Integración con módulos clínicos

Cuando `cs_cima` está instalado, aparece el campo **"Medicamento (Catálogo)"** en los formularios de:

### 3.1 Líneas de prescripción

En `Atención Médica > Prescripciones`, al añadir una línea de medicamento:

1. Campo **"Buscar en Catálogo CIMA"** — escribe el nombre y busca en el catálogo local
2. Al seleccionarlo:
   - El campo "Nombre del Medicamento" se **autocompleta** con el nombre oficial
   - El campo "Vía" se **autocompleta** con la vía de la ficha CIMA (si el campo estaba vacío)
   - Aparece el enlace **"Ficha CIMA"** para consultar la información completa
3. Se registra automáticamente un **uso en el log** de ese medicamento

> Si el medicamento no está en el catálogo local, primero impórtalo desde `CIMA > Importar desde CIMA`, luego vuelve a la prescripción.

### 3.2 Registros de analgesia

En `Atención Médica > Analgesia`:
- Campo **"Medicamento (Catálogo)"** — igual que en prescripciones
- Al seleccionar: autocompleta "Medicación / medida" y "Vía"

### 3.3 Rescates PRN

En `Atención Médica > Rescates PRN (monitoras)`:
- Campo **"Medicamento (Catálogo)"** — vincula el PRN al catálogo oficial
- Al seleccionar: autocompleta "Medicamento" (nombre texto libre) y "Vía"

### 3.4 Líneas de tratamiento

En `Atención Médica > Tratamientos > Ítems del tratamiento`:
- Campo **"Medicamento (Catálogo)"** — para tratamientos farmacológicos
- Al seleccionar: autocompleta la descripción y la vía

---

## Parte 4 — Registro de uso (solo administradores)

**Ruta:** `CIMA > Registro de Uso`

Log automático de cada vez que un medicamento del catálogo se ha utilizado en el sistema. Se crea automáticamente — no requiere acción manual.

Cada entrada registra:
| Campo | Descripción |
|-------|-------------|
| Medicamento | Qué fármaco se usó |
| Fecha | Cuándo |
| Tipo de Uso | Prescripción / Analgesia / Rescate PRN / Ingreso |
| Residente | Para quién |

Útil para:
- Auditorías de uso de fármacos
- Detectar polimedicación
- Informes de consumo por medicamento

---

## Flujo típico completo

### Escenario: Añadir lorazepam al catálogo y prescribirlo

1. **Importar el medicamento:**
   - `CIMA > Importar desde CIMA`
   - Busca: `lorazepam 1mg`
   - Selecciona el resultado correcto (verifica laboratorio y forma farmacéutica)
   - Haz clic en **"Importar seleccionados"**
   - El medicamento aparece en el catálogo con todos sus datos CIMA

2. **Verificar la ficha:**
   - `CIMA > Catálogo de Medicamentos` → abre el lorazepam importado
   - Comprueba: Requiere Receta ✓, Afecta a la Conducción (si aplica)
   - Marca **"Favorito del Centro"** si es de uso habitual

3. **Prescribir:**
   - `Atención Médica > Prescripciones > Nuevo`
   - Residente + Médico + Fecha
   - Añadir línea → campo "Buscar en Catálogo CIMA" → escribe `lorazepam` → selecciona
   - Se autocompleta nombre y vía → ajusta dosis y frecuencia
   - Activa la prescripción

4. **Resultado:**
   - La prescripción queda vinculada al catálogo oficial
   - Se crea un registro de uso en el log
   - La hoja de emergencias muestra el medicamento con nombre oficial

---

## Casos de uso frecuentes

### "Busco un medicamento y no aparece en el catálogo"
No está importado todavía.
1. Ve a `CIMA > Importar desde CIMA`
2. Búscalo por nombre
3. Impórtalo
4. Vuelve al formulario donde lo necesitabas

### "El medicamento aparece como 'Retirado/Suspendido'"
La AEMPS ha revocado o suspendido su autorización. Informa al médico — es posible que deba prescribirse una alternativa.

### "Quiero saber cuántas veces se ha usado el Diazepam este mes"
1. `CIMA > Catálogo de Medicamentos` → abre la ficha del Diazepam
2. Haz clic en **"Ver usos"** (o el contador de usos)
3. En la lista de usos, filtra por fecha desde el inicio del mes

### "La búsqueda CIMA no devuelve resultados"
Posibles causas:
- La API CIMA está temporalmente caída (servicio público, puede tener mantenimientos)
- La opción "Activar búsqueda CIMA" está desactivada en ajustes
- El término de búsqueda tiene menos de 2 caracteres
- El nombre escrito no coincide con la denominación oficial (prueba con el principio activo)

### "Quiero importar todos los medicamentos habituales del centro de una vez"
El wizard permite importar hasta 30 resultados por búsqueda. Estrategia:
1. Busca por principio activo (ej: `diazepam`, `omeprazol`, `metformina`)
2. Selecciona todas las presentaciones relevantes
3. Importa
4. Repite con cada principio activo habitual

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| "Escribe al menos 2 caracteres para buscar" | Consulta demasiado corta | Escribe más caracteres |
| "Selecciona al menos un medicamento para importar" | No se marcó ningún checkbox | Marca la casilla "Importar" en al menos un resultado |
| "No se encontró el medicamento en CIMA" | El nº de registro no existe o la API falló | Reintenta o busca con otro término |
| El campo "Buscar en Catálogo CIMA" no aparece | `cs_cima` no está instalado | Instala el módulo desde Ajustes > Aplicaciones |
| La URL Ficha CIMA no abre | El nº de registro CIMA es incorrecto o el medicamento fue retirado | Verifica el nregistro en la ficha del catálogo |
| No se autocompleta la vía al seleccionar | El medicamento fue importado antes de que se añadiera el mapeo de vías | Reimporta el medicamento desde el wizard |
