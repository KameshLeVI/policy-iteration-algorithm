# POLICY ITERATION ALGORITHM

## AIM

To develop a Python program to find the optimal policy for the given MDP using the policy iteration algorithm.

## PROBLEM STATEMENT

The bandit slippery walk problem is a reinforcement learning problem in which an agent must learn to navigate a 7-state environment in order to reach a goal state. The environment is slippery, so the agent has a chance of moving in the opposite direction of the action it takes.

### States

The environment has 7 states:

- Two Terminal States: **G**: The goal state & **H**: A hole state.
- Five Transition states / Non-terminal States including **S**: The starting state.

### Actions

The agent can take two actions:

- R: Move right.
- L: Move left.

### Transition Probabilities

The transition probabilities for each action are as follows:

- **50%** chance that the agent moves in the intended direction.
- **33.33%** chance that the agent stays in its current state.
- **16.66%** chance that the agent moves in the opposite direction.

For example, if the agent is in state S and takes the "R" action, then there is a 50% chance that it will move to state 4, a 33.33% chance that it will stay in state S, and a 16.66% chance that it will move to state 2.

### Rewards

The agent receives a reward of +1 for reaching the goal state (G). The agent receives a reward of 0 for all other states.

## Graphical Representation 
![image](https://github.com/KameshLeVI/policy-iteration-algorithm/assets/120780633/d19c9d51-76f6-41c8-8c6a-2873a69a75cb)


## POLICY ITERATION ALGORITHM

The algorithm implemented in the **policy_iteration** is a method used to find the optimal policy in a Markov decision process (MDP).
Here's a step-by-step explanation of the algorithm:

1. Initialize the policy **pi**. In this implementation, a random action is chosen for each state **s** in the MDP **P**. The initial policy is represented by the lambda function **pi=lambda s:{s:a for s,a in enumerate(random_actions)}[s]**, where **random_actions** is a list of randomly chosen actions for each state.

2. Enter a loop that continues until the policy **pi** is no longer changing. This is determined by comparing the previous policy (**old_pi**) with the current policy computed in the loop.

3. Store the previous policy as **old_pi** for comparison later.

4. Perform policy evaluation using the function **policy_evaluation**. This step calculates the state-values (**V**) for each state **s** given the current policy **pi**. The state-values represent the expected cumulative rewards starting from state **s** following policy **pi** and discounting future rewards by a factor of **gamma**. The function **policy_evaluation** is called with the arguments **pi**, **P**, **gamma**, and **theta**.

5. Perform policy improvement using the function **policy_improvement**. This step updates the policy **pi** based on the current state-values **V**. The function **policy_improvement** is called with the arguments **V**, **P**, and **gamma**.

6. Check if the policy has converged by comparing the previous policy **old_pi** with the current policy **{s:pi(s) for s in range(len(P))}**. If they are the same for all states **s**, the loop is exited.

7. Return the final state-values **V** and the optimal policy **pi**.

To summarize, policy iteration iteratively improves the policy by alternating between policy evaluation and policy improvement steps until convergence is reached. The algorithm guarantees to find the optimal policy for the given MDP **P** with a discount factor **gamma**.

## POLICY IMPROVEMENT FUNCTION

```
Developed By: Kamesh D
Reg No: 212222240043
```
```py
def policy_improvement(V, P, gamma=1.0):
    Q = np.zeros((len(P), len(P[0])), dtype=np.float64)
    # Write your code here to implement policy improvement algorithm
    for s in range(len(P)):
      for action in range(len(P[s])):
        for prob, next, r, done in P[s][action]:
          Q[s][action] += prob*(r + gamma*V[next] * (not done))
    new_pi = lambda s :{s:a for s, a in enumerate(np.argmax(Q, axis = 1))}[s]


    return new_pi
```

## POLICY ITERATION FUNCTION

```
Developed By: Kamesh D
Reg No: 212222240043
```
```py
def policy_iteration(P, gamma=1.0, theta=1e-10):
    random_actions = np.random.choice(tuple(P[0].keys()), len(P))
    # Write your code here to implement the policy iteration algorithm
    pi = lambda s: {s:a for s, a in enumerate(random_actions)}[s]
    while True:
      old_pi = {s:pi(s) for s in range(len(P))}
      V = policy_evaluation(pi, P)
      pi = policy_improvement(V, P)
      if old_pi == {s:pi(s) for s in range(len(P))}:
        break
    return V, pi
```

## OUTPUT:
![Screenshot 2024-03-12 143123](https://github.com/KameshLeVI/policy-iteration-algorithm/assets/120780633/29641168-8f4e-4443-b19e-7003ea6ba51c)

![Screenshot 2024-03-12 143136](https://github.com/KameshLeVI/policy-iteration-algorithm/assets/120780633/321322f3-65d3-4804-8f38-1def216537b5)

![Screenshot 2024-03-12 143145](https://github.com/KameshLeVI/policy-iteration-algorithm/assets/120780633/81340e85-f96a-4fa9-8ef6-459864e62cec)

## RESULT:

Thus the Python program to find the optimal policy for the given MDP using the policy iteration algorithm is completed.
