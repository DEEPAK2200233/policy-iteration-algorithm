# POLICY ITERATION ALGORITHM

## AIM
Write the experiment AIM.

## PROBLEM STATEMENT
Explain the problem statement.

## POLICY ITERATION ALGORITHM
The algorithm implemented in the policy_iteration is a method used to find the optimal policy in a Markov decision process (MDP).

Here's a step-by-step explanation of the algorithm:

Step 1 : Initialize the policy pi. In this implementation, a random action is chosen for each state s in the MDP P. The initial policy is represented by the lambda function pi=lambda s:{s:a for s,a in enumerate(random_actions)}[s], where random_actions is a list of randomly chosen actions for each state.

Step 2 : Enter a loop that continues until the policy pi is no longer changing. This is determined by comparing the previous policy (old_pi) with the current policy computed in the loop.

Step 3 : Store the previous policy as old_pi for comparison later.

Step 4 : Perform policy evaluation using the function policy_evaluation. This step calculates the state-values (V) for each state s given the current policy pi. The state-values represent the expected cumulative rewards starting from state s following policy pi and discounting future rewards by a factor of gamma. The function policy_evaluation is called with the arguments pi, P, gamma, and theta.

Step 5 : Perform policy improvement using the function policy_improvement. This step updates the policy pi based on the current state-values V. The function policy_improvement is called with the arguments V, P, and gamma.

Step 6 : Check if the policy has converged by comparing the previous policy old_pi with the current policy {s:pi(s) for s in range(len(P))}. If they are the same for all states s, the loop is exited.

Step 7 : Return the final state-values V and the optimal policy pi.

To summarize, policy iteration iteratively improves the policy by alternating between policy evaluation and policy improvement steps until convergence is reached. The algorithm guarantees to find the optimal policy for the given MDP P with a discount factor gamma.

## POLICY IMPROVEMENT FUNCTION
### Name: Deepak Raj 
### Register Number: 212222240023
```
def policy_improvement(V, P, gamma=1.0):
    Q = np.zeros((len(P), len(P[0])), dtype=np.float64)
    # Write your code here to implement policy improvement algorithm
    for s in range(len(P)):
      for a in range(len(P[s])):
        for prob, next_state,reward, done in P[s][a]:
          Q[s][a]+= prob*(reward+gamma*V[next_state]*(not done))
          new_pi = lambda s: {s:a for s, a in enumerate(np.argmax(Q, axis=1))}[s]

    return new_pi
```
## POLICY ITERATION FUNCTION
### Name: Deepak Raj S
### Register Number: 212222240023
```
def policy_iteration(P, gamma=1.0,theta=1e-10):
  random_actions=np.random.choice(tuple(P[0].keys()),len(P))
  pi = lambda s: {s:a for s, a in enumerate(random_actions)}[s]
  while True:
    old_pi = {s:pi(s) for s in range(len(P))}
    V = policy_evaluation(pi, P,gamma,theta)
    pi = policy_improvement(V,P,gamma)
    if old_pi == {s:pi(s) for s in range(len(P))}:
      break
  return V,pi
```

## OUTPUT:
## optimal policy 
![image](https://github.com/user-attachments/assets/3509d430-5c68-401f-8604-49464851817c)

## optimal value function 
![image](https://github.com/user-attachments/assets/32890bb6-74c2-4ef1-ae48-0f72b889f075)

## success rate for the optimal policy
![image](https://github.com/user-attachments/assets/e0da132a-94d5-4909-aa8c-8b74c0d668aa)

## RESULT:

Write your result here
