# Quantifying Authorship Biases: Using Conditional Probability Engines to Distinguish AI-Generated Text from Human Discourse

Author: Isaac Oboh Yamoah

Affiliation: Stanford University: Probability for AI and Code in Place

## Abstract

As Large Language Models (LLMs) increasingly permeate digital communication, distinguishing machine-generated content from human writing has become a critical challenge across computational linguistics and cybersecurity. This paper explores the "Word Detective" framework, a data-driven application that models LLMs as conditional probability engines. By evaluating statistical distributions and token usage across large text corpora (such as the Reddit ELI5 dataset, medical, financial, and wiki domains), we quantify how specific lexical markers—such as the over-reliance on terms like "super"—serve as profound statistical "tells" or fingerprints for AI authorship. We examine the mathematical formulation of conditional probability in token prediction, compare raw probability versus ratio-based visualizations, and discuss the implications for automated authorship attribution tools.

---

## 1. Introduction

Large Language Models function fundamentally as conditional probability engines, predicting subsequent tokens based on preceding context. Consequently, generative models develop distinct stylistic and lexical biases that diverge from natural human discourse. While human writing exhibits high variance shaped by individual cognition, colloquialisms, and diverse lived experiences, LLMs optimize for high-probability token sequences, leading to predictable lexical signatures.

This research investigates how computational tools can leverage conditional probability to quantify these authorship disparities. By building an interactive analytical environment—the Word Detective app—we measure the exact probability of observing specific words given a designated author class (AI versus human) and analyze how these metrics can be visualized to surface distinct textual fingerprints.

---

## 2. Methodology & Mathematical Framework

To rigorously evaluate authorship classification, we define text authorship using discrete event spaces:

* Let $A$ represent the event that a given text block is AI-written.
* Let $H$ represent the event that a given text block is human-written.
* Let $W$ represent the event that a text block contains a specific target word $W$.

The probability of observing word $W$ conditional upon the author category is computed via standard relative frequency estimation over a corpus of size $n$:

$$\mathbb{P}(W \mid A) = \frac{\text{Count}(W \cap A)}{n_A}$$

$$\mathbb{P}(W \mid H) = \frac{\text{Count}(W \cap H)}{n_H}$$

### 2.1 Text Processing and Normalization Decisions

When calculating counts across large datasets, several preprocessing parameters significantly influence statistical robustness:

1. **Case Sensitivity:** Normalizing tokens via case-insensitive matching (e.g., treating "Super" and "super" identically) prevents artificial dilution of term frequencies.
2. **Handling Hard Zeros:** In sparse domains where a word never appears in a specific category, maintaining a hard zero ($\mathbb{P} = 0$) evaluates strict empirical presence, whereas smoothing techniques can be integrated to prevent overconfidence in finite datasets.

---

## 3. Results and Empirical Observations

Analysis of the Reddit ELI5 dataset revealed sharp contrasts in vocabulary selection between AI generators and human respondents.

* **The "Super" Phenomenon:** Initial single-word tracking identified "super" as an extreme statistical outlier. Empirical estimations demonstrated that $\mathbb{P}(\text{"super"} \mid A) \approx 0.302$ (appearing in roughly 30% of AI responses), whereas $\mathbb{P}(\text{"super"} \mid H) \approx 0.005$ (appearing in less than 1% of human responses).
* **Author Biases Across Domains:** By integrating a multi-domain dataset switcher into the framework (evaluating Reddit ELI5 alongside medical Q&A, financial Q&A, and CS/AI Wikipedia entries), we observed that specific lexical tells fluctuate depending on the domain's formal constraints, though generative models consistently display elevated usage rates for transitional and intensifier adjectives.

---

## 4. Visualization Techniques for Authorship Attribution

Effective communication of statistical disparities requires moving beyond raw tabular data. The Word Detective implementation utilizes:

* **Vertical Column Charts:** Replacing traditional tables with visual histograms allows analysts to compare $\mathbb{P}(W \mid A)$ and $\mathbb{P}(W \mid H)$ side-by-side at a glance.
* **Ratio Comparisons:** Rather than relying solely on absolute probabilities, analyzing the ratio between AI usage and human usage highlights the magnitude of distinct author biases.
* **Inverted Ranking Lists:** Flipping data sorts to surface the most *human*-sounding words illuminates terms heavily relied upon by human authors that generative models systematically underutilize.

---

## 5. Conclusion

The Word Detective framework demonstrates that distinguishing AI-generated text from human writing does not require complex black-box heuristics; it can be achieved through transparent, interpretable conditional probability calculations. By quantifying token distributions and visualizing usage ratios across domains, developers and researchers can effectively map linguistic fingerprints and build robust authorship scoring tools.

---
