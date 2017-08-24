# Tasklist for Demo Network Training

## Network Architecture

- [ ] Design a network architecture to suit Karl's needs. Here they are listed:

> Left:
> 1) R G B 3
> 2) G 4
> 3) G 5
> 4) G 6
> 5) G 7
> 6) G 8
> 7) G 9
> 8) G 10
> 
> Right:
> 1) G 11
> 2) G 12

## Training Code Modification

- [ ] Make modifications to training code to allow for flexible # of input frames and be able to assign any of the channels from each of these frames in a simple easy to read format.
- [ ] Experiment with Modal Info, try seeing where modal info can be inserted to optimize performance, as well as the maximum number of modal inputs before the network becomes confused at the differences between the modal inputs (LOWER PRIORITY)

## Inference Code Modification

- [ ] Make modifications to the training code to allow for flexible # of input frames, and use the custom network architecture designed above.
- [ ] On the inference side I'm guessing the networks will run MUCH too slow due to the conversion of so many frames of input into pytorch tensors seperately. I would do the following which Dustin suggested and assign this to Eric, since he knows more about TH and base Torch:

    > While using ROS camera capture, it’s not uncommon to experience slower camera streaming.   The memory management isn’t the best.  What I would recommend is using ZED SDK or V4L2 directly from a high-performance C/C++ library to THFloatTensor (or rather, THCudaTensor) and python.  To get the THFloatTensor/THCudaTensor containing the video frame into python, you can embed the interpreter into C/C++ and use the THP api to get the associated PyObject or use the PyTorch ffi extensions to retrieve the object from C/C++.  This will avoid extra memory copies.  This approach mirrors how I used to to it with LUA torch (using luaT library).   However, I also found this V4L2 package for python here:
    >  
    > https://pypi.python.org/pypi/v4l2
    >   
    > So you could get the camera video from that and create the torch.cuda.FloatTensor without leaving Python.  Or if you require ZED SDK, use the PyTorch ffi extensions from above to wrap ZED SDK as python.

    - If Eric ends up taking this on I can forward this entire thread to him contianing some more links and helpful info about the topic.
