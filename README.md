# Robotic Arm

A 4-DOF robotic arm built from scratch — mechanical design, torque
analysis, kinematics, and control — as a semester-long project.

## Specs
- 4 DOF (base yaw, shoulder pitch, elbow pitch, wrist pitch) + gripper
- 32 cm reach, 100 g payload capacity
- MG996R (shoulder, elbow), MG90S (wrist), SG90 (gripper)
- Arduino-controlled, PETG printed links

## Status
🔧 In progress — electronics bring-up

## Structure
- `calculations/` — torque sizing and kinematics derivations
- `cad/` — SolidWorks files and exports
- `firmware/` — Arduino code
- `docs/` — decision log and bill of materials
- `media/` — build photos/videos
