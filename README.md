# Gaming QoE Conference - Paper Reproduction

This repository contains the code and data needed to reproduce the experiments from our Gaming Quality of Experience research paper.

## 📋 Quick Start

### Prerequisites
- Python 3.11+ 
- pip or conda

### Installation

1. Clone this repository:
```bash
git clone <repository-url>
cd gaming-qoe-conference
```

2. **Request Dataset Access**: Contact the authors via email to obtain the preprocessed datasets required for reproduction. The datasets include:
   - `window_3_*.csv` (3-second windows)
   - `window_5_*.csv` (5-second windows) 
   - `window_10_*.csv` (10-second windows)
   - `window_15_*.csv` (15-second windows)

   Place these files in an `output/` directory in the repository root.

3. Create a virtual environment and install dependencies:
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### Running the Experiments

**Option 1: Full Paper Reproduction**
```bash
jupyter lab paper_repro.ipynb
```
Run all cells to reproduce the complete paper experiments.

**Option 2: Quick Validation**
```bash
python test_minimal_repro.py
```
Runs a minimal test to verify the setup is working.

**Option 3: Environment Validation**
```bash
python paper_repro_utils.py
```
Validates that all dependencies and datasets are available.

## �� Expected Results

### Main Experiment (3-Class QoE Classification on 10s Windows)
| Model | Accuracy | Macro F1 | Weighted F1 |
|-------|----------|----------|-------------|
| SVM | 82.46% | 81.04% | 81.40% |
| Random Forest | 82.22% | 81.37% | 81.54% |
| XGBoost | 81.21% | 80.39% | 80.52% |
| Logistic Regression | 77.19% | 75.36% | 75.65% |
| Decision Tree | 74.47% | 74.17% | 74.06% |

### Window Size Sensitivity Analysis
| Window Size | XGBoost Accuracy |
|-------------|------------------|
| 3s | 76.66% |
| 5s | 78.98% |
| 10s | 81.21% |
| 15s | 82.30% |

## 📁 Generated Artifacts

After running paper_repro.ipynb, the following files will be created:

### Tables
- artifacts/tables/results_3class_metrics.csv - Complete metrics for all models
- artifacts/tables/window_sensitivity_results.csv - Window size analysis results

### Figures  
- artifacts/figures/confusion_matrix_*.png - Confusion matrices for each model
- artifacts/figures/window_size_metrics.png - Window sensitivity plot

### Reproducibility
- artifacts/run_versions.txt - Environment and library versions
- artifacts/run_versions.json - Machine-readable version info

## 🔬 Methodology

### Data Splitting Strategy
We use **experiment-based splitting** where every 4th experiment is reserved for testing. This ensures:
- No data leakage between training and testing sets
- Test data comes from completely unseen gaming sessions  
- More realistic and conservative performance estimates
- Results that reflect true generalization capability

### Feature Engineering
- **30 network traffic features** extracted from gaming sessions
- Features include packet sizes, packet rates, and directional ratios
- Data from multiple window sizes (3s, 5s, 10s, 15s)

### QoE Classification
- **3-class QoE prediction** based on ping latency thresholds
- Classes: Good (Class 1), Fair (Class 2), Poor (Class 3)
- Evaluation using accuracy, macro F1, and weighted F1 scores

## 📦 Repository Structure

```
gaming-qoe-conference/
├── paper_repro.ipynb          # Main reproduction notebook
├── model_utils.py             # ML model utilities
├── rank.py                    # QoE ranking functions  
├── requirements.txt           # Python dependencies
├── output/                    # Preprocessed datasets (request from authors)
│   ├── window_3_*.csv        # 3-second window data
│   ├── window_5_*.csv        # 5-second window data  
│   ├── window_10_*.csv       # 10-second window data
│   └── window_15_*.csv       # 15-second window data
├── paper_repro_utils.py       # Validation utilities
├── test_minimal_repro.py      # Minimal test script
└── LICENSE                    # License file
```

## �� Troubleshooting

### Common Issues

**ModuleNotFoundError**
```bash
pip install -r requirements.txt
```

**Dataset not found**
Ensure all CSV files are present in the `output/` directory. If you don't have the datasets, please contact the authors via email to request access.

**Memory issues**
The notebooks require ~2GB RAM. Close other applications if needed.

### Validation Commands

Check environment setup:
```bash
python paper_repro_utils.py
```

## 📄 Citation

If you use this code or data in your research, please cite our paper:

```bibtex
@article{your-paper-2025,
  title={Gaming Quality of Experience Research},
  author={Your Name},
  journal={Conference Name},
  year={2025}
}
```

## 🤝 Contributing

This repository is designed for paper reproduction. For questions or issues:
1. Check that all dependencies are installed correctly
2. Verify dataset files are present and accessible
3. Run the validation utilities to diagnose problems

## 📞 Contact

### Dataset Access
To request access to the preprocessed datasets required for reproduction, please contact the authors via email. Include the following information:
- Your name and institutional affiliation
- Intended use of the datasets (research, education, etc.)
- Brief description of your research interests

**Email**: [yehonata.zion@msmail.ariel.ac.il]

### General Questions
For questions about the reproduction process, please open an issue in this repository.

---

**Note**: This repository contains only the code and preprocessed data needed for reproduction. The original raw gaming data and exploratory analysis are not included to maintain participant privacy and repository size.
