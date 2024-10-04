---
permalink: /
title: "Welcome!"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Currently, I am a Postdoctoral Research Scientist at Columbia University in the Causal Artificial Intelligence Lab, directed by [Dr. Elias Bareinboim](http://causalai.net). I am an [NSF-funded Computing Innovation Research Fellow](https://cifellows2021.org/2021-class/). I did my PhD in biomedical engineering, specializing in computational neuroscience and machine learning at Johns Hopkins University. I worked with Dr. Sridevi V. Sarma in the [Neuromedical Control Systems group](http://sarmalab.icm.jhu.edu/). I also jointly obtained a MS in Applied Mathematics and Statistics with a focus in statistical learning theory, optimization and matrix analysis. I was fortunate to be a [NSF-GRFP fellow, Whitaker International Fellow](https://icm.jhu.edu/2017/03/20/adam-li-selected-for-nsf-graduate-research-and-whitaker-international-fellowships/#.YH2ZT6lKj0o), [Chateaubriand Fellow](https://icm.jhu.edu/2017/06/16/adam-li-icm-phd-student-selected-for-chateaubriand-fellowship/#.YH2Zi6lKj0o) and [ARCS Chapter Scholar](https://icm.jhu.edu/2020/07/20/adam-li-icm-phd-student-receives-arcs-scholarship/#.YH2ZbKlKj0o) during my time at JHU. Outside of research, I am a scikit-learn maintainer and also contribute heavily to other open-source projects, such as MNE-Python, and PyWhy.

Research Interests
==================
My research is focused on telling a causal story from data, leveraging deep domain expertise, and tools from machine learning, causal inference, dynamical systems and deep learning. I am particularly interested in research that has translational impact in the real world. My research can be broadly categorized into the following areas:

1. Causal Inference: Structure learning and representation learning
2. High-dimensional data analysis and hypothesis testing
3. Applications of AI (e.g. biomedical)
4. Open-source and reproducibility

Causal Inference: Structure learning and representation learning
----------------------------------------------------------------
In my postdoc, I turned my attention to developing more general theory for understanding how to learn causal relationships in the sciences. The causal discovery problem has traditionally operated in the setting of a single domain. Moreover, before our paper, the setting of multiple-domains vs interventions were typically conflated. However, if we consider trying to learn fundamental principles mammalian brains use for decision-making, or movement, we commonly leverage data from both bonobos and humans. However, it is clear that not all experimentation in bonobos produce the same results when repeated in humans. How do we systematically leverage observations and experiments in both domains to learn shared causal structure? Our 2023 NeurIPS paper resolves this issue by demonstrating that interventions and domain-shifts are in fact different and proposes a theoretical characterization and an algorithm for learning causal relationships given observations and experiments arising from different environments. 

High-dimensional data analysis and hypothesis testing
-----------------------------------------------------
An important part of discovering robust causal relationships from data requires robust estimators that have desirable statistical properties. Towards this end, our work has developed variants of the famous Random Forest algorithm. We have developed random forests capable of manifold learning, which demonstrate significantly better performance compared to Convolutional Neural Networks when predicting surgical outcome in epilepsy patients and movement direction from human-EEG data. This study was published in SIAM and also released as open-source software on https://github.com/neurodata/scikit-tree. Furthermore, since random forests are universally consistent estimators, we leverage them to perform high-dimensional multivariate hypothesis-testing and estimation of information-theoretic quantities. These have been applied to study what various features of cell-free DNA are useful as an any-stage diagnostic for cancer. This work has been submitted and in review at Science.

Applications of AI (e.g. biomedical)
------------------------------------
This work started in my PhD, where I worked on developing an EEG-based biomarker for the seizure onset zone in epilepsy patients. There are over 10 million epilepsy patients in the world that don’t respond to medication and continue to have seizures, thus the only available treatment is to surgically remove the brain area responsible for seizures. However, we do not yet understand the underlying causes and mechanisms that lead to seizure generation. We were inspired by how neurons behave dynamically during a seizure and modeled our approach using this intuition. I developed a quantitative EEG biomarker that highlights the most epileptic brain regions, which would enable improved diagnosis of epilepsy and help guide surgical treatment of patients leading to seizure freedom. This research was published in multiple conferences and journals including Nature Neuroscience and was also FDA approved as a software-medical device.

Open-source and reproducibility
-------------------------------
I am also extremely passionate about open-source everything. I am a maintainer at scikit-learn, and help deliver production-ready ML solutions with battle-proven statistical models, such as Random Forests. In addition, I contribute to the overall development and maintainence of the package, working with amazing peers from all over the world.

For a list of my publications, see my [Google Scholar](https://scholar.google.com/citations?user=KxY17KcAAAAJ&hl=en). If there are any publications not publicly accessible, please shoot me a message and I'm happy to share with you.

Non-profit Work
---------------
For a summary of my involvement in nonprofit and charity work, see [here](/nonprofit)

## News
- **10/2024** - Our paper ["Disentangled Representation Learning in Non-Markovian Causal Systems"](https://causalai.net/r110.pdf) was accepted to **NeurIPS 2023**! Very thankful for my co-authors, Dr. Elias Bareinboim and Yushu Pan.
- **10/2023** - Our paper ["Causal discovery from observational and interventional data across multiple environments"](https://causalai.net/r98.pdf) was accepted to **NeurIPS 2023**! Very thankful for my co-authors, Dr. Elias Bareinboim and Dr. Amin Jaber.
- **08/2022** - Our paper ["Manifold Oblique Random Forests: Towards Closing the Gap on Convolutional Deep Networks"](https://arxiv.org/abs/1909.11799) was accepted to **SIMODS**!
- **08/2021** - Our paper ["Neural fragility as an EEG marker of the seizure onset zone"](https://www.nature.com/articles/s41593-021-00901-w) was accepted to **Nature Neuroscience**!
