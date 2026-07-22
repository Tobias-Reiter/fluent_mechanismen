# Mechanism

Reaction mechanism(s) for **ANSYS Fluent** (Fluent User-Defined Material Database / UDF material format) in Scheme.

## Mechanisms

| File  | Source | Short description |
| ---  | --- | --- |
| [`Glarborg148.scm`](./Glarborg148.scm)  | [Glarborg et al. (2018)](https://doi.org/10.1016/j.pecs.2018.01.002) | Detailed nitrogen-chemistry mechanism for combustion-generated NOx. It covers thermal NO, prompt NO, fuel-N pathways, NNH/N2O routes, reburning and SNCR-relevant NO reduction chemistry. The repository version is formatted as a Fluent material database and includes additional global tar/char conversion steps. |
| [`Li37.scm`](./Li37.scm)  | [Li et al. (2019)](https://doi.org/10.1016/j.fuel.2019.05.152) | Skeletal NOx mechanism for solid-fuel combustion CFD. It is a compact reduction of the detailed Glarborg-based nitrogen chemistry and was developed for NO formation, staged combustion and SNCR-relevant conditions in large-scale solid-fuel combustion. The repository version is formatted for Fluent and includes additional global tar/char conversion steps. |
| [`sch3step-edm.scm`](./sch3step-edm.scm) | Derived compact global CH4/CO/H2 subset in the Scharler six-step context; no explicit source is documented in the `.scm` file. Base source: [Scharler et al. (2021)](https://doi.org/10.1016/j.enconman.2021.114755). | Compact three-step global gas-phase mechanism for methane, carbon monoxide and hydrogen oxidation with finite-rate / eddy-dissipation variants. Use this when only a minimal global gas-phase oxidation scheme is required. |
| [`sch6step-edm.scm`](./sch6step-edm.scm)  | [Scharler et al. (2021)](https://doi.org/10.1016/j.enconman.2021.114755) | Global six-step gas-phase reaction scheme for biomass/gasification gas combustion in Fluent. It includes a lumped tar pseudo-species, light gas formation, ethylene and methane conversion, char-to-CO conversion, CO oxidation and H2 oxidation. |
| [`sch6step_n-edm.scm`](./sch6step_n-edm.scm)  | Based on the Scharler six-step scheme: [Scharler et al. (2021)](https://doi.org/10.1016/j.enconman.2021.114755). Repository extension for reactor-network coupling. | Variant of `sch6step-edm` with additional nitrogen species (`hcn`, `nh3`, `no`, `n2`). Intended for use with a reactor network to determine NOx emissions. The six global gas-phase reactions remain the same core oxidation scheme; detailed NOx conversion is expected to be handled in the reactor-network workflow. |

## Modeling notes

- In the cited biomass paper, `C` in the tar-cracking equation is explicitly `C(soot)`, not gaseous atomic carbon. It is also absent from the paper's gas-phase species list: the authors use the Moss-Brookes soot model and add tar-derived soot to its soot transport equation. `c` is retained here only as a numerical pseudo-species for compatibility with the existing volumetric reactions; reproducing the paper exactly requires a soot-source implementation instead of a gas-phase `c` material.
- `Li37.scm` includes the original Li37 PLOG pressure tables for reactions R18, R21-R23, R26-R27, R43, R65-R66, R76-R81 and R83-R87. PLOG pressures are in atm; Arrhenius factors and activation energies are stored in Fluent SI units.
- In the global mechanisms, zero-stoichiometry product entries are not removed blindly: `h2o` in CO oxidation has a finite-rate exponent of 0.5, while the zero-order `co2` product placeholders in the three-step mechanism are retained for the EDM product-side formulation.

## Usage (ANSYS Fluent)

1. In Fluent, open **Materials** → **Fluent Database** → **User-Defined…**
2. Load the `.scm` file (e.g. `sch6step-edm.scm`).
3. Assign the created mixture/material to the appropriate cell zone(s).
4. Enable Species Transport and select the reaction mechanism.
