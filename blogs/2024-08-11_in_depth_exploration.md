## In-Context Learning with Long-Context Models: An In-Depth Exploration

### MetaInfo
1. 2024-04
2. From CMU + Neubig
3. Note created on 2024-08-11.

### Abstract
1. Incresing the number of demonstrations can continue improving performance.
2. Compare with example retrieval + finetuning:
    - with short-context, example retrieval excels; with more demonstrations, advantages diminish.
    - more data with finetuning leads to outperforming perf than ICL.
  
3. Study properties of ICL & Long-Context:
   - long-context ICL is less sensitive to order than short-context ICL
   - grouping of same-label examples can negatively impact performance
   - performance boosts do not arise from cumulative gain from encoding many examples together; most of this gain comes from attending back to similar examples rather than task learning.

> Questions: Which source do ICL perf gain come from? How can we forcefully make them learn???


### Introduction
1. Advantages of ICL:  ease of implementation, small computational cost, and ability to reuse a single model across tasks.
2. Prev ICL focuses on short-context; with context-window increasing, long-context ICL has become an alternative to finetuning.
3. There exists a tradeoff between efficiency and performance between manyshot ICL and finetuning.
    > Note: The finetuning here referes to LORA finetune.
4. Conclusions:
   - With number of demonstrations increase, ICL behavior shift.
   - Long-context ICL is not sensitive to order; cannot benefit from example retrieval.
   -  the effectiveness of long-context ICL is not because of the continual refinement of a decision boundary during encoding but because of the retrieval from more relevant examples 
    > Questions: Can we use selected few demonstrations to reach long-context ICL perf.

### Experimental Setup
1. Datasets: 5 classification tasks
   - TREC
   - TREC-fine
   - Banking-77
   - Clinic-150
   - NLU
2. Model: 
    - Llama-2-7B (4096K tokens)
    - Llama-2-32K (32K)
    - Llama-2-80K (80K)
    - Mistral-7B-Instruct-v0.2 (32K)
3. constrained decoding (`to-be-reread`)
4. Evaluation:
   - subsample 250 from each dataset
   - acc + MarocF1

### Long-Context ICL
1. 
