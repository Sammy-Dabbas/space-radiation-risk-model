# Data Acquisition Plan

## Priority 1: Core Training Data (Start Here)

### 1. NASA OMNI2 Data (Solar/Geomagnetic Indices)
**Why:** Primary features for your ML model (F10.7, Kp, ap)
**Access:** https://omniweb.gsfc.nasa.gov/form/dx1.html
**How to get:**
- Select "OMNI2" dataset
- Choose daily averages
- Date range: Suggest 2000-2024 (covers multiple solar cycles)
- Parameters to download:
  - F10.7 index (Column 50)
  - Kp index (Column 38)
  - ap index (Column 39)
  - Dst index (Column 40)
  - IMF magnitude (Column 21)
  - Solar wind speed (Column 23)
- Format: ASCII text or CSV
- Save to: `data/raw/omni2_2000_2024.csv`

### 2. SILSO Sunspot Numbers
**Why:** Solar cycle phase indicator
**Access:** https://www.sidc.be/silso/datafiles
**How to get:**
- Download daily sunspot number: `SN_d_tot_V2.0.csv`
- Direct link: https://www.sidc.be/silso/INFO/sndtotcsv.php
- Format: CSV (Year, Month, Day, Decimal Date, SNvalue, StdDev, Observations, Indicator)
- Save to: `data/raw/sunspot_daily.csv`

### 3. ISS TLE Data (Orbital Parameters)
**Why:** ISS altitude/orbit features for LEO dose calculations
**Access:** https://celestrak.org/NORAD/elements/gp.php?GROUP=stations&FORMAT=tle
**How to get:**
- Current TLEs available directly
- Historical archive: May need Space-Track.org (free registration)
  - Register at: https://www.space-track.org/auth/createAccount
  - Query historical ISS TLEs by date range
- Alternative: Use Skyfield library to propagate recent TLEs backward
- Save to: `data/raw/iss_tle_history.txt`

### 4. GOES Proton Flux Data (SEP Events)
**Why:** Solar particle event detection and intensity
**Access:** https://www.swpc.noaa.gov/products/goes-proton-flux
**How to get:**
- NOAA NCEI archive: https://satdat.ngdc.noaa.gov/sem/goes/data/
- Select GOES satellite series (GOES-13 through GOES-18 for recent data)
- Download differential/integral proton flux
- Channels: >10 MeV, >50 MeV, >100 MeV
- Format: NetCDF or CSV
- Save to: `data/raw/goes_proton_flux/`

---

## Priority 2: Validation/Target Data

### 5. ISS Dosimetry Data
**Why:** Ground truth LEO dose rates for model validation
**Access:** NASA Technical Reports Server + published papers
**How to get:**
- Search NTRS: https://ntrs.nasa.gov
- Keywords: "ISS dosimetry", "TEPC", "BEAM radiation", "ISS radiation environment"
- Key papers to find:
  - "ISS Radiation Environment" reports
  - BEAM (Bigelow Expandable Activity Module) radiation studies
  - PADLES (Passive Dosimeter for Lifescience Experiments)
- Extract dose rate tables/figures
- Format: Manual extraction to CSV
- Save to: `data/raw/iss_dosimetry/`

### 6. MSL RAD Cruise Data (Optional - Deep Space Validation)
**Why:** Mars cruise dose rates for deep-space validation
**Access:** https://pds-ppi.igpp.ucla.edu/search/?sc=Mars%20Science%20Laboratory&facet=SPACECRAFT_NAME
**How to get:**
- Navigate to MSL RAD instrument data
- Download cruise phase data (Aug 2011 - Aug 2012)
- Format: PDS label files + binary data (may need parsing)
- Save to: `data/raw/msl_rad_cruise/`
**Note:** Lower priority unless you're validating deep-space predictions

---

## Priority 3: Reference Data (Download Once, Use for Conversions)

### 7. ICRP Conversion Coefficients
**Why:** Convert absorbed dose to effective dose (Sv)
**Access:** ICRP Publications 103 & 116
**How to get:**
- ICRP 103: Tissue weighting factors (Table in publication)
- ICRP 116: May need to extract from PDF or find tabulated versions
- Alternative: Look for publicly available implementations (e.g., PHITS, MCNP output)
- Format: Manual table extraction to CSV
- Save to: `data/raw/icrp_conversion_factors.csv`

### 8. NIST Stopping Power Tables
**Why:** Physics-based shielding calculations
**Access:** https://physics.nist.gov/PhysRefData/Star/Text/contents.html
**How to get:**
- Select particle type (protons, electrons, alphas)
- Select materials: Aluminum, Polyethylene, Water
- Download tables for energy range 1 MeV - 1000 MeV
- Format: ASCII tables
- Save to: `data/raw/nist_stopping_power/`

---

## Quick Start Workflow

### Step 1: Get the Essentials (Do This Today)
```bash
# Create download directories
mkdir -p data/raw/goes_proton_flux
mkdir -p data/raw/iss_dosimetry
mkdir -p data/raw/nist_stopping_power
```

1. **OMNI2**: Download via web form → `data/raw/omni2_2000_2024.csv`
2. **Sunspot**: Direct download → `data/raw/sunspot_daily.csv`
3. **GOES**: Download 2-3 years of recent data → `data/raw/goes_proton_flux/`

### Step 2: Register for Accounts (If Needed)
- Space-Track.org for historical ISS TLEs
- SPENVIS/AFRL for AE9/AP9 data (if you want trapped radiation belts)

### Step 3: Manual Extraction
- Search NTRS for ISS dosimetry papers
- Extract ICRP tissue weighting factors from publication

---

## Recommended Timeline

**Week 1:**
- ✅ Download OMNI2, sunspot, GOES data
- ✅ Register for Space-Track
- ✅ Get recent ISS TLEs

**Week 2:**
- Find and extract ISS dosimetry validation data
- Download NIST stopping power tables
- Start data cleaning/merging

**Week 3+:**
- Optional: MSL RAD, LRO CRaTER for additional validation
- Optional: AE9/AP9 if modeling trapped radiation belts

---

## Data Storage Structure

```
data/raw/
├── omni2_2000_2024.csv
├── sunspot_daily.csv
├── iss_tle_history.txt
├── goes_proton_flux/
│   ├── goes16_2020.csv
│   ├── goes16_2021.csv
│   └── ...
├── iss_dosimetry/
│   ├── beam_report_2016.csv
│   └── tepc_measurements.csv
├── nist_stopping_power/
│   ├── proton_aluminum.txt
│   ├── proton_water.txt
│   └── ...
└── icrp_conversion_factors.csv
```

---

## Next Steps After Data Acquisition

1. Create data loading scripts in `src/data_acquisition/`
2. Data cleaning and alignment (same time indices)
3. Feature engineering
4. Train/test split
5. Begin physics baseline model
