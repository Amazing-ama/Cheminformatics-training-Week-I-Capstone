# 🧬 Targeted CADD Workflow: EGFR Kinase Domain (PDB ID: 1M17)

**Author:** Amarachi Eze  
**Program:** The Insilico Lab — 3-Week Virtual Training in CADD (Cohort 4)  
**Target Protein:** Epidermal Growth Factor Receptor (EGFR) Kinase Domain  
**Computational Toolkit:** PyMOL, UCSF Chimera, DoGSiteScorer, PyRx (AutoDock Vina), BIOVIA Discovery Studio, SwissADME, ADMETlab 3.0, AlphaFold3  

---

## 📌 Executive Summary
This repository documents a complete 3-week **Structure-Based Drug Design (SBDD)** and **computational chemistry pipeline** conducted during **The Insilico Lab** virtual training program. 

The project investigates the **Epidermal Growth Factor Receptor (EGFR, PDB ID: 1M17)**—a key drug target involved in epithelial homeostasis and cell growth. The workflow progresses through three distinct computational phases:
1. **Target Selection & Protein Preparation:** Structural evaluation of experimental X-ray data, active binding pocket prediction, and molecular structure cleaning.
2. **Chemoinformatics & Molecular Docking:** Drug-likeness screening, binding affinity optimization across three FDA-approved inhibitors (**Erlotinib**, **Gefitinib**, **Lapatinib**), and ADMET pharmacokinetic profiling.
3. **AI Structural Validation:** Comparing AI-generated tertiary protein folds from **AlphaFold3** against experimental X-ray crystallographic structures.

---

## 🗓️ Phase 1: Target Selection, Pocket Mapping & Protein Preparation (Week 1)

* **Protein Target Selection:** Retrieved the crystal structure of the human EGFR kinase domain co-crystallized with 4-anilinoquinazoline inhibitor Erlotinib (**PDB ID: 1M17**, solved via X-ray Diffraction at **2.60 Å** resolution).
* **Biological Significance:** EGFR maintains tissue homeostasis and wound repair, but its dysregulation drives tumor growth.
* **Binding Site Identification:** Utilized **DoGSiteScorer** to map potential catalytic pockets. Identified **Pocket P_0 on Chain A** as the top-ranked active site, defined by key catalytic residues: `LEU694`, `VAL702`, `ALA719`, `ILE720`, `LYS721`, and `GLU738`.
* **Protein Preparation & Optimization:** Loaded raw PDB data into **UCSF Chimera (DockPrep)** to isolate Chain A, eliminate non-catalytic water molecules and solvent ions, optimize hydrogen atom placement, and assign formal charges. The prepared structure was exported as `1M17_prepared.pdb` for docking.

---

## 🧪 Phase 2: Drug-Likeness, Molecular Docking & ADMET Profiling (Week 2)

### 1. Drug-Likeness Screening (SwissADME)
Three small-molecule kinase inhibitors were retrieved from PubChem and evaluated against **Lipinski's Rule of Five** via **SwissADME**:
* **Erlotinib (CID: 176870):** MW = 393.44 Da, LogP = 3.31, HBD = 1, HBA = 6 — **0 Violations (Pass)**.
* **Gefitinib (CID: 123631):** MW = 446.90 Da, LogP = 4.11, HBD = 1, HBA = 7 — **0 Violations (Pass)**.
* **Lapatinib (CID: 208908):** MW = 581.06 Da (Exceeds 500 Da limit), LogP = 5.12, HBD = 2, HBA = 8 — **1 Violation (Acceptable)**.

### 2. Molecular Docking (PyRx / AutoDock Vina)
Ligand geometries were energy-minimized in **PyRx**. AutoDock Vina docking grids were centered around the DoGSiteScorer active site residues (`LEU694`, `VAL702`, `ALA719`, `ILE720`, `LYS721`, `GLU738`).
* **Erlotinib:** **-9.1 kcal/mol** (Rank 1st) — *Strongest binding affinity; extensive hydrogen bonding and hydrophobic contacts*.
* **Gefitinib:** **-8.0 kcal/mol** (Rank 2nd) — *Favorable binding affinity and pocket occupancy*.
* **Lapatinib:** **-7.0 kcal/mol** (Rank 3rd) — *Moderate affinity constrained by larger molecular weight*.

2D/3D non-covalent ligand-receptor interaction diagrams were visualized using **BIOVIA Discovery Studio**.

### 3. ADMET Pharmacokinetics & Safety (ADMETlab 3.0)
Pharmacokinetic profiles were predicted across Absorption, Distribution, Metabolism, Excretion, and Toxicity parameters:
* **Caco-2 Permeability:** Erlotinib (**-4.444**) exhibited superior intestinal permeability over Gefitinib (-4.911) and Lapatinib (-5.304).
* **Plasma Protein Binding (PPB):** Erlotinib (93.9%), Gefitinib (89.4%), and Lapatinib (**99.0%**—highest systemic retention).
* **Half-life & Clearance:** Erlotinib showed a half-life of 1.281 hours and clearance of 7.612, compared to Gefitinib (0.844 hours / 6.422) and Lapatinib (0.685 hours / 3.811).
* **Cardiotoxicity & Mutagenicity:** Erlotinib displayed a low **hERG inhibition liability (0.406)** and low **AMES mutagenicity risk (0.347)**, whereas Gefitinib (hERG 0.899) and Lapatinib (hERG 0.860) exhibited higher cardiotoxicity hazards.

---

## 🤖 Phase 3: AI-Based Structure Evaluation (Week 3)

To test the fidelity of AI structural prediction against experimental X-ray crystallography:
1. **Sequence Retrieval:** Downloaded the 322 amino acid FASTA sequence for 1M17 from RCSB PDB (`1M17.fasta`).
2. **AlphaFold3 Modelling:** Generated the tertiary structure model via the **AlphaFold3 Server** (`1M17predicted.cif`).
3. **Superimposition & Validation:** Aligned the predicted CIF structure onto the cleaned experimental PDB structure (`1M17 cleaned.pdb`) in **PyMOL** using `align predicted, experimental`.

### Structural Superimposition Metrics
* **RMSD Score:** **0.535 Å** across **1,838 aligned atoms**.
* **Structural Homology:** **Excellent** (< 2.0 Å threshold indicates high-precision structural fold matching).
* **pLDDT Confidence Insights:** AlphaFold3 modeled the catalytic core domain with high confidence. Lower pLDDT scores (yellow/orange regions) were limited to flexible terminal regions where AlphaFold modeled missing experimental residues.

---

## 📊 3-Week Data Summary Table

| Parameter / Metric | Erlotinib | Gefitinib | Lapatinib |
| :--- | :---: | :---: | :---: |
| **PubChem CID** | 176870 | 123631 | 208908 |
| **Lipinski Violations** | 0 (Pass) | 0 (Pass) | 1 (MW > 500 Da) |
| **AutoDock Vina Score** | **-9.1 kcal/mol** (1st) | -8.0 kcal/mol (2nd) | -7.0 kcal/mol (3rd) |
| **Caco-2 Permeability** | **-4.444** (Optimal) | -4.911 | -5.304 |
| **Plasma Protein Binding** | 93.9% | 89.4% | 99.0% |
| **Half-life (Hours)** | 1.281 | 0.844 | 0.685 |
| **Clearance** | 7.612 | 6.422 | 3.811 |
| **hERG Cardiotoxicity Risk** | **0.406** (Low) | 0.899 (High) | 0.860 (High) |
| **AlphaFold3 Alignment RMSD** | **0.535 Å** across 1,838 aligned atoms (Excellent Quality) | | |

---

---

## 🏷️ Acknowledgments
Grateful appreciation to **The Insilico Lab** for providing the structured curriculum and computational training framework!

`#CADD` `#DrugDiscovery` `#ComputationalBiology` `#Chemoinformatics` `#AlphaFold3` `#MolecularDocking` `#TheInsilicoLab`

## 📂 Repository Organization
