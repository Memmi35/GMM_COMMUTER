# Commuter Flow Estimation with Gaussian Mixture Models (GMM)

This repository contains the implementation, experiments, and results of my internship project on **cross-border commuter flow estimation** using **Gaussian Mixture Models (GMM)**.  
The work reproduces and extends the methodology presented in the reference paper:

> **Reference:**  
> [Extracting Commuters from Automated Road Traffic Counters: A Gaussian Mixture Approach*](https://www.researchgate.net/publication/391702221_Extracting_Commuters_from_Automated_Road_Traffic_Counters_A_Gaussian_Mixture_Approach)  
>

---

## 📂 Repository Structure

```
COMMUTER_GMM/
│
├── data/                    # Zipped datasets and preprocessed data for each corridor
│   ├── FinSwe_GMM.zip
│   ├── NorSwe_GMM.zip
│   └── DenSwe_GMM.zip
│
├── notebooks/               # Main analysis notebooks
│   ├── 00_data_overview.ipynb          # Overview of datasets, basic statistics
│   ├── 10_fit_gmm_fin_swe.ipynb        # Fit GMM for FIN–SWE
│   ├── 11_fit_gmm_nor_swe.ipynb        # Fit GMM for NOR–SWE
│   ├── 12_fit_gmm_den_swe.ipynb        # Fit GMM for DEN–SWE
│   ├── 20_daily_gmm_fin_swe.ipynb      # Daily GMM estimation (FIN–SWE)
│   ├── 21_eval_nor_swe.ipynb           # Evaluation metrics (NOR–SWE)
│   ├── 22_daily_gmm_den_swe.ipynb      # Daily GMM estimation (DEN–SWE)
│   ├── 30_eval_fin_swe.ipynb           # Compute KL, LLR, RMSE, MSE for FIN–SWE
│   ├── 31_eval_nor_swe.ipynb           # (Partial: KL only, LLR/RMSE not computed)
│   └── 32_eval_den_swe.ipynb           # Compute KL, LLR, RMSE, MSE for DEN–SWE
│
├── results/                 # Plots, tables, and saved results
│   └── GMM_methodology.pdf  # Methodological description and findings
│
└── requirements.txt         # Python dependencies
```

---

## 🧠 Methodology

- **Gaussian Mixture Models (GMM):**  
  Each weekday distribution is modeled as a mixture of Gaussians, fitted via the EM algorithm.
- **KL Divergence & Log-Likelihood Ratio:**  
  Metrics quantify divergence from baseline weekday profiles.
- **Daily Models:**  
  GMMs are fitted per-day to capture event-specific disruptions (holidays, COVID effects).
- **Visualization:**  
  Includes commuter share estimation, peak timing plots, and daily/weekly KL evolution.

---

## 📊 Results & Key Notes

- **FIN–SWE** and **DEN–SWE** corridors include full computation of:
  - KL divergence (daily + 7-day moving average)
  - Log-likelihood ratio (LLR)
  - RMSE & MSE between model and observed counts

- **NOR–SWE corridor:**  
  - Only KL divergence is computed.
  - **LLR, RMSE, and MSE were not calculated** because the official preprocessing code assigns any count `<= 50` as `NaN`, leading to too many missing values for reliable estimation.

---

## ⚙️ Setup

### 1. Clone the repository
```bash
git clone https://github.com/Memmi35/GMM_COMMUTER.git
cd GMM_COMMUTER
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the notebooks

Open JupyterLab or VSCode and explore the notebooks in order (start with `00_data_overview.ipynb`).

---

## 📈 Example Outputs

* **KL Divergence:** Detects distribution shifts during holidays and disruptions.
* **Commuter Share Plots:** Identify morning/evening commuting peaks.
* **Peak-based Error Metrics:** RMSE and MSE reported for FIN–SWE and DEN–SWE.

---

## 📌 Notes & Limitations

* The repository contains **reproducible pipelines** but is not fully automated — notebooks must be run manually in order.
* NOR–SWE evaluation metrics are **partially missing** for reasons explained above.
* Computations were performed using Google Colab (T4 GPU).

---

## 📚 Citation

If you use this code or methodology in your own work, please cite the reference paper and mention this repository.

```bibtex
@misc{gmm_commuter2023,
  author       = {Fares Memmi},
  title        = {Commuter Flow Estimation with Gaussian Mixture Models (GMM)},
  year         = {2025},
  url          = {https://github.com/Memmi35/GMM_COMMUTER},
  note         = {Reproduction and evaluation of GMM baseline for cross-border commuter traffic.}
}
```

---

## 📜 License

This project is released under the MIT License. See [LICENSE](LICENSE) for details.
