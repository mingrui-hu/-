#### Spatial Dropout 1D

 https://discuss.pytorch.org/t/spatial-dropout-in-pytorch/21400/4

>   In both Keras and PyTorch after applying embedding on [batch, time] sequence you get [batch, time, channels] tensor.
>
>   Keras’ SpatialDropout1D applies `[*, 1, *]` noise mask - i.e. drops out a subset of channels for all timestamps simultaneously, whereas PyTorch’s Dropout*D uses `[*, *, 1]` mask - it drops out all channels for a subset of timestamps.
>
>   So, if you just naively replace SpatialDropout1D() by nn.Dropout2d() it’ll work but with changed semantics - instead of dropping out whole embedding channels you’ll be dropping out whole words (in NLP case), which works less well in my experience.

```
x = x.permute(0, 2, 1)   # convert to [batch, channels, time]
x = F.dropout2d(x, p, training=self.training)
x = x.permute(0, 2, 1)   # back to [batch, time, channels]
```

