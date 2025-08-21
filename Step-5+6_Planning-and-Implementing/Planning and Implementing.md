**Write a sequence of tasks written using plain English**

Core inputs (Boolean):
TrainInbound: train Train nearing track.
TrainApproach (Left/Right), TrainEgress (Left/Right): train detected in approach zones (directional).
TrainAtCrossing: train occupying the crossing block.
TrackObstacle: obstacle/vehicle detected on the tracks (e.g.radar/LiDAR).
GateUpLimit, GateDownLimit: position limit switches.
EStop: emergency stop request from operator.
SystemHealthy: self-diagnostics OK (watchdog, sensor sanity checks).
Outputs:
CmdGateDown, CmdGateUp: actuator commands (mutually exclusive).
WarnLights, WarnBuzzer: road user warnings.
FaultIndicator: maintenance/alarm output.

Initialize: 
Verify SystemHealthy. If false, set WarnLights+WarnBuzzer ON, command CmdGateDown until GateDownLimit true; set FaultIndicator, else command CmdGateUp until GateUpLimit true.

Pre-warning: 
If (TrainInbound) then turn ON WarnLights+WarnBuzzer.

Secure crossing:
If (TrainApproachLeft OR TrainApproachRight) then command CmdGateDown until GateDownLimit is true.
When opposite (TrainEgress (Left/Right)) true and train at crossing is false then command CmdGateUp until GateUpLimit is true.

Obstacle protection: 
If TrackObstacle is true while gates are down, command CmdGateUp until false, maintain warnings.
Hold during passage: While TrainAtCrossing is true, keep gates down and warnings on.

Clearance logic to raise:
When TrainAtCrossing is false AND no approach is active AND TrackObstacle is false, start a clearance timer (e.g., a few seconds based on approach speed).
If the timer expires without any new detection, command CmdGateUp until GateUpLimit is true; then turn warnings OFF.

Interlocks & exclusivity: 
Never assert CmdGateUp and CmdGateDown together. If both would be true, prefer down.

Emergency stop: 
If EStop is true at any time, go to Step 1 fail-safe posture.

Self-check loop: 
If sensor contradictions occur (e.g., GateUpLimit and GateDownLimit true simultaneously, or near-approach active without far-approach ever having triggered), set FaultIndicator, force Step 1 behavior.

