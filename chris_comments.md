This is really cool! The parallels to the dosage compensation system in Anolis lizards is wild. Unlikely but could be worth checking if they are the same lncRNAs? Also, since you have Hi-C data, I think its definitely worth checking if Zmast forms specific long-range contacts with the rest of the X, if you haven’t already looked at that.

One thing that is strange to me: are you sure there is no W chromosome? Did you do a male versus female karyotype and/or FISH in the Coffing et al paper? I didn’t see any in a quick skim. It is strange because there are a couple of papers (Gao & Natsukari 1990 and Wang & Zheng 2017) that did karyotypes on quite a few individuals from various Octopus species and I would think the odd number of chromosomes would have jumped out to them. The karyotypes in the latter paper are really nice too. The main relevance to this paper would be if there were Z-linked genes that still had homologs on the W (it if exists) but that seems unlikely given your coverage results.

I am just listing comments here, as it is easier than commenting directly in the PDF. 

FIGURE 1
It would be nice to also quantify synteny conservation for each chromosome in a plot, maybe something like synteny breaks per Mb? This would make it easier to compare across chromosomes. For example, chromosome 11 also looks pretty highly conserved in the riparian plot.

TABLE 1
Has it been shown that females in all these species are ZO, rather than ZW?
I couldn’t easily find whether the same tissue was used for each species. I don’t necessarily think it matters as long as they are all somatic but would be nice to list the tissues somewhere.

FIGURE 3
Why not calculate differential methylation as female minus male so that the hypermethylation in females shows up as a positive value?
It is unclear if this figure is showing differential methylation across sequential bins along the chromosomes or some other measure.
Are you only considering CpG sites within gene bodies or across the whole chromosome? If the latter, do the results in Figure 3 still hold only when considering gene body methylation?
What fraction of methylated sites lie within versus outside of gene bodies? Is there a positive correlation between gene expression level and gene body methylation when considering autosomes and Z chromosome separately?
I think it would be interesting to look more into what is driving the differential methylation of the Z. Is it just that females show a bit more methylation at most genes or are there some genes/chromosome regions with large differences and others with small differences?
I’m not sure it is correct to call it female-specific hypermethylation: The Z seems to be more highly expressed than other chromosomes in both sexes, and in Fig S2 it shows increased methylation in both sexes (compared to autosomes) which makes sense given the correlation between expression and methylation. But I agree that the hypermethylation is more pronounced in females versus males.

TABLE 3
I am not following the logic of why (chromatin modifying) dosage compensation genes should be enriched on the Z. I would think that the major determinant of Z gene content would be sexual antagonism leading to an accumulation of male-biased genes and a loss of female-biased genes, i.e. the opposite of the demasculinization of the X seen in flies. I think this has been seen in birds and butterflies?
Could the chromatin modifying genes instead play a role in sex determination?

FIGURE 4
I am a little confused about the distinction between male-biased genes and genes that escape dosage compensation. If a male-beneficial gene happens to be on the Z, I would expect it to have higher expression in males versus females, independent of dosage compensation. Heterochromatin might also be a good place for such genes to reside, in order to ensure their suppression in females. For example, in Drosophila, ancestral Y genes that move off the Y tend to move into the heterochromatin of autosomes. I don’t see the source tissue for the expression data used in this analysis. If it was a tissue with minimal sexual antagonism, then maybe this is not an issue.

TABLES 4 &5:
I can’t tell from these tables which species the lncRNA is Z-linked versus located on a different chromosome, but maybe I am misreading them?

MOTIFS
It might be worth also looking for motifs that are enriched on the Z (or maybe Z A-compartments to focus on euchromatin) regardless of which genes they are near or how close to a gene they are. The MRE motif is highly enriched on the X in most Drosophila species (though not exclusively found there) just comparing chromosomes to chromosomes.

ZFEST/ZMAST
If I remember correctly, there is RNA-seq data from multiple tissues in Octopus? It would be interesting to see the expression of these lncRNAs across tissues and also just a genome browser-like plot to visualize the RNA-seq mapping, nearby genes, repeats, etc, for these two loci.
Is there small RNA data for any of the species that have these lncRNAs? The antisense orientation of Zfest with AMN makes me wonder if siRNAs and/or piRNAs are produced from the region of overlap, which would then silence AMN and potentially other genes if the small RNAs have targets in trans.
