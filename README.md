# Temperature Control-Enabled Programmable One-Pot Polymerase-Mediated DNA Synthesis
Temperature Control-Enabled Programmable One-Pot Polymerase-Mediated DNA Synthesis

---

# TEMPER: NGS Data Analysis Pipeline

Code repository for the NGS data analysis pipeline used in:
**"Programmable One-Pot Polymerase-Mediated DNA Synthesis Via Temperature Control"** *(Nature Communications, Under Revision)*.

## About the Project
**TEMPER** (TEmperature Mediated Programmable Enzymatic Reaction) is a terminator-free, one-pot enzymatic DNA synthesis method that uses temperature control to manage primer binding and product stability. 

This repo contains the dry-lab workflows used to process the raw sequencing data, decode the stored binary information, and reconstruct environmental temperature histories as demonstrated in the manuscript.

---

## Pipeline Overview

The scripts are organized into three main parts, mirroring the key applications in the paper:

### 1. Multi-Stage Synthesis & Scalability
Used to process large batches of NGS data to evaluate the system's scalability.
* **`step_1_6_NGS.ipynb` & `step_7_12_NGS.ipynb`**: Handles raw FASTQ preprocessing (quality control, merging, and mapping). It generates stacked bar charts comparing the target sequences (Top 5) against background noise.
* **`combine_all_step.ipynb`**: Merges the histogram data and read counts from all batches into a single CSV (`highlight_result.csv`). It also plots the final, publication-ready stacked bar graphs (`.png`, `.svg`).

### 2. DNA Data Storage (Accuracy & Decoding)
Scripts for decoding binary data and calculating bit-wise synthesis accuracy.
* **`DNA_data_storage_analysis_stage1.ipynb`**: Runs initial QC and FLASH merging to generate histograms. *Note: You need to run this first to find the optimal merge length (N-value) for your specific library.*
* **`DNA_data_storage_analysis_stage2.ipynb`**: Splits reads using the N-value found in Stage 1. It calculates the bit-wise frequencies of '0's and '1's, and computes the overall decoding accuracy to check for directional bias (e.g., 0→1 vs 1→0 errors).

### 3. Temperature Data Logger
Used for the environmental temperature monitoring application.
* **`Logger_analysis.ipynb`**: Calculates the ratio of Low (L) vs. High (H) temperature-dependent sequences. Outputs a normalized stacked bar chart (0–1 scale) to visualize the temperature exposure history.

---

## Dependencies

These notebooks are designed for a Linux/Ubuntu environment. The cells include `apt-get` commands for the necessary bioinformatics tools.
* **CLI Tools**: `fastp`, `flash`, `bwa`, `samtools`
* **Python Packages**: `pandas`, `numpy`, `biopython`, `pysam`, `matplotlib`

---

## Usage Guide

To reproduce the data from the paper, run the notebooks in the following order depending on your target application:

**For Batch Synthesis & Visuals:**
1. Run the `step_1_6` and `step_7_12` notebooks on your raw FASTQ files.
2. Run `combine_all_step.ipynb` to aggregate the metrics and plot the final graphs.

**For Data Storage & Accuracy:**
1. Run `stage1.ipynb` to determine your library's **N-value**.
2. Open `stage2.ipynb`, update the `sample_n_mapping` variable with your N-value, and run the notebook to get the final bit-wise accuracy report (`summary_combined.csv`).

**For the Temperature Logger:**
1. Run `Logger_analysis.ipynb` to extract the L/H base ratios and generate the temperature history plots.

---

## Reference
* **Title**: Programmable One-Pot Polymerase-Mediated DNA Synthesis Via Temperature Control
* **Authors**: Jinho Kim*, Jangho Choi*, Woojin Kim, Namjin Cho, Yushin Jung, Seongjun Park, Eunjin Choi, Chaerim Lee, Youngeun Kim, Taehoon Ryu, Hansol Choi, and Yeongjae Choi. (* Equal contribution)
* **Journal**: *Nature Communications* (Under Revision)
* **Contact**: hansol.choi@ewha.ac.kr (H.C.) / yeongjae@kaist.ac.kr (Y.C.)
