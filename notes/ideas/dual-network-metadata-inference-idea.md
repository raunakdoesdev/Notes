  # Dual Network Metadata Inference
  
  ## Expectations
  I'm not expecting the double network metadata inference to perform better than the standard Z2Color. I do expect it to perform better than a randomly generated vector as metadata inserted into Z2Color. The only advantage this new network has is that it's modal input isn't binary between modes. Even a human given just two frames of data from a camera would not be able to tell what mode you are in, from our current list of metadata modes.
  
  ## Temporal Expansion
  It maybe interesting to give SqueezeNet more frames for inference and build and LSTM or GRU into it.
  - [ ] Talk to SqueezeNet person about temporal expansion within the network, and the best location to place an LSTM or GRU within the network.
  
  The main problem is that more frames takes more time to run, which is not good. One idea could be giving SqueezeNet a non uniform series of time steps. Like the two most current time steps and then 3 more time steps from the past with a larger gap between them. As long as we are consistent with this, the network could learn more importaint details from the past and be better suited to calculating the mode.
  
  This might not even be neccessary for SqueezeNet. We could actually space out the images we are sending into squeezenet uniformly while only giving z2color (the driving network) the most recent two frames. Z2Color doesn't need memory if the metadata input is chosen well, but SqueezeNet does, and cares less about the present.
  
  ## Modes
  
  The modes we have right now aren't suited well for modal inference, I suggest we switch the current modes for things like:
  - Left
  - Right
  - Lane Change
  - Stop
  - Follow
  - Go
  
  Basically the idea is to have SqueezeNet's mrysfsys explicitly telling Z2Colors what actions to take, while Z2Color executes those actions smoothly and also maintains the basic security of the car (avoids obstacles ensures driveable terrain). This allows the vehicle to drive in **both structred and nonstructured conditions** and allows for easier integration of new data, it would be simpler to add GPS input to data for SqueezeNet while continuing to have the same behavior with the trained Z2Color network.
  
  ## Why SqueezeNet?
  
  SqueezeNet was chosen for a couple of reasons. The ImageNet problem is remarkably similar to the metadata inference problem, in both situations, you need to analyze different segments of the image and come to an understanding of what is in the image (stop sign or red light translates to stop mode), GPS next turn left and a stoplight translates to a left + lane change, and then a stop soon after, etc. We also need the network to be extremely fast and able to run on our model cars. The network that fits these characteristics is very clearly SqueezeNet.
