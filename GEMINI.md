# GEMINI.md — BEng CEA Greenhouse Two-Stage Ammonia Heat Pump Simulation

---

## 1. Project Context & Engineering Positioning

- **Author**: Fraser James Mclellan
- **Academic Origin**: BEng (Hons) Mechanical Engineering Individual Project Thesis (ENG 4110P, Grade A4 / First-Class band), University of Glasgow (2023–2024).
- **Core Domain**: Controlled Environment Agriculture (CEA), Industrial Thermal Systems & Low-Carbon Heating.
- **Audited Single Source of Truth**: `/home/fraser/Life/Career/Job-Applications/Portfolio/SOURCES.md`.

---

## 2. Facility & Cycle Specifications

### Greenhouse Geometry & Envelope
- **Location**: Chelmsford, Essex, UK (Hourly weather dataset 2018–2024, 52,560 hours).
- **Geometry**: $20\,\text{m} \times 20\,\text{m} \times 5\,\text{m}$ (Volume $V = 2,000\,\text{m}^3$, wall/roof surface area $A_{\text{wall}} = 800\,\text{m}^2$, ground surface area $A_{\text{ground}} = 400\,\text{m}^2$).
- **Thermal Transmittance**: Multi-wall PVC/polycarbonate walls ($U_{\text{wall}} = 3.0\,\text{W/(m}^2\text{K)}$); insulated ground floor ($U_{\text{ground}} = 1.2\,\text{W/(m}^2\text{K)}$).
- **Solar Transmittance**: $\tau = 0.70$.
- **Setpoint**: Constant interior air temperature $T_{\text{internal}} = 18.0^\circ\text{C}$.

### Two-Stage Ammonia ($NH_3$ / R-717) Heat Pump with Flash Tank
- **Natural Refrigerant**: Zero Ozone Depletion Potential ($ODP = 0$), Zero Global Warming Potential ($GWP = 0$).
- **Condenser Supply**: High-temperature delivery at $T_{\text{cond}} = 80.0^\circ\text{C}$ to hydronic heating loops.
- **Intermediate Flash Pressure**: $P_{\text{int}} = \sqrt{P_{\text{evap}} \cdot P_{\text{cond}}}$.
- **Mass Flow Equations**:
  $$\dot{m}_2 = \frac{Q_c}{h_4 - h_5}$$
  $$\dot{m}_1 = \dot{m}_2 \cdot \frac{h_3 - h_5}{h_2 - h_5}$$
- **Compressor Electrical Power**:
  $$W_{c1} = \dot{m}_1 (h_2 - h_1), \quad W_{c2} = \dot{m}_2 (h_4 - h_3), \quad W_{\text{total}} = W_{c1} + W_{c2}$$
- **Cycle Efficiency**:
  $$\text{COP} = \frac{Q_c}{W_{\text{total}}}$$

---

## 3. Audited Performance Benchmarks (v1.0 Thesis Baseline vs. v2.0 Calibrated Physics)

| Metric | Version | Air-Source (ASHP) | Ground-Source (GSHP) | Water-Source (WSHP) | Key Outcome |
|---|---|:---:|:---:|:---:|:---:|
| **Mean Annual COP [-]** | **v1.0 Baseline**<br>*v2.0 Calibrated* | 4.06<br>**4.35** | 4.11<br>**4.39** | **4.29**<br>**4.52** | WSHP maintains highest COP across both models |
| **Peak Compressor Demand [kW]** | **v1.0 Baseline**<br>*v2.0 Calibrated* | 82.04<br>**74.38** | 73.18<br>**64.90** | **62.71**<br>**58.82** | **20.9% to 23.6%** peak grid demand reduction |
| **6-Year Total Electricity [MWh]** | **v1.0 Baseline**<br>*v2.0 Calibrated* | 886.1<br>**878.5** | 877.9<br>**859.8** | **827.1**<br>**825.4** | **53.1 to 59.0 MWh** avoided grid electricity |
| **6-Year OPEX Savings (£0.23/kWh)** | **v1.0 Baseline**<br>*v2.0 Calibrated* | Baseline | £1,870<br>£4,301 | **£13,569**<br>**£12,213** | **£12.2k to £13.6k** operational savings |

---

## 4. Repository Structure

```
BEng-CEA-Heatpump/
├── GEMINI.md            ← Project governance & technical specs (this file)
├── README.md            ← 5-Stage Executive Engineering Briefing
├── requirements.txt     ← Pinned minimal dependencies
├── .gitignore           ← Standard Python / OS rules, ignores archive/
│
├── data/
│   ├── inputs/          ← Hourly weather (air, soil, solar) & ammonia tables
│   └── outputs/         ← Pre-computed 52,560-hr results for AS, GS, WS
│
├── notebooks/
│   ├── 01_Air_Source_Heat_Pump.ipynb
│   ├── 02_Ground_Source_Heat_Pump.ipynb
│   ├── 03_Water_Source_Heat_Pump.ipynb
│   └── 04_Comparative_Techno_Economic_Analysis.ipynb
│
├── figures/             ← Publication-grade 300 DPI PNG & vector SVG plots
├── docs/                ← Original BEng thesis PDF and presentation decks
└── archive/             ← Local gitignored backup of exploratory drafts & lectures
```

---

## 5. Execution Instructions

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Run notebooks via JupyterLab or headless execute:
   ```bash
   jupyter nbconvert --execute --inplace notebooks/*.ipynb
   ```

