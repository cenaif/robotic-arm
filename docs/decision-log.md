# Decision Log

Running record of design decisions and the reasoning behind them.
Update as-you-go, not reconstructed after the fact.

## DOF: 4 DOF + gripper (not 3, not 6)
3 DOF only gives planar reach with fixed wrist orientation — IK
collapses to the trivial 2-link law-of-cosines case. 6 DOF needs
either a constrained spherical-wrist geometry or numerical/Jacobian
IK, both out of scope for a first build. 4 DOF (base yaw, shoulder,
elbow, wrist pitch) gives a 3D workspace with closed-form geometric
IK that's still non-trivial.

## Microcontroller: Arduino, not Raspberry Pi
Servo control is a real-time PWM timing problem. Arduino's bare-metal
timing is simpler and more deterministic than the Pi's OS-scheduled
GPIO for this. Revisit a Pi only if a vision/compute stretch goal
gets added later — don't add that complexity up front.

## Structural material: 3D printed PETG (Rapid Prototyping Lab)
PLA is brittle and creeps under sustained servo-horn stress; PETG has
better layer adhesion and impact resistance. Free/cheap iteration
through the lab is the real value — expect 1-2 bracket redesigns once
servo horn mounting is seen in practice.

## Spec revision: 42 cm / 200 g → 32 cm / 100 g reach and payload
Original spec required 19.9-26.5 kg·cm at the shoulder, exceeding
MG996R's rated 11-13 kg·cm even before full safety factor. Rather
than upsizing the shoulder servo (which cascades — heavier
components downstream increase the load further up the chain),
trimmed the reach/payload target. Revised spec clears the original
parts list cleanly. Full numbers in calculations/torque-sizing.md.

## Wrist servo: MG90S over SG90
At the trimmed spec, wrist torque requirement is 1.5-2.0 kg·cm.
SG90 (~1.8 kg·cm rated) covers the 1.5x safety factor but not 2x.
MG90S (~2.2 kg·cm, metal gear, same price/footprint) clears 2x
cleanly — cheap insurance, no redesign required.

## Elbow servo: MG996R kept despite being oversized
Elbow only needs 6.0 kg·cm at 2x SF; MG996R (11-13 kg·cm) is
oversized for this. Kept for now to avoid ordering a second servo
type before printing/assembly proves out the mechanical design —
downsizing later is a low-risk simplification, not shown here as
"open" since it doesn't block anything.
