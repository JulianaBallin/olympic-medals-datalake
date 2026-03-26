# Olympic Medals Data Lake

![Data Lake Architecture](https://via.placeholder.com/1200x400/1e3c72/ffffff?text=Olympic+Medals+Data+Lake)

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 1️⃣ Overview

This project implements a **local Data Lake** for Olympic Games medal data, integrating historical results (1896–2022) with the Paris 2024 Summer Olympics. The lake follows a **medallion architecture** (`raw` → `bronze` → `gold`), ensuring data quality, traceability, and reusability. Each dataset is accompanied by **JSON metadata**, and all transformations are documented in **Jupyter notebooks**. Final outputs include consolidated medal rankings, modality analyses, and gender‑based insights.

**Key features:**
- Ingestion of two public datasets (CSV)
- Conversion to **Parquet** for efficient storage
- **Metadata** for every dataset (source, fields, description)
- **Integration** of historical and 2024 data via joins
- **Gold‑layer analyses** with visualizations (medal tables, bar charts)
- Fully reproducible pipeline

---

## 2️⃣ Data Sources

| Dataset | Period | Source |
|---------|--------|--------|
| **Historical Olympics** | 1896 – 2022 | [Base dos Dados](https://basedosdados.org/dataset/62f8cb83-ac37-48be-874b-b94dd92d3e2b) |
| **Paris 2024** | 2024 | [Kaggle – Paris 2024 Olympic Summer Games](https://www.kaggle.com/datasets/piterfm/paris-2024-olympic-summer-games/data) |

Both datasets are placed in the `raw/` directory, each with a companion JSON metadata file.

---

## 3️⃣ Data Lake Structure

![Folder Structure](https://via.placeholder.com/800x400/2c3e50/ffffff?text=Directory+Tree+Preview)

```
olympic-medals-datalake/
├── README.md
├── metadata_schema.json
├── raw/
│   ├── olympics_historico.csv
│   ├── olympics_paris2024.csv
│   ├── olympics_historico.json
│   └── olympics_paris2024.json
├── bronze/
│   ├── medalhas_1986_2024.parquet
│   ├── medalhas_1986_2024.csv
│   ├── medalhas_1986_2024.json
│   ├── modalidades_1986_2024.csv
│   ├── modalidades_1986_2024.json
│   ├── atletas_por_sexo.csv
│   └── atletas_por_sexo.json
├── gold/
│   ├── analise_medalhas/
│   │   ├── medalhas_verao.csv
│   │   ├── medalhas_inverno.csv
│   │   ├── medalhas_total.csv
│   │   ├── medalhas_plot.png
│   │   ├── notebook.ipynb
│   │   └── metadata.json
│   ├── analise_modalidades/
│   │   └── ... (similar structure)
│   └── analise_genero/
│       └── ...
└── notebooks/
    ├── 01_conversao_parquet.ipynb
    ├── 02_integracao_bronze.ipynb
    └── 03_quadro_medalhas_gold.ipynb
```

**Layers explained:**
- **`raw/`** – original CSV files untouched, with JSON metadata.
- **`bronze/`** – data converted to Parquet, plus integrated datasets (union, joins) and their metadata.
- **`gold/`** – final analysis outputs (rankings, plots, summaries) organized by analysis topic.
- **`notebooks/`** – step‑by‑step Jupyter notebooks that build the entire pipeline.

---

## 4️⃣ How to Run

### Prerequisites
- Python 3.9+
- `pip install pandas pyarrow jupyter matplotlib`

### Steps
1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/olympic-medals-datalake.git
   cd olympic-medals-datalake
   ```

2. **Place the datasets**  
   Download the two CSV files and save them into `raw/`.  
   Ensure filenames match those expected in the notebooks (`olympics_historico.csv`, `olympics_paris2024.csv`).

3. **Run the notebooks in order**  
   Launch Jupyter:
   ```bash
   jupyter notebook notebooks/
   ```
   Execute sequentially:
   - `01_conversao_parquet.ipynb` – converts CSVs to Parquet and copies metadata to `bronze/`.
   - `02_integracao_bronze.ipynb` – performs joins and creates the three bronze‑layer datasets.
   - `03_quadro_medalhas_gold.ipynb` – generates medal rankings, plots, and saves them in `gold/analise_medalhas/`.

4. **Explore the results**  
   Check the `gold/` folder for CSV tables and PNG charts.

---

## 5️⃣ Results

### Medal Tables (Top 10 example)
| Country | Gold | Silver | Bronze | Total |
|---------|------|--------|--------|-------|
| United States | 1061 | 830 | 738 | 2629 |
| Soviet Union | 395 | 319 | 296 | 1010 |
| Germany | 305 | 305 | 312 | 922 |
| ... | ... | ... | ... | ... |

![Medal Plot](https://via.placeholder.com/800x400/4CAF50/ffffff?text=Medal+Ranking+Bar+Chart)

### Modality Participation
![Modality Analysis](https://via.placeholder.com/800x400/2196F3/ffffff?text=Top+Disciplines+by+Medal+Count)

### Gender Distribution
![Gender Analysis](https://via.placeholder.com/800x400/FF9800/ffffff?text=Athletes+by+Gender+Over+Time)

---

## 6️⃣ Metadata Schema

Every dataset in the lake includes a JSON file describing its content. The common schema is defined in `metadata_schema.json` and follows this structure:

```json
{
  "nome_dataset": "string",
  "fonte": "string",
  "descricao": "string",
  "campos_principais": ["field1", "field2"],
  "data_criacao": "YYYY-MM-DD",
  "observacoes": "string"
}
```

This ensures machine‑readable documentation and easy discovery.

---

## 7️⃣ Author

**Juliana Ballin**  
[GitHub Profile](https://github.com/julianaballin) (placeholder)  
Project developed as part of a Data Engineering activity.

---

## 8️⃣ License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

**Happy exploring!** 🏅
