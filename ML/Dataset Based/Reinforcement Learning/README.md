# Reinforcement Learning (RL)
```
*Index*
Important terms to learn : 
- Agent: The decision-maker in RL that interacts with the environment to learn a policy.
- Environment: The external system the agent interacts with, providing states and rewards.
- Actions: The choices the agent can make to influence the environment.
- Rewards: Feedback from the environment indicating how good or bad an action was.
- Policy: A strategy or mapping from states to actions that the agent uses to make decisions.
- Value Function: A function estimating the expected cumulative reward from a state (or state-action pair).

Important Algorithms :
- Q(Quality) Learning
- DQN (Deep Q Network)
- Proximal Policy Optimization (PPO)
- Asynchronous Advantage Actor-Critic(A3C)
- Actor-critic using Kronecker-Factored Trust Region (ACKTR)
- Soft Actor-Critic (SAC)
```
- There is no supervisor in this, only a reward signal, more like trial and error
- feedback from the environment is not instantaneous and delayed, i.e. decision made now will unfold after many steps in the future, may give negative rewards further down the line
- has a dynamic system, not like learning from dataset, NOT Independent and identically distributed data, in time , next data is more colleated to previous data
- actions of agent may affect the data it receives afterwards

## Reward Hypothesis

- A reward $R_t$ is a scalar feedback signal and it tells how good the agent is doing at time t. 
- **It maximises cumulative reward.**
- gives positive reward for good action and negative to actions which should be avoided.
- Sequential Decision making : select those actions which maximises total future rewards, even if it means giving up rewards now to get more rewards in the future

## History and State

- History = sequence of observations,actions and rewards $H_t = (A_1,O_1,R_1),...,(A_t,R_t,O_t)$
          = all observed variables till time t
- State= info used to determine what happens next = $\boxed{S_t = f(H_t)}$ = some function of history,i.e. observation,action and reward.
- Environmemt state $S^e_t$ = env's private representation, but this is not visible to the agent. we'll get to know this.
- Agent state $S^a_t$ =  agent's internal representation = info agent uses to pick it's next action = function of History $H_t$ .

## Information State

- Information state/Markov State contains all useful information from history.
- State $S_t$ is **Markov** iff $\boxed{P[S_{t+1}|S_t] = P[S_{t+1} | S_1,S_2,....,S_t]}$
- Future is independent of the past given the present, can throw away the history given the state as it already contains the useful part
- Only the **State** is enough to know the future.
- Eg : markov state for helicopter = position, velocity, rpm , wind direction , etc is enough and so we don't need the posuition or properties of env some 10 min ago or 20 min ago as it's irrelevant to predict next state.
- Non markov state would be only position and rpm(no velocity) and so for this we need to look at histroy to find it's velocity based on position.
- $S^e_t$ and $H_t$ both are markov.
- Agent state should be concrete and form there we'll know to take how much of the history to take and give to agent.
## Observability
- Full observability
  -  Agent directly observes env state 
  - Agent state=information state=environment state
  - $O_t = S^a_t = S^e_t$
  - This is **Markov Decision Process(MDP)**
- Partially obsrvability
  - Agent partially indirectl;y sees env.
  - Robot with camera isn't told corrdinates of position
  - Agent state != environment state
  - Partially observable MDP
  - Here' agent must make it's own state representation, either taking full history or taking most probable event in history or use linear combination of last state and present state as your new state (RNN concept is this only).

## Components of RL Agent

- Components are one/more of these:
  - Policy
    - Agent's behaviour function, how agent picks it's actions
    - One-one mapping from state to action. Some examples : 
        - Deterministic : action=$\pi(s)$
        -  
  - Value function : How good is each action/state, how much reward are we expecting, how much value this action is giving to us
  - Model : how agent represents the env, how agent thinks the env works