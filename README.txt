SOIL CARBON AND FIRE-WEATHER TRANSFORMERS

Open data_harmonization.ipynb from this folder and run it first.
Then open transformer_walkthrough.ipynb.
Run All loads the included weights and makes predictions.
To train, uncomment the training cells.

Setup (Python 3.12):

    python -m venv .venv
    source .venv/bin/activate
    python -m pip install -r requirements.txt
    jupyter lab data_harmonization.ipynb

Keep data/ and models/ beside the notebook. The notebook uses the GPU when available.
No external data downloads are needed.

Soil model source:
    tangarine_USE_THIS_VERSION_Hawaii_Soils_Transformer.ipynb

The soil model class, sequence function, dataset class, training configuration
and training/prediction loops are copied from that notebook. Source cells and
hashes are recorded in soil_production_source.json.

The soil sample comes from real observations. Coordinates and original IDs
are omitted and values are slightly perturbed. Acquisition dates in the
harmonization inputs are retained. Carbon
remains a site-level label. See data/soil_notes.json and
data/harmonization/soil_inputs.json for preparation details.

The fire sample contains real CFSv2 weather and historical perimeter-derived
bubble radii. Event IDs, dates, grid coordinates and source filenames are in
data/fire_events.json. The included fire checkpoint uses five DIAMETER bins:
0, 10, 100, 1000, 10000, infinity metres.

Use each set of weights with its matching normalization. Training new weights
requires retaining the new normalization as well.

Harmonization inputs are in data/harmonization/. The notebook aligns Landsat
bands, applies QA filtering and LOWESS smoothing, joins soil covariates, and
aligns weather with daily fire distributions. Database matching helpers show
how to extract new observations; those optional examples use your own source
files. The fire perimeter example also requires geopandas.

The modeling notebook reads data/soil_carbon_harmonized.csv and
data/fire_harmonized.csv. Both generated tables are included in this folder.
