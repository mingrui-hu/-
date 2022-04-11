## PyG 2.0 

- Stanford 2021 Graph Workshop

## Message Passing Scheme

### 1. aggregation operator

![image-20220307111428830](Untitled.assets/image-20220307111428830-16466228895802-16466230050584.png)

### 2. message passing interface: 

#### 2.1 `gather` & `scatter_` operator

#### 2.2 edge parallel space

- ![image-20220307111722471](Untitled.assets/image-20220307111722471.png)

### 2.3 fuse message and aggregation computation  

- for better memory efficiency $\mathit{O}(|V|)$

![image-20220307112122242](Untitled.assets/image-20220307112122242-16466232833385.png)

## 3. SOTA GNN layers

- ![image-20220307111828508](Untitled.assets/image-20220307111828508.png)

## 4. Mini-Batching in GNNs

### 4.1 small graphs

![image-20220307130427650](Untitled.assets/image-20220307130427650-16466294688886.png)

### 4.2 single giant graph

- `NeighborLoader`

![image-20220307130543635](Untitled.assets/image-20220307130543635.png)

## 5. Standard Graph Learning Tasks

![image-20220307130650935](Untitled.assets/image-20220307130650935-16466296124827.png)

## 6. packages & ecosystem

- ![image-20220307130835728](Untitled.assets/image-20220307130835728-16466297169158.png)

![image-20220307130854887](Untitled.assets/image-20220307130854887-16466297360569.png)

![image-20220307130921921](Untitled.assets/image-20220307130921921-164662976299210.png)



## 7. PyG 2.0: Advanced Representation Learning on Graphs  

### 7.1 Heterogeneous graph support

![image-20220307131159574](Untitled.assets/image-20220307131159574-164662992135311.png)

### 7.2 challenges

- Heterogeneous graph learning is notoriously challenging
  - **Different input feature distributions** across node and edge **types**
  - Necessity of learning node/edge **type dependent representations** 
    - non-shared weights across different node and edge types 
    - bipartite message passing
  - **Heterogeneous scalability** approaches 
    - Relational-wise neighborhood sampling
  - Complicated implementation 
    - requires **sequentially iterating over different** node and edge **types**
    - involves keeping track of different input feature dimensionalities  

### 7.3 Data Storage & Heterogeneous Connection

- `dict` for storing different types of node features
- ![image-20220307134155173](Untitled.assets/image-20220307134155173-164663171619613.png)
- a full example for **loading raw *.csv files** in the documentation  

### 7.4 Heterogeneous Graph Support

#### 7.4.1 Convert a Homogeneous GNN to Heterogeneous

- learning  **distinct parameters** for **each individual  edge type**  

- ![image-20220307134453982](Untitled.assets/image-20220307134453982-164663189510314.png)

- **Basis decomposition** for regularization

  ![image-20220307134635170](Untitled.assets/image-20220307134635170-164663199621715.png)

#### 7.4.2 conversion of homogeneous GNNs to heterogeneous ones

- `to_hetero(model, (node_types, edge_types))`
- `to_hetero_with_bases(model, (node_types, edge_types))`
- ![image-20220307135001609](Untitled.assets/image-20220307135001609-164663220266816.png)



#### 7.4.3 Heterogeneous Graph (Relational Neighbor) Samplers  

- **relational neighbor sampling**

- for scaling up to large scale graphs

- ![image-20220307135226010](Untitled.assets/image-20220307135226010-164663234706417.png)

  #### 7.4.5 Summary of resources

  ![image-20220307135432945](Untitled.assets/image-20220307135432945-164663247498118.png)

### 8. Graph Gym : Design Space Exploration

- Standardized GNN implementation/evaluation  
- GNN architectures in parallelization
- Hyper-parameter search and visualizations  

### 9. Future Plans

#### 9.1 Temporal Graph

<img src="Untitled.assets/image-20220307135704256.png" alt="image-20220307135704256" style="zoom:67%;" />

#### 9.2 Distributed Data

- While distributed training is possible, distributing data is currently **a user task**
- Scaling to **billions of nodes**  via distributing input data
- **Partitioning** input node and edge features  

#### 9.3 Auto-Scaling  

- Write GNNs in **full-batch mode** and let PyG  figure out the rest  
- GNNAutoScale (ICML 2021)  