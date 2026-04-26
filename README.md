[README(1).md](https://github.com/user-attachments/files/27101477/README.1.md)
# Alex Gatongo Arasa
### Clinical Officer → Health Informatics & MEL Specialist

> *Bridging frontline clinical experience with data systems that drive program decisions*

---

## About Me

I am a registered Clinical Officer with 4+ years of frontline experience in reproductive health, NCD management, and maternal & child health across public and private health facilities in Kenya. I am actively transitioning into Health Informatics and Monitoring, Evaluation & Learning — bringing a capability most MEL candidates cannot replicate: **I understand data at the point of generation.**

Having personally filled MOH registers, managed ANC4+ patient follow-up, and witnessed how data quality failures at facility level cascade into flawed county dashboards and donor reports, I built my informatics skills to fix that problem systematically — not just report it.

My technical work spans DHIS2 configuration, KoBoToolbox data pipelines, GIS-based health analytics, and MEL framework design — all grounded in Kenya MOH and PEPFAR MER standards. I can talk clinical to health workers and talk data to the technical team. That dual fluency is what strengthens health information systems at the point where they most often break.

---

## Technical Skills

| Domain | Tools & Methods |
|---|---|
| **Health Information Systems** | DHIS2 · KoBoToolbox · eCHIS · KenyaEMR · DATIM · KHIS2 |
| **MEL & Data Quality** | RDQA methodology · Verification Factor analysis · Indicator development · MEL Plan development · PEPFAR MER indicators (HTS_TST · TX_CURR · TX_PVLS) · Theory of Change · Logic Models · Results Frameworks |
| **Data & Analytics** | SQL · Python (openpyxl · requests · pandas) · Excel (pivot tables · COUNTIF/SUMIF · data cleaning) · R (in progress) · DHIS2 Maps · GIS spatial analysis |
| **Evaluation Methods** | Thematic analysis · Framework analysis · Mixed methods · Cost-effectiveness analysis · Sampling design · Gender-responsive MEL · GESI frameworks |
| **Clinical Background** | Clinical assessment & triage · NCD management · Maternal & child health · Reproductive health · ANC follow-up · MOH register management |

---

## Featured Projects

---

### 🏥 MMI Kenya — Full MEL Data System
*KoBoToolbox · DHIS2 · Python · XLSForm*

Most MEL portfolios show individual tools in isolation. This project demonstrates a complete, end-to-end MEL data system built for a PEPFAR-aligned HIV/PMTCT program — from data collection instrument design through automated pipeline to live program dashboard.

**What was built:**

- **Two production-grade XLSForm data collection instruments** — a Community HTS Register and a Mentor Mother Contact Log — with advanced skip logic, GPS capture, constraint validation, and client protection design (ID-based, not name-based)
- **Full DHIS2 program configuration** — 19 data elements with PEPFAR MER-aligned disaggregations, 9 calculated indicators, a sectioned monthly dataset, and an 8-visualization program performance dashboard
- **Automated Python pipeline** — pushes KoBoToolbox submissions to DHIS2 via API with data transformation, error handling, and import logging
- **Complete MEL framework** — log frame, indicator reference sheet, Theory of Change, assumption map, and RDQA protocols grounded in the FCDO VfM four E's framework

**Program context:** Five HIV/PMTCT facilities in Nairobi County informal settlements. Indicators include HTS positivity rate, 30-day linkage rate, EMTCT cascade completion, viral suppression rate (TX_PVLS), ART 12-month retention, and RDQA verification ratio.

---

#### 📊 Data and Testing

The DHIS2 instance is populated with programmatically generated test data simulating 12 months of program implementation across five facilities.

Test data was generated using a custom Python script (`generate_dhis2_data.py`) built on three design principles:

**1 — Evidence-based baseline values**
Facility baselines were derived from published PEPFAR Kenya program data, NASCOP annual reports, and Kenya DHS 2022 estimates for Garissa County. HIV positivity rates of 7–11% across facilities reflect the actual positivity range reported in northeastern Kenya's community testing programs. Viral suppression rates of 84–91% reflect NASCOP-reported TX_PVLS performance for facilities at comparable ART program maturity levels.

**2 — Realistic implementation trajectory**
The script models a four-phase implementation curve consistent with USAID implementing partner startup analyses:

| Phase | Months | Capacity | What it reflects |
|---|---|---|---|
| Early implementation | 1–3 | 65% | Staff recruitment, CHV training, community sensitization |
| Momentum building | 4–6 | 80% | Systems stabilizing, caseloads growing |
| Near-full operation | 7–9 | 92% | Mentor Mothers fully deployed, referral pathways functional |
| Steady state | 10–12 | 100% | Full program capacity, mature data systems |

**3 — Internal data consistency**
All generated values maintain the logical relationships enforced by PEPFAR DATIM validation rules:
- HIV positive results never exceed total tests conducted
- Cascade completions never exceed enrolled women with delivery outcomes
- Viral suppression numerators never exceed denominators
- RDQA verification ratios simulate real data quality improvement — poor in early months (0.78–0.92), improving to acceptable range (0.92–1.08) as data systems mature

The script uses a fixed random seed per facility-month combination — making the dataset fully reproducible. Running the script twice against the same DHIS2 instance produces identical results.

**Reproducing the test data:**
```bash
# Install dependencies
pip install requests python-dateutil

# Run against your DHIS2 instance
python generate_dhis2_data.py
```

> **Note:** All data in this repository is synthetic. No real patient data or facility records were used at any stage of this project.

---

### 🗺️ Garissa County Malaria Burden Mapping
*DHIS2 Maps · GIS · Spatial Analysis*

Malaria burden in Garissa County is unevenly distributed across facility catchments — yet resource allocation historically treated all sub-counties equally. This project uses DHIS2 Maps to conduct subnational GIS analysis of malaria incidence, producing choropleth and bubble map visualizations disaggregated by facility catchment.

Confirmed versus treated trend analysis is layered against OPD benchmarks to identify facilities where treatment gaps signal data quality issues or service delivery failures — with findings designed to inform evidence-based resource prioritization by the County Health Management Team.

---

### 📋 NCD Tracker Program
*DHIS2 Tracker · Program Rules · Clinical Decision Support*

Routine paper registers cannot flag overdue patients, track retention, or alert clinicians to dangerous clinical thresholds. This DHIS2 Tracker program brings individual-level NCD patient follow-up into the national HMIS infrastructure — with 8 clinical decision-support program rules, automated alerts for missed refills and abnormal BP, and outcome-level indicators tracking retention rate and BP control percentage.

All thresholds based on Kenya MOH NCD Clinical Guidelines 2020 and designed by a practicing Clinical Officer to reduce alert fatigue while supporting real clinical decisions.

---

### ✅ HMIS Data Quality Validation Framework
*DHIS2 · PEPFAR DQA · RDQA · Validation Rules*

Routine HMIS data in Kenya is frequently incomplete, inconsistent, and submitted late — undermining program decision making at every level. This DHIS2-based framework provides systematic, automated data quality monitoring aligned to the PEPFAR DQA five-dimension standard:

- 15 validation rules covering logical consistency
- Completeness monitoring with automated alerts
- Outlier detection using min/max bounds
- Reporting rate tracking at facility, sub-county, and county level
- Pre-visit completeness dashboards supporting RDQA
- Verification Factor tracking with 90–110% acceptable threshold

🔗 **Live demo & documentation:** [gatongoalex.netlify.app](https://gatongoalex.netlify.app)

---

## MEL Competencies

Beyond technical tools, my MEL practice is grounded in a complete conceptual framework covering:

- **Adaptive Management** — CLA framework, learning agendas, pause-and-reflect cycles, adaptation logs
- **Sampling & Data Collection Design** — Probability sampling, LQAS, RDQA, instrument design, mixed methods
- **Results-Based Management** — Log frame construction and critique, indicator development, VfM reporting
- **Qualitative Data Analysis** — Thematic analysis, framework analysis, content analysis, Most Significant Change
- **Gender-Responsive MEL** — GESI framework, USAID ADS 205, three-tier indicator design, feminist MEL
- **Cost-Effectiveness Analysis** — FCDO VfM four E's, CEA calculation, sensitivity analysis, DALY methods
- **Impact Evaluation Design** — RCTs, stepped-wedge, DiD, RDD, PSM, ITS

---

## Certifications & Education

**DHIS2 Academy** — 5 certifications:
- Aggregate Customization Fundamentals
- Aggregate Data Analysis Fundamentals
- Aggregate Data Capture & Validation Fundamentals
- Event Configuration Fundamentals
- Planning & Budgeting DHIS2 Implementations

**M&E Fundamentals** — Certified

**Kenya Medical Training College (KMTC) — Webuye**
Diploma in Clinical Medicine & Surgery · Graduated 2022

---

## Currently

- 📊 Building R skills — tidyverse, ggplot2, survey package, KDHS data workflows
- 🌍 Targeting MEL Officer roles with USAID, Global Fund, and UN-funded partners in Kenya
- 🔬 Completing KoBo → DHIS2 automated pipeline portfolio project
- 🤝 Open to volunteer and entry-level M&E / HIS opportunities in Kenya

---

## Connect

🌐 [Portfolio](https://gatongoalex.netlify.app) &nbsp;|&nbsp;
💼 [LinkedIn](https://linkedin.com) &nbsp;|&nbsp;
🐙 [GitHub](https://github.com/Bitange-Gatongo)

---

*Committed to data-driven health systems that serve underserved communities in Kenya.*
