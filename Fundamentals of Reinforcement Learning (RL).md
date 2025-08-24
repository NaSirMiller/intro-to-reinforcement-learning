# What is RL?
An area of machine learning (ML), where an intelligent _agent_ needs to learn through trial and error, how to take _actions_ inside an _environment_ in order to maximize a cumulative _reward_.

![[Pasted image 20250720154513.png]]
## Definitions
- Agent: An entity that learns to make decisions through the observation of states within an environment to maximize reward.
- Environment: The world the agent is learning in.
- State: The current version of the environment.
- Reward: A result of a sequence of actions that influence the agent's decision making.
- Cumulative Reward: The **total sum of rewards** an agent receives over time.
	- Preferred in problems that want to perform well in the **long run**
- Marginal Reward: The **incremental reward** gained by taking an action or making a decision relative to a baseline or previous choice.
	- Metric to analyze the immediate impact of an action
- Control problem: A problem where the goal is to learn/determine a strategy that directs how a system should behave over time to achieve an objective.
- Policy: A learned mapping from states to actions.
	- Solving a RL problem means finding the best possible policy, $\pi$.
	- Deterministic: Map each state to one action
		- $\pi(state)=action$
	- Stochastic: Map each state to a probability distribution over all possible actions.
		- $\pi(state)=(prob action 1, prob action2, ..., prob action N)$
	- Optimal: A policy where at state $s$ the agent chooses the action $a$ that maximizes the q-value function.
		- $\pi^{*}(s)=argmax_{\pi}E[R_{t} | s_{t} = s, \pi]$
			- $E[Rt​∣s_{t}​=s,π]$: The expected cumulative reward the agent receives starting from state $s$ at time $t$ if it follows policy $\pi$
			- $argmax_{\pi}$: Searching over all possible policies, choose the one that maximizes the expected return
* Value: A number associated with each state, $s$, of the environment that estimates how good it is for the agent to be in state $s$.
	* it is the cumulative reward the agent collects when starting at state $s$ and choosing actions according to policy $\pi$
- Value function: A learned mapping from states to values.
	- $v_{\pi}=$ _cumulative reward when the agent starts at state $s$ and follow policy $\pi$
	- Can infer an optimal policy, $\pi*$, from the optimal q-value function.
- q-value functions: A learned mapping of (action, state) pairs to values.
	- $q_{\pi}(s, a)=$ _cumulative reward when the agent starts at state $s$ takes action $a$ and follows policy $\pi$ thereafter
- Bellman Equation: The optimal value function (or q-value function).
	- $q_{\pi*}(s,a) = E[R_{t+1} + \gamma max_{a'}q_{\pi*}(s', a')]$
		- The optimal action-value of taking action $a$ in state $s$, under the best possible policy $\pi^{*}$ is equal to the expected immediate reward $R_{t+1}$ plus the discounted value of the best action in the next state $s'$
	- Can be transformed into an iterative procedure to find the optimal value function.
- Simulated environment: Mimics the real world so an agent can try actions and observe outcomes without real-world costs
		- Ex: OpenAI gym
- Epsilon: A parameter that controls the exploitation-exploration trade-off.
	- Ensures the agent explores the environment enough before drawing definite conclusions on what is the best action to take in each state.
	- Ranges is $[0, 1]$
	- Set at a large value, _i.e 50%_ and decrease after each episode such that the agent explores a lot in the beginning and less as it improves.
* Discount factor ($\gamma$): Weighs future rewards.
	* Usually set to decay
	* Range is $[0, 1]$
- Exploration-Exploitation Problem: The trade off between exploring new strategies versus sticking to already known approaches.
## Benefits of RL
1. Problems that do **not** have labeled input-output pairs
2. The environment of the problem is stochastic.
3. A model needs to interact with an environment.
4. Ideal for control problems.

### How to Generate Training Data
1. Simulated environments.
	- Pros:
		1. Resembles real world environment
	- Cons:
		1. Computationally expensive
		2. Difficult to implement

#### Popular Simulated Environments
1. OpenAI Gym: General purpose API that provides standardized API for a collection of environments.
2. MuJoCo: 3D environments for continuous control tasks (_i.e learning to walk_)
3. CARLA: Open urban driving simulator.
## Important Notes
1. An agent does not need to understand the environment to make decisions, it can learn through the observation of the state of the environment.
2. Stochastic policies are preferred in stochastic environments such as those where there are actions that are **not** deterministic.
3. We can use value functions rather than directly finding $\pi^{*}$
4. The optimal policy is not always greedy
5. Q-Learning methods focus on finding optimal q-value functions.
6. It is a best practice to set epsilon as decaying value
7. A mapping is simply of form $\pi(s)=a$

### Examples
#### Marginal versus Cumulative Reward
Given a game of capture the flag, lets map actions to rewards:
- +10 points for a kill
- +5 for capturing a flag
- -2 for dying
Now lets use an example sequence of actions:

| Action       | Marginal Reward | Cumulative Reward |
| ------------ | --------------- | ----------------- |
| Kill         | +10             | +10               |
| Die          | -2              | +8                |
| Flag capture | +5              | +13               |


