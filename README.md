# Cheminformatics-training-Week-I-Capstone
# 🧬 CADD Workflow: Targeted Inhibition of EGFR (PDB ID: 1M17)

**Author:** Amarachi Eze  
**Program:** The Insilico Lab — 3-Week Virtual Training in CADD (Cohort 4)  
**Target Protein:** Epidermal Growth Factor Receptor (EGFR) Kinase Domain  
**Key Tools Used:** PyMOL, UCSF Chimera, DoGSiteScorer, PyRx (AutoDock Vina), BIOVIA Discovery Studio, SwissADME, ADMETlab 3.0, AlphaFold3  

---

## 📌 Project Overview
This repository contains a comprehensive **Structure-Based Drug Design (SBDD)** and **computational chemistry workflow** targeting the **Epidermal Growth Factor Receptor (EGFR, PDB ID: 1M17)**. 

Over a 3-week virtual research program at **The Insilico Lab**, the structural integrity of EGFR was evaluated, binding pockets were mapped, small-molecule inhibitors (**Erlotinib, Gefitinib, and Lapatinib**) were benchmarked via molecular docking and ADMET profiling, and AI-based structural prediction (**AlphaFold3**) was evaluated against experimental X-ray crystallographic data.

---

## 🗓️ Weekly Workflow Summary

### 🔹 Week 1: Target Selection, Binding Site Mapping & Protein Preparation
* **Target Selection:** Selected the crystal structure of the EGFR tyrosine kinase domain complexed with 4-anilinoquinazoline inhibitor Erlotinib (**PDB ID: 1M17**, 2.60 Å resolution solved via X-ray Diffraction).
* **Binding Site Identification:** Utilized **DoGSiteScorer** to detect the primary binding pocket on **Chain A (Pocket P_0)**. Identified key active site residues: `LEU694`, `VAL702`, `ALA719`, `ILE720`, `LYS721`, and `GLU738`.
* **Protein Preparation:** Used **UCSF Chimera (DockPrep)** to remove non-catalytic water molecules and co-factors, add missing hydrogens and charges, and save the curated structure as `1M17_prepared.pdb`.

### 🔹 Week 2: Drug-Likeness, Molecular Docking & ADMET Profiling
* **Drug-Likeness Screening (SwissADME):** Screened three FDA-approved kinase inhibitors against Lipinski's Rule of Five:
  * **Erlotinib** (CID: 176870): 0 violations (MW: 393.44 Da, LogP: 3.31) — *Pass*
  * **Gefitinib** (CID: 123631): 0 violations (MW: 446.90 Da, LogP: 4.11) — *Pass*
  * **Lapatinib** (CID: 208908): 1 violation (MW: 581.06 Da > 500 Da, LogP: 5.12) — *Acceptable*
* **Molecular Docking (PyRx / AutoDock Vina):** Grid box centered on the DoGSiteScorer active site residues.
  * **Erlotinib:** `-9.1 kcal/mol` *(Rank 1 — Strongest predicted affinity)*
  * **Gefitinib:** `-8.0 kcal/mol` *(Rank 2)*
  * **Lapatinib:** `-7.0 kcal/mol` *(Rank 3)*
* **Interaction Mapping:** Visualization of 2D/3D non-covalent interactions (hydrogen bonding and hydrophobic interactions) in **BIOVIA Discovery Studio**.
* **ADMET Prediction (ADMETlab 3.0):** Comprehensive evaluation of Absorption, Distribution, Metabolism, Excretion, and Toxicity. Erlotinib demonstrated optimal Caco-2 permeability and favorable safety profiles compared to higher hERG inhibition risks observed in Gefitinib and Lapatinib.

### 🔹 Week 3: AI-Based Structure Prediction & Evaluation (AlphaFold3)
* **Sequence Extraction:** Retracted the 1M17 FASTA sequence from RCSB PDB.
* **AlphaFold3 Prediction:** Predicted 3D tertiary structure via the AlphaFold3 Server (`1M17predicted.cif`).
* **PyMOL Structural Superimposition:** Aligned the predicted AlphaFold3 model against the experimental cleaned structure (`1M17 cleaned.pdb`).
* **Validation Metric:** Achieved an **RMSD of 0.535 Å** across 1,838 aligned atoms, confirming near-identical structural homology (< 2.0 Å indicates excellent model quality). Minor lower pLDDT confidence regions (yellow/orange) were observed at flexible terminal ends.

---

## 📊 Key Results Benchmark

| Compound | PubChem CID | Lipinski Violations | Best Vina Docking Score (kcal/mol) | Rank | Key ADMET Insight |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Erlotinib** | 176870 | 0 | **-9.1** | **1st** | Superior Caco-2 permeability & balanced safety profile |
| **Gefitinib** | 123631 | 0 | **-8.0** | **2nd** | Moderate binding, elevated hERG liability |
| **Lapatinib** | 208908 | 1 (MW > 500) | **-7.0** | **3rd** | High plasma protein binding (99.0%), highest hERG risk |

---

## 📂 Suggested Repository Structure

├── week1_protein_prep/ │   ├── 1M17.pdb │   ├── 1M17_prepared.pdb │   └── pymol_screenshots/ ├── week2_docking_admet/ │   ├── ligands/ (Erlotinib.sdf, Gefitinib.sdf, Lapatinib.sdf) │   ├── pyrx_results/ │   ├── discovery_studio_2d_diagrams/ │   └── swissadme_admetlab_reports/ ├── week3_alphafold3/ │   ├── 1M17.fasta │   ├── 1M17predicted.cif │   └── pymol_alignment_overlay.png └── README.md

---

## 🏷️ Acknowledgments & Hashtags
Special thanks to **The Insilico Lab** team for providing the structure and virtual training framework!

`#CADD` `#DrugDiscovery` `#ComputationalBiology` `#Chemoinformatics` `#VirtualResearch` `#TheInsilicoLab`
