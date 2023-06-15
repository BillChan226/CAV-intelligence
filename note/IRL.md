## Inverse Reinforcement Learning

### Probabilistic Prediction of Interactive Driving Behavior via Hierarchical Inverse Reinforcement Learning

**Scenario**: ramp-merging scenario

![Definition-of-variables-for-the-highway-on-ramp-merge-scenario](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/Definition-of-variables-for-the-highway-on-ramp-merge-scenario.png)

+ **Deterministic Prediction**
+ **Probabilistic Prediction**

Human’s planning procedure is naturally **hierarchical**, involving both discrete and continuous driving decisions. The discrete driving decisions determine the gametheoretic outcomes of interaction such as to yield or to pass, whereas the continuous driving decisions inﬂuence details of the resulting trajectories in terms of smoothness, distances to other road participants and higher-order dynamics such as velocities, accelerations and jerks.





### Full Vehicle Trajectory Planning Model for Urban Traffic Control Based on Imitation Learning

**Remark1**: the lateral maneuver of lane changing should be coupled with longitudinal speed in the planning process to generate more realistic vehicle trajectories;

**Remark2**: human driving behaviors are natural baselines for CAVs;

**Remark3**: human-like CAV trajectories are less disruptive in the mixed traffic condition with HDVs;



## Multi-Agent Reinforcement Learning

### Single-Agent RL

> Markov Decision Process: is deﬁned by a tuple $(S,A,P,R,γ)$, where $S$ and $A$ denote the state and action spaces, respectively; $P : S × A \to ∆(S)$ denotes the transition probability from any state $s \in S$ to any state $s' \in S$ for any given action $a ∈ A$; $R : S × A × S \to R$ is the reward function that determines the immediate reward received by the agent for a transition from $(s,a)$ to $s′$ ; $\gamma \in [0,1)$ is the discount factor that trades oﬀ the instantaneous and future rewards.

The goal of solving the MDP is thus to ﬁnd a policy $\pi : S \to \Delta(A)$, a mapping from the state space S to the distribution over the action space $A$, so that a $t ∼ \pi(·|s_t )$ and the discounted accumulated reward is maximized.

![image-20230612132833872](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230612132833872.png)



**Action-value function (Q-function)**: 

![image-20230612133033178](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230612133033178.png)

**State-value function (V-function)**:

![image-20230612133118870](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230612133118870.png)

for any $s \in S$ and $a \in A$, which are the discounted accumulated reward starting from $(s_0,a_0) = (s,a)$ and $s_0= s$, respectively.



**Markovian property**: optimal substructure

+ model known (transition probability and the reward function): dynamic programming/backward induction
+ model unknown: model approximation (reinforcement learning)

#### Value-Based Methods

**Goal**: ﬁnd a good estimate of the Q-function. The (approximate) optimal policy can then be extracted by taking the greedy action of the Q-function estimate.

**Finite state, finite action spaces**

+ Q-learning

  ![image-20230612141951090](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230612141951090.png)

+ SARSA

+ Monte-Carlo tree search (MCTS): UCB, UCT

+ Temporal difference (TD) learning

  

#### Policy-Based Methods

**Goal**: PG searches over the policy space, which is usually estimated by parameterized function approximators like neural networks, namely, approximating $\pi(·|s) ≈ \pi_θ(·|s)$, and then it updates the parameter along the gradient direction of the long-term reward.

![image-20230612142006553](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230612142006553.png)

+ REINFORCE
+ G(PO)MDP
+ Actor-critic algorithms

Compared with value-based RL methods, policy-based ones enjoy better convergence guarantees, especially with neural networks for function approximation, which can readily handle massive or even continuous state-action spaces.

### Multi-Agent RL Framework

![image-20230612142207301](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230612142207301.png)



