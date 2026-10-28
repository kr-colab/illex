# Response to Mia's comments

DRAFT, 2026-10-19. New analyses are **not** in `main.tex`; each point ends with a proposed action.
Tags: **[DONE]** · **[TEXT]** · **[OPEN]**. Analysis scripts and the data-source list are not in the repo; they are on the cluster at `/sietch_colab/data_share/illex/genome_paper/responses/` (`scripts/`, `missing_data.md`). Cross-species inputs are Andy's canonical outputs (`/sietch_colab/adkern/illex/`), used read-only. See also the note on manuscript numbers at the end of `response_chris.md`.

---

## 1. Is methylation a cause or a consequence of transcription? [DONE + TEXT]
> DNA methylation could cause mRNA abundance differences or instead could be the consequence of transcriptional differences (Baubec et al. 2015) ...

**Response.** Agreed that methylation alone cannot identify upstream causes, and the text overreaches ("may contribute to its transcriptional upregulation"). In cephalopods, gene-body methylation rises with expression in a graded way rather than switching genes on or off. In *O. bimaculoides*, Macchi et al. (2022, [doi:10.1186/s12915-022-01404-1](https://doi.org/10.1186/s12915-022-01404-1)) find a direct correlation at mid-range expression. They also note that exceptions "argue against DNA methylation as a player in the dynamic regulation of gene expression", and that it may sustain constitutive expression or be "only a passenger of gene transcription". Our *Illex* data show the same graded pattern (mean methylation by expression ventile rises from ~25–35 to ~52, then dips at the very top).

**But the Z excess is not simply a readout of transcription.** If female Z hypermethylation were a passenger of upregulation, it should follow expression gene by gene. It does not:
- Per-gene female − male methylation on the Z does **not** track the female/male expression ratio (Spearman ρ = 0.05, p = 0.57, n = 160).
- Z genes that are **not expressed** are still heavily methylated (female median 60 vs 4 for unexpressed autosomal genes).
- **Intergenic** CpGs on the Z show the same female excess (21.0 vs 14.9; autosomes ~8 in both sexes).
- The shift is broad: 79% of Z genes are more methylated in females vs 43% on autosomes, along the whole chromosome.
- It is not a coverage artifact (female Z is half depth): at matched 20–29× coverage, female Z gene bodies are 62 vs male 53.

So the pattern is a **chromosome-wide female-biased state**, not a gene-by-gene consequence of expression. That is more interesting, but it still says nothing about causation.

**Chromatin accessibility in the same direction (Andy's data).** *O. bimaculoides* brain 10x Multiome ATAC (8F:2M; `adkern/illex/obimaculoides/ATAC_seq/results/atac_dosage_compensation_results.md`):
- At the whole-chromosome level, female Z accessibility is exactly at the copy-number expectation (Z:A = 0.50), i.e., there is no bulk opening of the single Z.
- Promoters and gene bodies show a small but significant ~5–6% excess above copy number (bootstrap CI excludes 1).
- As with methylation, per-gene ATAC F/M does not track expression sex-bias (ρ = 0.03).
- Caveat: both males are from one brain region and timepoint, so sex is partly confounded with sampling.

**Proposed action:** reframe the methylation section as "a female-biased, chromosome-wide epigenetic state on the Z" and present it as independent evidence that the female Z is in a distinct chromatin state. Remove the causal language, cite Macchi et al. 2022 and Baubec et al. 2015, and drop the "longest-maintained epigenetic sex-chromosome signature" sentence (one species only). Consider adding the ATAC result as a supplementary panel.

---

## 2. Why should chromatin modifiers be Z-linked? Need genome-wide comparisons [DONE + TEXT]
> It is not obvious to me that Z chromatin modifiers should be Z-linked ... comparison to autosomes ... in flies, only MOF is X-linked ... genome-wide, is there something (statistically) special about the Z-linked ones?

**Response on precedent.** Agreed: in *Drosophila* only *mof* is X-linked, and *Xist*'s partners are autosomal. No known mechanism requires Z-linkage of the machinery, and we should not imply it.

**Genome-wide controls** (Andy's classifier: `results/chromatin_genes_ille.csv`, 156 chromatin genes across the *Illex* genome):
- **The Z is the most chromatin-gene-dense chromosome in the genome**: 3.9 per 100 genes vs an autosomal median of 0.68 and maximum of 1.94 (rank 1/46; Fisher OR = 5.9, p = 7×10⁻⁶).
- **The conservation effect is Z-specific.** On autosomes, genes whose linkage is conserved across six species are *not* enriched for chromatin genes (OR = 0.85, p = 0.47); on the Z the same comparison trends positive (OR = 3.3, small n). Chromatin genes are not generally more conserved in linkage, so the Z result is not a generic property of chromatin genes.
- **Isoform switching is *not* special on the Z.** Using Andy's canonical *O. bimaculoides* DESeq2 (transcript level), bidirectional sex-biased isoform switching occurs in 0.73% of multi-isoform Z genes vs 0.88% on autosomes (Fisher p = 1). Chromatin genes switch somewhat more often than other genes (2.6% vs 0.8%, OR = 3.2, p = 0.08), but **none of the switching chromatin genes is Z-linked** in the current results (0/12 on Z; *PBRM1*, *SMARCC2*, *KDM3A* are autosomal). The manuscript's four switching genes (incl. *Domino*) use padj < 0.05 with no fold-change filter; with |lfc| > 1 there are three. The text should state the threshold.

**Proposed action.** Separate two claims the manuscript currently merges: (a) the Z is unusually enriched for chromatin genes (robust and Z-specific: keep, with the genome-wide comparison); (b) sex-biased isoform switching of chromatin regulators tracks compensation (involves autosomal genes, so not a Z-linked mechanism; frame accordingly). Present dosage sensitivity and sex determination as candidate explanations for (a) (see Chris's Table 3 point), not "retained to maintain cis-regulatory control".

---

## 3. Is "escape" in LINE-rich regions a dynamic-range artifact? [DONE]
> asserting that the generally low expression near LINE-enriched regions doesn't simply mean a lower dynamic range

**Analysis** (Andy's canonical `obimaculoides/results/z_gene_line_motif_data.tsv`, 298 Z genes):
- Expression level is **unrelated** to flanking LINE density (Spearman ρ = −0.025, p = 0.67). Median baseMean is flat across LINE quartiles (235, 233, 260, 229). Male- and female-biased genes have similar expression (115 vs 128, p = 0.53).
- Adding log expression as a covariate leaves the RTE-BovB × Motif B interaction intact (p = 0.007 → 0.004), and the BovB main effect (p = 0.004 → 0.002) and Motif B effect (p = 0.043 → 0.013) get stronger.
- So the LINE-associated pattern is **not** explained by lower expression or dynamic range.

**Two caveats we should state.**
- The simple male- vs female-biased LINE comparison depends on the LINE window: including the gene body gives p = 0.01; flanks only gives p = 0.14–0.27 (highest-baseMean transcript per gene, 24M:6F). The interaction model is the robust result.
- All significantly male-biased Z genes have log₂FC > 1 (median 2.2), i.e., more than the 2× expected from simple failure to compensate. They are actively male-upregulated, so calling them "escapees" is not accurate (see Chris, Fig. 4).

**Proposed action:** add the expression-matched control (one sentence + supplementary table), use one LINE window throughout (stated in Methods, figure regenerated from the script), and rename the category "male-biased" rather than "escape".

---

## 4. Motivate the CTCF analysis [TEXT]
**Response.** On the mammalian X, CTCF marks boundaries between inactivated and escape domains (Filippova et al. 2005; Horakova et al. 2012). In *Drosophila*, insulator proteins (CLAMP, CP190/BEAF) shape MSL spreading. Our own supplementary test is negative: CTCF density is not elevated at compensated/biased boundaries (p = 0.128), and the adjacent-gene effect disappears after controlling for distance.
**Proposed action:** add one sentence of motivation, move CTCF to the Supplement as a negative result, and remove it from the Discussion model ("CTCF insulators ... may sharpen these domain boundaries").

---

## 5. Why should a pioneer factor sit in the B compartment? [TEXT]
**Response.** Agreed: there is no a priori reason. A pioneer factor *binds* closed chromatin, but that does not predict where its own *gene* sits. The sentence conflates protein function with gene location.
**Proposed action:** report the *FoxA2* B-compartment location as an observation without functional interpretation, or drop it (single gene).

---

## 6. Reframe the LINE section: the inverse pattern is predicted [TEXT]
**Response.** Agreed; this is cleaner. If compensation means upregulating a single Z, TE-associated heterochromatin should *oppose* it. Lyon's model predicts the opposite only because X-inactivation is a silencing process.
**Proposed action:** rewrite the LINE paragraph and the Discussion heading ("Lyon's repeat hypothesis, inverted") to state the prediction first, then the observation. Given point 3, frame the observation around the BovB × Motif B interaction and male-biased genes.

---

## 7. The KDM3A model is speculative [DONE + TEXT]
**Analysis** (Andy's `obimaculoides/results/za_matched_per_sample.tsv`, 30 somatic samples, 15F:15M):

| model | KDM3A p |
|---|---|
| Z:A ~ 4 isoform proportions (manuscript) | 0.008 |
| + sex | 0.009 (R² 0.57 → 0.64) |
| Z:A ~ KDM3A + sex | 0.0001 |
| within females (n=15) / males (n=15), Spearman | ρ = 0.69, p = 0.004 / ρ = 0.75, p = 0.001 |
| + sex + tissue | **0.054** |
| neural samples only (12F:5M) | ρ = 0.35, **p = 0.16** |

The association is not driven by sex alone; it holds within each sex. But it is **largely confounded with tissue**: females are mostly neural (12/15), males span 10 tissues, and within neural tissue the association is not significant. KDM3A isoform proportion may be tracking tissue composition, which also shifts Z:A.

**Proposed action:** agree with Mia. Remove the Discussion "simple model" ("KDM3A's female isoform sets the demethylation rate; flanking LINE density sets the H3K9me deposition rate"). Keep KDM3A as one candidate in a sentence, report the within-sex and tissue-adjusted results, and name H3K9me2/3 CUT&Tag in female vs male tissue as the needed test.
