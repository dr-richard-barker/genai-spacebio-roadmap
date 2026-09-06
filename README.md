# GenAI × Space Biology: Roadmap

What's already covered across [dr-richard-barker](https://github.com/dr-richard-barker)'s 153 repos, read against a September 2026 Cell perspective on generative AI in biology — and where the open gaps are.

## Why this exists

Cross-referencing [Fifteen challenges for generative AI applications to cell biology](https://www.cell.com/cell/fulltext/S0092-8674(26)00802-0) (Dupire, Khan, Karaletsos, Kelley, Lundberg, Ma, Paull, Quake, Rabadan, Rowan, Sims, Tavazoie, Tsang, Zhang & Califano; *Cell*, Aug 17 2026, open access) against the actual, current contents of the `dr-richard-barker` GitHub account (153 repos, 145 public, pulled 2026-09-06), to surface concrete bioinformatics project ideas that build on existing infrastructure rather than starting from zero.

Everything under "current portfolio" below is drawn from the repos' own names/descriptions, not reconstructed from memory — several dozen of these repos were pushed in the week before this analysis was written.

## The paper, briefly

The authors (mostly Columbia/Califano-lab systems biology, alongside authors from Chan Zuckerberg Biohub, Stanford, and others) define "Gen-AI" narrowly: foundation-model/transformer architectures that learn a generalizable probability distribution over biological data, as opposed to (a) purely discriminative classifiers, (b) task-specific predictors, or (c) classical network/statistical ML. Their argument, in short:

- Gen-AI has clearly worked at the **molecular** level — protein structure/design, variant effect scoring — because that data is sequence-like, abundant, and high-quality (PDB, UniProt).
- It has **not** yet demonstrated the same success at the **cellular and multicellular** level (predicting cell state, tissue behavior, organismal response), and most published single-cell foundation models (they name scGPT and Geneformer specifically) fail to beat simple linear baselines once evaluated on genuinely held-out cell types, perturbations, or tissues.
- Their explanation isn't "just needs more scale" (they explicitly argue against Rich Sutton's "bitter lesson" here): biological data is ~1000x sparser than language data, and the combinatorial space of multi-way molecular interactions (e.g., a 47-protein ribosomal subunit) is too large for de novo learning. They argue biological priors — regulatory networks, protein-protein interaction graphs (STRING, PrePPI, ARACNe, ENCODE) — should be architecturally "pre-wired" into models as attention priors, not left for the model to rediscover from data alone.
- Most Gen-AI biology papers are benchmarked **retrospectively** on statistical metrics (e.g., AUC on cell-type classification) rather than **prospectively** validated the way CASP (protein folding) and DREAM (Sage Bionetworks community challenges) have done for decades. They want the field to adopt that discipline.
- They propose **15 concrete grand challenges**, Hilbert-problem-style, each with a suggested experimental validation design, success metric, and non-Gen-AI baseline, spanning four levels: molecular interactions/function → cell and system-level function → clinical/organismal translation.

### The 15 challenges (paraphrased)

| # | Challenge | One-line gist |
|---|---|---|
| 1 | Regulatory & signaling interactions | Predict combinatorial TF/co-factor logic on chromatin (e.g. super-enhancer condensates) |
| 2 | Epigenetic interactions | Predict chromatin/histone/methylation state from sequence + baseline omics |
| 3 | Cell-cell interactions | Predict which ligand from cell A sets the transcriptional state of cell B |
| 4 | Synthetic mechanisms | Design plasmids/promoters that behave predictably after cell engineering |
| 5 | Genome to function | Score the functional effect of a novel mutation/variant |
| 6 | Drug mechanism of action | Predict a drug's full on- and off-target proteome effect |
| 7 | Genome to phenotype | Predict the minimal genome/gene set sufficient for a living function |
| 8 | Cell state reprogramming | Predict which perturbation drives a specific cell-state transition |
| 9 | Logic biocircuit design | Design synthetic gene circuits implementing Boolean logic |
| 10 | Co-culture & microenvironment | Predict the minimal cell/reagent mix that keeps a co-culture viable |
| 11 | Biomarker identification | Find multi-omics biomarkers of drug/treatment response |
| 12 | Drug toxicity | Predict organ- or system-level toxicity before it's observed |
| 13 | Drug efficacy | Predict cell-state-specific drug sensitivity |
| 14 | Organismal responses | Predict response magnitude (e.g. vaccine titer) from pre-exposure baseline |
| 15 | Clinical trial outcome | Predict responder vs. non-responder fraction and mechanism |

Their consistent prescription for progress: anchor the model in a knowledge graph / network prior, and validate blind and prospectively.

## Current portfolio: what's already being investigated

Grouped by theme, with representative repos (not exhaustive — see the [full list](https://github.com/dr-richard-barker?tab=repositories)):

**Bulk multi-omics meta-analysis over NASA OSDR/GeneLab** — the largest single cluster. [OSDR_X-species_V2](https://github.com/dr-richard-barker/OSDR_X-species_V2) (22 datasets, 6 species), [arabidopsis-spaceflight-omics](https://github.com/dr-richard-barker/arabidopsis-spaceflight-omics), [astronaut-oncogene-biomarkers](https://github.com/dr-richard-barker/astronaut-oncogene-biomarkers), [astronaut-mineral-deficiency-multiomics](https://github.com/dr-richard-barker/astronaut-mineral-deficiency-multiomics), [veg05-integrated-omics](https://github.com/dr-richard-barker/veg05-integrated-omics), [SpaceMineralAtlas](https://github.com/dr-richard-barker/SpaceMineralAtlas), [OSD615-glycome-cytoskeleton-systems-biology](https://github.com/dr-richard-barker/OSD615-glycome-cytoskeleton-systems-biology), [Muscle-Atrophy-Multi-Omics-OSDR](https://github.com/dr-richard-barker/Muscle-Atrophy-Multi-Omics-OSDR).

**Reference-atlas-informed "decoder" models** — bespoke deconvolution/embedding models that already lean on external priors, the closest existing analog to what the paper is asking for. [Tropism_autodecoder_2026](https://github.com/dr-richard-barker/Tropism_autodecoder_2026) (1,337 samples deconvolved via a Salk single-cell atlas), [arabidopsis-drem-osdr](https://github.com/dr-richard-barker/arabidopsis-drem-osdr) (cell-type-weighted regulatory prior wired directly into a DREM model, not just used for annotation — SOG1/MYB3R recovered with a knockout control), [deepspace-seed-stress-decoder](https://github.com/dr-richard-barker/deepspace-seed-stress-decoder), [Circadian_decoder](https://github.com/dr-richard-barker/Circadian_decoder), [Redox_decoder](https://github.com/dr-richard-barker/Redox_decoder).

**Mechanistic/CFD biophysical modeling** — physics-anchored digital twins, in spirit exactly what the paper argues Gen-AI should be fused with. [LunarLeaf-CFD](https://github.com/dr-richard-barker/LunarLeaf-CFD), [Photorespiration_multiomics_microgravity](https://github.com/dr-richard-barker/Photorespiration_multiomics_microgravity), [microgreen-chamber-cfd](https://github.com/dr-richard-barker/microgreen-chamber-cfd), [spaceflight-plant-hardware-cfd](https://github.com/dr-richard-barker/spaceflight-plant-hardware-cfd).

**Image-based phenotyping / computer vision** — [cose-fiji](https://github.com/dr-richard-barker/cose-fiji), [astroroot](https://github.com/dr-richard-barker/astroroot), [AstroBotany_calibration_image_sharing_and_analysis](https://github.com/dr-richard-barker/AstroBotany_calibration_image_sharing_and_analysis), [TICTOC](https://github.com/dr-richard-barker/TICTOC), [Anthocyanin-Image-analysis](https://github.com/dr-richard-barker/Anthocyanin-Image-analysis).

**Curated knowledge bases / atlases** — [fungal-bgc-atlas](https://github.com/dr-richard-barker/fungal-bgc-atlas) (609 dossiers, relational DB + knowledge graph + dashboard), [AstroRegolith](https://github.com/dr-richard-barker/AstroRegolith), [SpaceMineralAtlas](https://github.com/dr-richard-barker/SpaceMineralAtlas).

**Countermeasure / drug & nutrition screening** — [Astronaut_flavenoids_and_biomarkers](https://github.com/dr-richard-barker/Astronaut_flavenoids_and_biomarkers) (already uses LINCS L1000 — one of the exact datasets the paper's Table 2 cites for its drug-MoA challenge), [Astronaut_brain_food](https://github.com/dr-richard-barker/Astronaut_brain_food).

**Closed-loop life support / synthetic ecology** — [LunarFarm-BLSS](https://github.com/dr-richard-barker/LunarFarm-BLSS), [osdr-plant-microbiome](https://github.com/dr-richard-barker/osdr-plant-microbiome), [Microbiome_of_seedlings_in_space](https://github.com/dr-richard-barker/Microbiome_of_seedlings_in_space), [biosim-nextgen](https://github.com/dr-richard-barker/biosim-nextgen).

**Cell-cell communication tooling present, not yet applied to a spaceflight dataset** — [CellChat_4_plants](https://github.com/dr-richard-barker/CellChat_4_plants), [ggPlantmap](https://github.com/dr-richard-barker/ggPlantmap).

**LLM/agentic tooling, forked but not yet built out for space biology** — [genai-stack](https://github.com/dr-richard-barker/genai-stack) (LangChain + Neo4j + Ollama), [openscience](https://github.com/dr-richard-barker/openscience), [Genesis](https://github.com/dr-richard-barker/Genesis), [habitat-sim](https://github.com/dr-richard-barker/habitat-sim).

**GWAS / genotype-level** — [arabidopsis-gwas-spaceflight](https://github.com/dr-richard-barker/arabidopsis-gwas-spaceflight), [brachypodium-gwas-spaceflight](https://github.com/dr-richard-barker/brachypodium-gwas-spaceflight).

Outside the bioinformatics scope of this review: the games/sim cluster (LunarSims, lunar-arcade, Lunar_Red_Alert, Settlers_of_the_Moon_or_Mars, mars-sim fork), hardware (Clinostat, LinearRobot, helmholtz-nmf-cage), and education/FAIR tooling (Space_Biology_Education.io, GeneLab_API_Tutorial, OSDR_jupyter_book.io).

## Gap analysis against the 15 challenges

| # | Challenge | Closest existing work | Status |
|---|---|---|---|
| 1 | Regulatory/signaling logic | `arabidopsis-drem-osdr` wires a regulatory prior into the model itself | **Partial** — proof of concept for one module (SOG1/MYB3R); not generalized |
| 2 | Epigenetic interactions | — | **Open gap** |
| 3 | Cell-cell interactions | `CellChat_4_plants`, `ggPlantmap` exist as tools | **Partial** — tool present, not yet applied to a spaceflight dataset |
| 4 | Synthetic circuit/plasmid design | — | Low relevance (mammalian/iPSC-engineering specific) |
| 5 | Genome to function (variant scoring) | GWAS repos localize loci | **Partial** — locus-level, no functional variant-effect scoring |
| 6 | Drug mechanism of action | `Astronaut_flavenoids_and_biomarkers` (LINCS L1000 reversal) | **Partial** — connectivity-mapping level, not regulon/protein-activity level |
| 7 | Genome/consortium to phenotype | `LunarFarm-BLSS`, `osdr-plant-microbiome` | **Open gap**, but the pieces to combine already exist |
| 8 | Cell state reprogramming (perturbation-response prediction) | Large perturbation-response omics corpus, but no predictive model over it | **Open gap** |
| 9 | Logic biocircuit design | — | Low relevance |
| 10 | Co-culture/microenvironment design | `LunarFarm-BLSS` measures a closed loop but doesn't optimize its composition | **Partial** |
| 11 | Biomarker identification | `astronaut-oncogene-biomarkers`, `astronaut-mineral-deficiency-multiomics` | **Best-covered challenge** in the portfolio |
| 12 | Drug/countermeasure toxicity | — | **Open gap** |
| 13 | Drug efficacy (cell-state-specific) | — | Low relevance (no space-flown PDX/organoid data) |
| 14 | Organismal response from baseline | `Astronaut_trends` looks at population trends, not individual baseline→response | **Open gap** |
| 15 | Trial-outcome prediction | — | Not directly applicable to space biology |

## Recommended next projects

Ordered roughly by how directly they build on infrastructure that already exists.

**A. Regulatory-network prior for the decoder family (extends Challenge 1).** Generalize what `arabidopsis-drem-osdr` already does for one module: reconstruct a plant stress-regulatory network from the pooled OSDR expression compendium (an ARACNe-style approach, the exact method the Cell paper cites), then wire it in as an explicit graph prior across `Tropism_autodecoder_2026`, `Circadian_decoder`, and `Redox_decoder` instead of training each purely on expression values. A head-to-head "prior-informed vs. naive" comparison is itself a publishable methods result, and it's the paper's central architectural recommendation.

**B. Perturbation-response prediction — a small "virtual plant cell" (Challenge 8).** The portfolio already has parallel perturbation-response transcriptomes for radiation dose, hypoxia/CO2, regolith substrate, and light spectrum (`Plant_response_to_radiation`, `Hypoxia_vs_elevated_CO2_in_spaceflight`, `AstroRegolith`, `VEGGIE_Tom_Red_Blue_Leaves_and_adv_roots`) but nothing that predicts response to an *untested* combination. Train on a subset of conditions, hold out one combination genuinely never modeled, and predict it blind before checking — the prospective-validation discipline the paper is explicitly asking the field to adopt.

**C. Out-of-distribution stress test of a plant single-cell foundation model (directly extends the paper's own critique).** `arabidopsis-spaceflight-omics` already integrates scPlantLLM. The paper's headline empirical finding is that scGPT/Geneformer collapse to linear-baseline performance on genuinely held-out cell types and perturbations. Nobody appears to have run that same benchmark for a plant foundation model — and spaceflight is about as out-of-distribution as plant transcriptomics gets relative to Earth-grown training atlases. This is a small, well-scoped, citable methods note.

**D. Apply the cell-cell communication tools you already forked (Challenge 3).** `CellChat_4_plants` and `ggPlantmap` exist but aren't yet pointed at a spaceflight dataset. Run them against a deconvolved output from `Tropism_autodecoder_2026` or `arabidopsis-drem-osdr` to ask, e.g., whether root cap–meristem ligand-receptor signaling shifts under altered gravitropism — a genuinely novel question in space plant biology.

**E. Minimal synthetic BLSS consortium via genome-scale metabolic models (Challenge 7).** Connect `LunarFarm-BLSS`, `osdr-plant-microbiome`, and `Microbiome_of_seedlings_in_space`: use GEMs (the same modeling approach already built for `Myco_tissue_RNAseq`) to computationally screen the minimal microbial/plant taxon set that sustains closed-loop nutrient cycling, then check the prediction against `LunarFarm-BLSS`'s already-measured findings.

**F. Regulon-based countermeasure MoA screening (Challenge 6).** Extend `Astronaut_flavenoids_and_biomarkers` past connectivity mapping to VIPER/metaVIPER-style protein-activity inference — the actual tool the Cell paper's own authors cite for this challenge — to surface indirect/off-target master regulators reversed by candidate flavonoid or nutrition countermeasures, not just the directly bound targets.

**G. Pre-flight "setpoint" predictor of individual spaceflight response (Challenge 14).** `Astronaut_trends` and `astronaut-mineral-deficiency-multiomics` already touch repeated-measures astronaut multi-omics. The open question they don't yet ask: does an individual's *pre-flight* baseline profile predict the *magnitude* of their in-flight transcriptional/physiological perturbation? This directly mirrors the immune-health-setpoint vaccine-response literature the paper cites (Tsang et al.) — same design, different exposure.

**H. A held-out "Space Biology DREAM Challenge" (methodological/community).** The amount of cleaned, harmonized OSDR meta-analysis infrastructure already built (`SpaceMineralAtlas`, `OSDR_X-species_V2`, `arabidopsis-spaceflight-omics`) is unusual. That's the raw material for organizing a genuine blind prospective benchmark — withhold a newly released OSDR dataset, invite predictions before un-blinding — mirroring CASP/DREAM, which the paper holds up as the standard the field currently fails to meet.

## A framing worth borrowing regardless of which project comes next

The paper's tier 1 (retrospective, statistical) vs. tier 2 (prospective, biological-discovery) split is a useful thing to state explicitly in any writeup: does a model classify better on held-out samples from the *same* batch/experiment, or did it correctly predict an experiment nobody had run yet? Most of the existing decoder/biomarker repos are currently evaluated in the tier 1 sense; several of the ideas above (B, C, H especially) are ways to earn a tier 2 claim.

## Lower priority / not pursued here

Challenges 4 and 9 (synthetic plasmid/circuit design) are mammalian/iPSC-cell-engineering specific with no natural analog in the current data landscape. Challenges 13 and 15 (PDX-style efficacy, clinical-trial-outcome prediction) don't map cleanly onto space biology, which has no equivalent trial infrastructure. Noted for completeness, not recommended as next steps.

## Sources

- [Dupire et al., "Fifteen challenges for generative AI applications to cell biology," *Cell*, Aug 17 2026](https://www.cell.com/cell/fulltext/S0092-8674(26)00802-0) (open access)
- [github.com/dr-richard-barker](https://github.com/dr-richard-barker) — repository list pulled via `gh repo list` on 2026-09-06
