# CAV-intelligence

This repository contains the algorithms implementation for vehicles scheduling, dispatching and planning in complicated scenarios such as intersection, junction etc.



## Learnable Driving Policies

**Goal**: To enable CAVs(Connected and Autonomous Vehicle) to imitate the driving policy of HDVs(Human-Driven Vehicle), we apply inverse reinforcement learning to learn weight parameters for our designed cost function so that the learned policy can generate trajectories close to the ground truth trajectories.



**Scenario**: semi-structured driveways(the driveways are mostly curved lines, however no roadlanes are given and the vehicles are not obliged to follow general traffic rules)



**Cost Function Design**: the peculiarity of the scenario results in the special design of cost functions. A reference design for cost functions in structured roadways are given [here](https://journals.sagepub.com/doi/pdf/10.1177/03611981221077263?casa_token=PXPXk8dnYnEAAAAA:MIeZKgh95GF0x8GJ_94hqZBNKUJ9T4NM9_ecZoUjv-vla_jtglaQOVihJz1KKd1cfFfDGrUnwGT4Ug). However, in this paper the author considers structured driveways with conventional driving behaviors(in-lane following and lane changing), which is easier since the dimension of the action space is degraded. Here in this semi-structured driveway scenarios, we need to adapt these cost function terms accordingly.