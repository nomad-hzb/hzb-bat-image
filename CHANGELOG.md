# Changelog

All notable changes to this NOMAD oasis will be documented in this file.

## [0.2.5]

### nomad-battery-space plugin v0.2.5

#### Changed
- **Documentation** rewritten for the current data model: entry types, links between entries (incl. precursors/processing), measurements; updated schema class diagram and coin cell setup visualization; theme aligned with the NOMAD documentation

#### Fixed
- `SeparatorSample` no longer overwrites its own thickness with the thickness of its separator stock
- New ELN entries are prefilled: `ElectrolyteStock.state` with `Liquid`, `CoinCellBattery.case_crimp` with `manual`

### Oasis

#### Added
- Link to the current `CHANGELOG` on the Oasis description page (landing page)

#### Changed
- **Upgrade to NOMAD 2.0.1**; the new GUI (v2) is now the default
- **New URLs**:
  - `/` new GUI (v2), `/gui/` classic GUI (v1), `/select-gui` to choose the preferred GUI
  - `/backend/` NOMAD API, NORTH, `alive`
  - Old `/nomad-oasis/...` links are redirected automatically
- Technical:
  - Elasticsearch 9 replaces Elasticsearch 7; `docker-compose.es7.yaml` for the direct index migration (see the [NOMAD 2.0 migration guide](https://docs.nomad-lab.eu/howto/oasis/migrate/v2.0.html))
  - Temporal services (server, admin tools, PostgreSQL) added
  - Python >= 3.11, `nomad-gui==2.0.1` as plugin
  - `docker-compose.yaml` restructured; images configurable via `.env` (`APP_IMAGE`, `JUPYTER_IMAGE`, `IMAGE_TAG`, ...)
  - Docs only built into the image if `NOMAD_DOCS_REPO` and `NOMAD_DOCS_REPO_REF` are set
  - Jupyter image: conda environment replaced instead of merged
  - CI: GitHub actions v7, no plugin tests skipped
  - README: domain/HTTPS setup, migration notes, FAQ for MongoDB on newer Linux kernels

#### Fixed
- Keycloak URL for NORTH (`.../fairdi/keycloak/auth`)

## [0.2.4]

### nomad-battery-space plugin v0.2.4

#### Added
- **Precursors/processing for derived samples**: `ElectrodeMaterial`, `ElectrolyteStock` and `SeparatorStock` can be derived from other entries of the same type by processing (e.g. spray drying); elements of precursors are included in `aggregated_elements`
- **Measurement entry** "HZB Battery: Measurement" (`BS_Measurement`): upload raw data files of any format (e.g. `.dta`, `.nxs`) and link them to one or more battery samples
- **Search app**: new filter "Project Name" and `authors` column in the results
- `SeparatorStock`: new `synthesis` section
- `ElectrolyteStock` and `SeparatorStock`: `elemental_composition` and `pure_substance` available in the ELN
- Mass and volume from `product_info` are copied to the weights sections if not set
- Ontology links (CHEBI, PATO, EMMO electrochemistry, TFSCO) for several classes and quantities

#### Changed
- **Search app** renamed to "Battery Data Space Search"; filter groups with human-readable labels (e.g. "Electrode Material")
- `ElectrodeSample` only inherits the thickness of its electrode sheet if no thickness is set
- Compatibility with NOMAD 2.0.0

### Oasis

#### Added
- **New GUI (v2)** installed; nginx redirects to the new GUI
- Entry point for Voila notebooks in `nomad.yaml`

#### Changed
- Upgrade to NOMAD 1.4.3 (incl. new NORTH setup from the upstream template)
- Technical: MongoDB 8.0.4, pynxtools plugins deactivated, `nomad-gui` unit tests skipped in CI

#### Fixed
- Starting NORTH tools with `oauthenticator>=16`
- Duplicate pyzmq installation in the Jupyter image

## [0.2.3] 

- Improved and refined search app
- Fixed issues in the CI/CD github pipeline

## [0.2.2] 

- New Voila launching app for voila notebooks 
  
## [0.2.1] 

- Minor bug fixes in the data schema

## [0.2.0] 

### Added

- **New Data Model**: Complete refactoring with **3-tier electrode architecture**
- **Search App Interface**: New search app with filter menus for battery data discovery

### Changed
- Reorganized helper classes and utilities structure
- Dependencies: Pinned nomad-baseclasses to v1.0.1

## [0.1.0]

### Added
- Custom logos
- Added netcdf4 to image to improve performance in some cases

### Changed
  - Upgrade to NOMAD 1.4.2
    - Configuring whitelist via environment variables
    - Possibility to create PATs via api
    - ...
  - Schema extension for Voila (batch upload)

### Initial Release of ``nomad-battery-space`` plugin
