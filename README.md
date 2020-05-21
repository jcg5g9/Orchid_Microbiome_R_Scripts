# Soil_Microbiome
# Aim 1 - Taxonomic Analysis
### File: ORCHIDS_TAX_CONFIDENCE.Rmd

Purpose: Here, my goal is to summarize the full community dataset by determining the total number of OTUs, the total number of rarefied sequence reads per site, the total number of rarefied reads across the entire dataset, and the total number of phyla. My first analysis determines the proportion of all OTUs that are classified taxonomically to each taxonomic level (kingdom, phylum, class, order, family, genus, species). This analysis allows us to determine the approximately confidence with which each taxonomic level can be analyzed. I also aim to determine the top 10 phyla in the dataset (the 10 phyla with the highest abundance across the whole dataset). To do this, I calculate the relative abundance of each phylum by totalling the number of reads across all sites for each phylum and dividing by the total number of reads in the whole dataset. I arrange the phyla in order from greatest to lowest relative abundance and only select the top 10 most abundant phyla.

INFO FOR FULL DATASET:

Total Number of Sites: 24
Rarefied Reads per Site: 54,631
Total Rarefied Reads in the dataset [54,631 X 24]: 1,311,144
Total OTUs: 84,960
Total Phyla: 61
    
INFO FOR TOP TEN PHYLA: 

Total Number of Sites: 24
Rarefied Reads per Site: average number 53324.5 (97.61 % of total)
Total Rarefied Reads in the dataset [sum of reads across sites]: 1,279,788 (97.61 % of total)
Total OTUs: 79,588 (93.68 % of the total)

# Aim 2 - Distribution Analysis
### File: ORCHIDS_DISTRIBUTION_ANALYSIS.Rmd

Purpose: For Aim 2, my goal is to determine the best fitting frequency distribution for the raw microbial OTU abundance data. For this analysis, I am only using OTUs represented within the top 10 most abundant phyla, which were determined and listed in the Aim 1 .rmd file. I first plot the probability density distribution of all OTUs, both as an average across all sites and then separately for each site. Based on the visual appearance of the distribution, I assess the fit of four potential distributions (negative binomial, normal, poisson, and weibull) using the bblme package in R. I then test for the best fitting distribution using AIC Model comparison methods.

# Aim 3 - Multivariate Analysis of All Data: NMDS
### File: ORCHIDS_NMDS_ALL_DATA.Rmd

Purpose: For Aim 3, my goal is to assess patterns in microbial community composition based on three predictor variables (location, distance from orchid, and presence or absence of orchids) using multivariate methods (specifically NMDS and PERMANOVA). I conduct NMDS on all OTU raw abundance data within the top 10 most abundant phyla and plot the NMDS by each of the three predictor variables to look for possible patterns in composition. I assess the optimal stress for this analysis and plot the NMDS at the optimal level of stress. I then use PERMANOVA to test for significant differences (using 9999 permutations) between groups for each of the three predictor variables

# Aim 4 - Individual Location Comparisons using all data
### File: ORCHIDS_LOCATION_COMPARISON.Rmd

Purpose: For Aim 4, I am assessing differences among the six locations in my dataset (Helton, Swale, Pawnee, Tarkio, Little Tarkio, and NE) using general linear mixed effect models with a negative binomial distribution (GLMM.NB). First, I assess differences among locations based on total OTU abundance. Then, I assess differences between locations within each of the top 10 most abundant phyla to see which phyla deviate between pouplations. I plot OTU abundance per location and per phylum in a single figure. 

# Aim 5 - Multivariate Analysis of All Data EXCEPT FOR SWALE LOCATION: NMDS
### File: ORCHIDS_NMDS_NO_SWALE.Rmd

Purpose: For Aim 5, I am re-assessing patterns of microbial community compostion among locations, distances from orchid, and presence or absence of orchids, excluding the SWALE location. SWALE was determined to be a significant outlier in OTU abundance in nearly all of the top 10 phyla, most likely due to ecological differences among SWALE and the other locations. The SWALE location was known to contain some cattle when field samples were collected; it is possible that the variation in microbial community composition in this location is partly a result. I assess community composition again using NMDS with all data in the top 10 most abundant phyla, grouping by location, distance from orchid, and presence or absence of orchids. I test for significant differences among predictor variables using PERMANOVA with 9999 permutation, using Location as a random effect or distance from orchid as a randome effect, where appropriate. 

# Aim 6 - Individual Distance from Orchid Comparisons
### File: ORCHIDS_DISTANCE_COMPARISON.Rmd

Purpose: For Aim 6, I am assessing differences in microbial composition at varying distances away from orchid plants (from 0 cm away, 100 cm away, and 200 cm away). I am assessing these distances as a continuous variable even though I do not have other distance measurements between the listed benchmarks. Because I am considering distance to be continuous, I am assessing differences in microbial composition using general linear mixed effect models (with phylum and location used separately as random effects in different general linear mixed models) and plotting using continuous linear trendlines by phylum. I first test for an overall trend in microbial composition from 0 cm to 200 cm for all OTU abundance data. I then divide the dataset into the top 10 most abundant phyla and assess trends in each phylum separately.

# Aim 7 - Individual Presence-Absence of Orchid Comparisons
### File: ORCHIDS_PRESENCE_ABSENCE_COMPARISON.Rmd

Purpose: For Aim 7, I am assessing differences in microbial composition between locations where orchids are known to be present (Tarkio, Little Tarkio, North Evans) and locations where orchids are known to be absent (Pawnee, Helton). I am using general linear mixed effect models with a negative binomial distribution and using distance from the orchids as a random effect. I first aim to determine if there is a significant differences in overall OTU abundance between present and absent locations (across all phyla). I then aim to determine if there are differences at any of the top 10 most abundant phyla. 

# Aim 8 - Presence-Absence Comparisons at the Order Level
### File: ORCHIDS_ORDER_COMPARISON.Rmd

Purpose: For Aim 8, I am again assessing differences in microbial composition between locations where orchids are known to be either present or absent, but I am analyzing the data at the Order level rather than the phylum level. I chose to assess differences no lower than the Order level given that the proportion of assigned taxonomic groups drops substantially after the order level (based on my analysis in Aim 1). Also, I chose only to assess Order-level differences for the presence-absence predictor variable, because I am most interested in characterizing differences in the bacterial microbiome associated with orchids, rather than among different locations. Since I saw nearly significant differences in microbiome composition between present-absent locations based on NMDS and general linear mixed models (and not between distances, either with NMDS or with general linear mixed models), I am only analyzing the presence-absence variable at the order level.

To assess differences at the Order level, I first obtain individual datasets for each of the top 10 phyla with raw abundance by order. For each order within each phylum, I run separate general linear models (with no random effects). I then correct for multiple comparisons using the false discovery rate method.

# Aim 9 - Alpha Diversity Analysis
### File: ORCHIDS_ALPHA_DIVERSITY.Rmd

Purpose: For Aim 9, I am assessing alpha diversity both for the entire dataset (all OTUS within all top 10 phyla) and for each of the individual top 10 phyla. More precisely, I am assessing differences in evenness using the Shannon Diversity Index. I am looking for differences in diversity between all predictor variables, including locations, distance from orchids, and presence or absence of orchids. 

# Aim 10 - Rank Abundance Analysis
### File: ORCHIDS_RANK_ABUNDANCE.Rmd

Purpose: For Aim 10, I am assessing dominance of bacterial orders within any significant phyla detected in Aim 9. I am exploring dominance using rank abundance curves derived from the R package BiodiversityR

# UNUSED CODE
### File: ORCHIDS_UNUSED.Rmd

All code in this file is miscellaneous, unused code from the Soil_Microbiome Orchids R Project