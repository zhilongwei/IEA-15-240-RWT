# IEA Wind 15-MW RWT OpenFAST Model with ESOMOOR Mooring Design

This folder contains OpenFAST input files for the IEA 15-MW reference wind turbine
on the UMaine Semi-submersible platform, using the ESOMOOR mooring design and
Syrope polyester rope modeling.

Syrope line properties are documented in:

Wei, Zhilong; Bingham, Harry B.; Shao, Yanlin (2026). ESOMOOR D5.1: Extended
MoorDyn solver and validation report. Technical University of Denmark. Online
resource. https://doi.org/10.11583/DTU.31408806

## Polyester Rope Properties

- Minimum breaking load (MBL): `2.354e7 N`
- Original working curve: two-column lookup table in `owc.dat`
- Working-curve static stiffness: `4.20e8 N`
- Dynamic stiffness model:

    `dynamic_stiffness = a + b * mean_tension`

    where `a = 4.21e8 N` and `b = 18.18`.

## Environmental Conditions

Two sea-state and wind-speed combinations are defined:

- NSS:
    - `Hs = 2.05 m`
    - `Tp = 9.37 s`
    - `Wind speed = 10.59 m/s`
    - Power production
- ESS:
    - `Hs = 15.6 m`
    - `Tp = 16.7 s`
    - `Wind speed = 45.00 m/s`
    - Parked (idling)

## OpenFAST Cases

Eight `.fst` cases are provided:

- `IEA-15-240-RWT-UMaineSemi_constant_stiffness_NSS.fst`
    - Constant-stiffness model + NSS
    - Uses `a = 4.21e8` as the constant stiffness
- `IEA-15-240-RWT-UMaineSemi_constant_stiffness_ESS.fst`
    - Constant-stiffness model + ESS
    - Uses `a = 4.21e8` as the constant stiffness
- `IEA-15-240-RWT-UMaineSemi_viscoelastic_NSS.fst`
    - Viscoelastic model + NSS
    - Uses working-curve stiffness `4.20e8` and the dynamic stiffness expression
- `IEA-15-240-RWT-UMaineSemi_viscoelastic_ESS.fst`
    - Viscoelastic model + ESS
    - Uses working-curve stiffness `4.20e8` and the dynamic stiffness expression
- `IEA-15-240-RWT-UMaineSemi_syrope_Tmax_15_NSS.fst`
    - Syrope model with initial `Tmax = 0.15 * MBL` + NSS
- `IEA-15-240-RWT-UMaineSemi_syrope_Tmax_40_NSS.fst`
    - Syrope model with initial `Tmax = 0.40 * MBL` + NSS
- `IEA-15-240-RWT-UMaineSemi_syrope_Tmax_15_ESS.fst`
    - Syrope model with initial `Tmax = 0.15 * MBL` + ESS
- `IEA-15-240-RWT-UMaineSemi_syrope_Tmax_40_ESS.fst`
    - Syrope model with initial `Tmax = 0.40 * MBL` + ESS

## Run Example

```bash
openfast IEA-15-240-RWT-UMaineSemi_syrope_Tmax_15_ESS.fst
```