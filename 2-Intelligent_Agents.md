# Intelligent agents

## Agents

### Definitions
- __Agent:__ An agent is anything that can be viewed as perceiving its environment through sensors and acting upon that environment through actuators
- __Percept:__ Perceptual input (eg. text, image, sound, ... )
- __Rational Agent:__ For each possible percept sequence, a rational agent selects an action that maximizes performance measure, given evidence provided by the sequence, and built in knowledge in the agent
- __Performance Measure:__ Criterion for success
   - good vs bad
   - better vs worse
   - clear criterion vs less well defined
- __Rationality:__ reasonably correct
   - not perfection

### Environment types
##### Fully vs Partially
- Fully - everything seen shows all relevant information
- Partially - noise and inaccurate sensors, hidden/missing information

##### Deterministic vs Stochastic
- Deterministic - Next state completely depends on current state and next action by agent
- Stochastic - probabilistic; other factors involved (taxi driver cannot predict behavior of traffic)

##### Episodic vs Sequential
- episodic is self contained, independent situations
   - e.g. agent has to spot defective parts on an assembly. Looks solely at current part and not parts before
- Sequential - current decision affects future ones

##### Static vs Dynamic
- static - environment is fixed during decision making
- dynamic - environment changes while agent is deliberating

##### Discrete vs Continuous
- Discrete - finite number of states
- Continuous - smooth, infinite scale

##### Single agent vs Multi-agent
- single - one agent involved
- multi - more than one (adversarial or cooperative)

<img src="https://github.com/tvand08/Artificial_Intelligence_Review/blob/master/Images/Vacuum_World.png" width="200" height="200">
