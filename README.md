# Cell–cell communication at single-cell resolution

A ~1.5 h hands-on tutorial using [LIANA+](https://liana-py.readthedocs.io/) on MERFISH
data from the adult mouse brain.

## Setup

```bash
conda env create -f env.yml
conda activate sc-ccc-tutorial
jupyter lab
```

## Run order

Run `00_setup.ipynb` **before the session** — it downloads the dataset (~1.1 GB, needs
~3 GB RAM) and writes the prepared section to `data/brain_section.h5ad`, which the
other three notebooks load in a couple of seconds.

| notebook | question |
| --- | --- |
| `00_setup.ipynb` | download, subset, QC, normalise |
| `01_restricting_lr_methods.ipynb` | Which cell types talk to which — if they are close enough to? |
| `02_spatial_scales.ipynb` | At what distance does an interaction happen? |
| `03_local_hotspots.ipynb` | Where in the tissue does it happen? |

Notebooks 01–03 are independent and can be run in any order.

## Citation

Methods and code adapted from the [LIANA+ tutorials](https://liana-py.readthedocs.io/en/latest/notebooks/).

- **LIANA+**: Dimitrov et al. (2024), *Nature Cell Biology*.
- **`inflow` and LRIC**: part of an ongoing LIANA+ extension (Alsayah et al., in prep).
- **Data**: Yao et al. (2023), *Nature* — [WB_MERFISH_animal2_coronal](https://cellxgene.cziscience.com/collections/0cca8620-8dee-45d0-aef5-23f032a5cf09).
