# A Survey on Table-and-Text HybridQA: Definitions, Methods, Challenges and Future Directions

![](https://img.shields.io/badge/Status-building-brightgreen) ![](https://img.shields.io/badge/PRs-Welcome-red)

This repository contains a list of papers, datasets and leaderboards of the text-and-table HybridQA task, which is carefully and comprehensively organized. 
If you found any error, please open an issue or pull request.

## Introduction

The question-answering task with just text or tables to generate answers has been systematically studied, which we call the classic QA task.
These two sorts of evidence each have their advantages: textual evidence is prevalent in daily communication, while tabular evidence is a well-organized display of numerical information.
However, using the heterogeneous data that combines these two types of evidence is increasingly prevalent in real applications, particularly in fields demanding numerical reasoning, like the financial and scientific domains.
This technique is known as Table-and-Text Hybrid Question Answering (HybridQA).
Considering that HybridQA is still under-researched, we present this project to summarize the current development including benchmarks and their published-sota.

## Benchmarks and Leaderboard

### [HybridQA](https://hybridqa.github.io)
HybridQA is the first HybridQA benchmark, which is also the largest cross-domain benchmark to date.
Each question and answer is relayed on a single table and multiple texts.
Each text usually is a description of information of a table cell, for example, a hyperlink page of the cell, which is crawled from Wikipedia. 
For each case, the benchmark offers the golden text and table rows.
All answers to questions are the spans in evidence, which called span-based answers, and need one or more hops between heterogeneous data.

**Model**                                     |  **Organization**  |**Reference**                                                             | **Dev-EM** | **Dev-F1** | **Test-EM** | **Test-F1** | 
----------|---------------------------|-----------------------------------|---------------------------------------------------------------------------|---------|----------|------------------|
UL-20B           | Google    | [Tay et al. (2022)](https://arxiv.org/abs/2205.05131)                    |   -     | -    |  61.0  | -    |
MITQA            | IBM & IIT | [Kumar et al. (2021)](https://arxiv.org/pdf/2112.07337.pdf)              |   65.5  | 72.7 |  64.3  | 71.9 |
RHGN             | SEU       | [Yang et al. (2022)](https://link.springer.com/epdf/10.1007/s11227-022-05035-9?sharing_token=kouLCEDp9_vH1RkK8N9CAPe4RwlQNchNByi7wbcMAY4kj78xdT5rsS4-XKuj5N_XmnTRe7ko6X0kKaXyingc6wfoEGdQgx5hH9hDtcI6ivFPDd1p7A3RUWChRVmVBrgsvavXcujpAkPf2d1K1X-eE8ctae3eLrfxStzEdLP9uOs=)   |   62.8 | 70.4 |   60.6    |  68.1   |
POINTR + MATE    | Google    | [Eisenschlos et al. (2021)](https://arxiv.org/pdf/2109.04312.pdf)         |   63.3  | 70.8 |  62.7  | 70.0 |
POINTR + TAPAS   | Google    | [Eisenschlos et al. (2021)](https://arxiv.org/pdf/2109.04312.pdf)         |   63.4  | 71.0 |  62.8  | 70.2 |
MuGER<sup>2</sup>| JD AI     | [Wang et al. (2022)](https://arxiv.org/abs/2210.10350)                    | 57.1    | 67.3 | 56.3   |  66.2 |
DocHopper        | CMU       | [Sun et al. (2021)](https://arxiv.org/abs/2106.00200)                     |   47.7  | 55.0 |  46.3  | 53.3 |
HYBRIDER         | UCSB      | [Chen et al. (2020)](https://arxiv.org/abs/2004.07347)                    |   43.5  | 50.6 |  42.2  | 49.9 |
HYBRIDER-Large   | UCSB      | [Chen et al. (2020)](https://arxiv.org/abs/2004.07347)                    |  44.0   | 50.7 |  43.8  | 50.6 |
Unsupervised-QG  | NUS\&UCSB |  [Pan et al. (2020)](https://arxiv.org/abs/2010.12623)                    |    25.7 | 30.5 |   -    |  -   |

### [OTT-QA](https://ott-qa.github.io)
To lower the difficulties of answering, HybridQA annotates the related evidence to each example and the links of text and tables, which widens the gap with real-world applications.
To be more relevant to the practical applications, OTT-QA blends textual and tabular evidence of each example into one single corpus that contains more than five million items and removes the relation information between them, which is called the open-QA benchmark. 
So the most challenging part of this benchmark is to retrieve evidence of questions from millions of heterogeneous data, like open domain question answering. 
The questions and evidence of OTT-QA are all built based on the HybridQA.
Also, all its answers are the spans in the evidence.

**Model**                                     |  **Organization**  |**Reference**                                                             | **Dev-EM** | **Dev-F1** | **Test-EM** | **Test-F1** | 
----------|---------------------------|-----------------------------------|---------------------------------------------------------------------------|---------|----------|------------------|
CORE         | CMU + Microsoft Research      | [Ma et al. (2022)](https://arxiv.org/abs/2210.12338)                    |  49.0 | 55.7  | 47.3  | 54.1 |
OTTeR        | MSRA + Beihang                | [Huang et al. (2022)](https://arxiv.org/abs/2210.05197)                 |  37.1 | 42.8 | 37.3 | 43.1 |
CARP         | MSRA + Sun Yet-sen University      | [Zhong et al. (2021)](https://arxiv.org/pdf/2201.05880.pdf)                    |  33.2 | 38.6  | 32.5  | 38.5 |
Fusion+Cross-Reader         | Google      | [Chen et al. (2021)](https://arxiv.org/abs/2010.10439)                    |  28.1 | 32.5  | 27.2  | 31.5 |
Dual Reader-Parser | Amazon | [Alexander et al. (2021)](https://assets.amazon.science/09/2b/7acf41f24c998cd3c2361681e9db/dual-reader-parser-on-hybrid-textual-and-tabular-evidence-for-open-domain-question-answering.pdf)                                              |   15.8   |    -  |  -       | -        |
BM25-HYBRIDER   | UCSB      | [Chen et al. (2021)](https://arxiv.org/abs/2010.10439)                    |    10.3     | 13.0  |  9.7           | 12.8  |

### [FinQA](https://finqasite.github.io)
Some HybridQA answers generation require numeric reasoning compatibility, while the benchmarks with only span-based questions cannot fulfill this requirement.
FinQA is a finance HybridQA benchmark containing the questions of many standard financial analysis calculations. 
FinQA annotates the arithmetic answer in a domain-specific language (DSL), which consists of mathematical and table operations, to reduce the difficulty of formula generation and make it more interpretable.

| **Model** | **Orgnization** | **Reference** | **Dev-Execution Accuracy** | **Dev-Program Accuracy** | **Test-Execution Accuracy** | **Test-Program Accuracy** |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| PoT-SC<sub>code-davinci-002</sub> | University of Waterloo | [Chen et al.](https://arxiv.org/abs/2211.12588) | - | - | 68.1 | - |
| APOLLO | MSRA + Xiamen University | [Sun et al.](https://arxiv.org/pdf/2212.07249.pdf) | 69.79 | 65.91 | 67.99 | 65.60 |
| ELASTIC | Strath | [Zhang et al. (2022)](https://arxiv.org/pdf/2210.10105.pdf) | - | - | 68.96 | 65.21 |
| DyRRen | Nanjing University | [Li et al. (2022)](https://arxiv.org/pdf/2211.12668.pdf) | 66.82 | 63.87 | 63.30 | 61.29 |
| ReasonFuse | CAS | [Xia et al. (2022)](https://www.sciencedirect.com/science/article/pii/S0925231222011444#s0085) | 61.84 | 59.80 | 60.68 | 58.94 |
| FinQANet | UCSB | [Chen et al. (2021)](https://arxiv.org/pdf/2109.00122.pdf) | 61.22 | 58.05 | 61.24 | 58.86 |

### [TAT-QA](https://nextplusplus.github.io/TAT-QA/)
Although FinQA has presented well-annotated numerical reasoning questions, it ignores the questions with span-based answers.
Similar to the classic QA benchmark DROP, TAT-QA is a collection of financial HybridQA samples that includes questions with both span-based and arithmetic answers.  
Additionally, unlike the benchmarks mentioned above, each TAT-QA question is typically related to only five texts, which lowers the difficulty of retrieval. 
Just like FinQA, TAT-QA also provides the formulations of arithmetic questions.
| **Model** | **Orgnization** | **Reference** | **Dev-EM** | **Dev-F1** | **Test-EM** | **Test-F1** |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| RegHNT | CAS | [Lei et al.](https://arxiv.org/pdf/2209.07692.pdf) | 73.6 | 81.3 | 70.3 | 78.0 |
| UniRPG | Harbin Institute of Technology + JD AI Research | [Zhou et al. (2022)](https://arxiv.org/pdf/2210.08249.pdf) | 70.2 | 77.9 | 67.1 | 76.0 |
| PoT-SC<sub>code-davinci-002</sub> | University of Waterloo | [Chen et al.](https://arxiv.org/abs/2211.12588) | 70.2 | - | - | - |
| UniPCQA | CUHK | [Deng et al. (2022)](https://arxiv.org/pdf/2210.08817.pdf) | 68.2 | 75.5 | 63.9 | 72.2 |
| MHST | NUS | [Zhu et al. (2022)](https://arxiv.org/pdf/2207.11871.pdf) | 68.2 | 76.8 | 63.6 | 72.7 |
| GANO | National Institute of Advanced Industrial Science and Technology | [Nararatwong et al. (2022)](https://aclanthology.org/2022.aacl-main.72.pdf) | 68.4 | 77.8 | 62.1 | 71.6 |
| FinMath | Northeastern University | [Li et al. (2022)](http://www.lrec-conf.org/proceedings/lrec2022/pdf/2022.lrec-1.661.pdf) | 60.5 | 66.3 | 58.6 | 64.1 |
| TagOp | NUS | [Zhu et al. (2021)](https://aclanthology.org/2021.acl-long.254/) | 55.2 | 62.7 | 50.1 | 58.0 |

### [MultiHiertt](https://github.com/psunlpgroup/MultiHiertt)
Hierarchical tables, which contain multi-level headers, are common in the real world but are hard to be expressed and be understood by models because of the complex table structure. 
However, almost all tables of the previous benchmarks are flattened structures without multi-level headers.
To overcome this challenge, MultiHiertt collects and annotates many hierarchical tables compared with questions.
| **Model** | **Orgnization** | **Reference** | **Dev-EM** | **Dev-F1** | **Test-EM** | **Test-F1** |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| NAPG | Zhengzhou University + Peng Cheng Lab | [Zhang et al.](https://arxiv.org/pdf/2211.03462.pdf) | - | - | 44.19 | 44.81 |
| MT2Net | Yale | [Zhao et al.](https://aclanthology.org/2022.acl-long.454.pdf) | 37.05 | 39.96 | 36.22 | 38.43 |

### [GeoTSQA](https://github.com/nju-websoft/TSQA)
GeoTSQA is the first scenario-based question-answering benchmark with hybrid evidence, which requires retrieving and integrating knowledge from multiple sources and applying general knowledge to a specific case described by the scenario.
This benchmark is constructed on the multiple-choice questions in the geography domain from Chinese high-school exams.
Besides tables and text, each question is also provided with four options, from which model should select one as the answer.
| **Model** | **Orgnization** | **Reference** | **Accuracy** |
| ---- | ---- | ---- | ---- |
| TTGen | Nanjing University | [Li et al.](https://arxiv.org/pdf/2101.11429.pdf) | 39.7 |
