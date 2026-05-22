# Guía de Usuario — cs_purse_pocket
## Monedero y Fondos de Terceros

**Módulo:** `cs_purse_pocket` v19.0.2.0.0  
**Perfil:** Administración, dirección, recepción  
**Menú principal:** `Wallet Pacientes`

---

## ¿Para qué sirve?

Gestiona el dinero que las familias depositan para gastos personales de los residentes (tabaco, ropa, higiene, salidas, etc.). Cada paciente tiene **una cuenta monedero** donde se registran:
- **Recargas** — ingresos de dinero de la familia
- **Consumos/Imputaciones** — gastos descontados del saldo
- **Extractos** — resumen periódico enviado automáticamente a la familia

El sistema notifica a los familiares por email o WhatsApp cuando el saldo baja del umbral configurado, y envía un extracto semanal automático.

---

## Acceso al módulo

```
Menú superior → Wallet Pacientes
```

Submenús:
| Submenú | Qué contiene |
|---------|--------------|
| `Cuentas` | Una cuenta por paciente — el monedero principal |
| `Movimientos` | Todos los apuntes individuales (recargas, consumos, ajustes) |
| `Recargas` | Ingresos de dinero de familiares |
| `Imputaciones` | Gastos repartidos entre uno o varios pacientes |
| `Liquidaciones` | Extractos periódicos (manuales o automáticos) |
| `Categorías` | Tipos de gastos configurables |
| `Vínculos familiares` | Relación paciente ↔ familiar pagador |

---

## Parte 1 — Configuración inicial (una sola vez)

### 1.1 Configurar cuentas contables del monedero

> Requiere rol de administrador contable.

**Ruta:** `Ajustes > (buscar "monedero")` o `Ajustes > Contabilidad > Monedero Pacientes`

| Campo | Descripción | Ejemplo |
|-------|-------------|---------|
| Cuenta pasivo monedero | Cuenta donde se registra el dinero custodiado | `566 — Depósitos recibidos` |
| Cuenta banco/caja monedero | Cuenta de tesorería donde entra el efectivo | `570 — Caja` |
| Diario monedero | Diario contable para los asientos | `Monedero Pacientes` |

### 1.2 Crear categorías de gasto

**Ruta:** `Wallet Pacientes > Categorías > Nuevo`

Las categorías clasifican los movimientos (recargas y consumos) para obtener informes por tipo de gasto.

**Pasos:**
1. Haz clic en **Nuevo**
2. Escribe el nombre (ej: `Tabaco`, `Higiene`, `Salida terapéutica`, `Ropa`)
3. Selecciona el tipo:
   - `Recarga` — solo aparece en recargas
   - `Consumo` — solo aparece en consumos
   - `Ajuste` — solo en ajustes manuales
   - `Ambos` — disponible en todos los movimientos
4. El código se genera automáticamente (editable si quieres uno personalizado)
5. Guarda

**Categorías recomendadas para empezar:**

| Nombre | Tipo |
|--------|------|
| Tabaco | Consumo |
| Higiene personal | Consumo |
| Ropa y calzado | Consumo |
| Salida terapéutica | Consumo |
| Actividad de ocio | Consumo |
| Transferencia familiar | Recarga |
| Efectivo en mano | Recarga |

---

## Parte 2 — Vínculos familiares

### ¿Qué es un vínculo familiar?
Relaciona a un **paciente** con el **familiar o tutor** que paga sus gastos. Un paciente puede tener varios familiares vinculados. Los vínculos determinan:
- Quién puede hacer recargas
- A quién se envían las notificaciones (alertas de saldo bajo, extractos semanales)

### 2.1 Crear un vínculo familiar

**Ruta:** `Wallet Pacientes > Vínculos familiares > Nuevo`

**Requisito previo:** El familiar debe existir como **contacto en Odoo** con la etiqueta `Familiar` (o similar que contenga "famil"). Si no existe, créalo en `Contactos > Nuevo`.

> **Importante:** El familiar debe ser un sub-contacto del paciente en Odoo (padre → hijo en la jerarquía de contactos) para que los campos de selección funcionen correctamente.

**Pasos:**
1. Haz clic en **Nuevo**
2. Campo **Paciente:** selecciona el paciente (filtra por etiqueta "Paciente")
3. Campo **Familiar pagador:** selecciona el familiar (filtra por etiqueta "Familiar")
4. Campo **Parentesco:** escribe la relación (ej: `Madre`, `Padre`, `Cónyuge`, `Tutor legal`)
5. Campo **Canal de notificación:** elige cómo recibirá los avisos
   - `Solo email` — requiere que el familiar tenga email
   - `Solo WhatsApp` — requiere móvil y módulo WhatsApp configurado
   - `Email y WhatsApp` — ambos canales
6. Guarda

> Un paciente no puede ser su propio familiar pagador. El sistema lo impide.

[SCREENSHOT: Ficha vínculo familiar con paciente, familiar y canal configurados]

---

## Parte 3 — Cuenta Monedero (alta del monedero)

### 3.1 Crear la cuenta monedero de un paciente

> Cada paciente puede tener **una sola cuenta monedero** por compañía. El sistema lo impide si intentas crear una segunda.

**Ruta:** `Wallet Pacientes > Cuentas > Nuevo`

**Pasos:**
1. Haz clic en **Nuevo** (la referencia se genera automáticamente: `WALLET/XXXX/NNNNN`)
2. Campo **Paciente:** selecciona el paciente
3. Campo **Responsable:** usuario responsable de esta cuenta (se auto-rellena con el usuario actual)
4. Configura las opciones de alerta:
   - **Umbral alerta saldo bajo (€):** importe mínimo antes de enviar aviso a la familia (por defecto: 50 €)
   - **Activar alerta saldo bajo:** marca/desmarca para activar o desactivar esta alerta
   - **Extracto semanal automático:** activa el envío semanal del extracto a la familia
5. Opciones avanzadas:
   - **Permitir saldo negativo:** si se activa, el paciente puede quedar en negativo
   - **Límite negativo:** máximo negativo permitido (solo visible si "Permitir saldo negativo" está activo)
6. Añade notas si lo necesitas
7. Guarda — el estado inicial es `Abierto`

**Estados posibles:**
| Estado | Significado |
|--------|-------------|
| `Borrador` | Cuenta creada pero no activa todavía |
| `Abierto` | En uso, acepta recargas y consumos |
| `Bloqueado` | Suspendida temporalmente (no acepta movimientos) |
| `Cerrado` | Alta del paciente — la cuenta se cierra con liquidación final |

[SCREENSHOT: Ficha cuenta monedero con saldo, totales y configuración de alertas]

### 3.2 Ver el saldo y resumen de una cuenta

En la ficha de la cuenta verás:
- **Saldo:** saldo actual en tiempo real (calculado de todos los movimientos publicados)
- **Total recargas:** suma histórica de todos los ingresos válidos
- **Total consumos:** suma histórica de todos los gastos válidos

> Desde la ficha del **residente** (`Centro Sanitario > Residentes`) también puedes ver el saldo en el bloque "Datos Económicos" si el paciente tiene monedero abierto.

---

## Parte 4 — Recargas (ingresos de dinero)

### ¿Qué es una recarga?
Documento que registra que un familiar ha ingresado dinero al monedero del paciente. Confirmar una recarga crea automáticamente un movimiento de entrada en el monedero.

### 4.1 Registrar una recarga

**Ruta:** `Wallet Pacientes > Recargas > Nuevo`

**Pasos:**
1. Haz clic en **Nuevo** (referencia automática: `FUND/XXXX/NNNNN`)
2. Campo **Paciente:** selecciona el paciente — el sistema busca automáticamente su monedero
3. Campo **Familiar pagador:** solo aparecen los familiares vinculados a ese paciente más el propio paciente
4. Campo **Monedero:** se rellena automáticamente (un paciente = un monedero)
5. Campo **Importe:** cantidad ingresada (debe ser mayor que 0)
6. Campo **Método de pago:**
   - `Efectivo` — dinero en mano entregado en recepción
   - `Transferencia` — ingreso bancario
   - `Tarjeta` — pago con tarjeta
   - `Otro`
7. Campo **Referencia externa:** (opcional) número de transferencia, resguardo, etc.
8. Añade notas si lo necesitas
9. Haz clic en **Confirmar**

Al confirmar:
- El estado pasa a `Confirmada`
- Se crea automáticamente un movimiento de entrada en el monedero
- El saldo del paciente sube inmediatamente

**Estados:**
| Estado | Acción |
|--------|--------|
| `Borrador` | Recarga creada, no aplicada todavía |
| `Confirmada` | Aplicada al monedero — el saldo ya ha subido |
| `Cancelada` | Anulada (solo administrador de monederos) |

> **Cancelar una recarga confirmada:** genera automáticamente un movimiento de ajuste inverso. Requiere permisos de administrador de monederos.

[SCREENSHOT: Recarga confirmada con paciente, familiar y método de pago]

---

## Parte 5 — Imputaciones (gastos)

### ¿Qué es una imputación?
Documento que descuenta dinero del monedero de uno o varios pacientes por un gasto concreto (compra de tabaco, ropa, actividad, etc.).

### 5.1 Imputación simple (un solo paciente)

**Ruta:** `Wallet Pacientes > Imputaciones > Nuevo`

**Pasos:**
1. Haz clic en **Nuevo** (referencia automática: `ALLOC/XXXX/NNNNN`)
2. Rellena:
   - **Descripción:** qué se ha comprado (ej: `Tabaco semana 20 al 26 mayo`)
   - **Fecha:** fecha del gasto
   - **Categoría:** tipo de gasto (ej: `Tabaco`)
   - **Importe total:** cantidad total del gasto
   - **Método de reparto:** `Manual`
3. En el bloque **Líneas**, haz clic en **Añadir una línea**:
   - Selecciona el **Paciente**
   - El sistema autocompleta su **Monedero**
   - El **Importe** se asigna automáticamente al total (si solo hay un paciente = 100%)
4. Haz clic en **Validar**

Al validar:
- Se descuenta el importe del monedero de cada paciente
- Se crean movimientos de consumo individuales
- El estado pasa a `Validada`

### 5.2 Imputación colectiva (varios pacientes)

Útil cuando un gasto se reparte entre varios residentes (ej: excursión grupal, compra de alimentos especiales).

**Pasos:**
1. Crea la imputación con el importe total
2. Selecciona el **Método de reparto:**
   - `Igualitario` — divide el total entre todos los pacientes en partes iguales
   - `Manual` — tú asignas el importe de cada paciente
   - `Por porcentaje` — indicas el porcentaje de cada paciente
3. Añade una línea por cada paciente
4. Si el método es `Igualitario`, al añadir líneas el sistema reparte automáticamente
5. Si hay 2 pacientes y editas el importe de uno, el otro se ajusta al remanente automáticamente
6. Haz clic en **Validar**

> El sistema valida que la suma de las líneas sea igual al importe total antes de validar.

[SCREENSHOT: Imputación colectiva con 3 pacientes y reparto igualitario]

### 5.3 Cancelar una imputación

Solo el **administrador de monederos** puede cancelar imputaciones ya validadas.

Al cancelar:
- Se generan movimientos de ajuste inversos en cada monedero afectado
- El saldo de los pacientes se restaura
- El estado pasa a `Cancelada`

---

## Parte 6 — Liquidaciones (extractos)

### ¿Qué es una liquidación?
Extracto del monedero para un período concreto que muestra:
- Saldo inicial del período
- Total de recargas del período
- Total de consumos del período
- Total de ajustes
- Saldo final

Se genera manual o automáticamente (cron semanal) y puede enviarse a la familia.

### 6.1 Generar una liquidación manualmente

**Ruta:** `Wallet Pacientes > Liquidaciones > Nuevo`

**Pasos:**
1. Haz clic en **Nuevo** (referencia automática)
2. Campo **Paciente:** selecciona el paciente — el monedero se autoselecciona
3. Campo **Desde / Hasta:** período del extracto
4. Haz clic en **Generar**

Al generar:
- El sistema calcula saldo inicial, recargas, consumos, ajustes y saldo final del período
- El estado pasa a `Confirmada`
- Se vinculan los movimientos del período a la liquidación

### 6.2 Estados de la liquidación

| Estado | Descripción |
|--------|-------------|
| `Borrador` | Creada, pendiente de generar |
| `Confirmada` | Generada con datos calculados |
| `Bloqueada` | Cerrada definitivamente (no editable) |

### 6.3 Liquidación final (cierre del monedero al dar de alta al paciente)

Al dar de alta un paciente, se debe hacer una liquidación final que cierra el monedero:
1. Genera la liquidación con el período completo
2. Haz clic en **Liquidar** (botón en la ficha de la liquidación)
3. El sistema:
   - Si hay saldo positivo: crea un movimiento de cierre que lleva el saldo a cero (dinero a devolver a la familia)
   - Si hay saldo negativo: crea un ajuste de regularización de deuda
   - Cierra el monedero (estado `Cerrado`)

### 6.4 Extracto semanal automático

Si en la cuenta monedero del paciente tienes activado **"Extracto semanal automático"**, cada lunes el sistema:
1. Genera la liquidación de la semana anterior (lunes a domingo)
2. La envía por email y/o WhatsApp a todos los familiares vinculados con ese canal activado

> Si en esa semana no hubo ningún movimiento, no se genera ni envía el extracto.

---

## Parte 7 — Movimientos (auditoría)

### ¿Qué son los movimientos?
Registro inmutable de cada apunte individual en el monedero. Se generan automáticamente al confirmar recargas o validar imputaciones. No se pueden editar ni borrar una vez publicados.

**Ruta:** `Wallet Pacientes > Movimientos`

**Tipos de movimiento:**
| Tipo | Dirección | Origen |
|------|-----------|--------|
| `Recarga` | Entrada (+) | Confirmar una recarga |
| `Consumo` | Salida (−) | Validar una imputación |
| `Ajuste de entrada` | Entrada (+) | Reversión de un consumo |
| `Ajuste de salida` | Salida (−) | Reversión de una recarga |
| `Apertura de liquidación` | Entrada (+) | Proceso de liquidación |
| `Cierre de liquidación` | Salida (−) | Liquidación final al dar de alta |

> Los movimientos publicados **no pueden borrarse**. Solo un administrador de monederos puede revertirlos (genera un movimiento contrario que cancela el efecto).

### 7.1 Revertir un movimiento (solo administradores)

1. Abre el movimiento desde `Wallet Pacientes > Movimientos`
2. Haz clic en **Revertir** (botón visible solo para administradores)
3. Escribe el motivo de la reversión
4. Se crea un movimiento contrario que cancela el efecto en el saldo

---

## Flujo típico completo

### Escenario: Nuevo residente ingresa en el centro

1. **Crear vínculo familiar:** `Wallet Pacientes > Vínculos familiares > Nuevo`
   - Paciente: el residente
   - Familiar pagador: madre/padre/tutor
   - Canal: `Solo email` (si tiene email) o `Email y WhatsApp`

2. **Crear cuenta monedero:** `Wallet Pacientes > Cuentas > Nuevo`
   - Seleccionar el paciente
   - Configurar umbral de alerta (ej: 30 €)
   - Activar extracto semanal
   - Guardar — estado inicial `Abierto`

3. **Primera recarga:** `Wallet Pacientes > Recargas > Nuevo`
   - Paciente + Familiar pagador + Importe + Método de pago
   - Confirmar

4. **Gastos semanales:** `Wallet Pacientes > Imputaciones > Nuevo`
   - Tabaco, higiene, salidas, etc.
   - Un registro por tipo de gasto o un registro semanal consolidado

5. **El extracto se envía solo** cada lunes a la familia (si el extracto automático está activo)

6. **Alta del paciente:** generar liquidación final → Liquidar → el monedero queda cerrado

---

## Casos de uso frecuentes

### "Un familiar llama preguntando cuánto le queda al residente"
1. Ve a `Wallet Pacientes > Cuentas`
2. Busca por nombre del paciente
3. El campo **Saldo** muestra el importe actual

O desde la ficha del residente: `Centro Sanitario > Residentes > [paciente]` → bloque "Datos Económicos".

### "Cobrar la semana de tabaco a varios residentes a la vez"
1. Ve a `Wallet Pacientes > Imputaciones > Nuevo`
2. Descripción: `Tabaco semana 19-25 mayo`
3. Importe total: suma de todos
4. Método: `Igualitario` o `Manual`
5. Añade una línea por cada paciente
6. Validar

### "Me he equivocado en el importe de una recarga"
1. Abre la recarga en `Wallet Pacientes > Recargas`
2. Si está en borrador: edita y confirma correctamente
3. Si ya está confirmada: cancélala (requiere administrador) y crea una nueva con el importe correcto

### "La familia dice que no recibe el extracto semanal"
1. Ve a `Wallet Pacientes > Cuentas` → abre la cuenta del paciente
2. Verifica que **"Extracto semanal automático"** está marcado
3. Ve a `Wallet Pacientes > Vínculos familiares` → abre el vínculo de ese paciente
4. Verifica que el familiar tiene **email** y que el canal incluye `email`
5. Verifica en los ajustes del servidor que el cron `Wallet: extracto semanal` está activo

### "El saldo del residente está en negativo"
Por defecto, el sistema no permite saldo negativo. Si aparece negativo es porque:
- En la cuenta se activó "Permitir saldo negativo"
- Hubo ajustes manuales por un administrador

Para resolverlo: registra una recarga de la familia por el importe necesario para cubrir el negativo.

---

## Alertas automáticas

### Alerta de saldo bajo
- **Cuándo:** diariamente, cuando el saldo cae por debajo del umbral configurado
- **Cooldown:** máximo una alerta cada 7 días por cuenta
- **Destinatarios:** todos los familiares vinculados con canal email o WhatsApp activo
- **Configuración:** umbral en la ficha de la cuenta monedero, campo "Umbral alerta saldo bajo"

### Extracto semanal
- **Cuándo:** cada lunes para la semana anterior (lunes a domingo)
- **Condición:** solo si hubo al menos un movimiento esa semana
- **Destinatarios:** mismos que la alerta de saldo bajo

---

## Errores y avisos comunes

| Situación | Causa | Solución |
|-----------|-------|----------|
| "Only one wallet per patient and company" | Ya existe una cuenta monedero para ese paciente | Busca la cuenta existente en `Wallet Pacientes > Cuentas` |
| "No hay saldo suficiente" | El consumo supera el saldo disponible | Registra una recarga primero o activa "Permitir saldo negativo" |
| "El pagador no está vinculado al paciente" | El familiar no existe en `Vínculos familiares` | Crea el vínculo familiar antes de registrar la recarga |
| "Allocated amount must match total amount" | Las líneas de imputación no suman el total | Ajusta los importes de las líneas hasta que cuadren |
| "Wallet account must be in open state" | La cuenta está bloqueada o cerrada | Revisa el estado de la cuenta monedero |
| El familiar no aparece en la lista de pagadores | No tiene vínculo familiar creado o la etiqueta no contiene "famil" | Crea el vínculo o corrige la etiqueta del contacto |
