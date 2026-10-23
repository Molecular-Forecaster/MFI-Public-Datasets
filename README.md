# MFI Public Datasets

This repository contains public Cytochrome P450 (CYP) site-of-metabolism (SoM) datasets for nine CYP isoforms, distributed in three parallel formats:

- **SMILES TSV** for lightweight tabular use
- **JSON** for structured programmatic use
- **MOL2** for 3D/atom-level workflows with explicit SoM markings

## Related resources

- **ChemRxiv paper title**: *Experimental Data Analysis and Improved Cytochrome P450 Site-of-Metabolism Prediction for Drug Discovery* ([link](https://chemrxiv.org/doi/full/10.26434/chemrxiv.15009130/v2))
- **Canopy/Willow technology**: Learn more about Molecular Forecaster's platform and Willow CYP metabolism prediction capabilities at [molecularforecaster.com/willow](https://molecularforecaster.com/willow/).

## Repository layout

```text
CYP-SoMs/
  SMILES/   # TSV files (SMILES + molecule name)
  json/     # JSON files (compound metadata + SoM breakdown)
  mol2/     # MOL2 files (3D structures + SoM markers and references)
LICENSE     # Apache License 2.0
```

## File naming convention

For each isoform `CYPx`:

- `CYP-SoMs/SMILES/MFI-CYPx-SoM-Set-SMILES.tsv`
- `CYP-SoMs/json/MFI-CYPx-SoM-Set.json`
- `CYP-SoMs/mol2/MFI-CYPx-SoM-Set.mol2`

The following isoforms are included:

- CYP1A2
- CYP2A6
- CYP2B6
- CYP2C8
- CYP2C9
- CYP2C19
- CYP2D6
- CYP2E1
- CYP3A4

## Dataset sizes

Each isoform has matching record counts across TSV, JSON, and MOL2.

| Isoform | Entries |
|---|---:|
| CYP1A2 | 320 |
| CYP2A6 | 104 |
| CYP2B6 | 178 |
| CYP2C8 | 172 |
| CYP2C9 | 275 |
| CYP2C19 | 271 |
| CYP2D6 | 366 |
| CYP2E1 | 160 |
| CYP3A4 | 579 |
| **Total** | **2425** |

## Data format details

### 1) SMILES TSV (`CYP-SoMs/SMILES/*.tsv`)

Tab-separated table with header:

- `SMILES`: molecular SMILES string
- `Molecule`: compound name

Example header:

```tsv
SMILES	Molecule
```

### 2) JSON (`CYP-SoMs/json/*.json`)

JSON array of compound objects. Observed top-level fields:

- `compound_name` (string)
- `smiles` (string)
- `som_breakdown` (array of SoM annotations)
- `source_dataset` (string)
- `source_reference` (string)

`som_breakdown` entries contain:

- `atom_index` (integer, atom index aligned to structure atom numbering)
- `atom_type` (string)
- `classification` (string; observed values: `primary`, `secondary`, `tertiary`)

Notes:

- `atom_type` values are preserved as provided in source data (including minor spacing variants such as `aromatic C` and `aromatic  C`).

### 3) MOL2 (`CYP-SoMs/mol2/*.mol2`)

Multi-molecule MOL2 files with standard TRIPOS sections and extra FORECASTER metadata blocks.

Observed conventions:

- In `@<TRIPOS>ATOM`, SoM atoms are marked by `*` in the atom label (e.g., `C3*`).
- `@<FORECASTER>Metabolite_Reference_Set` lists SoM categories (PRIMARY/SECONDARY/TERTIARY), dataset source, atom index, and atom type.
- `@<FORECASTER>Metabolite_Reference_Publication` stores literature reference text.

## Mapping between formats

Within each isoform:

- TSV, JSON, and MOL2 describe the same compound set.
- JSON contains the richest machine-readable SoM annotation.
- MOL2 provides structure-level SoM marking for atom-centric workflows.
- TSV is a compact representation for fast filtering and model input preparation.

## License

This dataset is distributed under the Apache License 2.0. See [LICENSE](./LICENSE).
