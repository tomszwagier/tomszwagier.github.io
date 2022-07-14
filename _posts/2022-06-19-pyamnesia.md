---
title: 'pyAMNESIA'
subtitle: 'Work during my research internship at Cossart Lab'
date: 2022-06-19
permalink: /posts/2022/06/pyamnesia/
tags:
  - neuroscience
  - calcium imaging
  - image processing
  - python package
---

**pyAMNESIA** is a **py**thon pipeline for analysing the **A**ctivity and **M**orphology of **NE**urons using
**S**keletonization and other **I**mage **A**nalysis techniques.

*[Theo Dumont](https://theodumont.github.io/) and I developed this python toolbox during a research internship at
 [CENTURI](https://centuri-livingsystems.org/), [INMED](https://www.inmed.fr/en), 
 [Cossart lab](https://www.inmed.fr/en/developpement-des-microcircuits-gabaergiques-corticaux-en). For more information,
  you can check the official documentation of our toolbox [pyAMNESIA](https://pyamnesia.readthedocs.io/en/latest
 /overview_introduction.html).*

---

# Motivation
In the context of studying the mechanisms by which hippocampal assemblies evolve during the development of mice 
(5 to 12 days), we dispose of some two-photon calcium imaging videos, such as this one:

![Alt Text](/images/posts/pyamnesia/calcium_imaging.gif)
*A two-photon calcium imaging movie.*

The analysis of these calcium imaging videos may be split into two different parts:

- the evolution of the **morphology**, being the number of elements (somata, neurites...) and their visible connexions;
- the evolution of the **neuronal activity**, being the transients characteristics and the coactivity of the aforementioned elements.

In the state-of-the-art calcium imaging pipelines such as [Suite2p](https://github.com/MouseLand/suite2p) and [CaImAn
](https://github.com/flatironinstitute/CaImAn), somata are segmented to subsequently
 study the evolution of their activity. In such cases, pixels in the region of a soma can reliably be considered as coactive, making the soma a *morphological* **and** *functional* entity.

Here, we want to study the **whole neural structure** of the hippocampus; not only the somata but also the neurites linking them. And there is **no obvious correlation** between the morphological "branches" that one can see on the videos, and the neurites, that are coactive functional entities. This is mainly due to the Z-axis projection - which "hides" vertical neurites and creates overlaps - but also to imaging hazards, or simply neurites that only activate partially during a neural transmission. Therefore, we do not know *a priori* whether a visible "branch" is a functional entity or not. We thus need to **separate** the morphological and the functional approaches, and try to build some **coherent structures** that could be considered as entities, in order to analyse their **coactivity** later.

Here is the problem we are trying to answer:

How can we use calcium imaging to get **statistics** on the evolution of interneurons in the hippocampus (morphology *and* activity) during **mice development**?
- **input:** a calcium imaging ``.tif`` sequence
- **output:** clusters of coactive pixels & morphological statistics


# Functionalities

We split our approach in three parts:

![Alt Text](/images/posts/pyamnesia/structure.png)
*Structure of the approach*

1. The `skeletonization` module focuses on the **morphological** analysis of the data, by computing the underlying *morphological skeleton* of the sequence.
2. The`clustering` module performs an **activity analysis** of the elements in the sequence, whether they be pixels (no prior skeleton analysis) or branches (see the module page for more information about this). Its goal is to return clusters of coactive pixels.
3. The `factorization` module has a similar goal to the clustering module. It returns independent components of **coactive pixels**, but uses **matrix factorization techniques** to do so.

![Alt Text](/images/posts/pyamnesia/output_examples.png)
*From left to right: a skeletonized image; a cluster; a factorization component*

Whereas the skeletonization part focuses on the **morphological** aspect of the analysis, both of the clustering and factorization modules tackle the **activity analysis** of it. As shown on the diagram above, the skeleton module is prior to the two others.

---
*For more information, you can check the official documentation of our toolbox 
[pyAMNESIA](https://pyamnesia.readthedocs.io/en/latest/overview_introduction.html).*