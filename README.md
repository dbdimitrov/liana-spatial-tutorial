# Cell–cell communication with LIANA+

Hands-on tutorials for inferring cell–cell communication with
[LIANA+](https://liana-py.readthedocs.io/). They start with a shared introduction, followed
by two parts:

```
tutorials/
  00_intro_ccc.ipynb   # shared intro: LIANA+ basics on dissociated scRNA-seq
  spot/                # Part 1: spot-based spatial transcriptomics (Visium)
  image/               # Part 2: single-cell resolution (MERFISH)
```

1. **`tutorials/spot/`: spot-based spatial transcriptomics.** 10X Visium data from a human
   heart after myocardial infarction (Kuppe et al., 2022).
2. **`tutorials/image/`: single-cell resolution.** Imaging-based MERFISH data from the
   adult mouse brain (Yao et al., 2023). Part 2 builds on Part 1.

## Setup

```bash
conda env create -f environment.yml
conda activate sc-ccc-tutorial
jupyter lab
```

Every notebook loads its data with a `li.ds.*` function and caches it in `data/anndata/` at the
repository root. If a file is already there, it is used as-is. Otherwise it is downloaded. So
if you were given the h5ad files, place them as follows:

```
data/
  anndata/Visium_19_CK297.h5ad              # li.ds.kuppe_2022()   (~45 MB)
  anndata/WB_MERFISH_animal2_coronal.h5ad   # li.ds.yao_2023()     (~1.1 GB)
  brain_section.h5ad                        # written by tutorials/image/00_setup.ipynb
```

## Introduction

`tutorials/00_intro_ccc.ipynb` covers LIANA+ methods and resources, `rank_aggregate` and
plotting, using a small dissociated scRNA-seq dataset (PBMCs, bundled with scanpy). Start here.

Exercises: compare individual methods; (advanced) build your own consensus with `li.mt.AggregateClass`.

## Part 1: spot-based (Visium)

| notebook | covers | exercise |
| --- | --- | --- |
| `01_bivariate_local.ipynb` | Local and global bivariate metrics (`li.mt.bivariate`): spatially co-expressed LR pairs, TF activities, cell-type compositions | Does the local metric matter? (cosine vs Pearson) |
| `02_misty.ipynb` | Learning multi-view spatial relationships with MISTy | Where is an LR interaction active? (bivariate scores as MISTy targets, cell-type compositions as predictors) |

Run them in order. Each notebook is self-contained, so none depends on another's output.

Exercises follow the same format in both parts: a task box, a `# your turn` cell, and a collapsed **▶ Solution**.

## Part 2: single-cell resolution (MERFISH)

Run `tutorials/image/00_setup.ipynb` **first**. It downloads the dataset (~1.1 GB, needs ~3 GB RAM) and
writes the prepared section to `data/brain_section.h5ad`. The other three notebooks load that
file in a couple of seconds. If you were given `brain_section.h5ad`, you can skip `00_setup`.

| notebook | question |
| --- | --- |
| `00_setup.ipynb` | download, subset, QC, normalise |
| `01_restricting_lr_methods.ipynb` | Which cell types talk to which, if they are close enough to? |
| `02_spatial_scales.ipynb` | At what distance does an interaction happen? |
| `03_local_hotspots.ipynb` | Where in the tissue does it happen? |

Notebooks 01–03 are independent and can be run in any order.

## Citation

Methods and code adapted from the [LIANA+ tutorials](https://liana-py.readthedocs.io/en/latest/notebooks/).

- **LIANA+**: Dimitrov et al. (2024), *Nature Cell Biology* 26:1613–1622.
- **Benchmark motivating spatial restriction**: Dimitrov et al. (2022), *Nature Communications* 13:3224.
- **Microenvironments (hard restriction)**: Garcia-Alonso et al. (2021), *Nature Genetics* 53:1698–1711 (CellPhoneDBv3).
- **Proximity weighting (soft restriction)**: Jin et al. (2024), *Nature Protocols* (CellChatv2).
- **MISTy**: Tanevski et al. (2022), *Genome Biology* 23:97.
- **`inflow` and LRIC**: part of an ongoing LIANA+ extension (Alsayah et al., in prep).
- **Data (Part 1)**: Kuppe et al. (2022), *Nature* 608:766–777. Visium slide `Visium_19_CK297` (ischemic zone).
- **Data (Part 2)**: Yao et al. (2023), *Nature*. [WB_MERFISH_animal2_coronal](https://cellxgene.cziscience.com/collections/0cca8620-8dee-45d0-aef5-23f032a5cf09).
