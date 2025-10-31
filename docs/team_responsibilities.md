# Team Responsibilities

## 1. Sammy — Machine Learning & Data Modeling Lead

### Data Engineering
- ✅ Collect & preprocess NASA radiation datasets (OMNI2, GOES, sunspot, TLE)
- Build `ingest.py` - data loading and ingestion pipeline
- Build `features.py` - feature engineering and preprocessing
- Handle missing values, time alignment, feature scaling
- Create train/test/validation splits

### Physics Model (Baseline)
- Implement simplified shielding calculations (exponential attenuation)
- Use NIST stopping power tables for dose calculations
- Compute baseline dose estimates from GCR/SPE spectra
- Mission geometry calculations (altitude, shielding variation)
- Document physics equations and assumptions

### Machine Learning
- Build `train.py` - model training pipeline (XGBoost, RandomForest, or hybrid)
- Build `evaluate.py` - model evaluation and metrics (MAE, MAPE, R²)
- Feature engineering (solar indices, orbital parameters, SEP flags)
- Model hyperparameter tuning and optimization
- Compare physics baseline vs ML model performance
- Model interpretability (feature importance, SHAP values)

### Deliverables
- `src/data_acquisition/ingest.py`
- `src/data_acquisition/features.py`
- `src/ml_models/train.py`
- `src/ml_models/evaluate.py`
- `models/` folder with trained model artifacts
- Jupyter notebooks documenting ML methodology
- Graphs: predicted vs actual dose rates
- Research figure: model accuracy vs physics baseline

### Git Branch
- `ml-sammy` - ML model development and data preprocessing

---

## 2. Partner (Mehdi) — Biomedical, Research & Visualization Lead

### Biological Dose Conversion & Risk Model
- Research ICRP 103 tissue weighting factors
- Research ICRP 116 fluence-to-dose conversion coefficients
- Implement `risk.py`:
  - Convert absorbed dose (mGy/Gy) → effective dose (Sv)
  - Risk classification logic (Low/Moderate/High)
  - Map effective dose to cancer risk estimates (REID)
- Research NASA Space Cancer Risk (NSCR) model
- Define and validate risk band thresholds

### Research & Documentation
- Literature review: radiation health effects, astronaut studies
- Write project research background and abstract
- Write Methods section (biological aspects, dose conversion)
- Write Introduction, Discussion, and Health Implications sections
- Contextualize dose rates (vs background, medical procedures)
- Document degenerative health risks (CNS, cardiovascular)
- Mission duration exposure limits (30-day, 1-year, career)

### Validation Data
- Search NASA Technical Reports for ISS dosimetry papers
- Extract measured dose rates from publications
- Find BEAM, TEPC, PADLES data
- Organize validation dataset with proper citations

### Streamlit Dashboard & Visualization
- Design and build `app_streamlit.py`:
  - Interactive mission simulation interface
  - Dose accumulation curve visualization
  - Risk band display and interpretation
  - Comparison across missions (ISS, Gateway, Mars)
  - Health context annotations
- Create case studies with health implications
- Dashboard screenshots and demo graphs
- Export functionality for predictions

### Project Management
- Manage project structure and organization
- Write comprehensive `README.md`
- Create `reports/abstract.md`
- Maintain documentation
- Final poster or report integration

### Deliverables
- `src/physics/risk.py`
- `src/visualization/app_streamlit.py`
- `docs/abstract.md`
- `README.md`
- Streamlit dashboard screenshots
- Final poster/write-up integrating medical risk and ML findings

### Git Branch
- `biomed-mehdi` - health model, dashboard, and documentation

---

## Shared Responsibilities

### Project Planning
- Define mission profiles (ISS, Lunar Gateway, Mars transit)
- Agree on shielding scenarios (areal density values)
- Set validation metrics and success criteria
- Timeline and milestone tracking

### Validation & Testing
- Compare model predictions to measured ISS dose rates
- Sanity checks (does Mars prediction match MSL RAD?)
- Cross-validate risk bands with published limits
- Interpret discrepancies between physics model and ML model

### Paper/Poster Writing
- Abstract (both contribute)
- Introduction (health partner leads)
- Methods: Physics & ML (you lead), Dose conversion & Risk (partner leads)
- Results (collaborative interpretation)
- Discussion (partner leads health implications, you lead technical)
- Conclusions (both)

---

## Suggested Workflow

### Phase 1: Data & Setup (Week 1-2)
**You:**
- Download OMNI2, sunspot, TLE data ✅
- Set up data pipeline
- Initial exploratory analysis

**Partner:**
- Research ICRP conversion factors
- Find ISS dosimetry validation papers
- Document NASA risk model (NSCR)

### Phase 2: Baseline Models (Week 3-4)
**You:**
- Implement physics-based dose calculations
- Feature engineering
- Prepare ML training data

**Partner:**
- Implement dose conversion (mGy → Sv)
- Define risk band thresholds
- Extract validation dose rates from literature

### Phase 3: ML Model (Week 5-6)
**You:**
- Train XGBoost model
- Hyperparameter optimization
- Model validation

**Partner:**
- Validate predictions against published dose rates
- Check risk classifications against astronaut limits
- Health interpretation of model errors

### Phase 4: Dashboard & Analysis (Week 7-8)
**You:**
- Build Streamlit dashboard
- Mission simulation tools
- Visualization

**Partner:**
- Test dashboard usability
- Add health context annotations
- Risk communication features

### Phase 5: Documentation (Week 9-10)
**Both:**
- Write Methods, Results, Discussion
- Prepare poster/presentation
- Create figures and tables

---

## Communication & Tools

### Regular Check-ins
- Weekly sync meetings
- Shared Google Doc/Overleaf for writing
- Slack/Discord for quick questions

### Shared Resources
- This GitHub repo (you manage, partner can view/comment)
- Google Drive folder for papers, figures, notes
- Shared Zotero/Mendeley library for citations

### Decision Points (Need Both)
- Mission profile definitions
- Risk band threshold values
- Validation success criteria
- Publication target and timeline
