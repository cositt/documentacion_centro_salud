# Guía de usuario — cs_dni_ocr: OCR de DNI/NIE

## ¿Para qué sirve este módulo?

`cs_dni_ocr` permite fotografiar el DNI o NIE de un futuro residente (anverso y reverso) y extraer automáticamente su número identificativo, nombre completo y dirección mediante OCR (reconocimiento óptico de caracteres). El resultado se graba directamente en la ficha del contacto de Odoo, eliminando la transcripción manual y los errores asociados.

Flujo típico: el familiar o trabajador envía fotos del DNI por WhatsApp → el sistema las importa, ejecuta OCR y rellena el campo NIF/VAT del contacto.

---

## Acceso al módulo

El módulo no tiene menú propio. Toda la funcionalidad se accede desde la ficha de un **Contacto**:

> Contactos → (abre un contacto) → pestaña **DNI OCR**

---

## Parte 1 — Pestaña DNI OCR en el contacto

Cuando se instala el módulo, todos los contactos de Odoo ganan una nueva pestaña **DNI OCR** con:

| Elemento | Descripción |
|----------|-------------|
| **DNI/NIE extraído** | Último número identificativo reconocido (solo lectura) |
| **Nueva captura desde WhatsApp (anverso)** | Botón para crear captura e importar anverso desde adjuntos de WhatsApp del contacto |
| **Nueva captura desde WhatsApp (reverso)** | Igual para el reverso |
| **Tabla de capturas** | Lista de todas las capturas OCR vinculadas al contacto |

### Campos de la tabla de capturas

| Campo | Significado |
|-------|-------------|
| Referencia | Nombre de la captura (editable) |
| DNI anverso | Imagen del anverso (subida o importada de WhatsApp) |
| DNI reverso | Imagen del reverso |
| DNI/NIE | Número extraído o escrito manualmente |
| Estado | `Borrador` → `Procesado` / `Revisión` / `Error` |

---

## Parte 2 — Estados de una captura

```
Borrador ──► [Procesar OCR] ──► Procesado  (DNI/NIE detectado automáticamente)
                           └──► Revisión   (OCR terminó pero no encontró DNI válido)
                                    │
                                    ▼
                              [Confirmar DNI] ──► Procesado
                              (revisión manual)
```

| Estado | Significado |
|--------|-------------|
| **Borrador** | Imágenes subidas, aún no procesadas |
| **Procesado** | OCR completado, DNI/NIE aplicado al contacto |
| **Revisión** | OCR terminó sin DNI válido — requiere corrección manual |
| **Error** | Fallo técnico en el proceso (p. ej. tesseract no instalado) |

---

## Parte 3 — Flujo de importación desde WhatsApp

El caso más habitual en Equilibrium: el familiar envía fotos del DNI por WhatsApp, que llegan como adjuntos en el chat del contacto.

### Paso a paso

1. Abrir la ficha del contacto (Contactos → buscar por nombre).
2. Ir a la pestaña **DNI OCR**.
3. Pulsar **Nueva captura desde WhatsApp (anverso)**.
4. Se abre el wizard **Seleccionar imagen de WhatsApp**:
   - El campo **Aplicar a** viene preseleccionado (`Anverso`).
   - La lista **Imagen de WhatsApp** muestra los adjuntos de imagen vinculados al contacto (ordenados por fecha, más recientes primero). Incluye imágenes recibidas por WhatsApp en el chat del contacto.
5. Seleccionar la imagen del anverso del DNI → pulsar **Aplicar**.
6. Repetir con **Nueva captura desde WhatsApp (reverso)** o usar el botón **Subir desde WhatsApp (reverso)** dentro de la fila de la captura recién creada.
7. Con anverso y reverso cargados, pulsar **Procesar OCR** en la fila de la captura.
8. El sistema ejecuta tesseract-ocr en el servidor y en segundos actualiza el estado.

> [SCREENSHOT: wizard de selección de imagen WhatsApp mostrando lista de adjuntos del contacto]

---

## Parte 4 — Subida directa de imagen (sin WhatsApp)

Si las fotos no llegaron por WhatsApp sino por email o USB:

1. En la tabla de capturas, hacer clic en el icono de descarga del campo **DNI anverso** y subir el fichero JPG/PNG.
2. Repetir para **DNI reverso**.
3. Pulsar **Procesar OCR**.

---

## Parte 5 — Qué hace el OCR automáticamente

Al pulsar **Procesar OCR** el sistema:

1. Ejecuta `tesseract-ocr` (idioma `spa+eng`) sobre anverso y reverso.
2. Extrae el texto bruto de cada cara.
3. Detecta el número DNI/NIE con validación del dígito de control.
4. Extrae nombre completo (bloques APELLIDOS + NOMBRE del DNI), dirección y país si aparecen en el reverso.
5. Guarda adjuntos de evidencia vinculados a la captura.
6. **Si DNI/NIE detectado:**
   - Estado → **Procesado**
   - Rellena el campo `DNI/NIE extraído` en el contacto.
   - Si el campo NIF/VAT del contacto estaba **vacío**, lo rellena automáticamente.
   - Si el nombre, dirección o ciudad del contacto estaban **vacíos**, los rellena con los datos OCR. *(Nunca pisa datos ya existentes.)*
   - Añade mensaje en el chatter del contacto confirmando el reconocimiento.
7. **Si no detectado:**
   - Estado → **Revisión**
   - Añade mensaje en el chatter explicando el motivo.

---

## Parte 6 — Resolución manual (estado Revisión)

Cuando el OCR no puede leer el DNI (foto borrosa, reflejos, DNI deteriorado):

1. Pulsar **Ver resultado** en la fila de la captura — se abre la ficha completa con el texto OCR extraído en pestañas.
2. Revisar el texto del anverso y reverso para localizar el número.
3. Escribir el número correcto en el campo **DNI/NIE** de la fila (formato: `12345678A` para DNI, `X1234567A` para NIE).
4. Pulsar **Confirmar DNI**.
   - El sistema valida el dígito de control.
   - Si es correcto: estado → **Procesado**, aplica al contacto.
   - Si es incorrecto: muestra error con instrucciones de formato.

> [SCREENSHOT: fila en estado Revisión con campo DNI/NIE editable y botón Confirmar DNI]

---

## Flujo completo con ejemplo real

**Contexto:** Ingresa María García López. Su hija envía fotos del DNI por WhatsApp.

1. Ir a **Contactos** → abrir o crear contacto "María García López".
2. En el chat del contacto, las fotos de WhatsApp ya aparecen como adjuntos.
3. Pestaña **DNI OCR** → **Nueva captura desde WhatsApp (anverso)**.
4. Wizard: seleccionar la imagen del anverso → **Aplicar**.
5. En la tabla: botón **Subir desde WhatsApp (reverso)** → seleccionar reverso → **Aplicar**.
6. Pulsar **Procesar OCR**.
7. Resultado en 3–5 segundos:
   - Estado: **Procesado**
   - DNI/NIE: `12345678Z`
   - Campo NIF/VAT del contacto: `12345678Z` (si estaba vacío)
   - Campo DNI/NIE extraído: `12345678Z`
8. En la pestaña principal del contacto, NIF/VAT ya aparece relleno. La admisión puede continuar.

---

## Casos de uso frecuentes

### Foto enviada por WhatsApp pero no aparece en el wizard
- Verificar que la imagen está vinculada al contacto correcto (no a otro).
- El wizard muestra máximo 200 adjuntos recientes. Si hay muchos, buscar por nombre de fichero.
- Alternativa: descargar la imagen del móvil y subirla directamente en el campo **DNI anverso**.

### DNI de NIE (extranjero)
- Funciona igual. El sistema detecta formato `X/Y/Z + 7 dígitos + letra` y valida el dígito de control NIE.

### El NIF/VAT ya tenía un valor diferente
- El sistema **no lo sobreescribe**. Solo rellena NIF/VAT si estaba vacío.
- El número detectado sí queda guardado en **DNI/NIE extraído** para referencia.
- Si necesitas actualizar el NIF/VAT, edítalo manualmente en la pestaña principal del contacto.

### Varias capturas para el mismo contacto
- Se puede acumular múltiples capturas (p. ej. renovación de DNI, segunda lectura con mejor foto).
- Cada captura es independiente. El campo **DNI/NIE extraído** del contacto refleja el último número aplicado.

### El contacto ya tiene NIF/VAT correcto
- Crear la captura sirve igualmente para guardar evidencia documental (las imágenes quedan como adjuntos en el registro de captura).

---

## Errores y avisos comunes

| Mensaje / Situación | Causa | Solución |
|---------------------|-------|----------|
| `No se encontró tesseract en el servidor` | tesseract-ocr no está instalado en el servidor Odoo | Pedir al administrador que instale `tesseract-ocr` y `tesseract-ocr-spa` |
| Estado → Revisión sin error | Foto con reflejos, borrosa o DNI muy deteriorado | Usar foto con más luz, sin flash directo; o escribir el número manualmente y pulsar Confirmar DNI |
| `Indique un DNI/NIE válido` al confirmar | El número escrito no supera la validación del dígito de control | Verificar el número letra a letra; el formato exacto es `8 dígitos + letra` (DNI) o `X/Y/Z + 7 dígitos + letra` (NIE) |
| `El adjunto seleccionado no contiene binario accesible` | El adjunto de WhatsApp no tiene datos binarios accesibles (enlace externo sin descarga local) | Descargar la imagen en el móvil, guardarla como archivo y subirla directamente |
| NIF/VAT no se actualiza aunque OCR funciona | El contacto ya tenía NIF/VAT con valor | Comportamiento correcto (no se pisa). Actualizar manualmente si hace falta |
| `OCR detectó X pero no se pudo guardar también en NIF/VAT` | Módulo de validación VAT rechaza el formato | El número queda en DNI/NIE extraído. Editar NIF/VAT manualmente en la pestaña principal |
