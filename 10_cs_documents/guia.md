# Guía de usuario — cs_documents: Gestión de documentos clínicos y administrativos

## ¿Para qué sirve este módulo?

`cs_documents` proporciona un repositorio centralizado de documentos por residente: contratos de ingreso, consentimientos informados, informes médicos, DNI, autorizaciones, informes de alta y documentación judicial. Cada documento tiene tipo, estado (pendiente → firmado), fechas y archivos adjuntos. El módulo permite saber de un vistazo qué documentación falta para cada residente y dónde está guardada.

---

## Acceso al módulo

> Menú principal → **Documentos** → **Todos los documentos**

También se accede desde la ficha del residente (pestaña **Documentos** o smart button, según configuración del módulo cs_resident).

---

## Parte 1 — Lista de documentos

La lista muestra todos los documentos con código de color:

| Color | Estado |
|-------|--------|
| Amarillo | Pendiente (falta por recibir o firmar) |
| Verde | Firmado |
| Gris | Caducado |

### Filtros rápidos disponibles

| Filtro | Resultado |
|--------|-----------|
| **Pendientes** | Solo documentos con estado `Pendiente` |
| **Firmados** | Solo documentos ya firmados |
| **Agrupar: residente** | Agrupa todos los documentos por residente |
| **Agrupar: tipo** | Agrupa por tipo de documento |
| **Agrupar: estado** | Agrupa por estado |

> [SCREENSHOT: lista de documentos con filas coloreadas y filtros aplicados]

---

## Parte 2 — Tipos de documento

| Tipo | Uso habitual |
|------|-------------|
| **Contrato de ingreso** | Acuerdo firmado al inicio del internamiento |
| **Consentimiento informado** | Autorización del residente o tutor para tratamientos |
| **Informe médico** | Informes externos (hospitalarios, especialistas) |
| **DNI / Pasaporte** | Copia del documento de identidad |
| **Autorización** | Permisos específicos (salidas, visitas, procedimientos) |
| **Informe de alta** | Documentación de salida / alta médica |
| **Documentación judicial** | Tutelas, incapacitaciones, medidas cautelares |
| **Otro** | Cualquier documento que no encaje en las categorías anteriores |

---

## Parte 3 — Estados de un documento

```
Pendiente ──► Recibido ──► Firmado
    │
    └──► Caducado  (cuando vence la fecha de caducidad)
```

| Estado | Significado |
|--------|-------------|
| **Pendiente** | Documento pedido o esperado, aún no recibido |
| **Recibido** | Documento en poder del centro, pendiente de firma o verificación |
| **Firmado** | Documento completado y firmado por todas las partes |
| **Caducado** | Documento que ha superado su fecha de caducidad |

---

## Parte 4 — Crear un documento

1. Ir a **Documentos** → **Todos los documentos** → botón **Nuevo**.
2. Rellenar los campos:

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| **Residente** | Sí | El residente al que pertenece el documento |
| **Tipo de documento** | Sí | Seleccionar de la lista de tipos |
| **Estado** | Sí | Por defecto `Pendiente` |
| **Fecha** | No | Fecha del documento (por defecto hoy) |
| **Fecha de caducidad** | No | Si el documento caduca (p. ej. DNI, autorizaciones temporales) |
| **Archivos adjuntos** | No | Subir uno o varios ficheros (PDF, imagen, Word...) |
| **Observaciones** | No | Notas internas sobre el documento |

3. La **Referencia** se calcula automáticamente con el formato `[Tipo] — [Nombre residente]`.  
   Se puede editar manualmente si se necesita un nombre diferente.
4. Pulsar **Guardar**.

> [SCREENSHOT: formulario de nuevo documento con campos rellenos]

---

## Parte 5 — Adjuntar archivos

Un documento puede tener **varios archivos** adjuntos (p. ej. anverso y reverso de un DNI, varias páginas de un contrato).

- En el formulario, sección **Archivos adjuntos**: arrastrar ficheros o pulsar el botón de subida.
- Formatos admitidos: cualquiera (PDF, JPG, PNG, DOCX, etc.).
- Los adjuntos quedan vinculados al registro y son accesibles desde el chatter del documento o desde la vista de adjuntos de Odoo.

---

## Flujo completo con ejemplo real

**Contexto:** Nuevo ingreso de Pedro Martín. Hay que registrar el contrato de ingreso y el DNI.

1. **Contrato de ingreso:**
   - **Nuevo** → Residente: `Pedro Martín` → Tipo: `Contrato de ingreso` → Estado: `Pendiente`.
   - Guardar. (El contrato está pendiente de que la familia lo firme.)
   - Cuando llega firmado: cambiar estado a `Firmado`, adjuntar el PDF escaneado.

2. **DNI:**
   - **Nuevo** → Residente: `Pedro Martín` → Tipo: `DNI / Pasaporte` → Estado: `Recibido`.
   - Adjuntar foto anverso y reverso.
   - Fecha de caducidad: la que indica el DNI.
   - Guardar.

3. Ir a la lista y filtrar por residente `Pedro Martín` → ver de un vistazo qué documentos faltan (amarillo = pendiente).

---

## Casos de uso frecuentes

### Documentación judicial (tutelas, incapacitaciones)
- Tipo: `Documentación judicial`.
- Adjuntar la resolución judicial en PDF.
- Estado: `Recibido` al tenerla, `Firmado` cuando esté verificada por dirección.
- Sin fecha de caducidad (las tutelas no caducan salvo revisión judicial).

### Autorización temporal de salida
- Tipo: `Autorización`.
- Fecha de caducidad: fecha de fin del permiso.
- Cuando vence, cambiar estado a `Caducado` o crear una nueva autorización si se renueva.

### Buscar todos los documentos pendientes del centro
- Filtro **Pendientes** → vista de todos los documentos amarillos.
- Agrupar por **Agrupar: residente** para ver qué le falta a cada uno.

### Renovar un DNI caducado
- Abrir el documento existente → cambiar estado a `Caducado`.
- Crear nuevo documento tipo `DNI / Pasaporte` con la nueva fecha de caducidad y el fichero actualizado.

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| No aparece el menú **Documentos** | El módulo no está instalado o el usuario no tiene permiso | Pedir al administrador que verifique la instalación y los permisos de grupo |
| La referencia aparece como `Nuevo documento` | No se ha seleccionado residente y tipo todavía | Rellenar ambos campos; la referencia se calcula al guardar |
| No se puede adjuntar un fichero grande | Límite de tamaño de adjunto de Odoo (por defecto 25 MB) | Comprimir el fichero o pedir al administrador que suba el límite en la configuración de sistema |
| El documento no aparece en la ficha del residente | El módulo cs_resident no muestra el smart button de documentos | Acceder desde el menú **Documentos** filtrando por residente |
