---
layout: project
title: Meta 'Omic Classification
git: https://github.com/asgray/Meta-omic-ML-Classification
thumb: /assets/images/projects/metagen_thumb.png
tools: [Python, pandas, scikit-learn, Google Cloud]
---

This project examined and compared the performance of four machine learning classifiers on metagenomic and metatranscriptomic samples.

<!--more-->

Naïve Bayes, Support Vector Machines, Random Forests and K-Nearest Neighbor Classifiers are applied using the protein family composition of an ‘omic sample to determine if that sample came from a donor with Crohn’s Disease or from a donor without Inflammatory Bowel Disease. All the algorithms were at least somewhat successful depending on the data preparation, with several combinations resulting classification accuracies higher than 90%. Overall, these algorithms had higher accuracies on the metagenomic data than on the metatranscriptomic data. The dataset was sourced from the Inflammatory Bowel Disease Multi’omics Database (ibdmdb.org) and came in the form of protein families per sample by percent.

The apparent advantage of metagenomic over metatranscriptomic gene family composition data for classification of Crohn’s Disease is noteworthy. The difference in classification accuracy was highly dependent on the algorithm and the preparation of the data and ranged from an insignificant few tenths to a full ten percent. This implies that Crohn’s Disease is more dependent on the reservoir of potential protein expression in the gut microbiota than on the most common behaviors of the population. It is also interesting to note that previously reported OTU-based classification accuracies are typically around 70%. With proper tuning and feature selection, function-based classification could be even more accurate. However, this was not a conclusive analysis. The next steps in the project are to perform the same analysis on similar datasets covering different diseases, and to perform more sophisticated feature selection. Protein family features might be selected based on their known association with disease, or by replacing protein families as features with Gene Ontology terms.

Download the full paper **[Here](https://github.com/asgray/Meta-omic-ML-Classification/raw/master/AGray_final_writeup.pdf)**
