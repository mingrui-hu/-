![image-20220307145627045](graphgym.assets/image-20220307145627045-164663618813836.png)

## Key Concept

### 1. Node Embeddings

![image-20220307145735983](graphgym.assets/image-20220307145735983-164663625692337.png)

### 2. GNN

![image-20220307145756853](graphgym.assets/image-20220307145756853-164663627770038.png)



## Challenges

### 1. Implementing a GNN Pipeline

![image-20220307145853724](graphgym.assets/image-20220307145853724-164663633479939.png)



### 2. Find Best GNN Design

- GNN Layer
- Aggregation
- Operator

![image-20220307145947877](graphgym.assets/image-20220307145947877-164663638894840.png)



## GraphGym Solution

### 1. Modularized GNN Pipeline

- Head Dict
- ![image-20220307150143641](graphgym.assets/image-20220307150143641-164663650493241.png)

### 2. Design Space

- Intra-Layer -> mainly aggregation + tricks
- Inter-Layer -> GNN layer wise connection design
- Learning Configuration

![image-20220307150231201](graphgym.assets/image-20220307150231201-164663655294242.png)

### 3. Configuration file

![image-20220307150444263](graphgym.assets/image-20220307150444263-164663668583243.png)



### 4. Parallelism

### 5. Domain Application in Finance

![image-20220307150751768](graphgym.assets/image-20220307150751768-164663687292444.png)

## Resources

- ![image-20220307150833455](graphgym.assets/image-20220307150833455.png)

- ![image-20220307150939131](graphgym.assets/image-20220307150939131.png)

## Open Graph Benchmark ： Large Scale Challenge 2021

### 1. Observations：

- Many novel techniques developed for the OGB-LSC large graphs
  - New **mini-batch sampling** for heterogeneous graphs
  - New **label propagation** methods using GNNs.
  - New **knowledge graph embedding** models 
  - New **self-supervised learning** methods for GNNs
  - **Deeper, bigger, and more expressive GNNs**  
    - <img src="graphgym.assets/image-20220307152212618.png" alt="image-20220307152212618" style="zoom:50%;" />
    - <img src="graphgym.assets/image-20220307152236292.png" alt="image-20220307152236292" style="zoom:50%;" />
    - 
    - 