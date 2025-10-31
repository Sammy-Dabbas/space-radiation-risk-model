# Data Sources Reference

## Core Environment & Dose Datasets

### AE9/AP9/SPM Radiation Belt Model Data
- **Purpose:** Trapped electron and proton climatology with uncertainty
- **Use Case:** LEO/ISS conditions and SPE background filtering
- **Access:** Free registration required
- **URL:** https://www.vdl.afrl.af.mil

### Badhwar-O'Neill 2020 (BON2020) Galactic Cosmic Ray Model
- **Purpose:** Current NASA GCR spectra implementation with improved solar activity handling
- **Use Case:** Baseline GCR flux calculations for all mission profiles
- **URL:** https://software.nasa.gov
- **Reference:** Primary paper available at software page

### CREME Suite (CREME96/CREME-MC/CREME2009)
- **Purpose:** GCR and SEP spectral models and transport utilities
- **Use Case:** Mission studies, alternative GCR/SEP spectra
- **URLs:**
  - Portal: https://creme.isde.vanderbilt.edu
  - Technical refs: https://sites.srl.caltech.edu

### MSL RAD (Mars Science Laboratory) Dose Data
- **Purpose:** Cruise phase and surface radiation measurements
- **Use Case:** Deep-space validation and Mars comparisons
- **URL:** https://pds-ppi.igpp.ucla.edu

### LRO CRaTER Radiation Data
- **Purpose:** Lunar orbit dose and LET context
- **Use Case:** Validation for Lunar Gateway mission profiles
- **Products:** EDR and processed DDR products
- **URL:** https://pds.nasa.gov

### ISS Dosimetry
- **Purpose:** TEPC and area dosimeter studies, including BEAM report comparisons
- **Use Case:** LEO dose rate anchors and validation
- **URL:** NASA Technical Reports Server

---

## Solar Activity and SEP Sources

### NOAA SWPC GOES Proton Flux
- **Purpose:** Time series for >10 MeV and higher integral channels
- **Use Case:** Direct inputs for SPE labeling and features
- **URL:** https://www.swpc.noaa.gov
- **Data:** Real-time and historical proton flux data

### NOAA/NASA SEP Event Lists
- **Purpose:** Event catalogs with start/end, peak flux, thresholds for >10 MeV
- **Use Case:** Supervision labels for SPE detection
- **URL:** https://ngdc.noaa.gov

### ESA SEPEM Reference Data Set (RDS v3)
- **Purpose:** Harmonized multi-mission SEP proton data and event list (1974-present)
- **Use Case:** Long-term SPE climatology and training data
- **URLs:**
  - Main: https://sepem.eu
  - Docs: Space Weather journal

---

## Solar/Geomagnetic Indices for Features

### NASA OMNI2/OMNIWeb
- **Purpose:** Solar wind, IMF, Kp, ap, F10.7 indices
- **Use Case:** Model covariates and solar cycle controls
- **Access:** API and file export available
- **URL:** https://omniweb.gsfc.nasa.gov
- **Key Variables:**
  - F10.7 (solar radio flux)
  - Kp/ap (geomagnetic activity)
  - Solar wind speed, IMF components

### SILSO International Sunspot Number
- **Purpose:** Daily and monthly sunspot numbers
- **Use Case:** Solar cycle phase features
- **URL:** https://sidc.be

---

## Orbit/Mission Geometry

### ISS Ephemeris (TLE Archives)
- **Purpose:** Historical TLEs for altitude/inclination time series
- **Use Case:** Mission geometry features (altitude, latitude, shielding variation)
- **Sources:**
  - CelesTrak: https://celestrak.org
  - Space-Track API: Requires registration

---

## Shielding and Conversion References

### NIST ESTAR/PSTAR/ASTAR
- **Purpose:** Stopping power and ranges for electrons, protons, alphas
- **Materials:** Al, polyethylene, water, etc.
- **Use Case:** Simplified exponential attenuation and areal density studies
- **URL:** https://www.nist.gov/pml/stopping-power-range-tables

### ICRP 103 Tissue Weighting Factors
- **Purpose:** Effective dose estimates
- **Use Case:** Converting absorbed dose to effective dose (Sv)
- **URL:** https://www.icrp.org

### ICRP 116 Fluence-to-Dose Conversion Coefficients
- **Purpose:** Standard coefficients for dose and organ doses
- **Use Case:** Converting particle fluence to organ-specific dose
- **URL:** https://www.icrp.org

---

## NASA Risk Model References

### NASA Space Cancer Risk Model (NSCR)
- **Purpose:** REID/REIC calculation framework
- **Use Case:** Calibrating Low/Moderate/High risk bands
- **URL:** NASA Technical Reports Server
- **Key Reports:**
  - Space Radiation Cancer Risk Projections and Uncertainties
  - NSCR model documentation

---

## Pipeline Integration Map

### Daily Driver Features
- **Sources:** OMNI2, SILSO, ISS TLEs
- **Variables:**
  - F10.7 solar flux
  - Kp/ap indices
  - Sunspot number
  - ISS altitude
  - Mission geometry flags
  - Shielding areal density

### Labels/Targets
- **ISS:** TEPC/PADLES data, BEAM report
- **Deep-space validation:** MSL RAD cruise data
- **Lunar orbit:** LRO CRaTER data

### Physics Priors
- **GCR Spectra:** BON2020 or CREME
- **Attenuation:** NIST stopping-power tables
- **Method:** Exponential attenuation baseline

### SEP Handling
- **Detection:** GOES flux + SEPEM event metadata
- **Features:** Event intensity, duration, integrated flux

### Effective Dose & Risk Band
- **Conversion:** ICRP 103 weights + ICRP 116 coefficients
- **Risk Mapping:** Consistency check against NSCR documentation
- **Output:** mGy (absorbed dose), Sv (effective dose), Risk band (Low/Moderate/High)
