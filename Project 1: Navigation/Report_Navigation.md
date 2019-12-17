## Report for Project 1. Navigation

### Introduction
In this project, the Deep Q-learning algorithm, which belongs to the value-based methods in deep reinforcement learning was applied to solve a specific environment using Unity Machine Learning Agents, which provide convenient environments for training intelligent agents. In this environment, an agent was trained to navigate to collect bananas in a squared world. Two kinds of color, i.e., blue and yellow, of bananas are demonstrated. The agent would be rewarded with -1 if it collected a blue banana, and would be rewarded with 1 if it collected a yellow banana. Thus, it is expected that the agent should try to collect yellow bananas and to avoid blue bananas while acting. In particular, the agent has four available actions, which are moving forward, moving backward, turning left and turning right.

### Deep Q-Learning Algorithm
In order to understand how to train the agent, the algorithm, i.e. Deep Q-Learning (Mnih et al., 2015), should be spelled out in the first place. At first, according to the basic idea of Q-Learning, the optimal Q-values are updated based on the action-value function using rewards and the current Q-values. The strategy to find the optimal values is then:

![Q](https://github.com/tnyng/udacity-deep-reinforcement-learning/blob/master/Project%201:%20Navigation/pics/qvalue.PNG)

 As it is expected that the predicted Q-values from the trained Q-network should be as close as possible to the optimal Q-values, the loss function for training the Q-network then can be written as:

![Loss](https://github.com/tnyng/udacity-deep-reinforcement-learning/blob/master/Project%201:%20Navigation/pics/dqn_loss.PNG),

 which uses the mean-squared error as the estimator.

After figuring out how the loss function looks like, we could turn to the algorithm of DQN. The core contribution of the algorithm is the introduction of replay buffer as well as experience replay. The idea of experience replay derives from the consideration of the sequence of observation. Since the observation is a time series, the update of the Q-values is highly correlated, and thus the results will be affected by the data distribution. For the purpose of removing these correlations in sequence, the transitions, which are the experience tuples *(S,A,R,S')*, will be gradually stored in the replay buffer. The next steps are then randomly sampling minibatch of the transitions from the replay buffer and performing gradient descent. 

### Implementations and Results
The hyperparameters for training the agent are listed as followed:

- Replay buffer size: 1e5
- Batch size: 64
- Discount factor (Gamma): 0.99
- Tau: 1e-3
- Learning rate: 5e-4
- Update frequency: 4

- Maximum number of training episodes (n_episodes): 2000
- Maximum number of timesteps per episodes (max_t): 1000
- Starting value of epsilon (eps_start): 1.0
- Minimum value of epsilon (eps_end): 0.1
- Multiplicative factor (per episode) for decreasing epsilon (eps_decay): 0.995

The environment was solved in 413 episodes, which means that the average score exceeded 13 after 413 episodes. The trend of the scores in the training process is plotted as:

![Result](https://github.com/tnyng/udacity-deep-reinforcement-learning/blob/master/Project%201:%20Navigation/pics/result.jpg)

And the actions the agent take with trained weights can be viewed as:

![Trained](https://github.com/tnyng/udacity-deep-reinforcement-learning/blob/master/Project%201:%20Navigation/pics/trained.gif)

### Ideas of Future Work
The algorithm of Deep Q-Learning was used to train the agent, and the score it got seems also fair. However, I have barely applied the nature DQN algorithm and did not extent the method to its variants like Double DQN, Dueling DQN or DQN with prioritized experience replay. Using these improvement of DQN might lead to a better performance of training the agent. Moreover, as I only slightly changed the hyperparameters the previous exercise provides, which showed already results better than the benchmark, it is also meaningful to do a hyperparameters search in the future to find a better set to make improvements.



Reference:

Mnih, V., Kavukcuoglu, K., Silver, D., Rusu, A. A., Veness, J., Bellemare, M. G., ... & Petersen, S. (2015). Human-level control through deep reinforcement learning. Nature, 518(7540), 529.
