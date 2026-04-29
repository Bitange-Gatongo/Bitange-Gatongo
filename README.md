# MMI Kenya — Complete MEL Data System

> A production-grade Monitoring, Evaluation and Learning data system built for a PEPFAR-aligned HIV/PMTCT community health program in Nairobi County informal settlements.

---

## What This Repository Contains

This repository demonstrates a complete, end-to-end MEL data pipeline — from mobile data collection in the field through automated transfer to a live program performance dashboard.

```
Field (CHV tablet)
    │
    ▼
KoBoToolbox Forms          ← Session 1: XLSForm design
    │
    ▼
Python Pipeline            ← Session 3: Automated API transfer
    │
    ▼
DHIS2 Program Dashboard    ← Session 2: Configuration and visualization
```

---

## Repository Structure

```
mmi-kenya-mel-system/
│
├── forms/
│   ├── community-hts-register/
│   │   ├── mmi_hts_v1.xlsx          # XLSForm — Community HTS Register
│   │   └── README.md                # Form documentation
│   │
│   └── mentor-mother-contact-log/
│       ├── mmi_mm_v1.xlsx           # XLSForm — Mentor Mother Contact Log
│       └── README.md                # Form documentation
│
├── pipeline/
│   ├── kobo_to_dhis2_pipeline.py    # KoBoToolbox → DHIS2 automated transfer
│   ├── generate_dhis2_data.py       # Test data generator (12 months)
│   └── README.md                    # Pipeline documentation
│
├── dhis2/
│   └── configuration_guide.md       # DHIS2 setup documentation
│
└── README.md                         # This file
```

---

## Program Context

**Program:** MMI Kenya HIV/PMTCT Community Health Program
**Target population:** HIV-positive pregnant women and key populations in Nairobi County informal settlements (Mathare, Korogocho, Mukuru)
**Facilities:** 5 target public health facilities
**Donor framework:** PEPFAR MER-aligned, USAID RBM framework

---

## MEL System Components

### 1. Data Collection — KoBoToolbox XLSForms

Two production-grade data collection instruments built in XLSForm:

**Community HTS Register** (`mmi_hts_v1.xlsx`)
- 43 questions across 6 sections
- GPS coordinate capture for location verification
- Advanced skip logic — 15 relevant conditions
- Constraint validation — age bounds, phone format, date validation
- Client protection design — ID-based not name-based
- Targets: CHVs conducting community HIV testing

**Mentor Mother Contact Log** (`mmi_mm_v1.xlsx`)
- 41 questions across 6 sections
- PMTCT cascade tracking — ART, delivery, EID, prophylaxis
- Protection monitoring — GBV and mental health screening
- Quality contact measurement — duration-based
- Targets: Mentor Mothers supporting HIV-positive pregnant women

### 2. DHIS2 Configuration

Complete DHIS2 2.42 program configuration:

| Component | Count | Details |
|---|---|---|
| Data elements | 19 | PEPFAR MER-aligned, coded |
| Categories | 4 | Sex, Age Band, KP Type, HTS Result |
| Category combinations | 5 | Including full PEPFAR MER disaggregation |
| Indicators | 9 | Calculated from data element pairs |
| Dataset sections | 4 | HTS, PMTCT/MM, ART, RDQA |
| Dashboard visualizations | 8 | Line, bar, gauge, stacked, combined |

**Indicators configured:**

| Indicator | Formula |
|---|---|
| HIV Positivity Rate | HTS_TST_POS / HTS_TST × 100 |
| 30-Day Linkage Rate | HTS_LINKED_30 / HTS_TST_POS × 100 |
| EMTCT Cascade Completion | PMTCT_CASCADE / PMTCT_DELIVERY × 100 |
| Viral Suppression Rate | TX_PVLS_NUM / TX_PVLS_DEN × 100 |
| ART 12-Month Retention | TX_RET_NUM / TX_RET_DEN × 100 |
| EID Coverage | EID_DONE / EID_ELIGIBLE × 100 |
| RDQA Verification Ratio | RDQA_SOURCE / RDQA_REPORTED |
| MM Contact Rate | MM_CONTACTS / PMTCT_ENROLLED |
| Referral Completion Rate | HTS_REFERRAL / HTS_TST_POS × 100 |

### 3. Automated Pipeline

Python pipeline connecting KoBoToolbox to DHIS2:

- Authenticates with both systems via API tokens
- Pulls all submissions with automatic pagination
- Aggregates individual records into monthly facility totals
- Maps KoBoToolbox field values to DHIS2 data element UIDs
- Pushes aggregate values via DHIS2 dataValueSets API
- Logs every operation to `pipeline.log` for audit trail
- Handles errors gracefully — skips bad records, continues processing

**Transformation logic:**

```
KoBoToolbox individual records     →    DHIS2 aggregate values
─────────────────────────────────────────────────────────────
session_date field                 →    Monthly period (YYYYMM)
sub_location field                 →    Org unit UID
hts_result = positive (count)      →    HTS_TST_POS value
referral_outcome = accepted (count)→    HTS_REFERRAL value
art_initiated = yes (count)        →    HTS_LINKED_30 value
```

---

## Data and Testing

The DHIS2 instance is populated with programmatically generated test data
simulating 12 months of implementation across 5 facilities.

**Generation principles:**

1. **Evidence-based baselines** — HIV positivity rates (7–11%), viral suppression
   (84–91%), and retention rates (80–88%) derived from NASCOP annual reports
   and PEPFAR Kenya program data for comparable facility types.

2. **Realistic implementation trajectory** — Four-phase ramp-up curve:

   | Phase | Months | Capacity |
   |---|---|---|
   | Early implementation | 1–3 | 65% |
   | Momentum building | 4–6 | 80% |
   | Near-full operation | 7–9 | 92% |
   | Steady state | 10–12 | 100% |

3. **DATIM-consistent validation** — Positive results never exceed total tests,
   cascade completions never exceed deliveries, suppression numerators
   never exceed denominators.

4. **RDQA trajectory** — Verification ratios deliberately show poor data
   quality early (0.78–0.92) improving to acceptable range (0.92–1.08)
   as data systems mature — reflecting real PEPFAR facility patterns.

```bash
# Reproduce the test dataset
pip install requests python-dateutil
python generate_dhis2_data.py
```

> **Note:** All data is synthetic. No real patient records were used.

---

## MEL Framework Behind This System

This technical system is grounded in a complete MEL conceptual framework:

- **Results framework** — Log frame with 4 output and 4 purpose-level indicators
- **Indicator reference sheets** — 12-component specifications for all 9 indicators
- **Theory of Change** — Explicit assumption map with criticality/confidence ratings
- **RDQA protocols** — Quarterly verification ratio assessment with 0.90–1.10 threshold
- **Adaptive management** — Pause-and-reflect cycle fed by dashboard data
- **PEPFAR MER alignment** — HTS_TST, TX_CURR, TX_PVLS, TX_NEW per MER guidance
- **GESI integration** — Sex and age disaggregation, KP-specific indicators
- **VfM framework** — Cost per output tracking design built into dataset structure

---

## Technical Requirements

```
Python 3.11+
requests
python-dateutil
openpyxl

DHIS2 2.38+
KoBoToolbox account (free tier sufficient)
```

---

## Author

**Alex Gatongo Arasa**
Clinical Officer → Health Informatics & MEL Specialist
Nairobi, Kenya

🌐 [Portfolio](https://gatongoalex.netlify.app) |
💼 [LinkedIn](https://linkedin.com/in/alex-arasa-316b54214) |
🐙 [GitHub](https://github.com/Bitange-Gatongo)
