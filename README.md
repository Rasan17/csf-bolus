# CSF Bolus Study Calculator (PVI, $R_{out}$, & Time Constant $\tau$)

An interactive neurosurgical clinical calculator for recording and analyzing the **Marmarou CSF Bolus Injection Test**, computing the **Pressure-Volume Index (PVI)**, **Resistance to CSF Outflow ($R_{out}$)**, and the **Time Constant of Pressure Decay ($\tau$)**, paired with continuous mono-exponential decay curve fitting, 1st/2nd order differential analysis, and semi-logarithmic linear regression.

Developed by **Dr G Narenthiran MB ChB BSc(MedSci)(Hons) FEBNS FRCS(SN)**, Neurosurgery Research Listserv, UK.

> ⚠️ **Disclaimer:** The CSF-bolus calculator should not be used for clinical purposes and the user should verify the calculations.

---

## 🔬 Clinical Principles & Mathematical Framework

In a bolus injection infusion test, a discrete volume ($V_{inf}$) is introduced rapidly (over a few seconds) rather than continuously. Because a bolus creates a transient pressure spike followed by an exponential decay rather than a steady-state plateau, Anthony Marmarou’s mathematical model is used to analyze the entire pressure-time recovery curve.

### 1. Intracranial Compliance ($C$) & Baseline ICP ($P_b$)
- **Baseline Intracranial Pressure ($P_b$):** The resting steady-state pressure prior to the perturbation, which contextualizes whether baseline intracranial hypertension exists.
- **Intracranial Compliance ($C$):** Compliance represents the spatial buffering capacity of the intracranial space—its ability to accommodate volume changes without sharp rises in pressure. Derived from the immediate pressure-volume response:
  $$C = \frac{\Delta V}{P_{peak} - P_b} \quad [\text{mL}/\text{mmHg}]$$
  *Significance:* Low compliance indicates the intracranial vault is "stiff," and even small volume additions trigger dangerous spikes in pressure.

---

### 2. Pressure-Volume Index (PVI)
Introduced by Marmarou et al. (1975, 1978), the **PVI** characterizes the exponential pressure-volume curve slope, defined as the volume increment required to raise baseline pressure tenfold:
$$\text{PVI} = \frac{\Delta V}{\log_{10}\left(\frac{P_{peak}}{P_b}\right)} \quad [\text{mL}]$$

- **Normal Adult:** $> 18 \text{ mL}$ (mean $\approx 25 \text{ mL}$)
- **Borderline / Elderly:** $13 - 18 \text{ mL}$
- **Pathological / Low Compliance:** $< 13 \text{ mL}$

---

### 3. Time Constant of Pressure Decay ($\tau$)
Following bolus injection, the pressure decay curve closely follows a mono-exponential relaxation function:
$$P(t) = P_b + (P_{peak} - P_b) \cdot e^{-t / \tau}$$

The time constant $\tau$ represents the rate at which pressure returns to baseline:
$$\tau = R_{out} \times C \quad [\text{min}]$$
*Significance:* A prolonged time constant signifies sluggish CSF absorption kinetics across the arachnoid villi into the dural venous sinuses.

#### Practical Determination of $\tau$:
1. **Linear Regression of Logarithmic Decay:**
   Taking the natural logarithm of the excess pressure above baseline:
   $$\ln[P(t) - P_b] = \ln(P_{peak} - P_b) - \frac{1}{\tau} \cdot t$$
   Plotting $\ln[P(t) - P_b]$ against time $t$ yields a straight line with slope:
   $$\text{Slope} = -\frac{1}{\tau} \implies \tau = -\frac{1}{\text{Slope}}$$
2. **Integral Area Under the Curve (AUC):**
   For a pure mono-exponential decay:
   $$\text{AUC} = \int_{0}^{\infty} [P(t) - P_b] \, dt = (P_{peak} - P_b) \cdot \tau \implies \tau = \frac{\text{AUC}}{P_{peak} - P_b}$$

---

### 4. Resistance to CSF Outflow ($R_{out}$)
The fundamental equation calculates $R_{out}$ by dividing the total pressure-time integral (the area under the recovery curve above baseline) by the volume of the injected bolus ($V_{inf}$):
$$R_{out} = \frac{\int_{0}^{\infty} [P(t) - P_b] \, dt}{V_{inf}} = \frac{\text{AUC}}{V_{inf}}$$

Since $\text{AUC} = (P_{peak} - P_b) \cdot \tau$ and $C = \frac{V_{inf}}{P_{peak} - P_b}$, the outflow resistance simplifies directly to:
$$R_{out} = \frac{\tau}{C} \quad [\text{mmHg}\cdot\text{min}/\text{mL}]$$

#### Clinical Thresholds:
| $R_{out}$ Value | Interpretation | Recommendation |
|---|---|---|
| **$< 10 - 12 \text{ mmHg}\cdot\text{min}/\text{mL}$** | **Normal** | Low probability of shunt benefit based on resistance alone. |
| **$10 - 12 \text{ mmHg}\cdot\text{min}/\text{mL}$** | **Borderline** | Equivocal; correlate with clinical tap test and DESH neuroimaging. |
| **$> 12 - 18 \text{ mmHg}\cdot\text{min}/\text{mL}$** | **Pathological** | Impaired CSF absorption capacity; supports diagnosis of communicating hydrocephalus or NPH with high probability of shunt response. |

---

## 📈 Four Linked Scientific Visualizations

1. **Graph 1: Pressure Decay Curve $P(t)$ vs Time**
   - Discrete empirical data points $(t_i, P_i)$.
   - Mono-exponential decay curve $P(t) = P_b + (P_{peak} - P_b)e^{-t/\tau}$.
   - Vertical dashed reference line and badge marking $\tau$ ($t = \tau$, pressure decayed to $P_b + \frac{\Delta P}{e}$).
   - **ICP Safety Threshold Line** (customizable red dashed horizontal reference line with alert badge, default 30 mmHg).
2. **Graph 2: Rate of Pressure Decay (First Derivative $\frac{dP}{dt}$)**
   - $\frac{dP}{dt} = -\frac{P_{peak} - P_b}{\tau} e^{-t/\tau}$ showing instantaneous recovery velocity.
3. **Graph 3: Curvature & Decay Deceleration (Second Derivative $\frac{d^2P}{dt^2}$)**
   - $\frac{d^2P}{dt^2} = \frac{P_{peak} - P_b}{\tau^2} e^{-t/\tau}$ tracking stabilization toward steady state.
4. **Graph 4: Semi-Logarithmic Linearization Plot ($\ln[P(t) - P_b]$ vs $t$)**
   - Scatter points of measured $\ln[P(t) - P_b]$.
   - Linear regression line demonstrating goodness-of-fit ($R^2$) where linear slope equals $-1/\tau$.

---

## ⚡ Key Features
- **Primary Hero Cards**: Highlights **1) PVI**, **2) $R_{out}$**, and **3) Time Constant $\tau$** with formulas, values, and clinical classifications.
- **Editable Clinical Recording Table**: Add, edit, and delete reading pairs $(t, P)$ with live real-time auto-calculation of $\Delta P$ and $\ln[P - P_b]$.
- **ICP Safety Threshold**: User-customizable threshold with dynamic red dashed warning line and alert banner.
- **Clinical Presets**:
  - *1. Normal Adult (10 mL bolus, $R_{out} \approx 7.2$)*
  - *2. NPH / High $R_{out}$ (10 mL bolus, $R_{out} \approx 16.0$)*
  - *3. Stiff Brain / Low PVI (5 mL bolus, $P_{peak} = 40$ mmHg)*
  - *4. Standard 5 mL Bolus*
- **Clinical Documentation Generator**: One-click EHR report copy (Epic/Cerner format), Print/PDF view, Email summary, and CSV data export.
- **Dark and Light Mode Support**.
- **Offline Reliability**: Bundled local `chart.umd.min.js`.

---

## 👨‍⚕️ Author & Attribution
- **Author**: © Dr G Narenthiran MB ChB BSc(MedSci)(Hons) FEBNS FRCS(SN), 2026; `g_narenthiran@hotmail.com`
- **Developed by**: Dr G Narenthiran FRCS(SN), Neurosurgery Research Listserv, UK; `g_narenthiran@hotmail.com`
- **Dedication**: *Dedicated to my mother Mrs Nirmaladevy Ganesalingam BSc*

---

## 📚 Key Clinical References
1. Marmarou A, Shulman K, LaMorgese J. Compartmental analysis of compliance and outflow resistance of the cerebrospinal fluid system. *J Neurosurg* 1975;43(5):523-534.
2. Marmarou A, Shulman K, Rosende RM. A nonlinear analysis of the cerebrospinal fluid system and intracranial pressure. *J Neurosurg* 1978;48(3):332-344.
3. Tans JT, Boon AJ. How to evaluate cerebrospinal fluid dynamics. *Acta Neurochir Suppl* 2002;81:49-53.
4. Czosnyka M, Czosnyka Z, Momjian S, Pickard JD. Cerebrospinal fluid dynamics. *Physiol Meas* 2004;25(5):R51-R76.
5. Kosteljanetz M. CSF dynamics and pressure-volume relationships in patients with normal pressure hydrocephalus. *Acta Neurol Scand Suppl* 1986;108:1-23.
