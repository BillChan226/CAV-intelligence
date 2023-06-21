## Inverse Reinforcement Learning

### Probabilistic Prediction of Interactive Driving Behavior via Hierarchical Inverse Reinforcement Learning

**Scenario**: ramp-merging scenario

![Definition-of-variables-for-the-highway-on-ramp-merge-scenario](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/Definition-of-variables-for-the-highway-on-ramp-merge-scenario.png)

+ **Deterministic Prediction**
+ **Probabilistic Prediction**

Human’s planning procedure is naturally **hierarchical**, involving both discrete and continuous driving decisions. The discrete driving decisions determine the gametheoretic outcomes of interaction such as to yield or to pass, whereas the continuous driving decisions inﬂuence details of the resulting trajectories in terms of smoothness, distances to other road participants and higher-order dynamics such as velocities, accelerations and jerks.

![image-20230619145056166](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230619145056166.png)





### Driving Behavior Modeling Using Naturalistic Human Driving Data With Inverse Reinforcement Learning

2 important integral facets in AV driving policy:

+ **Human-like**: AVs and human drivers share the road in the near future, which requires AVs to act like humans, thus being predictable and interpretable to other human drivers;
+ **Personalized**: AVs should make decisions according to the user’s personal preferences

**Prior assumption** to use IRL: rational drivers choose actions that optimize their internal reward functions

**Assumption 2**: a human driver follows a stochastic policy, which induces a distribution over generated candidate trajectories, and we assume the distribution is a **Boltzmann distribution** (exponential distribution) related to the returns of trajectories.

The probability of a trajectory is proportional to the exponential of the reward of that trajectory:
$$
P(\zeta|\theta)=\frac{e^{R(\zeta)}}{Z(\theta)}=\frac{e^{\theta^Tf_\zeta}}{Z(\theta)}
$$
However, partition function $Z(\theta)$ requires integrating over the entire class of possible trajectories!!

**Measure**: discretize the trajectory space, and reduce the original space of possible trajectories to small sub-spaces.

thus:
$$
P(\zeta|\theta)=\frac{e^{\theta^Tf_\zeta}}{Z(\theta)}\approx\frac{e^{\theta^Tf_\zeta}}{\sum_{i=1}^Me^{\theta^Tf_\zeta i}}
$$
Goal of Maximum entropy IRL:
$$
\max_\theta J(\theta)=\max_\theta\sum_{\zeta\in D}logP(\zeta|\theta)
$$


#### Related works:

**Driving Behavior Modeling**

+ **Intention estimation**: identify what a driver intends to do in the immediate future
  + Parametric model:
    + **IDM**: intelligent driver model
    + **MOBIL**: minimizing overall braking induced by lane changes
  + Data-driven model:
    + Hiden Markov model
+ **Motion prediction**: predicts the future physical states of a vehicle
  + Parametric model: parametric models generally postulate some structure about the problem, and thereby they are high interpretable and computationally efﬁcient. However, the parametric models are not very expressive to reﬂect complex dynamics and the parameters are hard to specify;
  + Data-driven model: data-driven models enjoy a strong performance but lack interpretability and generalization, which limits their application to safety-critical problems;
+ **Pattern analysis**: extract features or patterns from human driving data that can help us understand the traits of driving behaviors







### Full Vehicle Trajectory Planning Model for Urban Traffic Control Based on Imitation Learning

**Remark 1**: the lateral maneuver of lane changing should be coupled with longitudinal speed in the planning process to generate more realistic vehicle trajectories;

**Remark 2**: human driving behaviors are natural baselines for CAVs;

**Remark 3**: human-like CAV trajectories are less disruptive in the mixed traffic condition with HDVs;



### Maximum Entropy Deep Inverse Reinforcement Learning

Reward Function Approximation with **Deep Architectures**:

Deep architectures are suitable for IRL algorithms (scalable to MDPs) as **they explicitly exploit the depth-breadth trade-off**.

![image-20230620112245580](https://raw.githubusercontent.com/BillChan226/Notebook/main/image/image-20230620112245580.png)

**State reward**:
$$
r \approx g(f, \theta_1, \theta_2, \dots , \theta_n)
$$
**MAP estimation**: Maximize the joint posterior distribution of expert demonstrations, under a **given reward structure** and model parameter $\theta$ :
$$
L(\theta)=\log P(D,\theta|r)=\log P(D|r)+\log P(\theta)
$$
**Derivation**:
$$
P((D,\theta)|r)=P(D|(\theta,r)*P(\theta|r)
$$
**Assumption**: the parameters $\theta$ and the expert demonstrations $D$ are conditionally independent given the reward structure $r$:
$$
\max_{\theta} P((D,\theta)|r)\equiv\max P(D|r)*P(\theta)
$$

therefore by separating into the gradient of the loss with respect to the rewards $r$ and the gradient of the reward with respect to the network’s weights obtained via backpropagation, we have:
$$
\frac{\partial L_D}{\partial \theta}=\frac{\partial L_D}{\partial r}*\frac{\partial r}{\partial \theta}
$$
Usually, the linear reward function assumes that:
$$
R(\zeta)=\sum_t r(s_t)=\theta^T f_\zeta=\theta^T \sum_{s_t \in \zeta }f(s_t)
$$
**Assumption 2**: the distribution is a Boltzmann distribution related to the returns of trajectories, meaning that the higher the return is, the higher possiblity this trajectory is likely to happen.

Thus:
$$
L(\theta)=P(\zeta|\theta) \approx \frac{e^{\theta^T f_\zeta}}{\sum_{i=1}^M e^{\theta^T f_\zeta i}}
$$
However without such assumption, we can only take the reward structure and loss function generally:
$$
\frac{\partial L_D}{\partial \theta}=\frac{\partial L_D}{\partial r}*\frac{\partial r}{\partial \theta}=(\mu_D - E[\mu])*\frac{\partial}{\partial \theta} g(f, \theta)
$$















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



