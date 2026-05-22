# Guía de usuario — cs_residential_stock: Inventario residencial

## ¿Para qué sirve este módulo?

`cs_residential_stock` extiende el módulo de **Inventario** de Odoo para añadir:

1. **Ubicaciones de stock vinculadas a residencias y habitaciones** — cada residencia tiene su propia ubicación de almacén dentro de la jerarquía estándar de Odoo.
2. **Categorías de suministro residencial en productos** — clasificar productos según su uso en el centro (comida, limpieza, farmacia, material sanitario, higiene personal).
3. **Campos adicionales en albaranes y movimientos** — vincular movimientos de stock a un residente, zona de limpieza o firma del responsable.

El resultado: el equipo puede ver el stock exacto en cada residencia (y habitación), registrar consumos por residente, y tener trazabilidad de los suministros del centro.

---

## Acceso al módulo

El módulo no tiene menú propio; sus funciones están integradas en el módulo **Inventario** de Odoo:

| Dónde acceder | Ruta |
|---------------|------|
| Ver existencias por ubicación | Inventario → Control de existencias → **Almacenes residenciales** → **Existencias por ubicación** |
| Ver árbol de ubicaciones residenciales | Inventario → Control de existencias → **Almacenes residenciales** → **Ubicaciones (árbol)** |
| Productos clasificados | Inventario → Control de existencias → **Productos Equilibrium** |
| Existencias de una residencia | Ficha de Residencia → botón **Stock de residencia** |

---

## Parte 1 — Jerarquía de ubicaciones

Al instalar el módulo y crear una residencia, se genera automáticamente la siguiente estructura de ubicaciones en el almacén principal de Odoo:

```
[Almacén principal]
└── Almacenes residenciales      ← raíz común (creada automáticamente)
    ├── EQ1                      ← ubicación de Residencia 1
    │   ├── Habitación 101       ← ubicación de habitación (si se crea)
    │   └── Habitación 102
    └── EQ2                      ← ubicación de Residencia 2
```

- La **raíz "Almacenes residenciales"** es un hijo directo del stock principal del almacén de la compañía.
- Cada **residencia** tiene su propia ubicación interna. El nombre de la ubicación se actualiza automáticamente si se cambia el nombre o código de la residencia.
- Las **habitaciones** pueden tener su propia sub-ubicación dentro de la residencia (configurado desde la ficha de la habitación en cs_resident).

### Generar la ubicación de una residencia manualmente

Si la residencia se creó antes de instalar el módulo o sin almacén configurado:

1. Abrir la ficha de la residencia (Menú Equilibrium → Residencias → seleccionar una).
2. Pulsar **Generar ubicación de stock**.
3. La ubicación se crea bajo "Almacenes residenciales" y queda visible en el campo **Ubicación de stock de la residencia**.

> **Requisito previo:** Debe existir al menos un almacén en Inventario para la compañía activa.

---

## Parte 2 — Productos Equilibrium

Los productos del catálogo de Odoo pueden marcarse con una **categoría de suministro residencial** para filtrarlos y gestionarlos de forma diferenciada.

### Clasificar un producto

1. Ir a la ficha del producto (Inventario → Productos, o Compra → Productos).
2. Pestaña **Inventario** → campo **Categoría suministro residencial**.
3. Seleccionar la categoría apropiada.

| Categoría | Ejemplos |
|-----------|---------|
| **Comida** | Alimentos, bebidas, suplementos dietéticos |
| **Limpieza** | Detergentes, desinfectantes, bayetas, fregonas |
| **Farmacia** | Medicamentos, preparados farmacéuticos |
| **Material sanitario** | Guantes, gasas, jeringuillas, termómetros |
| **Higiene personal** | Jabón, champú, pañales, toallitas |
| **Otros** | Cualquier suministro que no encaje en las anteriores |

Los productos sin categoría residencial no aparecen en la vista **Productos Equilibrium**.

### Ver todos los productos Equilibrium

> Inventario → Control de existencias → **Productos Equilibrium**

Muestra solo los productos con categoría residencial asignada. Permite kanban, lista o formulario.

---

## Parte 3 — Ver existencias por ubicación

### Desde el menú global

> Inventario → Control de existencias → **Almacenes residenciales** → **Existencias por ubicación**

Muestra el stock de **todas las residencias** agrupado por ubicación. Permite ver de un vistazo qué stock hay en cada residencia y habitación.

### Desde la ficha de una residencia

1. Abrir la ficha de la residencia (cs_resident → Residencias).
2. Pulsar el smart button **Existencias** (o botón **Ver stock de residencia**).
3. Se abre la vista filtrada para esa residencia concreta, agrupada por ubicación (habitación).

---

## Parte 4 — Albaranes con información residencial

Cuando se crea o procesa un albarán de inventario (recepción, entrega, transferencia interna), el módulo añade tres campos opcionales en el albarán y en cada línea de movimiento:

| Campo | Nivel | Descripción |
|-------|-------|-------------|
| **Residente** | Albarán y movimiento | Vincula el movimiento a un residente concreto (p. ej. consumo de pañales de un residente específico) |
| **Zona de limpieza** | Albarán y movimiento | Zona del centro donde se consume el producto de limpieza |
| **Firma del responsable** | Albarán y movimiento | Imagen de firma para auditoría del movimiento |

### Propagación automática desde albarán a líneas

- Si se rellena **Residente** en la cabecera del albarán, al confirmar o validar el albarán ese valor se propaga automáticamente a todas las líneas de movimiento que aún no tengan residente asignado.
- Lo mismo para **Zona de limpieza** y **Firma del responsable**.
- Las líneas que ya tengan estos campos informados no se sobreescriben.
- También se propagan en tiempo real al editar los campos del albarán (sin necesidad de confirmar).

### Categoría residencial en líneas de movimiento

- En cada línea de movimiento, el campo **Categoría residencial** se calcula automáticamente desde la categoría del producto (campo de solo lectura para referencia rápida).

---

## Flujo completo con ejemplo real

**Contexto:** Llega el pedido semanal de suministros para Residencia EQ1 (pañales, detergente, guantes).

1. En Inventario, el almacén recibe la notificación de recepción (o se crea un albarán manual):
   - Tipo de operación: `Recepción`.
   - Ubicación destino: `Almacenes residenciales / EQ1`.

2. En el albarán, rellenar:
   - **Residente**: dejar vacío (son suministros generales, no de un residente específico).
   - **Zona de limpieza**: `Baños` (si el detergente es para baños).

3. En las líneas, verificar que cada producto tiene la categoría correcta:
   - Pañales → `Higiene personal`.
   - Detergente → `Limpieza`.
   - Guantes → `Material sanitario`.

4. **Validar** el albarán. El stock se actualiza en `Almacenes residenciales / EQ1`.

5. Al día siguiente, enfermería consume 10 paquetes de guantes para María García:
   - Crear albarán de tipo `Transferencia interna` de EQ1 a Consumo (o Virtual Locations/Production).
   - En cabecera: **Residente** = `María García`.
   - Al confirmar, el residente se propaga a la línea de guantes automáticamente.
   - Validar.

6. Ver el stock actual:
   - Ficha de EQ1 → **Existencias** → ver los guantes reducidos.

---

## Casos de uso frecuentes

### Control de stock de pañales por residente
- Registrar cada consumo con un albarán de transferencia interna con el campo **Residente** rellenado.
- Consultar el historial de movimientos filtrando por residente en la vista de movimientos de stock.

### Asignar stock a una habitación específica
- Crear una sub-ubicación bajo la residencia vinculada a la habitación (desde la ficha de la habitación en cs_resident o desde Inventario → Ubicaciones).
- Los movimientos a esa sub-ubicación aparecen en el árbol de la residencia y en las existencias de la habitación.

### Auditar quién recibió un suministro
- Usar el campo **Firma del responsable** en el albarán o movimiento: subir imagen de la firma o captura.
- La firma queda como adjunto vinculado al movimiento para trazabilidad.

### Ver todo el stock de limpieza del centro
- **Inventario** → **Productos Equilibrium** → filtrar por Categoría: `Limpieza` → ver stock disponible.
- O desde **Existencias por ubicación** → agrupar por producto → filtrar por categoría residencial `Limpieza`.

### Registro de zona de limpieza
- Al registrar consumo de productos de limpieza: rellenar **Zona de limpieza** (`Cocina`, `Baños`, `Habitaciones`, `Lavandería`, `Comedor`, `Otros`).
- Permite informes de consumo por zona para justificar el gasto de productos de limpieza.

---

## Errores y avisos comunes

| Mensaje | Causa | Solución |
|---------|-------|----------|
| `No hay almacén de inventario disponible` | No existe ningún almacén en Inventario para la compañía activa | Crear un almacén en Inventario → Configuración → Almacenes antes de usar las funciones residenciales |
| La ubicación de stock no aparece en la residencia | La residencia se creó sin almacén disponible o antes de instalar el módulo | Abrir la ficha de la residencia y pulsar **Generar ubicación de stock** |
| El campo **Residente** no aparece en el albarán | El módulo cs_residential_stock no está instalado o el usuario no tiene permiso de stock | Verificar instalación del módulo y grupo de usuario |
| El stock no se refleja en la ubicación correcta | El albarán usó una ubicación diferente (p. ej. la raíz del almacén en vez de la ubicación de la residencia) | Verificar que la ubicación destino del albarán es la de la residencia (`Almacenes residenciales / EQ1`) |
| La categoría residencial no aparece en los movimientos | El producto no tiene categoría residencial asignada | Abrir la ficha del producto → pestaña Inventario → asignar la categoría |
