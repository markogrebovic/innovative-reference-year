# innovative-reference-year
This is the code used in the analysis described in the paper Deep Sequence-Based Models for Generating Reference Climate Datasets in Buildings' Energy Efficiency Assessment submitted to PeerJ Computer Science. Includes data preprocessing, reference year extraction, and RNN model implementation.

# Deep Sequence-Based Models for Generating Enhanced Reference Climate Datasets in Buildings’ Energy Efficiency Assessment

## Description
Evaluating building energy efficiency typically relies on compact climate models—known as typical meteorological years (TMY) or reference years (RY)—rather than multi-decadal raw datasets. While standardized approaches based on Finkelstein-Schafer (FS) statistics (such as EN ISO 15927-4) select representative historical months, they often omit extreme climate trends and microclimatic variations.

This repository implements both the standardized FS statistical method and advanced deep sequence models—including Recurrent Neural Networks with Long Short-Term Memory (LSTM), Gated Recurrent Units (GRU), and hybrid 1D Convolutional-RNN architectures (Conv1D-LSTM, Conv1D-GRU)—in Python. Using 23 years (2002–2024) of daily meteorological data across four distinct climate zones in Montenegro (Podgorica, Nikšić, Bar, and Pljevlja), the deep learning models achieve over 25–30% accuracy improvements in temperature forecasting compared to the FS benchmark. Furthermore, dynamic heat flow rate density ($Q_h$ and $Q_c$) through a four-layer opaque wall is computed in accordance with **EN ISO 13786** to evaluate real-world engineering impacts.

## Dataset Information
The underlying daily meteorological data originates from the publicly available NOAA Global Surface Summary of the Day (GSOD) database. 

* **Coverage Period:** 2002–2024 (23 consecutive years).
* **Locations / Climate Zones (Montenegro):**
  * `PG` – Podgorica (Sub-Mediterranean climate, low elevation: 49 m).
  * `NK` – Nikšić (Continental/Mediterranean subtype, elevation: 647 m).
  * `BR` – Bar (Coastal Mediterranean climate, elevation: 6 m).
  * `PV` – Pljevlja (Humid continental climate, elevation: 784 m).
* **Features Included:** Daily mean temperature (`TEMP`), daily maximum temperature (`MAX`), daily minimum temperature (`MIN`), relative humidity (`RHUM`, converted from dew point `DEWP`), precipitation (`PRCP`), visibility (`VSB`), daily mean wind speed (`WDSP`), and maximum wind speed (`MXSPD`).
* **Data Splitting:**
  * **FS Method & DL Training/Validation:** 2002–2023.
  * **Model Testing / Verification:** 2024 (Leap day Feb 29 removed for 365-day compatibility).

## Code Information
The code base contains end-to-end Python scripts for climate data preprocessing, standard statistical generation, deep learning sequence modeling, and building dynamic thermal analysis.

* **FS Method Implementation:** Implements standardized CDF calculations and month selection per EN ISO 15927-4.
* **Deep Sequence Architectures:**
  * 1-layer and 2-layer LSTM / GRU models with layer sizes of 32, 64, and 128 neurons.
  * Hybrid Conv1D-RNN networks using 1D temporal convolution (kernel size $k=3$, stride $s=2$) for spatial-temporal downsampling.
  * Input & Output sequences: 365 time steps (predicting a full annual cycle).
* **Thermal Assessment Module:** Dynamic heat transfer matrix formulation according to EN ISO 13786 and EN ISO 52016-1 for calculating $Q_h$ (heating) and $Q_c$ (cooling) flux densities.

## Repository Setup

Clone the repository and navigate into the root directory:

```bash
git clone [https://github.com/markogrebovic/innovative-reference-year.git](https://github.com/markogrebovic/innovative-reference-year.git)
cd innovative-reference-year


## Requirements
The project relies on Python 3.8+ and standard scientific/deep learning packages:

```bash
numpy>=1.21.0
pandas>=1.3.0
scipy>=1.7.0
matplotlib>=3.4.0
seaborn>=0.11.0
tensorflow>=2.8.0
scikit-learn>=0.24.0
