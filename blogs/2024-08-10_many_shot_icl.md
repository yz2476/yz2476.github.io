## Many-Shot In-Context Learning

### MetaInfo
1. From Google DeepMind
2. 2024-05
3. Note created on 2024-08-10.

### Abstract

1. Few-Shot In-Context Learning ==> a few shots
2. Many-Shot In-Context Learning ==> hundreds or thousands of shots
3. When extending from few-shot ICL to many-shot ICL, they observed significant performance gains across both generative and discriminative tasks.
4. Main bottleneck of many-shot ICL is lack of shots (the answer Y of shots). To address this challenge, they propose:
   - Reinforced ICL: uses model-generated chain-of-thought rationales in place of human rationales.
   - Unsupervised ICL: we remove rationales altogether, and prompt the model only with domain-specific inputs.
   - Results show both approaches are effective, especially on complex-reasoning tasks.
5. Compared with few-shot ICL, many-shot ICL is effective at overriding pretraining biases, can learn high-dimensional functions with numerical inputs, and performs comparably to fine-tuning.
6. Next-token prediction loss as an indicator of ICL performance, is limited.


> An implicit information: For ICL, there defaultly contains chain-of-thought rationals.

### Introduction
1. Adding number of shots in ICL can reduce the need for finetuning, potentially make LLMs more versatile and adaptable.
2. Genimi 1.5 Pro ==> 1M tokens.
3. Tasks:
   - Problem Solving: MATH, GSM8K
   - Question-Answering: GPQA
   - Summarization: XSum, XLSum
   - Algorithmic Reasoning: BBH
   - Reward Modeling: Code Verifier
   - low-resource machine translation: FLORES
   - Planning: Logistics
   - Sentiment Analysis: FP
4. High-Relevant Concurrent Works (This paper addresses much longer context windows.):
   - [Many-shot jailbreaking](https://www-cdn.anthropic.com/af5633c94ed2beb282f6a53c595eb437e8e7b630/Many_Shot_Jailbreaking__2024_04_02_0936.pdf)
   - [In-Context Learning with Long-Context Models: An In-Depth Exploration](https://arxiv.org/pdf/2405.00200)

5. One of the key contributions: Previously the quality of shots (especially the answer Y) are highly emphasized, this paper explores to use either model-generated rationales or remove answer Y (with only questions as inputs). Both works well!
   - Motivation for ReinforcedICL: [Beyond human data: Scaling self-training for problem-solving with language models](https://openreview.net/pdf?id=lNAyUngGFK)
   - Motivation for UnsupervisedICL: [AN EXPLANATION OF IN-CONTEXT LEARNING AS IMPLICIT BAYESIAN INFERENCE](https://openreview.net/pdf?id=RdJVFCHjUMI)

6. It studies how the learning dynamics of in-context learning changes from few-shot to the many-shot regime. We find that with sufficient examples, ICL can overcome pre- training biases, perform comparably to full fine-tuning, and solve high-dimensional prediction tasks with numerical inputs, namely sequential parity prediction and linear classification.

    > Questions: Can it achieve that LLMs learn new knowledge (against pretrained ones) by simply adding demonstrations?

7. It demonstrate that long-context scaling laws based on next-token prediction loss may not reliably predict ICL performance on problem-solving and reasoning tasks.
    > How to prove it?

### Scaling In-Context Learning (Inference Analysis)

1. Evaluation Setups:
    - Gemini 1.5 Pro with 1M tokens
    - Greedy Decoding
    - Randomly sample shots multiple times using different seeds, and report avg results
    - Visualize performance on different seeds
    - Use KV-Caching
    - All less than K-shot examples are included in K-shot examples. (the only variable is just the new shots)
  
2. Task 1: Machine Translation
    - Key: From English to low-resource languages.

3. Task 2: Abstractive Summarization:
    - Key: Same task, generalize from A dataset to B dataset.
    - Key: On the same dataset, improve first then decline when using more shots.

4. Task 3: Planning Task - Logistics Domain
    - Key: Interesting topic
    - Key: Qucikly improve performance, far from SOTA.
  
5. Task 4: Reward Modeling: Learning Code Verifiers
    - `To-Read-Carefully Again`

### Many-shot Learning without Human-Written Rationales

1. Address the challenges of unavailability of high-quality shots.
2. ReinforcedICL:
   - Potential Issues: False Positive
3. UnsupervisedICL:
   - prompt: (1) a preamble, such as, “You will be provided questions similar to the ones below:”, (2) a list of unsolved inputs or problems, and (3) a zero-shot instruction or a few-shot prompt with outputs for the desired output format. 
   - Explanation: when the LLM already possesses the required knowledge to solve a task, any information inserted in the prompt that can narrow down what knowledge is needed for the task becomes helpful. This would be consistent with the view that ICL simply “locates” latent concepts (e.g., math problem-solving) the LLM acquired during pre-training. As such, any of the prompt components – inputs, outputs, and their mapping – can help locate such concepts.

> Questions: Sometimes ICL overrides the pretrained knowledge. Sometimes ICL just try to locate and reuse the pretrained knowledge.

4. Problem-solving: Hendrycks MATH & GSM8K
   - ICL improves and then drops. RICL and UICL improves higher with a plateu (no obvious drop)
   - Just presenting Questions (instead of Q&A) appears to be better in this domain.
   - Generalizable among different datasets of the same domain.
     - Motivated by [Beyond Human Data: Scaling Self-Training for Problem-Solving with Language Models](https://openreview.net/pdf?id=lNAyUngGFK)
  
5. Question Answering: Google-Proof QA (GPQA)
    - `TLDR;`
  
6. Algorithmic and Symbolic Reasoning: Big-Bench Hard
    - `TLDR;`

### Analyzing Many-Shot ICL
1. 