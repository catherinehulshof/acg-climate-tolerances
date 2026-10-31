# ACG climate niches × leaf tolerances

Data and (later) code for a study of tree species in the Área de Conservación
Guanacaste (ACG), Costa Rica. The study tests whether leaf heat tolerance
(Tcrit, T50, T95) and turgor loss point track the limits of species' realized
climatic niches, and how exposed each species is to future climate.

> Hulshof, C. M., Hardley, S., López Bustamante, P., Ortiz-Colín, P., Terry, C. N.,
> & Guadamúz, A. *Leaf thermal and hydraulic tolerances track the climatic limits
> of tropical tree niches, but range size sets local exposure.* In preparation for
> *Functional Ecology*.

This repository currently holds only the GBIF records used in the analysis. It
is the public source of the GBIF derived dataset that cites them. The full
analysis code and the plot microclimate data will be archived with the paper:
the microclimate data at the Environmental Data Initiative (EDI), the code with
a DOI.

## `data/gbif_derived_dataset/`

The Botanical Information and Ecology Network (BIEN) withholds coordinates for
six of the study species. For these species, occurrence records came directly
from GBIF.

**Species:** *Eugenia monticola*, *E. siggersii*, *E. truncata*, *E. valerii*
(including records under *E. costaricensis*), *Pouteria reticulata* and *Vitex
cooperi*.

**Retrieval:** with `rgbif::occ_search` on 30 October 2026, using these filters:
- `basisOfRecord = PRESERVED_SPECIMEN`;
- with coordinates;
- no geospatial issues;
- `occurrenceStatus = PRESENT`.

**Cleaning:** with CoordinateCleaner. Records were removed if they were:
- invalid, zero or equal coordinates;
- at sea;
- at country capitals or centroids;
- at biodiversity institutions;
- duplicates;
- outside the tropical and subtropical Americas (125°W–30°W, 56°S–40°N);
- reported with coordinate uncertainty above 5 km.

The remaining records were thinned to one per species per 2.5′ cell.

**Use:** the retained records were combined with CHELSA V2.1 climate to
estimate each species' realized climatic niche.

| File | Contents |
|---|---|
| `gbif_records_used.csv` | The 1,221 records used (228 / 59 / 30 / 119 / 688 / 97 per species, in the order above) |
| `gbif_derived_dataset_counts.csv` | Records used per GBIF source dataset (110 datasets): `datasetKey,count`, no header. This is the upload file for GBIF derived-dataset registration |

**Columns of `gbif_records_used.csv`:**

| Column | Description |
|---|---|
| `gbif_key` | GBIF occurrence key (gbif.org/occurrence/<key>) |
| `gbif_dataset_key` | GBIF source dataset key (gbif.org/dataset/<key>) |
| `species` | Species as measured in the study |
| `longitude`, `latitude` | Decimal degrees, WGS84 |
| `coord_uncertainty_m` | Reported coordinate uncertainty (m); NA = not reported |
| `country` | ISO 3166-1 alpha-2 code |
| `locality` | Locality text as published |
| `date_collected` | Collection date as published; NA = not reported |
| `catalog_number` | Specimen catalogue number |

Missing values are `NA`. The file is UTF-8 CSV.

## Citation and licence

Please cite the GBIF derived dataset (DOI to be added on registration) and the
paper. Each record keeps the licence of its source dataset (CC0, CC BY or CC
BY-NC). See each `gbif_dataset_key` on GBIF. No additional licence is applied
to these records here.

Contact: Catherine M. Hulshof, Virginia Commonwealth University (cmhulshof@vcu.edu).
