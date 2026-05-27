# Material-Mechanism

Reaction mechanism(s) for **ANSYS Fluent** (Fluent User-Defined Material Database / UDF material format) in Scheme.

## sch6step-edm: Global 6‑step gas‑phase reaction scheme (Scharler et al., 2021)

The reaction mechanism **`sch6step-edm`** included in [`sch6step-edm.scm`](./sch6step-edm.scm) is based on the **global 6‑step gas‑phase reaction scheme** reported in:

> Scharler, R., Archan, G., Rakos, C., von Berg, L., Lello, D., Hochenauer, C., & Anca‑Couce, A. (2021). *Emission minimization of a top‑lit updraft gasifier cookstove based on experiments and detailed CFD analyses.* **Fuel, 285**, 119047. https://doi.org/10.1016/j.fuel.2020.119047

### Species

The material database defines the following species (as used by the mechanism file):

- `c` (solid carbon)
- `c2h4` (ethylene)
- `ch4` (methane)
- `co`
- `co2`
- `h2`
- `h2o`
- `o2`
- `c2.35h3.97o1.53` (lumped tar pseudo‑species)
- `n2` (inert)

### Reactions (6‑step scheme)

This mechanism contains **six global reactions** (“reaction‑1” … “reaction‑6”).

> Note: The exact stoichiometry and Arrhenius parameters are defined in [`sch6step-edm.scm`](./sch6step-edm.scm). In Fluent these are used with the *finite‑rate / eddy‑dissipation* model.

1. **Tar cracking / devolatilization**: lumped tar → light gases + CO/CO₂ + soot/char
2. **CO oxidation**: CO + 0.5 O₂ → CO₂
3. **H₂ oxidation**: H₂ + 0.5 O₂ → H₂O
4. **CH₄ oxidation**: CH₄ + 1.5 O₂ → CO + 2 H₂O (global)
5. **C₂H₄ oxidation**: C₂H₄ + 2 O₂ → 2 CO + 2 H₂O (global)
6. **Water–gas shift (WGS)**: CO + H₂O ⇌ CO₂ + H₂

## Usage (ANSYS Fluent)

1. In Fluent, open **Materials** → **Fluent Database** → **User-Defined…**
2. Load the `.scm` file (e.g. `sch6step-edm.scm`).
3. Assign the created mixture/material to the appropriate cell zone(s).
4. Enable Species Transport and select the reaction mechanism.

## License

If you plan to publish or redistribute modified versions, consider adding a license file (e.g. MIT, BSD‑3‑Clause, GPL‑3.0) and clarifying citation requirements.
