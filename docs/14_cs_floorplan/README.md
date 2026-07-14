# Guía de Usuario — cs_floorplan
## Plano de Residencia

**Módulo:** `cs_floorplan` v1.0.0  
**Depende de:** `cs_resident`  
**Perfil:** Todos (ver plano y reubicar residentes) / Editor de Layout (mover y crear habitaciones)  
**Acceso:** desde la ficha de **Residencia**, botón inteligente **Plantas**

---

## ¿Para qué sirve?

Sustituye el plano en papel/PDF suelto por un **plano interactivo dentro del programa**:

- Vista rápida de qué habitaciones están **libres, ocupadas, parciales o en mantenimiento** (color)
- **Reubicar residentes** arrastrando su nombre de una habitación a otra
- Organizar el plano **a mano** (esquemático, sin imagen de fondo real) — cada centro dibuja su propia distribución
- Varias **plantas** por residencia, cada una con su propio lienzo
- **Imprimir** el plano en PDF

---

## Acceso al módulo

```
Ficha de Residencia → botón "Plantas" → elegir/crear planta → pestaña "Plano"
```

---

## Parte 1 — Plantas

### 1.1 Crear una planta

**Ruta:** ficha de Residencia → botón **Plantas** → Nuevo

| Campo | Obligatorio | Descripción |
|-------|:-----------:|-------------|
| Nombre | ✓ | Ej. "Planta Baja", "Primera Planta" |
| Residencia | ✓ | Se completa sola si venís desde la ficha de residencia |
| Secuencia | — | Orden de aparición en la lista de plantas |

Una residencia puede tener tantas plantas como haga falta — cada una con su propio lienzo independiente.

---

## Parte 2 — El lienzo del plano

### 2.1 Colores de las habitaciones

| Color | Significado |
|-------|-------------|
| 🟢 Verde | Libre (0 ocupados) |
| 🟡 Amarillo | Parcialmente ocupada (queda al menos 1 plaza libre) |
| 🔴 Rojo | Llena (sin plazas libres) |
| ⚪ Gris | En mantenimiento o cerrada |

Cada caja muestra el número de habitación, ocupados/capacidad, y el nombre de cada residente activo alojado ahí dentro.

### 2.2 Reubicar un residente

Arrastrá el nombre del residente desde su caja actual y soltalo sobre la caja de la habitación destino.

- Si la habitación destino **no tiene plazas libres**, se bloquea el movimiento (aviso en pantalla).
- El cambio se guarda al instante — no hace falta guardar la ficha.

> **Importante:** esto solo funciona en **modo vista normal**. Si el botón dice "Terminar edición" estás en modo edición de layout, y ahí los residentes no se pueden arrastrar a propósito — salí de ese modo primero (botón "Terminar edición").

### 2.3 Editar el layout (mover y redimensionar habitaciones)

Solo disponible para usuarios del grupo **"Plano - Editor de Layout"**.

**Ruta:** pestaña Plano → botón **Editar plano**

- Arrastrá una caja para reposicionarla.
- Arrastrá la esquina inferior derecha para redimensionarla.
- Botón **+ Habitación**: crea una habitación nueva directamente en el lienzo (abre el formulario estándar de habitación con la planta y residencia ya completadas).
- Botón **Terminar edición** para volver al modo vista y poder reubicar residentes de nuevo.

### 2.4 ¿Quién puede editar el layout?

| Rol | Ver plano | Reubicar residentes | Mover/crear habitaciones |
|-----|:---------:|:--------------------:|:--------------------------:|
| Usuario interno normal | ✓ | ✓ | ✗ |
| Grupo "Plano - Editor de Layout" | ✓ | ✓ | ✓ |

El grupo se asigna en `Ajustes → Usuarios y Compañías → Usuarios → pestaña Permisos`.

---

## Parte 3 — Imprimir el plano

**Ruta:** ficha de Planta → botón **Imprimir plano**

Genera un PDF con la misma distribución de habitaciones y residentes que ves en pantalla.

---

## Preguntas frecuentes

**¿Por qué no puedo mover una habitación en el plano?**  
Necesitás pertenecer al grupo "Plano - Editor de Layout". Pedile a un administrador que te lo asigne.

**¿Por qué no puedo arrastrar a un residente?**  
Comprobá que no estás en modo "Editar plano" (ahí solo se mueven las cajas de habitación, no los residentes).

**¿Por qué un residente no aparece en el plano?**  
No tiene una habitación asignada todavía. Andá a `Residentes → [residente] → campo Habitación` y asignásela — ahí sí aparece en el lienzo.

**¿Puedo tener varias plantas por residencia?**  
Sí, cada planta es independiente con su propio lienzo y sus propias habitaciones.

**¿El plano usa la imagen real del edificio de fondo?**  
No, es esquemático — vos colocás las cajas a mano representando cada habitación, no hay imagen de plano arquitectónico de fondo.
