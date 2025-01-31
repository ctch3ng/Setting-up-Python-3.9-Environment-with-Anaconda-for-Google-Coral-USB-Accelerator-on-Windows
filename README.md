# Setting up Python 3.9 Environment with Anaconda for Google Coral USB Accelerator on Windows

This document provides a guide for creating and using a Python 3.9 virtual environment with Anaconda on Windows to run models with Google's Coral USB Accelerator. It references the official [Coral documentation](https://coral.ai/docs/accelerator/get-started/#1-install-the-edge-tpu-runtime) and demonstrates how to verify the setup with a sample classification script.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Create and Activate the Anaconda Environment](#create-and-activate-the-anaconda-environment)
4. [Install Coral Dependencies](#install-coral-dependencies)
5. [Clone the PyCoral Repository and Install Additional Requirements](#clone-the-pycoral-repository-and-install-additional-requirements)
6. [Run a Sample Classification](#run-a-sample-classification)

---

<a id="introduction"></a>
## 1. Introduction

Google’s Coral USB Accelerator provides an Edge TPU for accelerating machine learning inference on-device. While many examples focus on Linux environments, it is possible to make it work on Windows with Anaconda. This guide will help you set up Python 3.9 in a new Anaconda environment, install the required packages, and run a classification example to confirm that the Coral USB Accelerator is functioning correctly.

---

<a id="prerequisites"></a>
## 2. Prerequisites

- A Windows system with [Anaconda](https://www.anaconda.com/) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) already installed.
- The Google Coral USB Accelerator and its corresponding driver/firmware package, which can be downloaded from the [Edge TPU Runtime](https://coral.ai/docs/accelerator/get-started/#1-install-the-edge-tpu-runtime) site.
- Basic knowledge of using the command line on Windows (Anaconda Prompt or a similar terminal).

**Important Note**: After downloading the Edge TPU runtime ZIP file, right-click on the file, select **Properties**, and click **Unlock** under Attributes before unzipping.

---

<a id="create-and-activate-the-anaconda-environment"></a>
## 3. Create and Activate the Anaconda Environment

Open an **Anaconda Prompt** (or any terminal that has conda available) and run:

```bash
conda create -n py39_coral python=3.9 -y
conda activate py39_coral
```

This creates a new environment named `py39_coral` and activates it, ensuring that any further Python installations happen within this isolated environment.

---

<a id="install-coral-dependencies"></a>
## 4. Install Coral Dependencies

Within the activated environment, install PyCoral and other required packages:

```bash
pip install --extra-index-url https://google-coral.github.io/py-repo/ pycoral~=2.0 numpy<2
```

If you have not already installed Git, you can do so by:

```bash
conda install git
```

---

<a id="clone-the-pycoral-repository-and-install-additional-requirements"></a>
## 5. Clone the PyCoral Repository and Install Additional Requirements

Create a folder and clone the PyCoral repository:

```bash
mkdir coral
cd coral
git clone https://github.com/google-coral/pycoral.git
cd pycoral
```

Then, install any extra requirements needed for the sample scripts. For the image classification example:

```bash
bash examples/install_requirements.sh classify_image.py
```

---

<a id="run-a-sample-classification"></a>
## 6. Run a Sample Classification

To verify the setup, run the sample classification script:

```bash
python examples/classify_image.py \
  --model test_data/mobilenet_v2_1.0_224_inat_bird_quant_edgetpu.tflite \
  --labels test_data/inat_bird_labels.txt \
  --input test_data/parrot.jpg
```

If everything is configured correctly, you should see an output describing the bird species inferred from the provided image.

