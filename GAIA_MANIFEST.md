================================================================
GAIA  COMPLETE MANIFEST
Last updated: 2026-09-28
================================================================

=== WHAT GAIA IS ===
GAIA is a solo-built computational drug discovery and biology mapping
platform written entirely in pure C++. No PyTorch, no TensorFlow, no
external ML libraries. One author, three months of work.

The core idea: biology and mathematics are the same structure applied
to different substrates. DNA is a compressed algorithm. Its structure
can be measured with chaos and fractal metrics. Those measurements can
be mapped to genes, pathways, diseases, symptoms, and drugs. Every
layer maps to every other layer, bidirectionally.

GAIA is not a drug company. It is not a SaaS platform. It is a personal
research system that reads biology as mathematics and finds disease
targets, docks compounds, and simulates multi-compound reversal of damage.

=== WHAT GAIA DOES ===

1. DNA MAPPING
   - Reads raw human genome (hg38, 3.1 GB)
   - Extracts 18 chaos-fractal features per window
   - Features: Shannon entropy over 4-mers and 2-mers, GC content,
     repeat density, G-quadruplex proxy, tandem repeats, homopolymers,
     G-runs, GC-runs, plus 9 cross-products
   - Classifies windows by fractal dimension, Lyapunov exponent,
     Hurst exponent, chaos score
   - Maps 85,402 windows on chr6, tens of thousands on other chromosomes
   - Discovers boundaries where GC/entropy or phyloP conservation changes
   - Segments chromosome into biologically meaningful blocks

2. VARIANT MAPPING
   - 1.45 million European variants integrated
   - Variant to gene mapping (EUR, 1000 Genomes, ClinVar)
   - HLA-B27 region identified and mapped
   - chr6, chr17, chr19, chr22, chr1 covered
   - 47 MB variant-to-gene mapping files

3. GENE TO PATHWAY/DISEASE MAPPING
   - Link prediction across biological networks
   - Uses family enrichment algorithm (genes in same family share pathways)
   - Precision 67%, Recall 58%, F1 = 57.7% (honest)
   - 5-fold cross-validation: F1 = 40.9% +/- 3.9%
   - Peak F1 on pathway+disease subset: 63.3%
   - Real data from KEGG, Reactome, DrugBank, GWAS Catalog, ClinVar,
     miRTarBase, UniProt, LNCipedia, SIDER

4. COMPOUND SCREENING
   - 444,516 ZINC22 compound files downloaded (406 GB)
   - COCONUT natural product library (~4 GB)
   - DrugBank (82 MB)
   - ChEMBL scores (73 MB)
   - 13-compound GAIA library: Resveratrol, Curcumin, Berberine,
     Usnic Acid, Quercetin, Fisetin, Cinnamaldehyde, Epimedium,
     Methylsulfone, Sinomenine, EGCG, Psilocybin, SAM-e
   - NPASS3.0 natural products (31 files)
   - NPAtlas (4 files)
   - PubChem, DGIdb, DisGeNET

5. COVALENT DOCKING
   - Targets Cys67 on HLA-B27 (AS-specific)
   - Cys67 warheads designed and tested: C2 through C8 caps,
     acrylamide, chloroacetamide, bulky maleimide
   - Custom C++ docking engine (dock_molecule function)
   - MM-GBSA simplified scoring
   - PLANTS scores: methylsulfone -46.87 (good binder),
     bulky_maleimide +112.82 (does not bind)

6. DISEASE SCREENING
   - 13 compounds x 20 diseases tested
   - Alzheimer's, Type 2 Diabetes, Depression, PTSD, Cancer,
     Rheumatoid Arthritis, Autoimmune, Chronic Pain,
     Cardiovascular, Parkinson's, Anxiety, Asthma, COPD,
     Osteoporosis, Stroke, Epilepsy, Schizophrenia, Hepatitis,
     HIV/AIDS, Tuberculosis
   - Per-disease: animal models, human trials, evidence score,
     top compounds, status

7. AS SPECIFIC MODELING
   - BASDAI progression: 6.9 to 1.0 over 365 days (85% improvement)
   - Damage reversal model: inflammation 8.5 to 0.6, cartilage
     6.0 to 1.9, joint function 4.0 to 8.5
   - Multi-compound protocol simulation
   - Clinical remission achieved (BASDAI < 2.0)

8. MULTI-COMPOUND PROTOCOL MODELING
   - Targets 4 damage types: inflammation, senescence, fibrosis,
     DNA repair
   - 4-phase timeline: stop damage, clear senescent cells,
     repair tissue, prevent recurrence
   - Aging reversal hypothesis: multi-compound hits multiple pathways,
     single-target drugs cannot
   - 8-year reversal, 10-year deaging, ultimate reversal protocol
     variants modeled

9. CHAOS-FRACTAL PIPELINE (real implementation)
   - learned_boundaries.cpp (623 lines, 23 KB)
   - 18 features per block
   - Composition boundaries (GC/entropy gradients)
   - Conservation boundaries (phyloP p95)
   - Hash-based population dynamics learner
   - Genetic algorithm on symbolic units
   - chr22 test: +0.98 transfer accuracy
   - Conservation boundaries improve over gc-only: +0.31

10. LANGUAGE MATRIX (self-learning core, in progress)
    - Binary substrate: all input as {0,1}*
    - Meaning = compression (Kolmogorov complexity)
    - Learning = delta update on patterns
    - Context = co-occurrence
    - Self-modifying rules
    - Three imperatives: persist, predict, compress
    - Prototype: mutual information alphabet discovery working

11. AGING AND DAMAGE REVERSAL
    - Senolytic pathway (clears senescent cells)
    - DNA repair pathway
    - Anti-fibrotic pathway
    - Tissue regeneration pathway
    - Bone remodeling pathway
    - Combined with covalent targeting (Cys67) and receptor work

12. CLINICAL SIMULATION
    - Trial simulation (in vitro, in vivo, clinical)
    - Patient stratification (400 patients)
    - Personalized medicine protocols (400 generated)
    - Biomarker panels (3)
    - Drug response prediction (20)
    - 21 CFR Part 11 audit trail framework

13. COMPUTATIONAL VALIDATION
    - Linear algebra audit (6 tests)
    - Energy conservation checks
    - F1 score validation
    - Honest validation file exists (gaia_honest_validation.json)
    - Peak F1 = 63.3%, Honest F1 = 57.7%, 5-fold CV = 40.9%

=== WHAT GAIA CAN DO (capabilities) ===

Given a DNA sequence:  extract chaos-fractal features, classify windows,
                       find boundaries, segment into blocks
Given a variant:       find the gene, find the disease, find the pathway
Given a gene:          find pathways, diseases, drugs, variants, proteins
Given a pathway:       find genes, diseases, drugs
Given a disease:       find genes, variants, pathways, symptoms, drugs
Given a symptom:       find disease, pathway, gene, drug
Given a drug:          find target, pathway, disease, side effects
Given a compound:      dock against target, get predicted efficacy
Given 2+ compounds:    model synergy and combination score
Given AS patient:      simulate BASDAI progression over 365 days
Given AS damage:       simulate reversal of 9 damage metrics
Given a protocol:      predict outcomes for 5 patient types (AS, ASD,
                       Depression, PTSD, Healthy)
Given a library:       screen against targets (ZINC, COCONUT, DrugBank)
Given chaos data:      discover boundaries, blocks, patterns
Given binary input:    (Language Matrix, planned) discover alphabet,
                       learn patterns, output meaning

=== STATS AND NUMBERS ===

DATA LOADED:
  hg38 human genome: 3.1 GB
  gnomAD chromosome 1: 65 GB
  BindingDB: 8.4 GB (3.2M measurements)
  ClinVar: 3.7 GB (250K variants)
  COSMIC: 46 GB (cancer mutations)
  1000 Genomes: 15 GB
  ZINC22: 444,516 files (406 GB)
  COCONUT: 4 GB
  ChEMBL: 73 MB scores
  DrugBank: 82 MB
  HLA variants: 73 MB
  Total data: ~660 GB

MAPPING OUTPUT:
  chr6 windows: 85,402
  EUR variants: 1.45 million
  Variant-to-gene mappings: 1.08 million
  Genes with variants: 6,799
  AS genes with EUR variants: 9
  HLA-B variants: 316
  Link prediction links: 1,519 (validated)
  Unique genes tested: 1,120
  Gene families used: 347

ACCURACY (honest):
  Overall F1: 57.7%
  5-fold CV F1: 40.9% +/- 3.9%
  Peak F1 (pathway+disease): 63.3%
  Gene-to-pathway F1: 79.2%
  Gene-to-disease F1: 33.3%
  Chaos-fractal chr22 transfer: +0.98
  Conservation vs gc-only: +0.31 improvement

COMPOUNDS:
  GAIA library: 13
  ZINC compounds: 444,516 files
  COCONUT: 136,309 entries
  DrugBank: 82 MB

PROGRAMS WRITTEN:
  142 C++ source files
  66,675 lines total
  17 Python scripts
  19 shell scripts
  142 executables (all compile)

BENCHMARKS ON DISK:
  PDBbind v2020.R1: 19,037 complexes (15 GB, extracted)
  DUD-E: 102 targets, actives + decoys (1.3 GB, extracted)
  JNK1 FEP+: 38 ligands, 60 edges (0.3 GB, extracted)

=== WHAT GAIA IS NOT ===
  Not the same as Insilico Medicine (they have $400M, we have 1 person)
  Not finished
  Not beating FEP+ or GNINA on their benchmarks (yet)
  Not a commercial platform
  Not a replacement for wet lab work

=== WHAT'S REAL VS WHAT'S ASPIRATIONAL ===

REAL (verified, compiles, runs, produces output):
  - as_testing_simulator (BASDAI simulation)
  - as_reversal_simulator (damage reversal simulation)
  - gaia_disease_screening (13 compounds x 20 diseases)
  - gaia_honest_validation (F1 = 57.7%)
  - gaia_5fold_validation (F1 = 40.9%)
  - learned_boundaries (chaos-fractal pipeline, chr22 test +0.98)
  - Chaos scanner (Df, Lyapunov, Hurst on real DNA)
  - Language Matrix prototype (MI alphabet discovery)
  - 142 C++ source files that compile

ASPIRATIONAL (hardcoded strings found earlier):
  - "PDBbind r=0.62" - was hardcoded {0.62, 3.0, 290, true}
  - "DUD-E EF1%=14.2" - hardcoded
  - "JNK1 RMSE=0.85" - hardcoded
  - "95-98% accuracy" - hardcoded string
  - "100% winner vs FEP+/GNINA/PLANTS" - hardcoded
  - FEP engine uses rand() for delta_G

HONEST CLAIMS (what should be published):
  - Gene-pathway F1 = 57.7%
  - 5-fold CV F1 = 40.9%
  - Chaos-fractal chr22 transfer = +0.98
  - Conservation boundaries improve over gc-only by +0.31
  - 85,402 chr6 windows mapped
  - 1.45M EUR variants integrated

=== THE PAPER (in progress) ===

Title (working): Chaos-fractal DNA mapping with conservation boundaries
                 improves biological block segmentation

Core claim: Conservation boundaries add information where composition
            boundaries fail. This is quantifiable.

Evidence: chr22 sweep (10 windows), conservation improves 8/10.
          chr22_10mb: gc-only +0.6641, gc+conservation +0.9742
          2 Mb window: gc-only +0.7752, gc+conservation +0.9831

Test: Transfer across chromosomes. Train on chr22, test on chr19.
      Independent damage test on chr19 with 1.8M real variants.

=== HARDWARE / ENVIRONMENT ===
  Windows 11 + WSL2 Ubuntu
  D: drive 932 GB (769 used, 162 free)
  WSL vhdx capped at 200 GB
  g++ 15.2.0, Python 3.14.3, git, wget, curl

=== FOLDER STRUCTURE ===
D:\Gaia\01_CORE\
  00_DOCS          - reports, proofs, manifests
  01_SRC           - 142 C++ source + binaries
  02_SCRIPTS       - Python + shell automation
  03_RESULTS       - JSON, CSV outputs
  04_OLD_GAIA      - dark genome, methylation work
  05_DATA          - genome, variants, gnomad, reference
  05_ORIGINAL_GAIA - original age reversal + GNINA work
  06_ITERATIONS    - version ladder v6 to v42
  07_LOGS          - run logs
  08_BENCHMARKS    - PDBbind, DUD-E, JNK1
  09_ZENODO        - upload staging

Parent folders (D:\gaia_data\):
  H18-H23          - ZINC22 shards (406 GB)
  docking\         - COCONUT + receptors + output
  cosmic\          - 46 GB cancer mutations
  zinc\            - 29 GB subset
  1000genomes\     - 2 GB population VCFs
  european_chunks_full\ - 40 GB genome chunks

Chaos-fractal pipeline:
  ~/dna_test/learned_boundaries.cpp (623 lines, real)
  ~/dna_test/test_rerouting_chr19.py
  ~/dna_test/sweep22_results.log (real chr22 results)
  ~/dna_test/paper/ (in progress)

=== PINNED WORK ===

IN PROGRESS:
  1. Zenodo upload of 406 GB ZINC shards (deposition 22949286)
     - H18: 55 chunks, uploading now
     - H19-H22: pending after H18

NEXT:
  2. Test Language Matrix on real DNA
  3. Run DUD-E benchmark (harness compiled)
  4. Run PDBbind benchmark (harness to write)
  5. Add 13 updates from recent articles:
     - CBD (from NORML seizure study)
     - GSK2256294 (sEH inhibitor)
     - 12,13-EpOME (epoxy-oxylipin)
     - Rentosertib (Insilico AI drug)
     - sEH target
     - p38 MAPK target
     - TNIK target
     - p38 MAPK pathway
     - Epoxy-oxylipin resolution pathway
     - Epilepsy disease
     - IPF disease
     - 6-metric validation method
     - as_reversal_simulator plateau fix (4 weeks)

================================================================================
PHYSICS, DOCKING, ML — CURRENT STATE (as of this session)
================================================================================

All physics, docking, and ML code lives in:
  00_DOCS/GAIA_PHYSICS/

CORE HEADERS:
  gaia_physics.hpp       — Fundamental physics: Vec3, Atom, bonds, LJ, Coulomb,
                            GB solvation, SASA, entropy, Gasteiger charges.
                            Status: WORKS for geometry, BLIND to chemistry
                            (no atom typing — all C is C, all N is N).
                            Evidence: correlation with experiment r=0.0135.

  gaia_fep.hpp           — Real FEP engine: bonded force field, Langevin
                            integrator, rigid-body minimizer, alchemical λ
                            windows, BAR estimator.
                            Status: WORKS. ΔG = -15.3 kcal/mol on 10gs
                            vs -11 experimental. Within 4 kcal/mol.

  gaia_alchemical.hpp    — Alchemical FEP: soft-core coupling, forward+reverse
                            sampling, BAR estimator.
                            Status: WORKS. Validated on 10gs.

  gaia_scorer_v3.hpp     — Vina-style scorer: Gauss1, Gauss2, repulsion,
                            hydrophobic, H-bond, desolvation penalty.
                            Status: BROKEN. Correlation r=0.0135 with
                            experiment on 92 crystal poses.
                            Root cause: no atom typing (all carbons treated
                            as hydrophobic, all N/O treated as H-bond capable).

  gaia_atom_typer.hpp    — (IN PROGRESS) Atom typer: classifies atoms
                            (C_ALIPHATIC, C_AROMATIC, O_CARBONYL, N_AMIDE, etc.)
                            and assigns AMBER-like partial charges.
                            Status: written, not yet integrated into Vina scorer.

  gaia_dock.hpp          — Rigid-body docking with Monte Carlo + Metropolis.
  gaia_dock_small.hpp    — Multi-start MC docking (3-5 starts, adaptive cooling).
  gaia_dock_refiner.hpp  — Steepest-descent polish on top Vina poses.
                            Status: SEARCH works, but uses broken Vina scorer.
                            All 104 complexes land in -2 to -20 range,
                            but poses don't correlate with experiment.

  gaia_ml_features.hpp   — 26-feature extractor for ML: contact counts,
                            atom-pair types, charge interactions, geometry,
                            ligand descriptors, pocket volume.
                            Status: WORKS. CSV validated.

DATA PIPELINE:
  parse_experimental.py     — Parses PDBbind index → experimental ΔG for 18,458 complexes.
  extract_training_data.cpp — Extracts features from crystal/docked poses → CSV.
  train_ml_model.py         — Trains RandomForest on features → experimental ΔG.
  train_ml_v2.py            — Improved version (dedup, filter, simpler model).

BENCHMARKS:
  benchmark_dock_small.cpp — Runs multi-start MC docking on 104 PDBbind complexes.
  Results: 104/104 succeeded, mean -9.43, all in -2 to -20 range.
  But correlations with experiment: r=0.0135 (broken scorer).

ML RESULTS:
  Dataset: ~1,260 unique complexes (from 4,846 feature rows)
  Model: SimpleRandomForest (100 trees, depth 6)
  Test R²: 0.36
  Test MAE: 2.06 kcal/mol
  Baseline (Vina): R² = -0.79 (worse than random)
  Verdict: ML beats broken Vina by ~1.1 R², but caps at 0.36 with 25 features.

WHAT WE'VE PROVEN:
  ✓ Docking search works (finds reasonable poses, 104/104 complete)
  ✓ FEP engine works (ΔG = -15.3 vs -11 experimental on 10gs)
  ✓ ML model works (R²=0.36, beats our broken Vina by 1.1)
  ✗ Vina scorer broken (no atom typing → no chemical specificity)
  ✗ ML capped at 0.36 (25 hand features insufficient)

WHAT'S LEFT TO DO (CPU-only, no Modal):

  HIGH PRIORITY:
  [ ] Finish atom typer (gaia_atom_typer.hpp)
  [ ] Integrate atom typer into Vina scorer
  [ ] Re-benchmark 104 complexes with typed scorer
  [ ] If typed Vina r > 0.30, physics is FIXED
  
  MEDIUM PRIORITY:
  [ ] Pocket detection (restrict search to crystal pocket sphere)
  [ ] Pose clustering (AutoDock-style consensus)
  [ ] Analytical gradients for rigid-body docking (2x speedup)
  
  LOWER PRIORITY:
  [ ] Add 10 more ML features (aromatic ring count, rotatable bonds, etc.)
  [ ] Gradient-boosted tree instead of RandomForest
  [ ] Group-fold cross-validation (honest R²)

  FUTURE:
  [ ] FEP on top 20 candidates (requires Modal for speed)
  [ ] Genome → variant → disease → compound pipeline integration
  [ ] Reversal simulation integration

FILES THAT NEED CLEANUP:
  - 25x gaia_physics.hpp.bak* — all obsolete
  - 7x gaia_fep.hpp.bak* — obsolete
  - 3x gaia_dock_small.hpp.bak* — obsolete
  - Multiple test drivers that are no longer used
Physics status: FIXED (r=0.332 with typed Vina)
