# Zero-Day IoT Network Intrusion Detection

## Overview
Traditional ML models achieve high accuracy on known attacks but struggle with novel, 
unseen threats. This project evaluates five machine learning models under a strict 
zero-day protocol on the CIC-IoT-2023 dataset, where six attack types are completely 
withheld from training to simulate real-world unknown threats.

## Published Research
**"Evaluating Machine Learning Model Robustness for Novel IoT Attack Detection"**  
Chandana B, Ravindra Kumar Singh, Sathish P K  
*MAI 2025 — 5th International Conference on Machine Vision and Augmented Intelligence*  
*Lecture Notes in Electrical Engineering, Springer (Accepted, In Press)*

## Dataset
**CIC-IoT-2023** — Canadian Institute for Cybersecurity  
- 33 attack types across 105 real IoT devices  
- 7 attack categories: DDoS, DoS, Recon, Web-based, Brute Force, Spoofing, Mirai  
- 97.6% attack traffic (heavily imbalanced)

## Zero-Day Simulation Protocol
Six attack types completely withheld from training:

| Attack | Family |
|--------|--------|
| ddos-rstfinflood | DDoS |
| ddos-slowloris | DDoS |
| dictionarybruteforce | Brute Force |
| dos-http_flood | DoS |
| recon-osscan | Reconnaissance |
| vulnerabilityscan | Reconnaissance |

## Models Compared
- Random Forest (supervised)
- Logistic Regression (supervised)
- Vanilla Autoencoder (unsupervised)
- Denoising Autoencoder (unsupervised)
- Supervised Autoencoder (hybrid)

## Key Results

### Overall Performance
| Model | Accuracy | F1 Score |
|-------|----------|----------|
| Random Forest | 98.96% | 97.33% |
| Supervised AE | 98.71% | 96.68% |
| Logistic Regression | 98.23% | 95.40% |
| Vanilla AE | 97.53% | 93.79% |
| Denoising AE | 96.53% | 91.15% |

### Zero-Day Detection Gap (Seen vs Unseen)
| Model | Accuracy Gap | Unseen Accuracy |
|-------|-------------|-----------------|
| Denoising AE | **4.52%** | 85.31% |
| Vanilla AE | 9.80% | 84.38% |
| Supervised AE | 9.94% | 84.84% |
| Logistic Regression | 13.69% | 79.69% |
| Random Forest | 15.17% | 81.25% |

Random Forest achieves the best overall accuracy but the largest drop on unseen 
attacks. Denoising Autoencoder has the smallest gap, indicating better 
generalisation to novel threats.

## Dataset Split
- Total: ~160,000 samples (stratified)
- Train/Val/Test: 70:15:15
- Training: 90,000 benign + 8,806 seen attack samples (27 types)
- Test: includes 640 unseen attack samples from 6 withheld types
- z-score normalization — scaler fit on training data only

## Notebooks
| File | Description |
|------|-------------|
| `PaperFinal.ipynb` | All 5 models — training, evaluation, zero-day gap analysis |

## Tech Stack
- Python, Pandas, NumPy, Scikit-learn
- TensorFlow / Keras
- Matplotlib, Seaborn

## License
MIT License — free to use with attribution.
