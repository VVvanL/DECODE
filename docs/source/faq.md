# FAQ

- The training does not converge, the loss goes up or stays up instead of going down
    > Please make sure to wait for a couple of epochs (~10). It is normal that strange things happen in the beginning. If that does not help, please reduce the learning rate by setting `param.HyperParameter.opt_param.lr`. You may try it in steps of decreasing the learning rate by a factor of 0.5.

- I get `CUDA out of memory` errors
    > This might happen if your GPU is 
    > 1. Doing multiple things, i.e. used not only for computation but also for the display
    > 2. old
    > 
    > If you have multiple GPU devices you may set: `device='cuda:1'` (where `1` corresponds to the respective index of the device, starting with 0). If you don't have multiple devices, you may want to reduce the batch size: `param.HyperParameter.batch_size`.

- I get errors like `No CUDA capable device found` or CUDA driver issues.
    > This could mean that you really don't have a CUDA capable device (e.g. only an AMD GPU), or that there are
    > driver issues. Please check the following
    ```python
      import spline
      import torch
      
      print(torch.cuda.is_available())
      print(spline.cuda_compiled)
      print(spline.cuda_is_available())
    ```
    > All above should return `True`. When the first one returns `False` it is likely that you experience a CUDA
    > driver issue.