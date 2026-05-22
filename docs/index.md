# Sistema Equilibrium — Documentación

**Centro Residencial Equilibrium · Odoo 19.0 Enterprise**

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

| # | Módulo | Guía | Perfil |
|---|--------|------|--------|
| 1 | `cs_resident` | [Residentes, Residencias, Habitaciones, Trabajadores](01_cs_resident/guia.md) | Todos |
| 2 | `cs_purse_pocket` | [Monedero y fondos de terceros](02_cs_purse_pocket/guia.md) | Administración |
| 3 | `cs_admission` | [Proceso de admisión guiado](03_cs_admission/guia.md) | Admisión / Dirección |
| 4 | `cs_medical_care` | [Atención médica y prescripciones](04_cs_medical_care/guia.md) | Médicos / Enfermería |
| 5 | `cs_cima` | [Catálogo de medicamentos CIMA](05_cs_cima/guia.md) | Médicos / Farmacia |
| 6 | `cs_psychology` | [Psicología y llamadas familiares](06_cs_psychology/guia.md) | Psicólogos |
| 7 | `cs_monitoring` | [Monitoreo diario y guardias](07_cs_monitoring/guia.md) | Monitoras |
| 8 | `cs_patient_followup_forms` | [Formularios de seguimiento](08_cs_patient_followup_forms/guia.md) | Todos |
| 9 | `cs_piai` | [Plan Individualizado de Atención Integral](09_cs_piai/guia.md) | Equipo terapéutico |
| 10 | `cs_documents` | [Gestión de documentos clínicos](10_cs_documents/guia.md) | Todos |
| 11 | `cs_dni_ocr` | [OCR de DNI en contactos](11_cs_dni_ocr/guia.md) | Admisión |
| 12 | `cs_residential_stock` | [Inventario residencial](12_cs_residential_stock/guia.md) | Logística |

---

## Orden recomendado (nuevo empleado)

1. [Guía 1 — Residentes](01_cs_resident/guia.md) — base conceptual
2. [Guía 11 — DNI OCR](11_cs_dni_ocr/guia.md) — antes de dar de alta pacientes
3. [Guía 3 — Admisión](03_cs_admission/guia.md) — proceso de ingreso completo
4. [Guía 2 — Monedero](02_cs_purse_pocket/guia.md) — si gestionas economía del paciente
5. Guías 4–7 según tu rol clínico
6. [Guía 9 — PIAI](09_cs_piai/guia.md) — cuando domines las guías 4–7
