# Earth-Observation Constellation Mission Design & Optimization using Ansys STK

## Overview

This project develops an automated **Earth-observation satellite constellation mission-analysis framework** using **Ansys Systems Tool Kit (STK) and Python**.

The mission is designed for **regional Earth-observation coverage over India**, with emphasis on evaluating how orbital and constellation design parameters influence:

- Regional coverage
- Revisit time
- Access opportunities
- Sensor visibility
- Illumination-constrained imaging
- Ground-station connectivity

The project extends a baseline single-satellite STK coverage model into a **parametric constellation-design and mission-optimization framework**.

---

## Mission Objective

The primary engineering objective is to determine an efficient LEO constellation capable of satisfying prescribed Earth-observation coverage and revisit requirements over India.

The design problem considers

\[
\mathbf{x}
=
[h,\;i,\;N_{sat},\;N_{planes},\;\Delta\Omega,\;\theta_{FOV}]
\]

where:

- \(h\) = orbital altitude
- \(i\) = orbital inclination
- \(N_{sat}\) = total number of satellites
- \(N_{planes}\) = number of orbital planes
- \(\Delta\Omega\) = RAAN spacing
- \(\theta_{FOV}\) = EO sensor field-of-view angle

The resulting mission architecture is evaluated using coverage and revisit-time performance metrics.

---

## Mission Architecture

The STK scenario contains:

- J2-perturbed LEO satellites
- Multi-plane satellite constellation
- Nadir-pointing Earth-observation sensors
- Regional coverage definition over India
- Coverage Figure of Merit
- Solar illumination constraints
- Ground stations
- Satellite-to-ground access analysis
- Automated STK–Python post-processing

---

## Methodology

### 1. Baseline Satellite Model

A baseline Earth-observation spacecraft is created in STK and propagated using the **J2 perturbation propagator**.

The spacecraft orbit is defined using classical orbital elements including:

- Semi-major axis / altitude
- Eccentricity
- Inclination
- RAAN
- Argument of perigee
- True anomaly

J2 propagation is used to account for the dominant Earth oblateness perturbation affecting long-duration LEO orbital geometry.

---

### 2. Earth-Observation Sensor

Each spacecraft carries a nadir-pointing **simple conic EO sensor**.

The sensor field of view is parameterized so that the effect of payload geometry on mission performance can be evaluated.

Primary sensor parameters include:

- Sensor half-angle
- Angular resolution
- Nadir orientation
- Ground footprint

---

### 3. Regional Coverage over India

India is represented as the primary geographic coverage region.

A discretized STK coverage grid is generated over the region and the satellite sensors are assigned as coverage assets.

STK computes access between the EO payload and individual coverage grid points throughout the mission duration.

Coverage quality is evaluated using an STK **Figure of Merit**.

---

## STK Scenario

Place your STK 3D visualization here:

```markdown
![STK Constellation](figures/stk_constellation_3d.png)
```

The 3D STK scenario visualizes:

- Satellite orbital planes
- Sensor footprints
- Ground tracks
- Regional coverage
- Ground stations

---

## Coverage Analysis

Coverage performance is extracted automatically from STK using Python.

The analysis evaluates:

- Instantaneous coverage
- Accumulated coverage
- Percentage region covered
- Coverage gaps
- Access duration
- Number of accesses
- Revisit time

The STK **Satisfied by Time** data provider is used to extract accumulated coverage history into Python for post-processing.

```markdown
![Coverage History](figures/coverage_history.png)
```

---

## Constellation Design

The baseline single-spacecraft mission is extended to multi-satellite configurations.

Several constellation architectures are evaluated by varying:

\[
N_{sat}
\]

\[
N_{planes}
\]

\[
\Delta\Omega
\]

and in-plane satellite phasing.

Representative configurations include:

| Configuration | Satellites | Orbital Planes |
|---|---:|---:|
| C1 | 1 | 1 |
| C2 | 2 | 1 |
| C3 | 4 | 2 |
| C4 | 6 | 3 |
| C5 | 8 | 4 |
| C6 | 12 | 4 |

Satellite true anomalies are distributed within each orbital plane while RAAN values are distributed between planes.

---

## Parametric Trade Studies

### Orbital Altitude

Representative LEO altitudes are investigated:

\[
h =
400,\;500,\;600,\;700,\;800\;km
\]

The analysis quantifies the trade-off between:

- Sensor footprint
- Orbital period
- Access frequency
- Coverage accumulation
- Revisit performance

```markdown
![Altitude Trade Study](figures/altitude_trade_study.png)
```

---

### Orbital Inclination

Orbital inclination is varied to determine its effect on regional accessibility over India.

The analysis identifies inclination ranges providing favorable coverage while avoiding unnecessary high-latitude coverage.

```markdown
![Inclination Trade Study](figures/inclination_trade_study.png)
```

---

### Sensor Field of View

The EO payload field-of-view angle is varied to investigate the coupling between sensor design and orbital architecture.

The study evaluates changes in:

- Ground footprint
- Instantaneous coverage
- Revisit time
- Accumulated regional coverage

```markdown
![Sensor FOV Trade Study](figures/fov_trade_study.png)
```

---

### Constellation Size

Increasing satellite count improves temporal coverage but increases system complexity and mission cost.

The constellation trade study compares:

\[
N_{sat}
=
1,\;2,\;4,\;6,\;8,\;12
\]

against mission-level metrics.

```markdown
![Constellation Trade Study](figures/constellation_trade_study.png)
```

---

## Revisit-Time Analysis

Revisit time is treated as a major Earth-observation performance metric.

For each constellation architecture, repeated accesses to the regional coverage grid are evaluated to determine:

- Mean revisit time
- Maximum revisit time
- Regional revisit distribution
- Improvement with satellite count

```markdown
![Revisit Analysis](figures/revisit_time_analysis.png)
```

---

## Illumination-Constrained Imaging

Geometric access does not necessarily correspond to a usable optical image.

Therefore, solar illumination constraints are incorporated into the STK coverage analysis.

A valid EO observation requires

\[
\text{Valid Imaging Access}
=
\text{Sensor Visibility}
\cap
\text{Acceptable Illumination}
\]

This prevents nighttime accesses from being counted as useful optical imaging opportunities.

```markdown
![Illumination Constraint](figures/illumination_constraint.png)
```

---

## Ground-Station Access Analysis

Representative Indian ground stations are included to assess communication opportunities between the EO constellation and the ground segment.

For each satellite, STK calculates:

- Acquisition of signal
- Loss of signal
- Contact duration
- Number of contacts
- Ground-station access windows

```markdown
![Ground Station Access](figures/ground_station_access.png)
```

This provides an additional mission-design constraint beyond geometric Earth coverage.

---

## Automated STK–Python Workflow

The mission-analysis process is automated using the STK Python API.

The Python workflow:

1. Launches STK / STK Engine
2. Creates the mission scenario
3. Generates satellites
4. Assigns orbital elements
5. Configures J2 propagation
6. Creates EO sensors
7. Generates constellation architectures
8. Defines the India coverage region
9. Computes coverage accesses
10. Creates Figures of Merit
11. Applies illumination constraints
12. Computes ground-station access
13. Extracts STK Data Providers
14. Converts results into Pandas DataFrames
15. Performs parametric trade studies
16. Generates mission-performance plots

---

## Optimization Problem

The constellation design can be represented as the constrained optimization problem

\[
\min_{\mathbf{x}}
J
=
w_1T_{revisit}
+
w_2N_{sat}
-
w_3C_{coverage}
\]

where

\[
\mathbf{x}
=
[h,\;i,\;N_{sat},\;N_{planes},\;\Delta\Omega,\;\theta_{FOV}]
\]

subject to mission requirements such as

\[
C_{coverage}\geq C_{required}
\]

and

\[
T_{revisit}\leq T_{maximum}.
\]

The objective is to identify a constellation that provides acceptable EO performance without unnecessarily increasing satellite count.

---

## Design Trade-Offs

The analysis demonstrates several important mission-design relationships:

- Increasing orbital altitude increases instantaneous ground footprint but changes revisit characteristics.
- Increasing inclination modifies the geographical distribution of accessible regions.
- Increasing sensor FOV improves coverage but represents increased payload capability.
- Increasing satellite count significantly improves revisit time.
- Increasing the number of orbital planes improves spatial distribution of accesses.
- RAAN spacing and satellite phasing strongly influence temporal coverage uniformity.
- Illumination constraints can substantially reduce usable optical imaging opportunities compared with purely geometric access.

---

## Repository Structure

```text
EO-STK-Constellation/
│
├── README.md
├── requirements.txt
├── main.py
│
├── stk/
│   ├── create_scenario.py
│   ├── create_satellite.py
│   ├── create_constellation.py
│   ├── create_sensor.py
│   ├── coverage_analysis.py
│   ├── ground_station_analysis.py
│   └── illumination_constraints.py
│
├── analysis/
│   ├── altitude_trade_study.py
│   ├── inclination_trade_study.py
│   ├── constellation_trade_study.py
│   ├── sensor_fov_trade_study.py
│   └── revisit_analysis.py
│
├── results/
│   ├── coverage_results.csv
│   ├── access_results.csv
│   └── constellation_comparison.csv
│
└── figures/
    ├── stk_constellation_3d.png
    ├── coverage_history.png
    ├── altitude_trade_study.png
    ├── inclination_trade_study.png
    ├── constellation_trade_study.png
    ├── fov_trade_study.png
    ├── revisit_time_analysis.png
    ├── illumination_constraint.png
    └── ground_station_access.png
```

---

## Software

- **Ansys Systems Tool Kit (STK)**
- **PySTK / STK Python API**
- Python
- NumPy
- Pandas
- Matplotlib

---

## Key Skills Demonstrated

This project demonstrates practical application of:

- Space mission analysis
- Orbital mechanics
- Satellite constellation design
- Earth-observation mission design
- STK
- Python automation
- Coverage analysis
- Revisit-time analysis
- Sensor modelling
- Orbital trade studies
- Mission optimization
- Data analysis and visualization

---

## Reference

The initial STK coverage workflow was developed with reference to the official **Ansys PySTK Satellite Coverage Analysis example** and subsequently extended from a single-satellite regional coverage problem to an Earth-observation constellation mission-design framework.

The final project extends the reference workflow through:

- Regional coverage over India
- Multi-satellite constellation generation
- Orbital parameter trade studies
- Sensor FOV analysis
- Revisit-time analysis
- Ground-segment modelling
- Illumination constraints
- Automated mission-performance comparison
- Constellation architecture optimization

---

## Author

**Priyanshi Paul**  
MS by Research — Aerospace Engineering  
Indian Institute of Technology Kanpur
