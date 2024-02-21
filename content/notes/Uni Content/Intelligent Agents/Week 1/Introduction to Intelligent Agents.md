---
title: "Introduction to Intelligent Agents"
---

# Agents and Environments

## Agents 
A computer system capable of autonomous action in some environment, in order to achieve its delegated goals

#### autonomy 
Capable of independent action without need for constant intervention

#### delegation
Acts on behalf of its user or owner

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221007150609.png]]

An agent **perceives** the environment through {sensors}
An agent **acts** on the environment through {actuators}

## Intelligent Agents

Exhibit, at least:
- Reactive behaviour
- Pro-active behaviour
- Social behaviour

### Properties

#### Reactive
Most environments are dynamic

A reactive system maintains an ongoing interaction with its environment and responds to changes that occur in it 

#### Pro-activeness 
- Generating and attempting to achieve goals
- Not driven solely by events
- Taking the initiative
- Recognising oppurtunities

#### Social Ability
The ability in agents to interact with other agents and humans via cooperation, coordination and negotiation

The real world is a multi-agent environment
Cannot attempt to achieve goals without taking others into account
Some goals can only be achieved by interacting with others

#### Rationality 
Agents will act in order to maximise (expected) utility

#### Learning/Adaptation
Agents improve performance over time

### Challenges
- How to represent goals and user preferences
- How to optimise the decision making
- How to learn and adapt and improve over time

## Multi-Agent System (MAS)
Consists of a number of Agents
Agents will act on behalf of users with different goals and motivations with one-another
To successfully interact agents require the ability to
- Cooperate
- Coordinate
- Negotiate

### Design Challenges
- How can cooperation emerge in societies of self-interested agents
- How can self-interested agents recognize conflict and how can they reach agreement
- How can autonomous agents coordinate their activities so as to cooperatively achieve goals

### Collaborative vs Self-Interested

#### Collaborative 
- Agents owned by the same operson/organisation
- Agent design can be controlled and made to coordinate
- More robust compared to 'centralised' system
- Agents easy to control - no incentive needed

#### self-interested/competitive
- Each agent works on behalf of someone else
- Each agent design is different - no control of design of other agents
- Each agents pursues own goals
- Still need to cooperate
- Need mechanisms for resolving conflicts of interest
