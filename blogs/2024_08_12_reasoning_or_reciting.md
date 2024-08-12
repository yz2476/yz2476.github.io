## Reasoning or Reciting? Exploring the Capabilities and Limitations of Language Models Through Counterfactual Tasks

### MetaInfo
1. From MIT & Boston, Jacob Andreas, Yoon Kim
2. 2024-03
3. Note created on 2024-08-12.

### Abstract
1. Problems: LLMs possess a certain degree of abstract reasoning capability. Are these capabilities general and transferable? Or they are just specialized to specific tasks seen during pretraining?

2. This paper studies this problem by disentangling several factors, using a proposed counterfact benchmark.

3. Non-trivial performance on counterfact tasks, however, far behind default setting tasks. LLMs possess abstract task-solving skills to an extent, they often also rely on narrow, non-transferable procedures for task-solving.

> Questions: Do LLMs really possess such skills/reasoning capabilities? Are LLMs able to use such capabilities? Are LLMs really using such abilities to perform tasks? 

### Introduction
1. Great background introduction of LLMs for the first paragraph. `to-be-repeated`
2. This paper tries to reveal the essential mechanism: To what extent does the perfor- mance of current LMs derive from their ability to deploy task-general reasoning skills, versus their ability to recognize and recall specific tasks seen frequently in pre-training?
   
    > Question: to what extent LLMs perform tasks out of their reasoning abilities, to what extent LLMs perform tasks using their pre-memorized info, and to what extent LLMs perform tasks using their recognization abilites.

3. Generalization:
   - Instance-level generalization
        - [Documenting large webtext corpora: A case study on the colossal clean crawled corpus.](https://arxiv.org/pdf/2104.08758)
        - [Data Contamination: From Memorization to Exploitation](https://aclanthology.org/2022.acl-short.18.pdf)
   - Task-level generalization (In this work, we are inter- ested in the models’ generalizability to new task variants, which has been less systematically studied for LMs)
     - [Quantifying Adaptability in Pre-trained Language Models with 500 Tasks](https://aclanthology.org/2022.naacl-main.346.pdf)
     - [Cross-Task Generalization via Natural Language Crowdsourcing Instructions](https://aclanthology.org/2022.acl-long.244.pdf)
     - [SUPER-NATURALINSTRUCTIONS: Generalization via Declarative Instructions on 1600+ NLP Tasks](https://aclanthology.org/2022.emnlp-main.340.pdf)

4. The paper designs a dataset. Each tasks contains a default setting and a counterfactual setting. It is expected to have a comparable performance on counterfactual and default tasks; if they employ procedures tailored to default task conditions, we expect a drop in the counterfactual performance.

5. Evaluate: GPT-4, GPT-3.5, Claude, PaLM-2.

6. Results & Conclusions: (1) above-random counterfactual performance for most tasks, indicating some degree of task generalizability. (2) performance on counter- factual task variants consistently and substantially degrades relative to the performance on the default settings, suggesting that these models’ ability on these tasks is supported at least in part by non- transferable, default-condition-specific behaviors rather than abstract, generalizable reasoning skills.

## Counterfactual Tasks
1. Conceptualization:
   - $f: X \rightarrow Y$
   - $f \in \{w_\text{default}, w_\text{counterfact}\}$, ecapsulating the conditions.
2. One potential confounder is that LLMs may fail due to failing to understand the prompt component that specifies the counterfactual conditions, i.e., $\text{prompting}(w_\text{counterfact})$. We control for this by designing task-specific counterfactual comprehension checks (CCCs) that test an LM’s surface understanding of the specified counterfactual world.

## Tasks
1. `TLDR;`

## Results
