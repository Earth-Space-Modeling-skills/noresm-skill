---
name: noresm
description: >
  Progressive-disclosure skill for the Norwegian Earth System Model (NorESM),
  a CESM-derived coupled climate / Earth-system model with NorESM-specific
  ocean (BLOM/MICOM-derived), aerosol (OsloAero), and biogeochemistry
  (HAMOCC, iHAMOCC). Covers the NorESM superproject, manage_externals
  bootstrap, the CESM-derived case workflow, NorESM-specific compsets,
  and the link to NorESM-1 / NorESM-2 documentation.
version: 0.1.0-scaffold
tags:
  - earth-science
  - climate-model
  - earth-system-model
  - noresm
  - blom
  - hamocc
  - oslo-aero
  - cesm-derived
  - norway
  - fortran
---

# NorESM (Norwegian Earth System Model) Guide

> **NorESM** = Norwegian Earth System Model, a CESM-derived coupled Earth-system model.
> Maintainer: NorESM Climate Modeling Consortium (Norwegian institutions)
> Source: https://github.com/NorESMhub/NorESM
> Docs: https://noresm-docs.readthedocs.io
> Website: https://www.noresm.org
> Skill author: Koutian Wu (ktwu01@gmail.com)
> Skill version: 0.1.0-scaffold

**What NorESM does:** Provides a coupled atmosphere–ocean–land–sea-ice climate model with Norwegian-developed components for ocean dynamics (BLOM, derived from MICOM, an isopycnal-coordinate ocean), ocean biogeochemistry (HAMOCC / iHAMOCC), and aerosols (OsloAero). The host framework is CESM (CIME-based case control, CMEPS coupler, CAM atmosphere, CTSM land, CICE sea-ice). Used by Norwegian climate research and contributes to CMIP.

**Who this skill is for:** Researchers running CMIP-class climate experiments with NorESM, developers porting NorESM to a new machine, and anyone needing to understand which parts are NorESM-specific vs inherited from CESM.

---

## Quick Decision Tree

```
"What do I need?"
│
├─ 🆕 What is NorESM, what is CESM-derived, what is NorESM-specific?
│  └─ Read: reference/overview.md
│
├─ 📥 Bootstrap the model (manage_externals, Externals.cfg)
│  └─ Read: reference/bootstrap.md
│
├─ 🚀 Run a case (CIME workflow, NorESM compsets)
│  └─ Read: reference/running-a-case.md  (also see cesm-skill)
│
├─ 🌊 BLOM ocean (isopycnal, MICOM-derived)
│  └─ Read: reference/blom-ocean.md
│
├─ 🧪 HAMOCC / iHAMOCC ocean biogeochemistry
│  └─ Read: reference/hamocc-bgc.md
│
├─ ☁️ OsloAero aerosol scheme
│  └─ Read: reference/osloaero.md
│
└─ 🐛 NorESM-specific build/run issues
   └─ Read: reference/debugging.md
```

---

## Repo Layout (verified from clone)

```
NorESM/
├── cime_config/                          # NorESM-specific CIME configuration
├── manage_externals/                     # External-component fetcher
├── Externals.cfg                         # Components for stable releases
├── Externals_continuous_development.cfg  # Components for development tip
├── img/                                  # Logo etc.
├── README.md
├── LICENSE.txt
├── LICENSE-CESM.txt
├── Copyright-CESM.txt
└── CONTRIBUTING.md
```

This is a **thin meta-repo**. The actual model code (CAM, CLM/CTSM, BLOM, CICE, HAMOCC, OsloAero) is fetched into a `components/` tree by `manage_externals/checkout_externals` based on `Externals.cfg`.

---

## Critical Rules

1. **The repo is intentionally tiny.** Don't be confused by the small footprint, you must run the externals tool to populate `components/`.
2. **Two externals files.** `Externals.cfg` (stable / release) vs `Externals_continuous_development.cfg` (CD tip). Pick deliberately.
3. **NorESM uses CIME.** The case workflow (`create_newcase`, `case.setup`, `case.build`, `case.submit`) is the same as CESM; differences are in compsets and component versions.
4. **Compsets:** standard NorESM2 compsets are `N`-prefixed (e.g., `NHIST`, `N1850`) where `N` denotes NorESM-specific component combinations.
5. **NorESM has its own license** layered on top of the CESM-derived parts. Read `LICENSE.txt`, `LICENSE-CESM.txt`, and `Copyright-CESM.txt`.

---

## Reference Index

| File | Topic |
|---|---|
| reference/overview.md | What is NorESM-specific |
| reference/bootstrap.md | manage_externals, Externals.cfg |
| reference/running-a-case.md | CIME workflow, NorESM compsets |
| reference/blom-ocean.md | Isopycnal ocean (BLOM/MICOM) |
| reference/hamocc-bgc.md | Ocean biogeochemistry |
| reference/osloaero.md | Aerosol scheme |
| reference/debugging.md | NorESM-specific issues |

## Status

Scaffold (v0.1.0-scaffold). Layout verified against the cloned NorESM superproject. Operational depth being filled in.
