# Compressed Universe — Little Red Dots in JWST surveys

Companion material for **Ginolfi et al.**, *Unsupervised selection and characterisation of Little Red Dots in JWST surveys with manifold learning*. This repository hosts two things:

1. an **interactive web viewer** of the UMAP manifold of ~242,000 JWST sources, and
2. a **machine-readable catalogue** of the new photometric LRD candidates
   (`lrd_candidates.csv`), *to be released publicly upon acceptance*.

Both are derived from the ASTRODEEP-JWST photometric catalogue
([Merlin et al. 2024](https://ui.adsabs.harvard.edu/abs/2024A%26A...691A.240M/abstract)),
embedded with UMAP and anchored by the spectroscopically-selected LRDs of
[de Graaff et al. 2025](https://ui.adsabs.harvard.edu/abs/2025A%26A...697A.189D/abstract).

---

## 1. Interactive viewer

**Live app:** https://micginolfi.github.io/compressedUniverse/

Each point is a JWST source placed on the two-dimensional UMAP map by the similarity
of its broadband colours, morphology and photometric redshift, so that objects with
similar SEDs lie close together. On the landing page you choose a dataset, then:

- **Inspect one object** — *click* a point to show its observed- and rest-frame SED
  and its DAWN JWST Archive (DJA) image cutout.
- **Stack a group** — use the **Box** or **Lasso** tool (plot toolbar) to drag a
  region around several points; the panel then shows their median stacked SED and
  redshift distribution.
- **Show / hide samples** — *click* a name in the legend to toggle a catalogue on or
  off; *double-click* to isolate it. This changes the overlay, not the map.
- **Recolour the map** — the **Color by** buttons switch between catalogues,
  photometric redshift, reference flux and stellarity.
- **Download a selection** — after drawing a Box/Lasso region, **Download CSV** saves
  the selected sources (coordinates, redshift, eight-band photometry) for follow-up.
- **Clear** — click empty map background to reset the view.

Overlaid reference samples include the spectroscopic anchor (de Graaff+25), the
photometric LRD catalogues of Kokorev+24 and Barro+26, brown dwarfs (Hainline+25,26),
and broad-line AGN (Baccus+25).

---

## 2. Candidate catalogue — `lrd_candidates.csv`

The **107 new photometric LRD candidates**: sources that fall inside the main LRD
region of the manifold but are **absent from existing photometric LRD catalogues**
and have no high-quality PRISM classification. They are ranked by locus centrality
(Mahalanobis distance to the main-region centre; rank 1 = most central). See the
paper for the selection and validation.

Plain CSV, one row per candidate, 107 rows.

| column | description | unit |
|---|---|---|
| `rank` | locus-centrality rank (1 = most central) | – |
| `astrodeep_id` | ASTRODEEP-JWST source ID (Merlin+24) | – |
| `field` | survey field (see key below) | – |
| `ra`, `dec` | position, J2000 | deg |
| `zphot` | photometric redshift (EAZY) | – |
| `zspec` | spectroscopic redshift, where available (blank otherwise) | – |
| `has_nirspec` | public DJA NIRSpec coverage (grating only; grade-3 PRISM excluded by construction) | bool |
| `mahal_dist` | Mahalanobis distance to the main-region centre (smaller = more central) | – |
| `class_star` | SExtractor stellarity, 0 (resolved) – 1 (point-like), on the F356W+F444W detection stack | – |
| `r50_px` | half-light radius | pixel |
| `mag_F444W` | AB magnitude in F444W | mag |
| `snr_F444W` | F444W signal-to-noise ratio | – |
| `f_F814W` … `f_F444W` | flux density in the eight bands F814W, F115W, F150W, F200W, F277W, F356W, F410M, F444W | μJy |

**Field key:** `A2744O` = Abell 2744 (GLASS/UNCOVER); `CEERSO` = CEERS (EGS);
`JADESGNO` / `JADESGSO` = JADES GOODS-North / GOODS-South; `PRIMERCO` / `PRIMERUO` =
PRIMER-COSMOS / PRIMER-UDS.

**Notes.** Fluxes are PSF-matched aperture photometry from ASTRODEEP-JWST. Photometric redshifts are the ASTRODEEP
EAZY values and can include catastrophic outliers at the extremes. The candidates are
not spectroscopically confirmed; `has_nirspec = True` marks the few with archival
grating coverage suitable for follow-up.

---

