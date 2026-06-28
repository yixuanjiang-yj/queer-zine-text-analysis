# Queer Zine Archive Project: Computational Text Analysis

**Yixuan Jiang**
DIGHUM101
UC Berkeley, Summer 2026

A digital humanities project using Python to analyze zines from the
[Queer Zine Archive Project (QZAP)](https://archive.qzap.org), a free
community archive of queer zines.

## Research Questions

1. What words and phrases most distinctively characterize individual zines
   in this sample?
2. How does the vocabulary of each zine reflect its community, politics,
   and moment?
3. Where are these zines located -- which places are named, and what
   geographies of queer life do they reflect or construct?

## The Data

QZAP hosts 532 digitized zines spanning 1970 to 2022. This project works
with a sample of ten zines selected for decade spread and thematic variety:

| Title | Year |
|-------|------|
| Gender Trash #1 | 1993 |
| Going Homo #3 | 1994 |
| TimTum: A Trans Jew Zine | 1999 |
| Doris #21 | 2003 |
| Queer Zine Explosion #20 | 2003 |
| Behind the Bars | 2006 |
| Gaysi #1 | 2011 |
| The Anarchistic Queer #1.1 | 2011 |
| Empty Orchestra #1 | 2012 |
| We Have Always Existed | 2022 |

QZAP does not provide a public API or bulk download option. The data
access notebook explains how the catalog was built programmatically
and how individual zines can be downloaded.

## Methods

- **Word frequency analysis** -- counts the most common words across
  all ten zines combined to identify shared vocabulary
- **TF-IDF (Term Frequency-Inverse Document Frequency)** -- identifies
  the words most distinctive to each individual zine
- **Named Entity Recognition (NER)** -- extracts place names from each
  zine's text using spaCy
- **Geocoding and mapping** -- converts place names to coordinates and
  visualizes them on an interactive map using folium

## Notebooks

The project is split into three notebooks, which should be run in order:

**`01_data_access.ipynb`** -- Builds a complete catalog of all 532 zines
in the QZAP archive by iterating through the archive's database. Also
provides a reusable function for downloading any zine from the catalog.
Note: this notebook takes approximately 25 minutes to run due to
respectful rate limiting between requests.

**`02_data_pipeline.ipynb`** -- Extracts and cleans text from the ten
selected zines, runs word frequency analysis and TF-IDF, and visualizes
the results. Also includes a decade-level analysis comparing vocabulary
across the 1990s, 2000s, and 2010s onward.

**`03_mapping.ipynb`** -- Extracts place names from each zine using
Named Entity Recognition, geocodes them, and displays them on an
interactive color-coded map. Connects geographic findings back to the
TF-IDF vocabulary results from notebook 2.

## How to Run

1. Clone this repository
2. Activate the DIGHUM101 Python environment
3. Run the notebooks in order: `01` → `02` → `03`

Note: `01_data_access.ipynb` must be run first to generate
`output/qzap_catalog.csv`, which `02_data_pipeline.ipynb` depends on.
The zine PDFs must also be present in `data/zines/` before running
notebook 2.

## Dependencies

- `pdfplumber` -- PDF text extraction
- `nltk` -- text preprocessing and stop words
- `sklearn` -- TF-IDF vectorization
- `spacy` -- Named Entity Recognition
- `geopy` -- geocoding place names
- `folium` -- interactive map
- `pandas` -- data handling
- `matplotlib` -- visualization

## Key Findings

- TF-IDF reveals that each zine's vocabulary is shaped by its specific
  community, politics, and decade. The 1990s zines tend toward
  identity-formation vocabulary, the 2000s zines toward established
  political discourse, and the 2010s onward toward intersectional and
  globally-reaching frameworks.
- The geographic map shows a strong concentration of place references
  in North America and Western Europe. International references appear
  almost exclusively in zines with explicitly diasporic or global
  politics.
- Zines with a narrower geographic footprint tend to have more locally-
  specific vocabulary, while zines with a wider geographic reach tend
  to have more ideological or identity-spanning vocabulary.

## Limitations

- OCR quality varies significantly across zines. Handwritten layouts
  and unusual fonts reduce text extraction accuracy.
- NER was trained on newspaper text and does not transfer cleanly to
  zine text, producing false positives that required manual verification.
- The sample of ten zines is small and purposively selected. Findings
  are suggestive rather than generalizable to the full archive.
- Zines are visual objects. Handwriting, illustration, and layout are
  entirely invisible to these computational methods.
