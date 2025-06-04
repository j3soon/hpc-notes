# General Discussions

This page contains paraphrased discussions that may be useful for future reference. Also note that these discussions are searchable from the search bar in the website.

For issues related to this page, please [open a GitHub issue](https://github.com/j3soon/hpc-notes/issues).

## Setting p-state on Ubuntu Desktop

Q: How to set p-state on Ubuntu Desktop?

A: Use `nvidia-settings -a "[gpu:0]/GPUPowerMizerMode=<MODE>"` to set the p-state. Example:

```sh
$ nvidia-settings -q "[gpu:0]/GPUPowerMizerMode"

  Attribute 'GPUPowerMizerMode' (pear:0[gpu:0]): 2.
    Valid values for 'GPUPowerMizerMode' are: 0, 1, 2 and 3.
    'GPUPowerMizerMode' can use the following target types: GPU.

$ nvidia-smi | grep -P "P\d"
| 34%   33C    P8             11W /  260W |       6MiB /  24576MiB |      0%      Default |
$ nvidia-settings -a "[gpu:0]/GPUPowerMizerMode=1"

  Attribute 'GPUPowerMizerMode' (pear:0[gpu:0]) assigned value 1.

$ nvidia-smi | grep -P "P\d"
| 33%   36C    P0             59W /  260W |       6MiB /  24576MiB |      0%      Default |
$ nvidia-settings -a "[gpu:0]/GPUPowerMizerMode=2"

  Attribute 'GPUPowerMizerMode' (pear:0[gpu:0]) assigned value 2.

$ nvidia-smi | grep -P "P\d"
| 34%   37C    P8             19W /  260W |       6MiB /  24576MiB |      0%      Default |
```

Reference:

- [Nvidia-settings does not set PowerMizerMode value properly](https://forums.developer.nvidia.com/t/nvidia-settings-does-not-set-powermizermode-value-properly/169361)
