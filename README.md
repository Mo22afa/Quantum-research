# Hybrid Quantum–Classical Malaria Detection

Research notebook comparing a fine-tuned EfficientNetB0 CNN, a classical MLP, and an 8-qubit hybrid quantum–classical classifier for malaria blood-cell image classification.

## Final test results

Evaluated on **4,134** images using the default classification threshold of 0.5.

| Model | Accuracy | Precision (infected) | Recall (infected) | F1 (infected) | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| CNN | 95.28% | 97.11% | 93.43% | 95.24% | 98.92% |
| Classical MLP | 95.09% | 97.15% | 93.00% | 95.03% | 98.93% |
| Hybrid Quantum | 95.26% | 96.64% | 93.86% | 95.23% | 98.88% |

**No demonstrated quantum advantage:** the hybrid model performed comparably to the classical CNN.

## Research pipeline

1. TensorFlow Datasets Malaria (27,558 cell images).
2. Image-level split into training (19,291), validation (4,133), and test (4,134).
3. Image preprocessing and fine-tuning of ImageNet-pretrained EfficientNetB0.
4. Extraction of 128-dimensional CNN features and training-only feature standardization.
5. Hybrid classifier with **8 qubits**, **3 variational layers**, and **72 quantum trainable parameters**, simulated using PennyLane / PyTorch.
6. Classical MLP baseline trained on the same features.
7. Validation and final-test comparisons using accuracy, precision, recall, F1, F2, ROC-AUC, and missed infections.

**Label mapping:** `0` = infected/parasitized, `1` = uninfected.

## Run

Open [Quantum_Malaria_Research.ipynb](Quantum_Malaria_Research.ipynb) in Google Colab and run the cells in order. Training the quantum simulator can be slow.

The notebook downloads the dataset and pretrained image weights. Training checkpoints created under `/content` are not included in this repository, so execute training to regenerate the models.

## Limitations

- The split is at image level; **patient-level isolation is not verified**, so data leakage across splits is possible.
- Training performance was not validated across repeated random seeds.
- Quantum computation uses a simulator rather than real quantum hardware.
- Notebook outputs reflect the uploaded run; the entire workflow has not been independently rerun here.
- Research prototype only; not intended for clinical diagnosis.

## References

- [TensorFlow Datasets — Malaria](https://www.tensorflow.org/datasets/catalog/malaria)
- Rajaraman et al. (2018). *Pre-trained convolutional neural networks as feature extractors toward improved malaria parasite detection in thin blood smear images*. [PeerJ](https://doi.org/10.7717/peerj.4568).
