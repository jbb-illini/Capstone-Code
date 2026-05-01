# Lake-Atmosphere Heat Flux Response to Cold Air Outbreaks Over Lake Erie

A 16-year, ice-type-resolved turbulent heat flux climatology for Lake Erie during cold air outbreak (CAO) conditions, derived from daily USNIC ASCII grid observations and ERA5 reanalysis atmospheric forcing.

## Overview

This project presents the first systematic climatology of sensible (QH) and latent (QE) heat fluxes over Lake Erie during CAO events, using a four-class surface type classification (open water, lead, rubble, smooth ice) and the bulk aerodynamic parameterization of Guest and Davidson (1991). A composite analysis of 27 CAO events (2010-2026) reveals consistent flux suppression following onset, with the Bowen ratio (QH/QE) remaining above 1.0 through day 6 post-onset before a brief dip at days 7-8 and recovery at day 9. Sub-grid surface heterogeneity systematically enhances QH relative to a uniform smooth-ice baseline, confirming that ice type distribution rather than total ice concentration governs lake-atmosphere energy exchange.

## Data Sources

- **USNIC ASCII Grid Product** - Daily Great Lakes ice charts at 1,275 m resolution, Dec-Mar 2010-2026 (2,063 grids)
- **ERA5 Reanalysis** - 2-m air temperature, dewpoint, and 10-m wind speed over Lake Erie domain (4 synoptic hours averaged to daily mean)
- **GLERL GLSEA** - Independent ice concentration product used for USNIC validation (r = 0.987, RMSE = 10.2%, bias = +6.4%)

## Key Findings

- Median Bowen ratio across the full cold-date population: 1.48; 68.8% of CAO ice-covered dates show sensible heat dominance
- CAO composite: QH declines 91% and QE 82% over 9 post-onset days as ice cover rises from ~51% to ~99%
- Bowen ratio robust to full parameter uncertainty space (Monte Carlo N = 500; p05 > 1.0 at day offsets 0-9 with n >= 8; minimum p05 = 1.14 at day 9)
- Result holds across AO phase stratification (positive AO n = 11, negative AO n = 19)

## Methods

1. USNIC ASCII grids reprojected from EPSG:3857 to EPSG:4326 and classified into four surface types using WMO SIGRID-3 concentration codes
2. Bulk aerodynamic fluxes computed following Guest and Davidson (1991) with Louis (1979) atmospheric stability correction
3. CAO events identified using ERA5 lake-mean Ta < -10 deg C sustained for at least 2 consecutive days; 30 events identified, 27 composited
4. Monte Carlo uncertainty analysis with uniform priors on Ta, wind speed, and ice-class surface temperatures

## Dependencies

- Python 3, Jupyter
- numpy, pandas, matplotlib, scipy
- xarray, rasterio, geopandas, shapely
- requests (ERA5 CDS API)

## Repository Contents

- `Capstone.ipynb` - Main analysis notebook (17 cells: data processing, flux computation, composite analysis, Monte Carlo, validation, AO stratification)
- `docs/` - Research notes
- `*.png` - Output figures
