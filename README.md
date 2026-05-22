# Guías de Usuario — Sistema Equilibrium

Centro Residencial Equilibrium · Odoo 19.0 Enterprise

---

## Mapa del sistema

```
cs_purse_pocket ──────────────────────────────────────┐
cs_resident (núcleo) ───────────────────────────────┐ │
                                                     ↓ ↓
cs_admission ─────────────────────────────── crea residente + wallet
                    │
                    ├─→ cs_medical_care ──── cs_cima (medicamentos)
                    ├─→ cs_psychology
                    ├─→ cs_monitoring
                    ├─→ cs_patient_followup_forms
                    └─→ cs_piai (depende de todos los anteriores)

cs_documents ─────── adjuntos a residente
cs_dni_ocr ───────── OCR en contactos (pre-admisión)
cs_residential_stock ─ inventario por residencia/habitación
```

---

## Índice de guías

| # | Módulo | Guía | Perfil de usuario |
|---|--------|------|-------------------|
| 1 | `cs_resident` | [Residentes, Residencias, Habitaciones, Trabajadores](01_cs_resident/README.md) | Todos |
| 2 | `cs_purse_pocket` | [Monedero y fondos de terceros](02_cs_purse_pocket/README.md) | Administración |
| 3 | `cs_admission` | [Proceso de admisión guiado](03_cs_admission/README.md) | Admisión / Dirección |
| 4 | `cs_medical_care` | [Atención médica y prescripciones](04_cs_medical_care/README.md) | Médicos / Enfermería |
| 5 | `cs_cima` | [Catálogo de medicamentos CIMA](05_cs_cima/README.md) | Médicos / Farmacia |
| 6 | `cs_psychology` | [Psicología y llamadas familiares](06_cs_psychology/README.md) | Psicólogos |
| 7 | `cs_monitoring` | [Monitoreo diario y guardias](07_cs_monitoring/README.md) | Monitoras |
| 8 | `cs_patient_followup_forms` | [Formularios de seguimiento](08_cs_patient_followup_forms/README.md) | Todos |
| 9 | `cs_piai` | [Plan Individualizado de Atención Integral](09_cs_piai/README.md) | Equipo terapéutico |
| 10 | `cs_documents` | [Gestión de documentos clínicos](10_cs_documents/README.md) | Todos |
| 11 | `cs_dni_ocr` | [OCR de DNI en contactos](11_cs_dni_ocr/README.md) | Admisión |
| 12 | `cs_residential_stock` | [Inventario residencial](12_cs_residential_stock/README.md) | Logística |

---

## Índice completo de secciones

### [1. cs_resident](01_cs_resident/README.md) — Residentes, Residencias, Habitaciones y Trabajadores

- [¿Para qué sirve?](01_cs_resident/README.md#para-qué-sirve)
- [Acceso al módulo](01_cs_resident/README.md#acceso-al-módulo)
- [Parte 1 — Residencias](01_cs_resident/README.md#parte-1--residencias)
- [Parte 2 — Habitaciones](01_cs_resident/README.md#parte-2--habitaciones)
- [Parte 3 — Trabajadores](01_cs_resident/README.md#parte-3--trabajadores)
- [Parte 4 — Residentes](01_cs_resident/README.md#parte-4--residentes)
- [Flujo típico completo](01_cs_resident/README.md#flujo-típico-completo)
- [Casos de uso frecuentes](01_cs_resident/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](01_cs_resident/README.md#errores-y-avisos-comunes)

### [2. cs_purse_pocket](02_cs_purse_pocket/README.md) — Monedero y Fondos de Terceros

- [¿Para qué sirve?](02_cs_purse_pocket/README.md#para-qué-sirve)
- [Acceso al módulo](02_cs_purse_pocket/README.md#acceso-al-módulo)
- [Parte 1 — Configuración inicial](02_cs_purse_pocket/README.md#parte-1--configuración-inicial-una-sola-vez)
- [Parte 2 — Vínculos familiares](02_cs_purse_pocket/README.md#parte-2--vínculos-familiares)
- [Parte 3 — Cuenta Monedero](02_cs_purse_pocket/README.md#parte-3--cuenta-monedero-alta-del-monedero)
- [Parte 4 — Recargas](02_cs_purse_pocket/README.md#parte-4--recargas-ingresos-de-dinero)
- [Parte 5 — Imputaciones](02_cs_purse_pocket/README.md#parte-5--imputaciones-gastos)
- [Parte 6 — Liquidaciones](02_cs_purse_pocket/README.md#parte-6--liquidaciones-extractos)
- [Parte 7 — Movimientos](02_cs_purse_pocket/README.md#parte-7--movimientos-auditoría)
- [Flujo típico completo](02_cs_purse_pocket/README.md#flujo-típico-completo)
- [Alertas automáticas](02_cs_purse_pocket/README.md#alertas-automáticas)
- [Casos de uso frecuentes](02_cs_purse_pocket/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](02_cs_purse_pocket/README.md#errores-y-avisos-comunes)

### [3. cs_admission](03_cs_admission/README.md) — Proceso de Admisión Guiado

- [¿Para qué sirve?](03_cs_admission/README.md#para-qué-sirve)
- [Acceso al módulo](03_cs_admission/README.md#acceso-al-módulo)
- [Los 7 pasos del proceso](03_cs_admission/README.md#los-7-pasos-del-proceso)
- [Paso 1 — Identificación](03_cs_admission/README.md#paso-1--identificación)
- [Paso 2 — Ubicación](03_cs_admission/README.md#paso-2--ubicación)
- [Paso 3 — Médico](03_cs_admission/README.md#paso-3--médico-opcional)
- [Paso 4 — Psicología](03_cs_admission/README.md#paso-4--psicología)
- [Paso 5 — Enfermería](03_cs_admission/README.md#paso-5--enfermería)
- [Paso 6 — Documentación](03_cs_admission/README.md#paso-6--documentación)
- [Paso 7 — Economía](03_cs_admission/README.md#paso-7--economía)
- [Completar la admisión](03_cs_admission/README.md#completar-la-admisión)
- [Accesos rápidos (smart buttons)](03_cs_admission/README.md#accesos-rápidos-smart-buttons)
- [Flujo típico completo](03_cs_admission/README.md#flujo-típico-completo)
- [Casos de uso frecuentes](03_cs_admission/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](03_cs_admission/README.md#errores-y-avisos-comunes)

### [4. cs_medical_care](04_cs_medical_care/README.md) — Atención Médica

- [¿Para qué sirve?](04_cs_medical_care/README.md#para-qué-sirve)
- [Acceso al módulo](04_cs_medical_care/README.md#acceso-al-módulo)
- [Parte 1 — Consultas Médicas](04_cs_medical_care/README.md#parte-1--consultas-médicas)
- [Parte 2 — Prescripciones](04_cs_medical_care/README.md#parte-2--prescripciones)
- [Parte 3 — Tratamientos](04_cs_medical_care/README.md#parte-3--tratamientos)
- [Parte 4 — Analgesia](04_cs_medical_care/README.md#parte-4--analgesia)
- [Parte 5 — Rescates asistenciales](04_cs_medical_care/README.md#parte-5--rescates-asistenciales)
- [Parte 6 — Tests y pruebas clínicas](04_cs_medical_care/README.md#parte-6--tests-y-pruebas-clínicas)
- [Parte 7 — Rescates PRN (monitoras)](04_cs_medical_care/README.md#parte-7--rescates-prn-monitoras)
- [Parte 8 — Seguimiento médico](04_cs_medical_care/README.md#parte-8--seguimiento-médico)
- [Parte 9 — Historia clínica](04_cs_medical_care/README.md#parte-9--historia-clínica-básica)
- [Parte 10 — Hoja de Emergencias](04_cs_medical_care/README.md#parte-10--hoja-de-emergencias)
- [Flujo típico completo](04_cs_medical_care/README.md#flujo-típico-completo)
- [Casos de uso frecuentes](04_cs_medical_care/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](04_cs_medical_care/README.md#errores-y-avisos-comunes)

### [5. cs_cima](05_cs_cima/README.md) — Catálogo de Medicamentos CIMA

- [¿Para qué sirve?](05_cs_cima/README.md#para-qué-sirve)
- [Acceso al módulo](05_cs_cima/README.md#acceso-al-módulo)
- [Configuración inicial](05_cs_cima/README.md#configuración-una-sola-vez)
- [Parte 1 — Importar desde CIMA](05_cs_cima/README.md#parte-1--importar-medicamentos-desde-cima)
- [Parte 2 — Catálogo de Medicamentos](05_cs_cima/README.md#parte-2--catálogo-de-medicamentos)
- [Parte 3 — Integración con módulos clínicos](05_cs_cima/README.md#parte-3--integración-con-módulos-clínicos)
- [Parte 4 — Registro de uso](05_cs_cima/README.md#parte-4--registro-de-uso-solo-administradores)
- [Flujo típico completo](05_cs_cima/README.md#flujo-típico-completo)
- [Casos de uso frecuentes](05_cs_cima/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](05_cs_cima/README.md#errores-y-avisos-comunes)

### [6. cs_psychology](06_cs_psychology/README.md) — Psicología y Llamadas Familiares

- [¿Para qué sirve?](06_cs_psychology/README.md#para-qué-sirve)
- [Acceso al módulo](06_cs_psychology/README.md#acceso-al-módulo)
- [Parte 1 — Evaluación psicológica inicial](06_cs_psychology/README.md#parte-1--evaluación-psicológica-inicial)
- [Parte 2 — Sesiones de psicología](06_cs_psychology/README.md#parte-2--sesiones-de-psicología)
- [Parte 3 — Citas en el calendario](06_cs_psychology/README.md#parte-3--citas-en-el-calendario)
- [Parte 4 — Llamadas y contactos familiares](06_cs_psychology/README.md#parte-4--llamadas-y-contactos-familiares)
- [Flujo típico completo](06_cs_psychology/README.md#flujo-típico-completo)
- [Casos de uso frecuentes](06_cs_psychology/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](06_cs_psychology/README.md#errores-y-avisos-comunes)

### [7. cs_monitoring](07_cs_monitoring/README.md) — Monitorización diaria

- [¿Para qué sirve?](07_cs_monitoring/README.md#para-qué-sirve-este-módulo)
- [Acceso al módulo](07_cs_monitoring/README.md#acceso-al-módulo)
- [Parte 1 — Checklists diarios](07_cs_monitoring/README.md#parte-1--checklists-diarios)
- [Parte 2 — Plantillas de checklist](07_cs_monitoring/README.md#parte-2--plantillas-de-checklist)
- [Parte 3 — Temperaturas corporales](07_cs_monitoring/README.md#parte-3--temperaturas-corporales)
- [Parte 4 — Temperaturas de alimentos (HACCP)](07_cs_monitoring/README.md#parte-4--temperaturas-de-alimentos-haccp)
- [Parte 5 — Guardias de monitoras](07_cs_monitoring/README.md#parte-5--guardias-de-monitoras)
- [Flujo completo con ejemplo real](07_cs_monitoring/README.md#flujo-completo-con-ejemplo-real)
- [Casos de uso frecuentes](07_cs_monitoring/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](07_cs_monitoring/README.md#errores-y-avisos-comunes)

### [8. cs_patient_followup_forms](08_cs_patient_followup_forms/README.md) — Motor de formularios dinámicos

- [¿Para qué sirve?](08_cs_patient_followup_forms/README.md#para-qué-sirve-este-módulo)
- [Acceso al módulo](08_cs_patient_followup_forms/README.md#acceso-al-módulo)
- [Arquitectura del módulo](08_cs_patient_followup_forms/README.md#arquitectura-del-módulo)
- [Parte 1 — Crear una plantilla](08_cs_patient_followup_forms/README.md#parte-1--crear-una-plantilla)
- [Parte 2 — Crear una evaluación](08_cs_patient_followup_forms/README.md#parte-2--crear-una-evaluación)
- [Parte 3 — Rellenar una evaluación](08_cs_patient_followup_forms/README.md#parte-3--rellenar-una-evaluación)
- [Parte 4 — Exportar a PDF](08_cs_patient_followup_forms/README.md#parte-4--exportar-a-pdf)
- [Parte 5 — Estados de una evaluación](08_cs_patient_followup_forms/README.md#parte-5--estados-de-una-evaluación)
- [Flujo completo con ejemplo real](08_cs_patient_followup_forms/README.md#flujo-completo-con-ejemplo-real)
- [Casos de uso frecuentes](08_cs_patient_followup_forms/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](08_cs_patient_followup_forms/README.md#errores-y-avisos-comunes)

### [9. cs_piai](09_cs_piai/README.md) — Plan Individualizado de Atención Integral

- [¿Para qué sirve?](09_cs_piai/README.md#para-qué-sirve-este-módulo)
- [Acceso al módulo](09_cs_piai/README.md#acceso-al-módulo)
- [Parte 1 — Ciclo de vida del PIAI](09_cs_piai/README.md#parte-1--ciclo-de-vida-del-piai)
- [Parte 2 — Crear un PIAI](09_cs_piai/README.md#parte-2--crear-un-piai)
- [Parte 3 — Valoraciones Iniciales](09_cs_piai/README.md#parte-3--valoraciones-iniciales)
- [Parte 4 — Diagnóstico / Formulación](09_cs_piai/README.md#parte-4--diagnóstico--formulación)
- [Parte 5 — Objetivos Terapéuticos](09_cs_piai/README.md#parte-5--objetivos-terapéuticos)
- [Parte 6 — Intervenciones](09_cs_piai/README.md#parte-6--intervenciones)
- [Parte 7 — Riesgos y Alertas Clínicas](09_cs_piai/README.md#parte-7--riesgos-y-alertas-clínicas)
- [Parte 8 — Plan Familiar y Restricciones](09_cs_piai/README.md#parte-8--plan-familiar-y-restricciones)
- [Parte 9 — Revisiones del PIAI](09_cs_piai/README.md#parte-9--revisiones-del-piai)
- [Parte 10 — Notas de Evolución](09_cs_piai/README.md#parte-10--notas-de-evolución)
- [Parte 11 — Plan de Prevención de Recaídas](09_cs_piai/README.md#parte-11--plan-de-prevención-de-recaídas)
- [Parte 12 — Plan de Alta](09_cs_piai/README.md#parte-12--plan-de-alta)
- [Parte 13 — Firmas y Validaciones](09_cs_piai/README.md#parte-13--firmas-y-validaciones)
- [Parte 14 — Registros integrados de otros módulos](09_cs_piai/README.md#parte-14--registros-integrados-de-otros-módulos)
- [Parte 15 — Informes PDF](09_cs_piai/README.md#parte-15--informes-pdf)
- [Flujo completo con ejemplo real](09_cs_piai/README.md#flujo-completo-con-ejemplo-real)
- [Vista de Monitoras](09_cs_piai/README.md#vista-de-monitoras-menú-residentes)
- [Errores y avisos comunes](09_cs_piai/README.md#errores-y-avisos-comunes)

### [10. cs_documents](10_cs_documents/README.md) — Gestión de documentos clínicos

- [¿Para qué sirve?](10_cs_documents/README.md#para-qué-sirve-este-módulo)
- [Acceso al módulo](10_cs_documents/README.md#acceso-al-módulo)
- [Parte 1 — Lista de documentos](10_cs_documents/README.md#parte-1--lista-de-documentos)
- [Parte 2 — Tipos de documento](10_cs_documents/README.md#parte-2--tipos-de-documento)
- [Parte 3 — Estados de un documento](10_cs_documents/README.md#parte-3--estados-de-un-documento)
- [Parte 4 — Crear un documento](10_cs_documents/README.md#parte-4--crear-un-documento)
- [Parte 5 — Adjuntar archivos](10_cs_documents/README.md#parte-5--adjuntar-archivos)
- [Flujo completo con ejemplo real](10_cs_documents/README.md#flujo-completo-con-ejemplo-real)
- [Casos de uso frecuentes](10_cs_documents/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](10_cs_documents/README.md#errores-y-avisos-comunes)

### [11. cs_dni_ocr](11_cs_dni_ocr/README.md) — OCR de DNI/NIE

- [¿Para qué sirve?](11_cs_dni_ocr/README.md#para-qué-sirve-este-módulo)
- [Acceso al módulo](11_cs_dni_ocr/README.md#acceso-al-módulo)
- [Parte 1 — Pestaña DNI OCR en el contacto](11_cs_dni_ocr/README.md#parte-1--pestaña-dni-ocr-en-el-contacto)
- [Parte 2 — Estados de una captura](11_cs_dni_ocr/README.md#parte-2--estados-de-una-captura)
- [Parte 3 — Flujo desde WhatsApp](11_cs_dni_ocr/README.md#parte-3--flujo-de-importación-desde-whatsapp)
- [Parte 4 — Subida directa de imagen](11_cs_dni_ocr/README.md#parte-4--subida-directa-de-imagen-sin-whatsapp)
- [Parte 5 — Qué hace el OCR](11_cs_dni_ocr/README.md#parte-5--qué-hace-el-ocr-automáticamente)
- [Parte 6 — Resolución manual](11_cs_dni_ocr/README.md#parte-6--resolución-manual-estado-revisión)
- [Flujo completo con ejemplo real](11_cs_dni_ocr/README.md#flujo-completo-con-ejemplo-real)
- [Casos de uso frecuentes](11_cs_dni_ocr/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](11_cs_dni_ocr/README.md#errores-y-avisos-comunes)

### [12. cs_residential_stock](12_cs_residential_stock/README.md) — Inventario residencial

- [¿Para qué sirve?](12_cs_residential_stock/README.md#para-qué-sirve-este-módulo)
- [Acceso al módulo](12_cs_residential_stock/README.md#acceso-al-módulo)
- [Parte 1 — Jerarquía de ubicaciones](12_cs_residential_stock/README.md#parte-1--jerarquía-de-ubicaciones)
- [Parte 2 — Productos Equilibrium](12_cs_residential_stock/README.md#parte-2--productos-equilibrium)
- [Parte 3 — Ver existencias por ubicación](12_cs_residential_stock/README.md#parte-3--ver-existencias-por-ubicación)
- [Parte 4 — Albaranes con información residencial](12_cs_residential_stock/README.md#parte-4--albaranes-con-información-residencial)
- [Flujo completo con ejemplo real](12_cs_residential_stock/README.md#flujo-completo-con-ejemplo-real)
- [Casos de uso frecuentes](12_cs_residential_stock/README.md#casos-de-uso-frecuentes)
- [Errores y avisos comunes](12_cs_residential_stock/README.md#errores-y-avisos-comunes)

---

## Orden recomendado de lectura (nuevo empleado)

1. Guía 1 (residentes) — base conceptual
2. Guía 11 (OCR DNI) — antes de dar de alta pacientes
3. Guía 3 (admisión) — proceso de ingreso completo
4. Guía 2 (monedero) — si gestionas economía del paciente
5. Guías 4–7 según tu rol clínico
6. Guía 9 (PIAI) — cuando domines las guías 4–7
