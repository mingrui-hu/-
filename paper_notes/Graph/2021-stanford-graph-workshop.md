



# 1. Dynamic Bipartite Graph for abuse detection in e-commerce

- <img src="2021-stanford-graph-workshop.assets/image-20220307152825053.png" alt="image-20220307152825053" style="zoom:80%;" />
- <img src="2021-stanford-graph-workshop.assets/image-20220307152855876.png" alt="image-20220307152855876" style="zoom:67%;" />
- <img src="2021-stanford-graph-workshop.assets/image-20220307152749017.png" alt="image-20220307152749017" style="zoom:80%;" />

## Dynamic Architecture: 3 phases

- ![image-20220307152944585](2021-stanford-graph-workshop.assets/image-20220307152944585-16466381861883.png)

### 1. User round: RNN phase

![image-20220307153141320](2021-stanford-graph-workshop.assets/image-20220307153141320-16466383033214.png)



### 2. Item&User Round: GNN Phase

- no learning parameters

![image-20220307153216565](2021-stanford-graph-workshop.assets/image-20220307153216565-16466383374695.png)

### 3. Prediction

## Scalable Training

![image-20220307154602697](2021-stanford-graph-workshop.assets/image-20220307154602697-16466391638016.png)



## Self-supervised Pretraining Framework

## Experiments:

![image-20220307154817065](2021-stanford-graph-workshop.assets/image-20220307154817065-16466392978817.png)



![image-20220307154840959](2021-stanford-graph-workshop.assets/image-20220307154840959-16466393221028.png)

![image-20220307154930685](2021-stanford-graph-workshop.assets/image-20220307154930685-16466393719089.png)

![image-20220307155005291](2021-stanford-graph-workshop.assets/image-20220307155005291-164663940617010.png)

## Conclusion

- **Integrating time series and graph information** leads to significant improvement in abuse detection
- **Alternating training** is a high-performing, scalable approach to node classification on dynamic graphs
- **Pretraining** on anomaly detection objectives can improve performance in label-sparse settings  

## References

![image-20220307155152221](2021-stanford-graph-workshop.assets/image-20220307155152221-164663951414511.png)

# 2. Large-Scale Reasoning over Knowledge Graphs  

- KGs are Heterogeneous graph

## Goal: Complex Logical Reasoning on KG

- For example:
  - Where did Canadian Turing Award winners graduate?
  - Who are current presidents of European countries which never held a (soccer) world cup?
  - Predict drugs that might target proteins that are associated with SARS-CoV2?
-   <img src="2021-stanford-graph-workshop.assets/image-20220307155614020.png" alt="image-20220307155614020" style="zoom:50%;" />
- <img src="2021-stanford-graph-workshop.assets/image-20220307155700084.png" alt="image-20220307155700084" style="zoom:50%;" />

## Traditional Approach

- <img src="2021-stanford-graph-workshop.assets/image-20220307155758382.png" alt="image-20220307155758382" style="zoom: 50%;" />

## Challenges

- **incomplete & noisy** 
  -  how to capture **uncertainty**?
  - how to impute **missing** relations?
- **completing the KG** creates **additional links**, which further slows down query answering

- **transversing** requires time exponential in query depth 
  - how to **efficiently** answer queries on **large graphs**

## Task: KG Reasoning -> Complex Link Prediction

![image-20220307160253882](2021-stanford-graph-workshop.assets/image-20220307160253882-164664017506214.png)

## Solution 

- Map Logical queries into embedding space
- Reasoning in the embedding space

### 1. Framework: Query2Box

- map logical operators in learning space 
- Key Insight
  - **Represent query as a box**
  - (logical) operations (Intersection etc.) are well defined over boxes
- Idea:
  - Embed nodes of the graph
  - For every logical operator learn a spatial operator
- So that:
  - Take an arbitrary logical query. Decompose it into a set of logical operators (∃,∧,∨)
  - Apply **a sequence of spatial operators** to **embed the query**
  - Answers to the query are **entities close to the embedding of the query**  (i.e. neighbors)
- <img src="2021-stanford-graph-workshop.assets/image-20220307161105471.png" alt="image-20220307161105471" style="zoom:50%;" />

### 2. Embedding Queries

- ![image-20220307161321576](2021-stanford-graph-workshop.assets/image-20220307161321576-164664080239016.png)
- <img src="2021-stanford-graph-workshop.assets/image-20220307161507793.png" alt="image-20220307161507793" style="zoom:50%;" />

### 3. Examples

<img src="2021-stanford-graph-workshop.assets/image-20220307161624045-164664098588018.png" alt="image-20220307161624045" style="zoom:50%;" />

### 4. Handle Disjunction

Given an arbitrary AND-OR query :

- Transform it into an DNF (disjunctive normal form)
- Answer each conjunctive query
- Overall answer is the union of conjunctive query answers  

## Benefits

- Scalability & efficiency
  - Any query can be reduced to **a couple of matrix operations** and **a single k-nearest neighbor search**  
- Generality
  - We can answer any query (even those we have never seen before)  
- Robustness to noise
  - Graph can contain missing and noisy relationships  

## Contrastive Self-supervised training

- <img src="2021-stanford-graph-workshop.assets/image-20220307162304810-164664138588019.png" alt="image-20220307162304810" style="zoom:50%;" />

## ==Large-Scale Training==

![image-20220307162440231](2021-stanford-graph-workshop.assets/image-20220307162440231-164664148113020.png)

![image-20220307162509189](2021-stanford-graph-workshop.assets/image-20220307162509189-164664150996621.png)

## References

- [Embedding Logical Queries on Knowledge Graphs. Hamilton, et al., NeurIPS 2018]
- [[Query2box: Reasoning over Knowledge Graphs in Vector Space Using Box Embeddings. Ren, et al., ICLR 2020]  

- Scaling up Logical Query Embeddings on Knowledge Graphs. H. Ren, H. Dai, B. Dai, X. Chen, D. Zhou,
  J. Leskovec, D. Schuurmans. ICML SSL workshop 2021.
- Beta Embeddings for Multi-Hop Logical Reasoning in Knowledge Graphs. H. Ren, J. Leskovec. NeurIPS 2020.
- LEGO: Latent Execution-Guided Reasoning for Multi-Hop Question Answering on Knowledge Graphs. H. Ren, H. Dai, B. Dai, X. Chen, M. Yasunaga, H. Sun, D. Schuurmans, J. Leskovec, D. Zhou. ICML SSL workshop 2021.
- Code:
  - https://github.com/snap-stanford/KGReasoning
  - https://github.com/snap-stanford/SrKG  