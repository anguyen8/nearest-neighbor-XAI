<!-- ----------------------------------------------------------- -->
<!--   PCNN: Probable-Class Nearest-Neighbor Explanations        -->
<!-- ----------------------------------------------------------- -->

<h2 align="center">
  PCNN: Probable-Class Nearest-Neighbor Explanations Improve<br/>
  Fine-Grained Image Classification Accuracy for AIs and Humans
</h2>

<h2 align="center">
  Transactions on Machine Learning Research
</h2>


<div align="center">
  <p style="font-size: 20px;">
    Giang Nguyen<sup>1*</sup>,
    Valerie Chen<sup>2</sup>,
    Mohammad Reza Taesiri<sup>3</sup>,
    Anh Nguyen<sup>1</sup>
  </p>
  <p>
    <sup>*</sup>Corresponding author · <sup>1</sup>Auburn University ·
    <sup>2</sup>Carnegie Mellon University · <sup>3</sup>University of Alberta
  </p>
</div>

<p align="center">
  <img src="figs/teaser.png" alt="PCNN teaser figure" width="80%"/>
</p>

---

## 📜 Abstract
> Nearest neighbors are traditionally used either to make final predictions (e.g. *k*-NN, SVMs) or to provide supporting evidence for a model’s decision.  
> **PCNN** takes a new path: we keep a pretrained image classifier **C** intact, then let an **image comparator** **S**
> 1. compare the query image against nearest neighbors drawn from each of the top-most probable classes, and  
> 2. re-weight **C**’s logits in a Product-of-Experts style.
  
> This simple plug-in consistently boosts accuracy on CUB-200, Cars-196, and Dogs-120.  
> A user study further shows that lay users make more accurate decisions when viewing PCNN’s *probable-class* neighbors versus seeing only top‑1‑class examples (prior work).

---

## 🗺️ Table of Contents
1. [Pre‑requisites & Pretrained Models](#pre-requisites--pretrained-models)
2. [Training Image‑Comparator Networks](#training-image-comparator-networks)
3. [Testing — Binary Classification & Re-ranking](#testing--binary-classification--re-ranking)
4. [Qualitative Visualizations](#qualitative-visualizations)
5. [Human‑Study Data](#human-study-data)
6. [Citation](#citation)

---

## Pre‑requisites & Pretrained Models
* Clone this repo and install the usual PyTorch / torchvision stack (CUDA 11+ recommended).  
* **Download** our pretrained backbones for CUB‑200, Cars‑196, and Dogs‑120  
  👉 <https://drive.google.com/drive/folders/1pC_5bEi5DryDZCaKb51dzCE984r8EnqW>

---

## Training Image‑Comparator Networks
### CUB‑200
1. In `params.py` set  
   ```python
   global_training_type = "CUB"
   self.set = "train"
   ```
2. Launch:
   ```bash
   sh train_cub.sh
   ```

### Cars‑196 & Dogs‑120
Same recipe; just set  
`global_training_type = "CARS"` **or** `"DOGS"`.

---

## Testing — Binary Classification & Re‑ranking
### CUB‑200
1. Edit `params.py`:
   ```python
   global_training_type = "CUB"
   self.set = "test"
   ```
2. Run:
   ```bash
   sh test_cub.sh
   ```

### Cars‑196 & Dogs‑120
Swap `global_training_type` to `"CARS"` or `"DOGS"` and execute the matching script to reproduce the main‑paper table:

<p align="center">
  <img src="figs/table1.png" alt="Main accuracy table" width="70%"/>
</p>

---

## Qualitative Visualizations
The following commands assume **CUB‑200**; substitute `"CARS"` / `"DOGS"` as needed.

| What you’ll see | How to run |
|-----------------|-----------|
| **Corrections** made by **S** | `python cub_visualize_corrections.py` <br/><img src="figs/correction1.png" width="270"/> |
| **Training pairs** used by **S** | `python cub_visualize_training_nns.py` <br/><img src="figs/training_pairs1.png" width="270"/> |
| **Failure cases** of **S**<br/>(set `VISUALIZE_COMPARATOR_CORRECTNESS=True`) | `python cub_infer.py` <br/><img src="figs/failure1.png" width="270"/> |
| Attention **heat‑maps**<br/>(set `VISUALIZE_COMPARATOR_HEATMAPS=True`) | `python cub_infer.py` <br/><img src="figs/heatmaps1.png" width="270"/> |

---

## Human‑Study Data
All stimuli for our CUB‑200 and Cars‑196 user studies are available at:  
<https://drive.google.com/drive/folders/1yNIOfypfy1vvI3Q3MAq9LNIVlyQ3WY-V>

---

## Citation
```bibtex
@article{
nguyen2024pcnn,
title={{PCNN}: Probable-Class Nearest-Neighbor Explanations Improve Fine-Grained Image Classification Accuracy for {AI}s and Humans},
author={Giang Nguyen and Valerie Chen and Mohammad Reza Taesiri and Anh Nguyen},
journal={Transactions on Machine Learning Research},
issn={2835-8856},
year={2024},
url={https://openreview.net/forum?id=OcFjqiJ98b},
note={}
}
```

---

<p align="center">🖼️ Questions? Open an issue or email nguyengiangbkhn@gmail.com 🖼️</p>
