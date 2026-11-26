# EEG-Based Modeling of Cognitive State and Workload in Architectural Design

Machine learning analysis of EEG-derived features during architectural design tasks, focusing on classification of task conditions and regression of self-reported cognitive workload in a small-sample dataset.

**Highlights:** Random Forest on two frontal EEG features reached **87.5% accuracy** on held-out participants (ChatGPT-assisted vs. non-AI design) · subject-aware cross-validation to avoid participant leakage · honest reporting of a negative workload-regression result

> Team project for **DS5006** at WPI by Xao Yiao, Touhid Islam, and Rachel Hurley.

## Dataset

- **34 participants**, each completing two ~30-minute architectural design phases:
  - **Task 1:** brain-only design
  - **Task 2:** revision using either conventional search or GenAI (ChatGPT)
- **EEG:** 16 wet electrodes over frontal, central, and parietal regions, sampled at 500 Hz
- **Workload:** post-task self-report survey
- **Modeling table:** one row per participant–task, with EEG-derived features and outcome variables

The raw EEG and survey data are not included in this repository because they are human-subjects data.

## Tools

Python · pandas · NumPy · scikit-learn (Random Forest, Logistic Regression, SVR, Ridge/Lasso/Elastic Net, PCA, GroupKFold) · matplotlib · seaborn · Google Colab

## Repository Contents

| File | Description |
|---|---|
| `Final project.ipynb` | Main analysis: feature engineering, classification, workload regression |
| `Window.ipynb` | Exploratory windowed-EEG analysis using a learned latent representation |
| `Final Project Report.docx` | Full written report |
| `Final presentation.pptx` | Class presentation slides |
| `methodology.png`, `output (1).png` | Figures used in this README |

## Methodology
<p align="center">
<img src="methodology.png" align="center" width="75%"/>
</p>



## 📊 Results

The strongest result was obtained for the **binary classification of ChatGPT-assisted vs. non-AI design tasks**. Initial models showed substantial overfitting, with testing accuracies of approximately **45–53%**. After reducing the feature space and focusing on frontal EEG activity, model generalization improved considerably.

### Classification Results

The final **Random Forest classifier** used only two EEG features:

- **Frontal θ/β slope**
- **Frontal (α+θ)/β slope**

Using subject-specific scaling, the final model achieved:

| Metric | Accuracy |
|---|---:|
| Training Accuracy | **95.8%** |
| Testing Accuracy | **86.7%** |
| Held-out Participant Accuracy | **87.5%** |

When evaluated on completely held-out participants, the model achieved **87.5% accuracy**, although the final test set contained only four participants.

These results suggest that changes in **frontal EEG activity over the full design session** may contain useful information for distinguishing AI-assisted from non-AI design conditions.

<p align="center">
  <img src="output (1).png" alt="EEG Classification Performance" width="850">
</p>

<p align="center">
  <em>Classification performance improved substantially after feature reduction and selection of frontal EEG features.</em>
</p>

### Workload Regression Results

The **workload regression task produced substantially weaker results**. PCA was used to reduce the high-dimensional EEG feature space, followed by comparison of several regression models including Ridge, Lasso, Elastic Net, Support Vector Regression (SVR), and Random Forest.

The best-performing model for the **Search/ChatGPT task** was SVR:

| Metric | Value |
|---|---:|
| Cross-validation R² | **−0.057** |
| Test R² | **−0.223** |

The negative R² values indicate that the regression models did **not generalize reliably to unseen participants**. Performance for the Brain-Only task was even weaker, suggesting that the available EEG features were insufficient for reliable prediction of self-reported workload in the current small-sample dataset.

### 🔑 Key Takeaway

> **EEG features showed promising predictive information for distinguishing ChatGPT-assisted from non-AI design conditions, but the available data did not support reliable prediction of self-reported cognitive workload.**

The classification results indicate that a small set of **frontal EEG features** may capture useful differences between AI-assisted and non-AI design conditions. However, because of the small dataset—particularly the limited held-out test sample—these findings should be interpreted as **preliminary evidence rather than definitive proof of generalizable EEG markers of AI-assisted design cognition**.

## License

Released under the [MIT License](LICENSE).

## Contact

Touhid Islam · tislam@wpi.edu
