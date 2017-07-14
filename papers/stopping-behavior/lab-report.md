# Emergent Speed Modulation Behavior in Multi-Modal Learning for Self Driving Cars

## Intro
Using our fleet of self driving model cars (SDMC) we have collected a large database of driving data under different modes of operation such as following other cars or acting like an animal by hiding in bushes.
## Hypothesis
By training a single network to have different behavioral modes based on input into the network we should see cross modal learning, where behavior present in one mode but not the other makes its way into how the network reacts in the mode without that behavior.
## Procedure
1. Train a network on two behavioral modes, direct and follow mode.
    - Follow mode consists of data with another car in the frame, that the car is actively trying to follow. This mode contains driving data, with a fair amount of speed modulation (slowing down or stopping when the car in front does the same)
    - Direct mode consists of data of the car by itself simply navigating on a path without crashing into obstacles. This mode contains driving mostly at a constant speed, without any stopping.
2. Continue showing it "epochs" or iterations of the entire dataset for training, calculating the online variance for each of the outputs of the network for each epoch of the dataset in each of the modes.
3. Run the network in both behavioral modes in real life, and evaluate their performance.
## Results
- The variance of the motor values in direct mode of the network clearly increase as the network is trained.
- The network commonly exhibits speed modulation behavior in appropriate circumstances when tested in direct mode on the street. (Show examples of network stopping in front of obstacle directly in front of it)
- Future data collection note, it may be interesting to compare the number of neurons that fire when the network is run in the two seperate modes on the same input, it may show some sort of increased correlation over time (demonstrating the network learns to associate things from both modes)

**Will obv. include graphs and stuff showing this data, but don't have all the data yet.**
## Analysis
- This suggests that as the network is trained more, useful behaviors tend to seep between behavioral modes as the network makes associations about it's environment.
## Conclsion
- These results should encourage training of a single network for multiple related behaviors, especially for tasks in self-driving cars since multiple tasks like a turn and a lane change, though fundamentally different have many shared behavioral characteristics.
