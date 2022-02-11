### pad & pack

https://androidkt.com/pads-and-pack-variable-length-sequences-in-pytorch/



## ranking vector

-   sort twice == rank

    https://math.stackexchange.com/questions/3607762/why-does-sorting-twice-produce-a-rank-vector

## zeros_like

-   By default, its `requires_grad = False`,  -> detached from the graph

## torch.sort

`sort_values, sort_indices = torch.sort()`

-   `sort_values` is differentiable 
-   `sort_indices` is not (b.c. inner `torch.argsort()`)

#### inplace gradient ReluBackward

`nn.ReLu(inplace=False)`
