# GALS approved data catalogue

Proposed repository: `Cesarito2021/global-als-catalogue`, public, branch `main`.
Proposed manifest URL:
`https://raw.githubusercontent.com/Cesarito2021/global-als-catalogue/main/catalogue.json`

This repository contains approved discovery metadata only. R package code is
maintained separately. Original point clouds remain at their source providers.
Every public index retains the dataset DOI, attribution, source licence and
original download URL. Dataset rights are governed by those source terms.

The initial discovery catalogue is empty. `verification/` contains a separate
smoke-test catalogue for public Zenodo record 10.5281/zenodo.14917551, retaining
its authors and CC BY 4.0 licence. It maps the author's 124 study-plot polygons
to the 2013 LAZ archive. These are study-plot footprints, not verified complete
point-level coverage. This test catalogue is not included in the root manifest.
No production contribution is approved by this demonstration.
Private requests, contacts, review notes, credentials and notifications must
never be added to this repository.

Maintainer workflow:

1. Review a pending request with the package's `review_contribution()` API.
2. Run `publish_catalogue(private_queue, staging_directory)` outside the queue.
3. Copy only `catalogue.json` and the generated `indexes/` into this repository.
4. Validate the staged catalogue before commit. Publish index objects before
   updating the manifest; a single Git commit also switches them together.
5. Verify the HTTPS manifest from a separate client. Package installations
   refresh it without CRAN updates once its stable URL is configured.

GALSdownloadeR validates manifests, public index structure and SHA-256 hashes.
Failure keeps the last complete local snapshot with a warning. Removing an
entry from the next manifest withdraws it from refreshed discovery. Offline
copies and Git history can retain previously published public metadata.

This is prepared local content. The repository and endpoint are not yet deployed.
