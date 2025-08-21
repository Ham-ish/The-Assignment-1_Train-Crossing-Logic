**Restate the problem in your own words.**
Describe the logical system behind a Train/Car intersection gate so that the gates go down when a train is near. The system should favor fail-safe behaviour

**Identify and describe all inputs and outputs of the system**
The inherent inputs and outputs of this system are the boolean inputs of TrainPresent and TrainInComing, and the output of GateState. Other inputs could be related to the way the system measures the trains distance from the gate

**Describe the context, constraints (technical, economic, social, environmental, legal), and stakeholders you can think about.**
Technical: 
Train detection will likely be needed on the track in both directions
Concerned about false positives/negatives
Economic:
Cost of Maintenance
Social:
Minimising car delays, but not at the cost of safety
Legal:
Comply with regulations and road rules and such

Stakeholders:
Car/Train drivers
Maintenance teams
Transportation infrastructure team
