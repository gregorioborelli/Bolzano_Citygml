# Bolzano CityGML / CityJSON

This repository contains **CityGML** and **CityJSON** datasets for the city of **Bolzano, Italy**.

The 3D building models were generated using [`roofer`](https://github.com/3DBAG/roofer), specifically the Docker image:

```text
3dgi/roofer:v1.0.0-beta.5
```

The resulting files are the output of the `roofer` reconstruction workflow, followed by additional post-processing steps.

---

## Repository overview

This repository provides 3D city model data for Bolzano in two open formats:

- **CityGML**
- **CityJSON**

The models include reconstructed building geometries generated from geospatial input data such as DSM data and  building footprints.

---

## Data sources

The input geospatial data was obtained from the GeoNetwork portal of the Autonomous Province of Bolzano / South Tyrol:

https://geonetwork1.civis.bz.it/geonetwork/srv/ita/catalog.search#/map

The input data includes, where available:

- DSM/DTM
- Building footprint data

---

## 3D model generation

The 3D city models were generated using `roofer` through Docker.

### Docker image

```text
3dgi/roofer:v1.0.0-beta.5
```
### Command used
```bash
docker run --rm \
  -v /path/to/data:/data \
  3dgi/roofer:v1.0.0-beta.5 \
  roofer \
  /data/Dsm/bolzano_combined_4.las \
  /data/Bolzano_Buildings.gpkg \
  /data/output/ \
  --lod13 \
  --lod22 \
  --id-attribute CODICE \
  --cj-scale 0.01 0.01 0.01 \
  --plane-detect-epsilon 0.3 \
  --plane-detect-min-points 20 \
  --complexity-factor 0.7 \
  --h-terrain-strategy user \
  --h-terrain-attribute QT_TERRA
```

Replace:

```text
/path/to/data
```

with the local directory containing the input datasets.

---

## Input files

The main input files used in the workflow are:

```text
/data/Dsm/bolzano_combined_4.las
/data/Inputdata/Bolzano_Buildings.gpkg
```

### `bolzano_combined_4.las`

.las file obtain by DSM and DTM.

### `Bolzano_Buildings_Simplified.gpkg`

Building footprint dataset used as the base geometry for the reconstruction process.

The attribute `CODICE` was used as the unique building identifier.

The attribute `QT_TERRA` was used as the terrain height attribute.

---

## Output files

The workflow produces 3D building models in SeqCityJSON and throuh 3Dcitydb v5 a citygml 




## Related publication

The complete workflow and detailed analysis are described in the paper:

**A 3DCityDB-Based Workflow for Scalable Urban Building Energy Modeling from Limited GIS Data**

Authors:

- **Gregorio Borelli**  
  Free University of Bozen-Bolzano, Italy & Idiap Research Institute, Switzerland  
  gregorio.borelli@student.unibz.it

- **Andrea Gasparella**  
  Free University of Bozen-Bolzano, Italy  
  andrea.gasparella@unibz.it

- **Giovanni Pernigotto**  
  Free University of Bozen-Bolzano, Italy  
  giovanni.prenigotto@unibz.it

- **Jerome H. Kampf**  
  Idiap Research Institute, Switzerland  
  jerome.kaempf@idiap.ch

---

## Citation

If you use this dataset, workflow, or derived 3D models, please cite the related publication:

```bibtex
@article{borelli_3dcitydb_workflow,
  title  = {A 3DCityDB-Based Workflow for Scalable Urban Building Energy Modeling from Limited GIS Data},
  author = {Borelli, Gregorio and Gasparella, Andrea and Pernigotto, Giovanni and Kampf, Jerome H.},
  note   = {}
}
```

## Disclaimer

The datasets are provided for research and reproducibility purposes.

Although care was taken during the reconstruction and post-processing workflow, the generated 3D geometries may contain errors or simplifications due to:

- source data quality
- point cloud density
- building footprint accuracy
- roof reconstruction limitations
- post-processing assumptions

Users should validate the data before using it for planning, engineering, legal, or operational purposes.

---

## Contact

For questions about the dataset, workflow, or related publication, please contact:

**Gregorio Borelli**  
Free University of Bozen-Bolzano, Italy & Idiap Research Institute, Switzerland  
gregorio.borelli@student.unibz.it
