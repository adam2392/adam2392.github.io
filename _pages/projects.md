---
title: "Research Projects"
layout: archive
permalink: /projects/
author_profile: true

---

## Current work

### Causal discovery across multiple domains

Discovering causal relationships is a central goal of science. There is an explosion of different datasets stemming from the same system. For example, one might have access to sequencing data and experimental CRISPR perturbations across different labs. Each lab is considered a separate domain, where distributions may shift due to changes in lab protocols. Another example is neural recordings in human patients. Although structural connections among different parts of the brain may be consistent across patients, each patient can be considered a different domain where the distribution of neural activity is different. Learning causal structure from these different distributions is not well characterized. We provide a theoretical characterization and learning algorithm for learning from observational and experimental data stemming from multiple domains.

Let us provide another example. Consider the medial temporal lobe (MT), premotor cortex (PM), somatosensory cortex (S1) and the motor cortex (M1). These regions have been hypothesized to work together to generate movement. Our overarching goal is to ultimately understand how these brain regions interact to facilitate movement in humans. In parallel, neuroscientists may also be interested in what portions of this computation differs in bonobos. Recording technology allows us to record electrophysiological activity in these brain regions for both bonobos and humans. We can also design an experiment, where we have subjects move a cursor in response to visual stimuli. Finally, we can also apply stimulation, or lesion experiments in bonobos that we could otherwise not do in humans. By systematically combining these observational and experimental distributions from both humans and bonobos, one can learn the following causal structure, where we not only get the cause-and-effect relationships among relevant brain regions, but also see where the computation may differ between humans and bonobos. This difference is indicated by the black-square, which we call an S-node. 

https://adam2392.github.io/files/human_and_bonobos_vignette.pdf

- [[Paper](https://causalai.net/r98.pdf), [code](https://github.com/py-why/dodiscover)] **Adam Li**, Amin Jaber, and Elias Bareinboim. “Causal discovery from observational and interventional data across multiple environments”. In: Neural Information Processing Systems (NeurIPS) (2023).

- [[Paper](https://arxiv.org/abs/2307.13868), [code](https://github.com/py-why/pywhy-stats)] Bridgeford, Eric W., Jaewon Chung, Brian Gilbert, Sambit Panda, **Adam Li**, Cencheng Shen, Alexandra Badea, Brian Caffo, and Joshua T. Vogelstein. "Learning sources of variability from high-dimensional observational studies." arXiv preprint arXiv:2307.13868 (2023).

### Modern random forests
Although random forest classifiers are extremely successful for tabular data, they are not state of the art for structured data. We develop a random forest algorithm better-suited for such data as images and time series by using structured projections of features which take into account the data geometry. This enables state of the art performance in biomedical settings with low sample sizes.
 
<!--  **Extensions for structured data such as images and time series** -->
 
- [[Paper](https://arxiv.org/abs/1909.11799), [code](https://github.com/neurodata/scikit-tree)] **Adam Li**, Ronan Perry, Chester Huynh, Tyler M. Tomita, Ronak Mehta, Jesus Arroyo, Jesse Patsolic, Benjamin Falk, and Joshua T. Vogelstein. “Manifold Oblique Random Forests: Towards Closing the Gap on Convolutional Deep Networks”. In: SIAM Journal on Mathematics of Data Science (SIMODS) (2022).
- [[Package](https://github.com/neurodata/scikit-tree)] A scikit-learn compliant Python package for honest random forests.

### Estimating mutual information in high-dimensions
<!-- **Calibration: an empirical study and downstream applications** -->
Posterior probabilities from machine learning classifies are typically overconfidant. We leverage "honesty" a fundamental property that can be imbued on random forests to prove that (conditional) entropy and therefore (conditional) mutual information can be estimated. We show robustness of our information-theoretic estimators in high-dimensions on the OpenML-CC18 datasets, fMRI data and EEG data.

<!-- - [[Paper](https://arxiv.org/abs/1907.00325), [code](https://github.com/rflperry/ProgLearn/tree/UF/benchmarks/uf_experiments)] **Ronan Perry**, Ronak Mehta, Richard Guo, Eva Yezerets, Jesús Arroyo, Mike Powell, Hayden Helm, Cencheng Shen, and Joshua T Vogelstein. “Random Forests for Adaptive Nearest Neighbor Estimation of Information-Theoretic Quantities”. In: arXiv preprint arXiv:1907.00325 (2021). -->

## Prior work

### Localizing the epileptogenic zone in drug-resistant epilepsy patients

My PhD thesis work focused on developing algorithms for seizure localization in drug-resistant epilepsy patients. I worked with multivariate time-series, such as intracranial EEG and scalp EEG data. I also did 2D and 3D image analysis with T1 MRI and CT scans of patients to understand the spatial relationships of epileptic networks. Specifically, I analyzed EEG data using dynamical systems, control theory, machine learning and statistics. I combined biological understanding of the brain with mathematical models of dynamical systems. I also utilized machine learning and statistical models to answer relevant hypothesis-driven questions, with a focus on learning manifold structure from a low number of samples. Moreover, I developed a suite of open-source software tools contributing to packages such as the Brain Imaging Data Structure (BIDS), MNE, The Virtual Brain (TVB), scikit-learn and other scientific packages.

- [[Paper](https://www.nature.com/articles/s41593-021-00901-w), [code]()] **Li, Adam**, Chester Huynh, Zachary Fitzgerald, Iahn Cajigas, Damian Brusko, Jonathan Jagid, Angel O. Claudio et al. "Neural fragility as an EEG marker of the seizure onset zone." Nature neuroscience 24, no. 10 (2021): 1465-1474.
- [[Paper](https://academic.oup.com/brain/article-abstract/146/6/2248/6979879)] **Adam Li**, Bernabei, John M., Andrew Y. Revell, Rachel J. Smith, Kristin M. Gunnarsdottir, Ian Z. Ong, Kathryn A. Davis, Nishant Sinha, Sridevi Sarma, and Brian Litt. "Quantitative approaches to guide epilepsy surgery from intracranial EEG." Brain 146, no. 6 (2023): 2248-2258.
- [[Paper](https://academic.oup.com/brain/article-abstract/145/11/3901/6835751), [code]()] Gunnarsdottir, Kristin M., **Adam Li**, Rachel J. Smith, Joon-Yi Kang, Anna Korzeniewska, Nathan E. Crone, Adam G. Rouse et al. "Source-sink connectivity: A novel interictal EEG marker for seizure localization." Brain 145, no. 11 (2022): 3901-3915.
- [[Paper](https://www.medrxiv.org/content/10.1101/2021.07.07.21259385.abstract)] **Li, Adam**, Patrick Myers, Nebras Warsi, Kristin M. Gunnarsdottir, Sarah Kim, Viktor Jirsa, Ayako Ochi, Hiroshi Otusbo, George M. Ibrahim, and Sridevi V. Sarma. "Neural Fragility of the Intracranial EEG Network Decreases after Surgical Resection of the Epileptogenic Zone." medRxiv (2021): 2021-07.
- [[Paper](https://ieeexplore.ieee.org/abstract/document/7963378)] **Li, Adam**, Sara Inati, Kareem Zaghloul, and Sridevi Sarma. "Fragility in epileptic networks: the epileptogenic zone." In 2017 American Control Conference (ACC), pp. 2817-2822. IEEE, 2017.
- [[Paper](https://direct.mit.edu/netn/article-abstract/02/02/218/2206)] **Li, Adam**, Bhaskar Chennuri, Sandya Subramanian, Robert Yaffe, Steve Gliske, William Stacey, Robert Norton et al. "Using network analysis to localize the epileptogenic zone from invasive EEG recordings in intractable focal epilepsy." Network Neuroscience 2, no. 02 (2018): 218-240.

### Diagnosing Epilepsy patients

While scalp EEG is important for diagnosing epilepsy, a single routine EEG is limited in its diagnostic value. Only a small percentage of routine EEGs show interictal epileptiform discharges (IEDs) and overall misdiagnosis rates of epilepsy are 20-30%. We aim to demonstrate how analyzing network properties in EEG recordings can be used to improve the speed and accuracy of epilepsy diagnosis - even in the absence of IEDs.

- [[Paper](https://www.medrxiv.org/content/10.1101/2023.08.12.23294018.abstract)] Myers, Patrick E., Kristín Gunnarsdóttir, **Adam Li**, Vlad Razskazovskiy, Dale Wyeth, Edmund Wyeth, Alana Tillery et al. "Diagnosing Epilepsy with Normal Interictal EEG Using Dynamic Network Models." medRxiv (2023): 2023-08.

## Open source

<!-- **Open source software** -->

Another core aspect of my research is the development of fundamental scientific software, which impacts hundreds to thousands of researchers. My contributions range from software for analyzing neural data, to general machine learning to scientific computing with sparse arrays.

- [[Paper](https://joss.theoj.org/papers/d91770e35a985ecda4f2e1f124977207), [Webpage](https://mne.tools/mne-icalabel/dev/index.html), [Github](https://github.com/mne-tools/mne-icalabel)] **Li, Adam**, Jacob Feitelberg, Anand Prakash Saini, Richard Höchenberger, and Mathieu Scheltienne. "MNE-ICALabel: Automatically annotating ICA components with ICLabel in Python." Journal of Open Source Software 7, no. 76 (2022): 4484.
- [[Github](https://github.com/sappelhoff/pyprep)] Appelhoff, S., A. J. Hurst, A. Lawrence, **A. Li**, Y. J. Mantilla Ramos, C. O’Reilly, L. Xiang, and J. Dancker. "PyPREP: A Python implementation of the preprocessing pipeline (PREP) for EEG data." (2022).
- [[Github](https://github.com/mne-tools/mne-bids)] Appelhoff, S., M. Sanderson, T. L. Brooks, M. van Vliet, R. Quentin, C. Holdgraf, M. Chaumon, **Li, A.**, et al. "MNE-BIDS: MNE-Python+ BIDS= easy dataset interaction." Organization for Human Brain Mapping (2020).
- [[Github](https://github.com/bids-standard/bids-validator)] Gorgolewski, C., et al. "Bids-standard/bids-validator: 1. 4. 3 (1.4. 3)[Computer software]." Geneva: Zenodo (2020).
- [[Paper](https://arxiv.org/abs/2309.05768), [Webpage](https://bids-specification.readthedocs.io), [Github](https://github.com/bids-standard/bids-specification)] Poldrack, Russell A., et al. "The Past, Present, and Future of the Brain Imaging Data Structure (BIDS)." arXiv preprint arXiv:2309.05768 (2023).
- [[Github](https://github.com/mne-tools/mne-python)] Larson, Eric, et al. (2023). MNE-Python (v1.5.1). Zenodo. https://doi.org/10.5281/zenodo.8322569
- [[Github](https://github.com/mne-tools/mne-connectivity)] **Li, A.**, McCloy, D., Larson, E., Westner, B., Kroner, A., & Gramfort, A. (2022). mne-connectivity (Version 0.2.0) [Computer software]. https://github.com/mne-tools/mne-connectivity
- [[Github](https://github.com/py-why/dodiscover)] **Li, A.**, Lee, J., Montagna, F., Trevino, C., & Ness, R. Dodiscover: Causal discovery algorithms in Python. [Computer software]. https://github.com/py-why/dodiscover
- [[Github](https://github.com/py-why/pywhy-graphs)] **Li, A.**, Lee, J., & Roy, A. Pywhy-Graphs:  Causal graphs that are networkx-compliant for the py-why ecosystem. [Computer software]. https://github.com/py-why/pywhy-graphs
- [[Github](https://github.com/py-why/pywhy-stats)] **Li, A.**, & Blöbaum, P. Pywhy-Stats: Statistical inference in Python. [Computer software]. https://github.com/py-why/pywhy-stats
- [[Github](https://github.com/pydata/sparse)] PyData/Sparse: Sparse multi-dimensional arrays for the PyData ecosystem.
