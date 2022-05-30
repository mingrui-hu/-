### Evaluation

https://cdlib.readthedocs.io/en/latest/reference/evaluation.html

#### 1. evaluation strategies

- ***Internal*** evaluation through **fitness scores**;
  - Fitness functions allows to summarize the characteristics of a computed set of communities
  - Modularity-based fitness scores
- *External* evaluation through **partitions comparison**.
  - compare different graph partition to assess their resemblance
  - External evaluation scores can be fruitfully used to **compare alternative clusterings** of the same network, but also to asses to what extent an identified node clustering matches a known ***ground truth* partition**.

#### 2. evaluation datasets

- both standard ***synthetic** network benchmarks* and ***real networks** with **annotated ground truth**s*
- [Synthetic Benchmarks](https://cdlib.readthedocs.io/en/latest/reference/benchmark.html)
  - ==no benchmark for edge attributed networks?==
  - **Heterogeneous network？**
- [Network Datasets with Annotated Communities](https://cdlib.readthedocs.io/en/latest/reference/datasets.html)

### Algorithm Table

| Algorithm                      | Network  |          |           |              |          | Communities |          |        |       |              |                |
| ------------------------------ | -------- | -------- | --------- | ------------ | -------- | ----------- | -------- | ------ | ----- | ------------ | -------------- |
|                                | Directed | Weighted | Bipartite | Feature-Rich | Temporal | Crisp       | Overlaps | Nested | Fuzzy | Hierarchical | Time           |
| agdl                           | x        | x        |           |              |          | x           |          |        |       |              | O(n^2)         |
| angel                          |          |          |           |              |          |             | x        |        |       |              | O(n)           |
| aslpaw                         |          |          |           |              |          |             | x        |        |       |              | O(kn)          |
| async_fluid                    |          |          |           |              |          | x           |          |        |       |              | O(m)           |
| belief                         |          |          |           |              |          | x           |          |        |       |              | O(kn)          |
| big_clam                       |          |          |           |              |          | x           | x        | x      |       |              | O(n)           |
| bimlpa                         |          |          | x         |              |          | x           |          |        |       |              | O(m)           |
| chinesewhispers                |          | x        |           |              |          | x           |          |        |       |              | O(km)          |
| condor                         |          |          | x         |              |          | x           |          |        |       |              |                |
| conga                          |          |          |           |              |          |             | x        |        |       |              |                |
| congo                          |          |          |           |              |          |             | x        |        |       |              | O(nm^2)        |
| core_expansion                 |          |          |           |              |          |             | x        |        |       |              | O(nlogn)       |
| cpm                            |          | x        |           |              |          | x           |          |        |       |              |                |
| CPM_bipartite                  |          |          | x         |              |          | x           |          |        |       |              |                |
| coach                          |          |          |           |              |          |             | x        |        |       |              |                |
| danmf                          |          | x        |           |              |          |             | x        |        |       |              |                |
| dcs                            |          | x        |           |              |          |             | x        |        |       |              |                |
| demon                          |          |          |           |              |          |             | x        |        |       |              |                |
| der                            |          | x        |           |              |          | x           |          |        |       |              |                |
| dpclus                         |          | x        |           |              |          |             | x        |        |       |              |                |
| edmot                          |          | x        | x         |              |          | x           | x        |        |       |              |                |
| ebgc                           |          |          |           |              |          |             | x        |        |       |              |                |
| ego_networks                   |          |          |           |              |          |             | x        |        |       |              | O(m)           |
| egonet_splitter                |          |          |           |              |          |             | x        |        |       |              | O(m^3/2 )      |
| eigenvector                    |          |          |           |              |          | x           |          |        |       |              |                |
| em                             | x        |          |           |              |          | x           | x        |        | x     |              |                |
| endntm                         |          |          |           |              |          |             | x        |        |       |              |                |
| eva                            |          |          |           | x            |          | x           |          |        |       |              |                |
| frc_fgsn                       |          |          | x         |              |          |             | x        |        | x     |              |                |
| ga                             |          |          |           |              |          | x           |          |        |       |              |                |
| gdmp2                          | x        |          | x         |              |          | x           |          |        |       |              |                |
| gemsec                         | x        |          |           |              |          | x           |          |        |       |              |                |
| girvan_newman                  |          |          |           |              |          | x           |          |        |       | x            |                |
| graph_entropy                  |          | x        |           |              |          |             | x        |        |       |              |                |
| greedy_modularity              |          |          |           |              |          | x           |          |        |       |              |                |
| head_tail                      |          |          |           |              |          | x           |          |        |       |              |                |
| hierarchical_link_communities  |          |          |           |              |          |             | x        |        |       |              |                |
| ilouvain                       |          |          |           | x            |          | x           |          |        |       |              |                |
| infomap                        | x        | x        |           |              |          | x           |          |        |       |              |                |
| infomap_bipartite              | x        | x        | x         |              |          | x           |          |        |       |              |                |
| ipca                           |          | x        |           |              |          | x           | x        |        |       |              |                |
| kclique                        |          |          |           |              |          |             | x        |        |       |              |                |
| kcut                           |          |          |           |              |          | x           |          |        |       |              |                |
| label_propagation              |          |          |           |              |          | x           |          |        |       |              |                |
| lais2                          |          |          |           |              |          |             | x        |        |       |              | O(cm + n)      |
| leiden                         |          |          |           |              |          | x           |          |        |       |              |                |
| lemon                          |          |          |           |              |          |             | x        |        |       |              |                |
| lfm                            |          |          |           |              |          |             | x        |        |       | x            | O(n^2 logn)    |
| louvain                        |          |          |           |              |          | x           |          |        |       |              |                |
| lpam                           |          |          |           |              |          |             | x        |        |       |              | O(2^m)         |
| lpanni                         |          |          |           |              |          |             | x        |        |       |              | O(n)           |
| lswl                           |          | x        |           |              |          | x           | x        |        |       |              |                |
| lswl_plus                      |          | x        |           |              |          | x           | x        |        |       |              |                |
| markov_clustering              |          |          |           |              |          | x           |          |        |       |              |                |
| mcode                          |          | x        |           |              |          | x           |          |        |       |              |                |
| mnmf                           |          |          |           |              |          |             | x        |        |       |              | O(n^2*m+n^2*k) |
| mod_m                          |          |          |           |              |          | x           |          |        |       |              | O(nd)          |
| mod_r                          |          |          |           |              |          | x           |          |        |       |              | O(nd)          |
| node_perception                |          |          |           |              |          |             | x        |        |       |              |                |
| multicom                       |          |          |           |              |          |             | x        |        |       |              |                |
| nnsed                          |          |          |           |              |          |             | x        |        |       |              | O(kn^2)        |
| overlapping_seed_set_expansion |          |          |           |              |          |             | x        |        |       |              |                |
| paris                          |          | x        |           |              |          | x           |          |        |       | x            |                |
| percomvc                       |          |          |           |              |          |             | x        |        |       |              |                |
| principled_clustering          |          |          |           |              |          |             | x        |        | x     |              |                |
| pycombo                        |          | x        |           |              |          | x           |          |        |       |              | O(n^2 logc)    |
| rb_pots                        | x        | x        |           |              |          | x           |          |        |       |              |                |
| rber_pots                      |          | x        |           |              |          | x           |          |        |       |              |                |
| ricci_community                |          |          |           |              |          | x           |          |        |       |              |                |
| r_spectral_clustering          |          |          |           |              |          | x           |          |        |       |              |                |
| sbm_dl                         |          |          |           |              |          | x           |          |        |       |              |                |
| sbm_dl_nested                  |          |          |           |              |          | x           |          |        |       |              |                |
| scan                           |          |          |           |              |          | x           |          |        |       |              | O(m)           |
| scd                            |          |          |           |              |          | x           |          |        |       |              |                |
| spectral                       |          |          | x         |              |          | x           |          |        |       |              |                |
| significance_communities       |          |          |           |              |          | x           |          |        |       |              |                |
| sibilarity_antichain           | x (DAG)  |          |           |              |          | x           |          |        |       |              |                |
| slpa                           |          |          |           |              |          |             | x        |        |       |              | O(kn)          |
| spinglass                      |          |          |           |              |          | x           |          |        |       |              |                |
| surprise_communities           | x        | x        |           |              |          | x           |          |        |       |              |                |
| symmnmf                        |          |          |           |              |          |             | x        |        |       |              |                |
| threshold_clustering           | x        | x        |           |              |          | x           |          |        |       |              |                |
| tiles                          |          |          |           |              | x        |             | x        |        |       |              |                |
| umstmo                         |          |          |           |              |          |             | x        |        |       |              |                |
| walkscan                       |          |          |           |              |          |             | x        |        |       |              |                |
| walktrap                       |          |          |           |              |          | x           |          |        |       |              | O(n^2 logn)    |
| wCommunity                     |          | x        |           |              |          |             | x        |        |       |              |                |

