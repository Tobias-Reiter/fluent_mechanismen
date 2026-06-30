# Material-Mechanism

Reaction mechanism(s) for **ANSYS Fluent** (Fluent User-Defined Material Database / UDF material format) in Scheme.

## Mechanisms

| File | Mechanism | Source | Short description |
| --- | --- | --- | --- |
| [`Glarborg148.scm`](./Glarborg148.scm) | `glarborg148_edm` | [Glarborg et al. (2018)](https://doi.org/10.1016/j.pecs.2018.01.002) | Detailed nitrogen-chemistry mechanism for combustion-generated NOx. It covers thermal NO, prompt NO, fuel-N pathways, NNH/N2O routes, reburning and SNCR-relevant NO reduction chemistry. The repository version is formatted as a Fluent material database and includes additional global tar/char conversion steps. |
| [`Li37.scm`](./Li37.scm) | `li37` | [Li et al. (2019)](https://doi.org/10.1016/j.fuel.2019.05.152) | Skeletal NOx mechanism for solid-fuel combustion CFD. It is a compact reduction of the detailed Glarborg-based nitrogen chemistry and was developed for NO formation, staged combustion and SNCR-relevant conditions in large-scale solid-fuel combustion. The repository version is formatted for Fluent and includes additional global tar/char conversion steps. |
| [`sch3step-edm.scm`](./sch3step-edm.scm) | `sch3step-edm` | Derived compact global CH4/CO/H2 subset in the Scharler six-step context; no explicit source is documented in the `.scm` file. Base source: [Scharler et al. (2021)](https://doi.org/10.1016/j.enconman.2021.114755). | Compact three-step global gas-phase mechanism for methane, carbon monoxide and hydrogen oxidation with finite-rate / eddy-dissipation variants. Use this when only a minimal global gas-phase oxidation scheme is required. |
| [`sch6step-edm.scm`](./sch6step-edm.scm) | `sch6step-edm` | [Scharler et al. (2021)](https://doi.org/10.1016/j.enconman.2021.114755) | Global six-step gas-phase reaction scheme for biomass/gasification gas combustion in Fluent. It includes a lumped tar pseudo-species, light gas formation, ethylene and methane conversion, char-to-CO conversion, CO oxidation and H2 oxidation. |
| [`sch6step_n-edm.scm`](./sch6step_n-edm.scm) | `sch6step_n-edm` | Based on the Scharler six-step scheme: [Scharler et al. (2021)](https://doi.org/10.1016/j.enconman.2021.114755). Repository extension for reactor-network coupling. | Variant of `sch6step-edm` with additional nitrogen species (`hcn`, `nh3`, `no`, `n2`). Intended for use with a reactor network to determine NOx emissions. The six global gas-phase reactions remain the same core oxidation scheme; detailed NOx conversion is expected to be handled in the reactor-network workflow. |

## Reaction overview

The exact stoichiometry, reaction orders, Arrhenius parameters and eddy-dissipation mixing rates are defined in the respective `.scm` files. The overview below is intentionally compact.

| Mechanism | Compact reaction scope |
| --- | --- |
| `glarborg148_edm` | Detailed gas-phase combustion and nitrogen chemistry, plus added global tar cracking / char conversion entries in the Fluent material database. Individual reactions are not listed here because the mechanism is large. |
| `li37` | Reduced NOx chemistry for solid-fuel combustion: hydrocarbon oxidation, HCN/NH3/NO interconversion, thermal / prompt / fuel-N pathways and SNCR-relevant reactions. Individual reactions are not listed here because the mechanism is still comparatively large. |
| `sch3step-edm` | 3 global steps: CH4 partial oxidation to CO/H2/H2O, CO oxidation to CO2, and H2 oxidation to H2O. |
| `sch6step-edm` | 6 global steps: tar pseudo-species cracking, C2H4 oxidation, CH4 partial oxidation, char-to-CO conversion, CO oxidation and H2 oxidation. |
| `sch6step_n-edm` | Same six global steps as `sch6step-edm`, with additional transported nitrogen species for reactor-network-based NOx evaluation. |

## Notes

- `sch6step_n-edm` is meant as a coupling mechanism for reactor-network-based NOx emission calculation, not as a standalone detailed NOx kinetic mechanism.
- `sch3step-edm` does not contain an explicit bibliographic source in the file. The source entry above should be verified if a formal publication citation is required.
- Earlier comments/README text may reference a Scharler entry as `Fuel, 285, 119047` with DOI `10.1016/j.fuel.2020.119047`. That DOI points to a different Fuel article. The source link used here follows the publication record for the Scharler cookstove CFD paper: `Energy Conversion and Management, 247, 114755`, DOI `10.1016/j.enconman.2021.114755`.

## Usage (ANSYS Fluent)

1. In Fluent, open **Materials** → **Fluent Database** → **User-Defined…**
2. Load the `.scm` file (e.g. `sch6step-edm.scm`).
3. Assign the created mixture/material to the appropriate cell zone(s).
4. Enable Species Transport and select the reaction mechanism.
