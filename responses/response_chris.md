# Response to Chris's comments

DRAFT, 2026-10-19. New analyses are **not** in `main.tex`; each point ends with a proposed action for us to decide on.
Tags: **[DONE]** analysis run · **[TEXT]** wording only · **[OPEN]** needs a decision or data we don't have.
Analysis scripts and the data-source list are not in the repo; they are on the cluster at `/sietch_colab/data_share/illex/genome_paper/responses/` (`scripts/`, `missing_data.md`). Most cross-species inputs are Andy's canonical outputs in `/sietch_colab/adkern/illex/`, which we used read-only.

> **Note for authors before revising.** Several manuscript numbers do not match Andy's *current* canonical result files. Before anything goes into the text we should decide which version is authoritative (see the end of this document).

---

## General

### Same lncRNAs as *Anolis*? [TEXT]
**Response.** Unlikely at the sequence level: even within cephalopods, *Zmast* retains only ~99 bp (1.4%) of specifically conserved sequence. A BLASTn/nhmmer search of the *Anolis* dosage-compensation lncRNA against our eight *Zmast*/*Zfest* sequences would settle it formally.
**Proposed action:** run the search; add one Discussion sentence on the convergence (male-upregulated Z/X with a sex-biased lncRNA) and the absence of homology.

### Does *Zmast* make specific long-range contacts with the Z? [DONE]
**Analysis.** Virtual-4C from the female *Illex* Hi-C (`annotations/promoters/hic/illex.promoters.mcool`, 50 kb, ICE-balanced). Viewpoints: *Zmast* (LOC_00003730, Z:10.14–10.16 Mb) and *Zfest* (XLOC_014991U, Z:21.52–21.54 Mb). Each is compared against all 765 Z bins (`responses/figs/zmast_zfest_virtual4C.png`, `responses/zmast_zfest_hic_summary.tsv`).

| viewpoint | long-range (>1 Mb) obs/exp | pctile | top-1% partner bins | pctile | cis (Z) fraction | pctile |
|---|---|---|---|---|---|---|
| *Zmast* | 1.16 | 79th | 7.5 | 58th | 0.78 | 74th |
| *Zfest* | 0.84 | 24th | 2.0 | 4th | 0.76 | 43rd |
| all Z bins (5–95%) | 0.70–1.32 | | 2–17 | | 0.72–0.81 | |

**Result: no evidence for specific long-range contacts.** Both loci look like ordinary Z bins. The *Zmast* profile tracks the Z's strong A/B compartment checkerboard rather than focal hubs.

**Caveats.** (1) The only *Illex* Hi-C library is female, where *Zmast* is nearly silent (15 vs 5,731 reads). (2) Hi-C measures where the *locus* sits, not where the *RNA* goes; RNA coating would need RAP/CHART/RADICL-seq.
**Male vs female Hi-C:** no public cephalopod Hi-C has both sexes labelled in its metadata. We sex-typed the three public *Sepia officinalis* Hi-C libraries by read depth on the Z (OZ199189.1) relative to the other 48 chromosomes, mapping 2–10 M reads to xcSepOffi3.1 (MAPQ ≥ 30):

| library | ENA sex | Z / autosome depth | Z rank among 49 chromosomes | inferred sex |
|---|---|---|---|---|
| ERR13731898 (Aquatic Symbiosis Genomics) | male | 0.45 | lowest (z = −8.4; autosomes 0.83–1.09) | **female** (ZO) |
| SRR32732124 (MPI Brain Research, somatic tissue) | not recorded | 0.85 | 6th lowest (z = −1.6; autosomes 0.79–1.1) | **male** (ZZ) |
| ERR16728563 (Darwin Tree of Life, tentacle) | not collected | – | – | unusable: ~1% of reads map to *S. officinalis* |

So the library labelled "male" in ENA is in fact female. That female library is also of low Hi-C quality: ~93% of same-chromosome pairs are unligated fragments < 1 kb apart, so only ~9% of pairs are informative (vs ~43% in the male library). At equal depth it would give ~10× fewer Z contacts, so we did not analyse it.

**Male *Sepia* (SRR32732124; *Zmast* expressed).** We repeated the virtual 4C on 60 M read pairs of the male library: each mate mapped to xcSepOffi3.1, MAPQ ≥ 30, deduplicated; 353,715 Z-involving pairs, 43,054 long-range Z–Z contacts; Z matrix ICE-balanced within the Z, 50 kb. Viewpoints: *Zmast* OZ199189.1:5.759–5.765 Mb, *Zfest* 54.476–54.498 Mb (`responses/sepia_zmast_zfest_hic_summary.tsv`, `responses/figs/sepia_zmast_zfest_virtual4C.png`).

| viewpoint (male *Sepia*) | long-range obs/exp | pctile | top-1% partner bins | pctile | cis (Z) fraction | pctile |
|---|---|---|---|---|---|---|
| *Zmast* | 1.04 | 61st | 6 | 12th | 0.46 | 54th |
| *Zfest* | 1.15 | 86th | 5 | 8th | 0.57 | 99th |
| all Z bins (5–95%) | 0.76–1.23 | | 4–27 | | 0.38–0.54 | |

**Result: in the sex that expresses it, the *Zmast* locus also shows no specific long-range contacts with the Z.** It is an ordinary Z bin on every metric, as in female *Illex*. *Zfest* has an unusually high cis fraction in male *Sepia* (99th percentile), but it is silent in males and was unremarkable in *Illex* (43rd percentile), so we don't read anything into it.
**Proposed action:** report as a negative result across two species and both sexes (one sentence + supplementary panel), keeping the caveat that Hi-C reports where the locus sits, not where the RNA goes.

### Is there really no W? [DONE + OPEN]
**Response.** We did not karyotype or FISH; the ZO inference rests on read depth. Evidence against a W:
- **Depth along the *Illex* Z** (HiFi, 50 kb windows): wherever depth is single-copy, the Z is hemizygous in the female along its whole length (normalized F/M = 0.51; 75% of Z windows < 0.6 vs 1.6% of autosomal windows). The only near-diploid stretches (0–2.7 Mb and the last ~250 kb) are at 2–9× autosomal depth in *both* sexes, i.e., collapsed repeats and the chromosome end, not a pseudo-autosomal region. So there is no W-shared (gametologous) region on the assembled Z.
- **Female-specific sequence** (`scripts/Illex_pseudoAutosomal.ipynb`): of 3,755 unplaced scaffolds (674 Mb), **none** show a female-only coverage pattern (female > 0.1×, male < 0.1×, F > 5× M). This is not currently reported in the paper.
- [OPEN] The DIAMOND search with *Nautilus* sex-linked genes described in Methods: no output located. Was it run? If not, remove it from Methods or run it.
- Karyotypes: a ZO female has 2n − 1 (91 in *Illex*, 59 in octopus). With many small, similar chromosomes, one missing chromosome is easy to overlook unless male and female spreads are compared explicitly. We can check whether Gao & Natsukari (1990) and Wang & Zheng (2017) report counts by sex.

**Proposed action:** add the unplaced-scaffold result to the Supplement (one sentence + table), fix the Methods for the *Nautilus* search, and add a sentence on the karyotype literature.

---

## Figure 1: quantify synteny per chromosome [DONE: changes a claim]
**Analysis.** For each *Illex* chromosome, the fraction of its ODP reciprocal-best-hit orthologs that lie on a single partner chromosome in each species, plus a reciprocal 1:1 score for octopus (`responses/synteny_partner_fidelity.tsv`, `responses/synteny_one_to_one_octopus.tsv`, `responses/figs/synteny_partner_fidelity.png`).

**Result: Chris is right.**
- Against octopus (mean of *O. bimaculoides* and *O. sinensis*), the Z keeps 91% of orthologs on one chromosome but **ranks 11th of 46**. chr11 (0.98), 36, 42, 3, 43, 31, 22, 32, 10 and 41 are as high or higher.
- Requiring a reciprocal 1:1 relationship: **chr11 ↔ Ob chr20 (0.97)** and **chr3 ↔ Ob chr12 (0.92)** are more conserved than **Z ↔ Ob Z (0.73)**. About a quarter of the octopus Z orthologs come from scattered *Illex* autosomes.
- GENESPACE collinear blocks are too sparse between squid and octopus (~5 hits per 100 genes) for breakpoints-per-Mb, so we used ortholog fidelity instead.

**Proposed action:** revise "synteny breaks down on every chromosome except the Z" to: the Z is one of a few chromosomes (with chr3 and chr11) retained as an intact unit since the decapod–octopod split. Add the bar plot to Fig. 1 or the Supplement.

---

## Table 1

### Are females ZO rather than ZW in all species? [TEXT + OPEN]
**Response.** Female hemizygosity has coverage-based support in *Illex* (this study), in the species in Coffing et al. (2025), and in *O. bimaculoides* ATAC (female Z:A accessibility = 0.50; Andy's Multiome analysis). In the remaining species the Z is inferred by synteny. Expression data also support sex identity in every species, via the conserved *Zmast*/*Zfest* markers.
**Proposed action:** add an "Evidence for ZO" column to Table 1 (coverage / ATAC / synteny only).

### Tissues [TEXT]
**Response.** Tissues per library are listed in the supplementary sample table (`tab:dc_samples`), but Table 1 doesn't point to it. They differ by species: *Illex* mantle; *E. scolopes* and *S. officinalis* neural; *O. bimaculoides* neural plus arm, eye, salivary gland, skin and oviduct.
**Proposed action:** add "Tissues per library are listed in Table S#" to the Table 1 caption and a short tissue column.

---

## Figure 3: methylation [DONE]
All numbers below are from the per-CpG HiFi calls (`scripts/data_output/Illex_methylation.covfilt.feat.tsv`), re-summarized by gene body vs intergenic (`responses/scripts/meth_by_feature.awk`).

### Plot female − male? [TEXT]
Agreed. **Proposed action:** flip to Female − Male so that female hypermethylation is positive, and drop the paragraph defending M − F.

### What does the figure show? Gene bodies or whole chromosome?
Per Methods, each box is the distribution across **genes** of the per-gene male − female mean CpG methylation over **gene bodies**; the boxes are not sequential bins. The legend should say this. The result also holds outside genes:

| mean CpG methylation (0–100) | autosomes F | autosomes M | Z F | Z M |
|---|---|---|---|---|
| gene bodies | 35.0 | 34.9 | **59.2** | **51.5** |
| intergenic | 8.2 | 8.7 | **21.0** | **14.9** |

The female excess on Z is present in gene bodies (+7.7) and intergenic DNA (+6.1); autosomes are equal between sexes in both.

### Fraction of methylated sites in gene bodies; expression–methylation correlation by Z vs autosomes
- About 19% of autosomal CpGs lie in gene bodies but they carry **~61% of methylated CpGs** (mod score ≥ 50) in both sexes, the typical invertebrate gene-body pattern (Macchi et al. 2022, *O. bimaculoides*, [doi:10.1186/s12915-022-01404-1](https://doi.org/10.1186/s12915-022-01404-1)).
- Methylation rises with expression in a graded way, as in *O. bimaculoides*. Mean gene-body methylation by expression ventile on female autosomes rises from ~25–35 at low expression to ~52 in the upper-middle range, then dips for the most highly expressed genes. On the Z, by expression quintile: females 55 → 67, males 44 → 65. Gene by gene the relationship is weak: across all genes Pearson r ≈ 0.19 in both sexes, and within the mid-expression range Spearman ρ = 0.10 in females and 0.02 in males. It is a trend across genes rather than a tight per-gene predictor.
- **Correction needed:** the manuscript's "genome-wide r = 0.396 (females), 0.318 (males)" comes from a ~200-gene table in `combine_exp_meth.ipynb`, not the genome. Across ~16,000 genes, Pearson r(log TPM, methylation) ≈ 0.19 in both sexes.

### What drives the Z difference: a broad shift or a few genes?
A **broad shift**. 79% of Z genes are more methylated in females (vs 43% of autosomal genes); the per-gene F − M median is +4.0 on Z (IQR 0.6–8.1) vs −0.3 on autosomes; Wilcoxon signed-rank on Z genes p = 1×10⁻¹⁶. The shift is present in every 5 Mb segment of the Z (median +1.7 to +5.9), and 28 of 203 Z genes exceed 2 SD of the autosomal F − M distribution.

**Not a coverage artifact.** Female Z sites have half the read depth, so we compared at matched coverage. At 20–29× depth, female Z gene bodies are 62.2 vs male Z 52.7 (female autosomes 24.9); intergenic 30.3 vs 12.6. Female Z methylation is ~60 at every depth bin.

### "Female-specific" hypermethylation [TEXT]
Agreed. The Z is more methylated than autosomes in **both** sexes (gene-body medians 0.31 vs 0.18 in males, 0.41 vs 0.19 in females); the excess is larger in females.
**Proposed action:** retitle to "Z hypermethylation, more pronounced in females"; fix the figure legend and section header.

---

## Table 3: why chromatin modifiers on the Z? Sexual antagonism? [DONE + TEXT]
**Masculinization test.** In *O. bimaculoides*, 35 of 63 sex-biased Z genes are male-biased (55.6%), vs 1,419/2,407 (59.0%) for the rest of the genome (Fisher OR = 0.87, p = 0.61). **The Z is not masculinized**, contrary to the simplest sexual-antagonism prediction for a Z (Rice 1984). This is worth reporting.

**Is the chromatin enrichment real and Z-specific?** Using Andy's genome-wide chromatin-gene classification for *Illex* (156 genes; `adkern/illex/results/chromatin_genes_ille.csv`):
- The Z has the **highest chromatin-gene density of all 46 chromosomes**: 3.9 per 100 genes vs an autosomal median of 0.68 and maximum of 1.94 (Fisher Z vs autosomes OR = 5.9, p = 7×10⁻⁶).
- On autosomes, genes whose linkage is conserved across six species are *not* enriched for chromatin genes (OR = 0.85, p = 0.47; `responses/chromatin_linkage_conservation_by_gene.tsv`). So "chromatin genes are generally conserved in linkage" does not explain the Z result.

**Logic.** Agreed the motivation is under-argued. Proposed framing: an observation with two non-exclusive explanations: (i) dosage-sensitive regulators are retained on the compensated chromosome because moving off it would perturb their dosage, or (ii) roles in sex determination or sexual development, as Chris suggests (cf. *DMRT1* on the bird Z). We cannot distinguish these.

---

## Figure 4: male-biased genes vs escapees [DONE: supports Chris]
**Analysis** (Andy's canonical table `obimaculoides/results/z_gene_line_motif_data.tsv`, 298 expressed Z genes, 30 somatic samples of mixed tissue).
- **Every** significantly male-biased Z gene (n = 24) has log₂FC > 1: median 2.18, IQR 1.64–3.89, max 9.75; 79% exceed 1.5. Failure to compensate can give at most a 2× male excess (log₂FC = 1). **These genes are actively upregulated in males**, not merely escaping compensation. Chris's alternative is supported.
- In the current canonical table, LINE density does not differ significantly between male- and female-biased Z genes (198 vs 139 bp/kb, MWU p = 0.14; 24M:6F). The manuscript's 174.2 vs 122.0, p = 0.029 (29M:18F) comes from an earlier gene set; see the note at the end.
- The RTE-BovB × Motif B interaction is robust (p = 0.007; 0.004 with an expression covariate).
- Heterochromatin as a refuge for male-beneficial genes (cf. ex-Y genes in *Drosophila*) is a good alternative reading of the LINE-dense, male-biased pattern.

**Proposed action:** reframe Fig. 4 as "male-biased Z genes", not "escapees"; state that the effect sizes exceed dosage expectations; discuss the sexual-antagonism/heterochromatin-refuge alternative; update the LINE statistics to the canonical version (or explain the difference). Tissue: *O. bimaculoides*, 30 somatic samples of mixed tissue (Table S#), stated in the legend.

---

## Tables 4 & 5: which species have Z-linked lncRNAs? [TEXT]
Both lncRNAs are Z-linked in all eight species, except *Zmast* in *E. scolopes*, which sits on a translocated Z fragment (LG10; footnote a of Table 4). The "Z chromosome" column lists accession names, which made this hard to read.
**Proposed action:** replace it with "Linkage" (Z / autosome) and give the accession in parentheses.

---

## Motifs: Z-wide enrichment regardless of gene proximity [DONE]
Andy's AME Z-vs-autosome run had produced empty output, so we scanned Motifs A (STREME-15) and B (STREME-20) across all 30 *O. bimaculoides* chromosomes (FIMO, both strands; `responses/motifAB_genome_density_obimac.tsv`). Density per Mb on Z was compared with autosomes, adjusting for chromosome GC content (Z GC 36.4% vs autosomal median 35.8%):

| motif | FIMO p < | Z sites/Mb | autosome median | fold | Z rank | GC-adjusted z |
|---|---|---|---|---|---|---|
| A | 10⁻⁶ | 3.17 | 2.67 | 1.19 | **1/30** | 2.26 |
| B | 10⁻⁶ | 21.86 | 20.29 | 1.08 | **2/30** | 2.61 |
| A | 10⁻⁵ | 23.25 | 22.73 | 1.02 | 13/30 | 1.27 |
| B | 10⁻⁵ | 181.8 | 173.8 | 1.05 | 6/30 | 1.62 |

**Result.** At the stringent threshold used to call motif presence in the paper (p < 10⁻⁶), both motifs are densest (A) or second densest (B) on the Z, but the enrichment is small (1.1–1.2-fold; GC-adjusted z ≈ 2.3–2.6) and fades at the looser threshold. This is weaker than the ~2-fold X enrichment of MREs in *Drosophila*.

**Caveat:** the motifs were *discovered* among Z genes, so some Z enrichment is expected from ascertainment alone. A clean test would rediscover motifs on held-out data, or scan motifs found without reference to the Z.
**Proposed action:** report as "modestly enriched on the Z (1.1–1.2-fold)", which fits the analogy to MREs (present genome-wide, slightly X-enriched); restrict to A-compartment bins if we want Chris's euchromatin version.

---

## *Zfest*/*Zmast* across tissues; browser view; small RNAs [DONE + TEXT]
**Tissue expression, *O. bimaculoides*** (TPM, medians; `responses/zmast_zfest_tissue_tpm_obimac.tsv`):

| tissue | *Zmast* ♂ | *Zfest* ♀ |
|---|---|---|
| neural | 652 (n=5) | 268 (n=12) |
| skin | 1,014 | 251 |
| arm / suckers / sucker rim | 139 / 487 / 478 | – |
| eye, lip, olfactory organ, hectocotylus | 540, 203, 762, 460 | – |
| posterior salivary gland | 70 | – |
| oviduct / ovary | – | 98 / 48 |
| **testis / ova (germline)** | **15** | **2.1** |

Both lncRNAs are expressed in every somatic tissue of the expressing sex (the other sex is ~0), and both are **low in the germline**. This fits a somatic, chromosome-wide role. Single-cell data for *O. vulgaris* (GSE193622, in Andy's tree) can resolve cell types.
**Browser view:** feasible for *Illex* (F/M RNA-seq coverage, Iso-Seq, gene models, repeats, Hi-C); proposed as a supplementary figure.
**Small RNAs:** no small-RNA data on disk for any of these species. Public octopus small-RNA datasets could be checked for reads antisense to the *Zfest*/*AMN* overlap; otherwise we list this as future work.

---

## Note for authors: manuscript numbers that differ from Andy's current outputs
| Manuscript | Current canonical output | Where |
|---|---|---|
| LINE density M vs F-biased Z genes 174.2 vs 122.0, p = 0.029 (29M:18F) | 198 vs 139, p = 0.14 (24M:6F) | `obimaculoides/results/z_gene_line_motif_data.tsv` |
| 47 sex-biased Z genes (18 F) in the motif analysis | 30 at padj < 0.05, \|lfc\| > 1 (6 F) | same |
| Four genes with bidirectional isoform switching incl. Z-linked *Domino* | 3 chromatin genes switch, none Z-linked | `obimaculoides/results/deseq2_sex_effect.csv` |
| "Genome-wide" methylation–expression r = 0.396 | ~200-gene table; genome-wide r ≈ 0.19 | `scripts/combine_exp_meth.ipynb` |
| "Synteny breaks down on every chromosome except the Z" | Z ranks 11/46; chr3, chr11 more conserved | this response |

Andy should confirm which DESeq2 version is canonical before any numbers are changed.
