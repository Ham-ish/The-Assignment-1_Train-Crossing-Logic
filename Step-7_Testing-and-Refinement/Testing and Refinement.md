**Propose at least four test cases based on input combinations.**

| # |                       Inputs (key ones)                       |                      Expected Output/State                     |                        Notes                        |
|:-:|:-------------------------------------------------------------:|:--------------------------------------------------------------:|:---------------------------------------------------:|
| 1 | Incoming Train: TrainInbound 1                                | Warnings ON                                                    | Pre-warning and secure sequence triggers correctly. |
| 2 | TrainApproachLeft=1, others 0                                 | Warnings ON; CmdGateDown until GateDownLimit=1; stay down      | Safe gate closure                                   |
| 3 | Train enters crossing: TrainAtCrossing=1                      | Gates held down;                                               | No raise while occupied.                            |
| 4 | After train clears: TrainAtCrossing=0, Approaches 0, Egress 1 | CmdGateUp until GateUpLimit=1; warnings OFF                    | Verifies safe raise.                                |
| 5 | Obstacle appears while gates down: TrackObstacle=1            | CmdGateUp until GateUpLimit=1; warnings ON                     | Entrapment prevention.                              |
| 6 | Estop Activated: Estop 1                                      | Force fail-safe: warnings ON; command down; set FaultIndicator | Emergency stop                                      |
| 7 | Power/health fault: SystemHealthy=0                           | Fail-safe posture (down + warn + fault)                        | Watchdog/diagnostic behavior.                       |

**Suggest improvements or refinements to the logic circuit.**

 - Refine entrapment safety 
 - Add an additional clearance timer to egress for additional safety
 - Add maximum down time flag that activates FaultIndicator check
