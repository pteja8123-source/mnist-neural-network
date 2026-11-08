# MNIST Neural Network

A Week 3 deep-learning project that builds a small **PyTorch neural network** to classify handwritten digits from 0 to 9.

## Project objectives

- Prepare image data for a neural network.
- Train a small multilayer perceptron.
- Plot training and validation loss and accuracy over epochs.
- Inspect the training/validation gap for signs of overfitting.
- Evaluate the selected model on a separate test set.

## Dataset

[MNIST](https://keras.io/api/datasets/mnist/) contains 28 × 28 grayscale images of handwritten digits. The notebook downloads the NumPy archive used by the official Keras loader and trains the network using PyTorch.

- Training: 54,000 images.
- Validation: 6,000 images, stratified from the original development set.
- Test: the official 10,000-image test set.
- Pixel normalization: divide by 255 to obtain values in [0, 1].

Dataset attribution: Yann LeCun and Corinna Cortes. See the linked MNIST documentation for dataset licensing information.

## Model and training configuration

```text
Flatten (28 × 28 → 784)
Linear (784 → 128)
ReLU
Dropout (0.20)
Linear (128 → 64)
ReLU
Linear (64 → 10)
```

- Library: PyTorch.
- Optimizer: Adam, learning rate 0.001.
- Loss: cross-entropy.
- Epochs: 15.
- Batch size: 256.
- Random seed: 42.
- Device: CPU; a GPU is not required.

The notebook selects the checkpoint with the lowest validation loss, then evaluates it on the test set. Training and validation curve metrics are both calculated in evaluation mode after each epoch so dropout does not distort their comparison.

## Evaluation and visualizations

The notebook includes code for:

- Training and validation loss curves.
- Training and validation accuracy curves.
- Test accuracy and cross-entropy loss.
- Macro precision, recall, and F1-score.
- A per-class classification report and confusion matrix.
- Sample predictions and misclassified images.

## Execution status and results

**The supplied notebook is unexecuted. No measured accuracy, training curves, or other results are included yet.** Run all cells to generate them. The final cell exports actual epoch metrics to `artifacts/training-history.csv` and configuration/results to `artifacts/run-summary.json`.

Before submitting, save the executed notebook with outputs and replace this status section with the measured results. Do not treat the configured training procedure as a completed experiment.

## Run in Google Colab

1. Download `mnist-neural-network.ipynb` from this repository.
2. Open [Google Colab](https://colab.research.google.com/).
3. Select **File → Upload notebook** and choose the file.
4. Select **Runtime → Run all**.
5. Check that training completes and the curves appear.
6. Download the executed notebook with outputs and upload it to this repository.

Internet access is required for the first dataset download. Colab normally includes the required libraries; install any missing packages using the command below.

## Run locally

```bash
pip install torch numpy pandas matplotlib scikit-learn notebook
jupyter notebook mnist-neural-network.ipynb
```

Run all cells from the top. Results may vary between package versions and hardware, even with fixed seeds.

## Repository structure

```text
mnist-neural-network/
├── mnist-neural-network.ipynb
└── README.md
```

Running the notebook creates `data/` for the dataset and `artifacts/` for generated results.

## Learning focus and limitations

The project introduces normalization, nonlinear activations, dropout, backpropagation, batching, and validation-based checkpoint selection. A widening training/validation gap or rising validation loss can indicate overfitting. Dropout is included as regularization, but no comparison without dropout is performed, so its effect cannot be isolated here.

One seed and one validation split do not quantify uncertainty. MNIST images are centered and grayscale; results on this benchmark do not establish performance on phone photos or other handwriting sources. A small convolutional neural network is a possible next experiment.

## References

- [MNIST documentation](https://keras.io/api/datasets/mnist/).
- [Official Keras MNIST loader and archive URL](https://github.com/keras-team/keras/blob/master/keras/src/datasets/mnist.py).
- [PyTorch optimization tutorial](https://docs.pytorch.org/tutorials/beginner/basics/optimization_tutorial.html).

Prepared for the SkillAudit.ai internship, Week 3.
