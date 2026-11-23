# GALS approved data catalogue

Repository: `Cesarito2021/global-als-catalogue`, public, branch `main`.
Manifest URL:
`https://raw.githubusercontent.com/Cesarito2021/global-als-catalogue/main/catalogue.json`

The shared metadata node of GALSHub and MichiChat. GALSHub (R package
GALSdownloadeR, `launch_app()`) and MichiChat both read this manifest with
`GALSdownloadeR::update_catalogue()`; MichiChat explores it, GALSHub also
downloads from the original providers. Contributions proposed in MichiChat
reach this catalogue only after maintainer approval.

This repository contains approved discovery metadata only. R package code is
maintained separately. Original point clouds remain at their source providers.
Every public index retains the dataset DOI, attribution, source licence and
original download URL. Dataset rights are governed by those source terms.

## Contents

`catalogue.json` (schema `gals-catalogue-v1`) lists content-addressed indexes
`indexes/<sha256>.tiles.geojson`. `sources.json` records each index's source
family, origin file, row count, attribution, reference and review date.

| Source | Archives / files |
|---|---|
| Servico Florestal Brasileiro (SFB), Zenodo | 221 + 6 ZIP archives of LAS/LAZ; `2014_JAM.zip` excluded |
| ForestScan Lope UAV-LS v2.0 (CEDA) | 150 UAV-LiDAR LAZ |
| SensOFOREST UAV lidar | 3 UAV-LiDAR LAZ (terrestrial TLS files excluded) |
| Epena-Ekolongouma UAV lidar | 2 UAV-LiDAR LAZ |

These are the audited indexes bundled in GALSdownloadeR 0.2.9
(`inst/extdata/source-indexes/`), published byte-identical. Footprints are
header boxes or campaign extents, not point-level coverage.

`verification/` contains a separate smoke-test catalogue for public Zenodo
record 10.5281/zenodo.14917551, retaining its authors and CC BY 4.0 licence.
It maps the author's 124 study-plot polygons to the 2013 LAZ archive. These are
study-plot footprints, not verified complete point-level coverage. This test
catalogue is not included in the root manifest.
Private requests, contacts, review notes, credentials and notifications must
never be added to this repository.

## Maintainer workflow

1. Review a pending request with the package's `review_contribution()` API.
2. Run `publish_catalogue(private_queue, staging_directory)` outside the queue.
3. Copy only `catalogue.json` and the generated `indexes/` into this repository.
4. From the GALSdownloadeR source, run
   `Rscript tools/source-audit/stage-shared-catalogue.R <this checkout>`. It
   re-adds the audited indexes, keeps approved contributions and rewrites
   `sources.json`. Step 3 alone would drop the audited indexes.
5. Validate the staged catalogue before commit. Publish index objects before
   updating the manifest; a single Git commit also switches them together.
6. Verify the HTTPS manifest from a separate client. Package installations
   refresh it without CRAN updates once its stable URL is configured.

GALSdownloadeR validates manifests, public index structure and SHA-256 hashes.
Failure keeps the last complete local snapshot with a warning. Removing an
entry from the next manifest withdraws it from refreshed discovery. Offline
copies and Git history can retain previously published public metadata.
