## RuntimeError: DataLoader worker (pid 4068913) is killed by signal: Killed.

https://github.com/pytorch/pytorch/issues/8976



我的原因:  `dmesg -T` --> killed worker OOM