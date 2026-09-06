# CSF Bolus Study Calculator (Marmarou Model: PVI, $R_{out}$, Compliance & Elastance)

An interactive neurosurgical clinical calculator for recording and analyzing the **Marmarou CSF Bolus Injection and Withdrawal Test**, computing the **Pressure-Volume Index (PVI)**, **Resistance to CSF Outflow ($R_{out}$)**, **Intracranial Compliance ($C_0$)**, and **Elastance ($E_0$)**, with continuous kinetic curve fitting, first and second order differential analysis, and real-time interactive scientific visualizations.

Developed by **Dr G Narenthiran MB ChB BSc(MedSci)(Hons) FEBNS FRCS(SN)**, Neurosurgery Research Listserv, UK.

> ⚠️ **Disclaimer:** The CSF-bolus calculator should not be used for clinical purposes and the user should verify the calculations.

---

## 🔬 Clinical Principles & Mathematical Framework

### 1. Pressure-Volume Index (PVI)
Introduced by Anthony Marmarou and colleagues (1975, 1978), the **Pressure-Volume Index (PVI)** characterizes the steepness of the exponential intracranial pressure-volume curve. It represents the theoretical volume of fluid increment ($\Delta V$) required to raise the baseline intracranial pressure ($P_0$) by one full decade (a factor of 10):

$$\text{PVI} = \frac{\Delta V}{\log_{10}\left(\frac{P_p}{P_0}\right)} \quad [\text{mL}]$$

- $\Delta V$: Injected fluid bolus volume in mL (typically 3.0 to 5.0 mL of preservative-free 0.9% saline) or withdrawn CSF volume.
- $P_0$: Baseline opening pressure (resting ICP) prior to bolus delivery (mmHg).
- $P_p$: Immediate peak intracranial pressure attained upon bolus completion (mmHg).

#### Adult Diagnostic Thresholds:
| PVI Value | Mechanical Interpretation | Clinical Implications |
|---|---|---|
| **$> 18 \text{ mL}$** | **Normal Cranial Compliance** | Preserved intracranial spatial buffering reserve. |
| **$13 - 18 \text{ mL}$** | **Borderline Compliance** | Moderate depletion of compensatory reserve (frequently noted in elderly/iNPH). |
| **$< 13 \text{ mL}$** | **Severely Reduced Compliance / High Elastance** | Critical exhaustion of craniospinal compliance; small volume additions produce steep, dangerous ICP spikes. |

---

### 2. Intracranial Elastance ($E_0$) & Compliance ($C_0$)
Because intracranial pressure varies exponentially with added volume ($P = P_0 \cdot 10^{\Delta V / \text{PVI}}$), intracranial elastance ($\frac{dP}{dV}$) increases linearly with instantaneous pressure:

$$\frac{dP}{dV} = \frac{\ln(10)}{\text{PVI}} \cdot P = \frac{2.3026}{\text{PVI}} \cdot P$$

At baseline resting pressure $P_0$:
- **Baseline Elastance ($E_0$)**:
  $$E_0 = \frac{2.3026 \cdot P_0}{\text{PVI}} \quad [\text{mmHg}/\text{mL}]$$

- **Baseline Intracranial Compliance ($C_0$)**:
  $$C_0 = \frac{1}{E_0} = \frac{\text{PVI}}{2.3026 \cdot P_0} \quad [\text{mL}/\text{mmHg}]$$

---

### 3. Resistance to CSF Outflow ($R_{out}$) via Pressure Decay
Following rapid bolus injection, intracranial pressure rises to $P_p$ and subsequently decays toward baseline $P_0$ as fluid is absorbed across the arachnoid villi into the dural venous sinuses. 

Marmarou's non-linear differential equation describes the rate of pressure decay:
$$\frac{dP}{dt} = - \frac{2.3026 \cdot P(t) \cdot (P(t) - P_0)}{\text{PVI} \cdot R_{out}}$$

Integrating this relationship yields the instantaneous resistance at any time $t$ along the recovery curve:
$$R_{out}(t) = \frac{t \cdot P_0}{\text{PVI} \cdot \log_{10}\left[ \frac{P(t)(P_p - P_0)}{P_p(P(t) - P_0)} \right]} \quad [\text{mmHg}/(\text{mL}/\text{min})]$$

- **Normal:** $< 10 \text{ mmHg}/(\text{mL}/\text{min})$
- **Borderline:** $10 - 12 \text{ mmHg}/(\text{mL}/\text{min})$
- **Pathological:** $> 12 \text{ mmHg}/(\text{mL}/\text{min})$ (strongly predictive of favorable response to shunt diversion in normal pressure hydrocephalus)

---

### 4. Decay Half-Time ($t_{1/2}$)
The time required for induced pressure elevation $(P_p - P_0)$ to fall by 50% ($P_{1/2} = P_0 + \frac{P_p - P_0}{2}$):

$$t_{1/2} = \frac{R_{out} \cdot \text{PVI} \cdot \log_{10}(2)}{P_0} \approx \frac{0.30103 \cdot R_{out} \cdot \text{PVI}}{P_0} \quad [\text{min}]$$

---

### 5. Three Linked Scientific Graphs

1. **Graph 1: Pressure Decay Curve $P(t)$ vs Time**
   - Empirical discrete data points $(t, P)$.
   - Continuous non-linear Marmarou kinetic decay curve:
     $$P(t) = \frac{P_0}{1 - \left(1 - \frac{P_0}{P_p}\right) e^{-t / \tau}} \quad \text{where } \tau = \frac{R_{out} \cdot \text{PVI}}{2.3026 \cdot P_0}$$
   - Peak Pressure marker ($P_p$ at $t=0$).
   - Half-decay marker ($t_{1/2}, P_{1/2}$).
   - **ICP Safety Threshold Line** (customizable red dashed horizontal reference line with alert badge, default 30 mmHg).

2. **Graph 2: Rate of Pressure Change (First Derivative $\frac{dP}{dt}$)**
   - Instantaneous velocity of pressure decay (mmHg/min).
   - Maximum absorption velocity peak marker.
   - Deceleration asymptote toward 0 mmHg/min as baseline equilibrium is restored.

3. **Graph 3: Curvature & Deceleration (Second Derivative $\frac{d^2P}{dt^2}$)**
   - Curvature dynamics (mmHg/min²) illustrating the transition from rapid early compliance damping to slow late outflow resistance absorption.

---

## ⚡ Key Features
- **Editable Clinical Recording Table**: Add, edit, or delete reading pairs $(t, P)$ with live auto-sorting.
- **Customizable ICP Safety Threshold**: Dynamic red dashed line (default 30 mmHg) with automated alert status if exceeded.
- **Clinical Presets**:
  - *Normal Adult Compliance*
  - *NPH / High $R_{out}$*
  - *Low PVI / Stiff Brain*
  - *CSF Withdrawal / Tap Bolus*
- **Biomechanical & Hydrodynamic Dashboard**: Live computation of PVI, $R_{out}$, $C_0$, $E_0$, $t_{1/2}$, and safety status.
- **Clinical Documentation & EHR Export**:
  - Copy formatted clinical note to clipboard (compatible with Epic, Cerner, EMIS, SystmOne).
  - Print / PDF export.
  - Email clinical report.
  - CSV file download.
- **Dark and Light Theme Support** with ultra-clean modern glassmorphism design.
- **Offline Reliability**: Bundled local `chart.umd.min.js` with CDN fallback.

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
