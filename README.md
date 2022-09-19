# Dataset for multi-epoch GLM
#### CURRENT epochs definitions: <br />
**Epoch-1**:	[estimated date of importation (MCC), 2021-12-25]<br />
**Epoch-2**:	[2021-12-26, 2022-01-15]<br />
**Epoch-3**:	[2022-01-16, 2022-01-31]

#### Transmission-lineages (from largest to smallest)
1. BA.1.17_DTA_175_n11351
2. BA.1_DTA_1207_n9727
3. BA.1.15_DTA_102_n2975
4. BA.1.1_DTA_1254_n2249
5. BA.1_DTA_1944_n1406
6. BA.1_DTA_1800_n944
7. BA.1.1_DTA_1467_n722
8. BA.1.15_DTA_700_n713

## Directory Layout
```
	.
	├── BA.1_DTA_1207_n9727
	├── BA.1_DTA_1800_n944
	├── BA.1.1_DTA_1254_n2249
	├── BA.1.1_DTA_1467_n722
	├── BA.1.15_DTA_102_n2975
	├── BA.1.15_DTA_700_n713
	├── BA.1.17_DTA_175_n11351
	├── BA.1_DTA_1944_n1406
	   ├── betweenness_centralities
	   │   ├── ltla_betweenCentral_epo_1.tsv
	   │   ├── ltla_betweenCentral_epo_2.tsv
	   │   └── ltla_betweenCentral_epo_3.tsv
	   ├── case_seq_residuals
	   │   ├── ltla_residual_epo_1.tsv
	   │   ├── ltla_residual_epo_2.tsv
	   │   └── ltla_residual_epo_3.tsv
	   ├── community_overlap_lvl_1
	   │   ├── multiLevel_lvl_1_infomap_overlap_NA_epo_1.csv
	   │   ├── multiLevel_lvl_1_infomap_overlap_NA_epo_2.csv
	   │   └── multiLevel_lvl_1_infomap_overlap_NA_epo_3.csv
	   ├── community_overlap_lvl_2
	   │   ├── multiLevel_lvl_2_infomap_overlap_NA_epo_1.csv
	   │   ├── multiLevel_lvl_2_infomap_overlap_NA_epo_2.csv
	   │   └── multiLevel_lvl_2_infomap_overlap_NA_epo_3.csv
	   ├── eigenvector_centralities
	   │   ├── ltla_eigenCentral_epo_1.tsv
	   │   ├── ltla_eigenCentral_epo_2.tsv
	   │   └── ltla_eigenCentral_epo_3.tsv
	   ├── grtCircle_distance.csv
	   ├── ltla_lat_long.tsv
	   ├── ltla_peak_times.tsv
	   ├── ltla_pop.tsv
	   ├── ltla_region.tsv
	   ├── mobility_matrices
	   │   ├── mobility_matrix_epo_1.csv
	   │   ├── mobility_matrix_epo_2.csv
	   │   └── mobility_matrix_epo_3.csv
	   └── tip_ltla_date_epo.tsv
```

- **tip_ltla_date_epo.tsv**<br />
A table containing tip-specific information, i.e. LTLA from which the genome was sampled (after aggregation), collection date and corresponding epoch.

- **ltla_region.tsv**<br />
A table for mapping each LTLA to its corresponding region.
```
ltla	NE	NW	YH	EM	WM	SW	E	SE	L
E06000018	0	0	0	1	0	0	0	0	0
E09000023	0	0	0	0	0	0	0	0	1
E09000022	0	0	0	0	0	0	0	0	1
...
```

- **ltla_pop.tsv**<br />
A table containing population size (from 2020 mid-year estimate by ONS) of each LTLA (after aggregation).

- **ltla_peak_times.tsv**<br />
A table containing timing of peak (with 2021-12-01 as arbitrary reference point) in the epidemic curve (estimated daily number of Omicron BA.1 cases) of each LTLA (after aggregation).

- **ltla_lat_long.tsv**<br />
A table containing the LAT/LONG coordinate of the centroid of each LTLA (after aggregation).

- **grtCircle_distance.tsv**<br />
A distance matrix where each element corresponds to the great circle distance (in km) between two LTLAs calculated using the Haversine formula (after LTLA aggregation).

- **mobility_matrix_epo_n.csv**<br />
A symmetric matrix where each element corresponds to the estimated weekly number of trips taken between the origin and destination LTLA, averaged over the corresponding epoch. Diagonal elements are taken to be 0. Off-diagonal elements that are zero are given a pseudo count of 0.001. Elements corresponding to trips involving at least one LTLA with no available mobility data are encoded as NA’s.

- **ltla_eigenCentral_epo_n.tsv**<br />
A table containing the eigenvector centrality measure of each LTLA calculated from an undirected mobility network averaged over the corresponding epoch.

- **ltla_betweenCentral_epo_n.tsv**<br />
A table containing the betweenness centrality measure of each LTLA calculated from an undirected mobility network averaged over the corresponding epoch. A pseudo count of 1e-6 is used for LTLAs with zero betweenness centrality.

- **multiLevel_lvl_1_infomap_overlap_NA_epo_n.csv**<br />
A symmetric matrix where each element is either “1” or “0” indicating whether the origin and destination LTLAs belong to the same community, as identified using the Infomap algorithm (a community detection algorithm by which each LTLA is assigned a community according to the multi-level solutions at level-1 clustering) applied to an undirected mobility network averaged over the corresponding epoch. Elements corresponding to LTLA pairs where at least one of which has no available mobility data are encoded as NA’s. 

- **multiLevel_lvl_2_infomap_overlap_NA_epo_n.csv**<br />
A symmetric matrix where each element is either “1” or “0” indicating whether the origin and destination LTLAs belong to the same community, as identified using the Infomap algorithm (a community detection algorithm by which each LTLA is assigned a community according to the multi-level solutions at level-2 clustering) applied to an undirected mobility network averaged over the corresponding epoch. Elements corresponding to LTLA pairs where at least one of which has no available mobility data are encoded as NA’s. 

- **ltla_residual_epo_n.tsv**<br />
A table containing the residuals from a simple linear regression between the number of genome samples (TL-specific) from each LTLA and the estimated cumulative number of Omicron BA.1 cases in that LTLA during the corresponding epoch. A positive constant is added to each residual to allow log-transformation.

