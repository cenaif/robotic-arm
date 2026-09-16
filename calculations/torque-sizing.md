# Torque Sizing

## Method
For each joint, sum the torque contributed by every link and payload
downstream of that joint, worst case (arm fully horizontal):

    τ_required = Σ (m_i × g × d_i)

where d_i is the horizontal distance from the joint to each downstream
mass's center. A safety factor of 1.5-2x is applied on top to account for
printed-part flex, dynamic loads during acceleration, and real servos
underperforming their datasheet stall rating.

## Revision 1: 42 cm reach, 200 g payload (rejected)

Link lengths: L1 = 18 cm, L2 = 15 cm, L3 = 9 cm

| Joint    | Static torque | ×1.5 SF   | ×2 SF     |
|----------|---------------|-----------|-----------|
| Wrist    | 2.1 kg·cm     | 3.2 kg·cm | 4.2 kg·cm |
| Elbow    | 6.5 kg·cm     | 9.8 kg·cm | 13.0 kg·cm|
| Shoulder | 13.3 kg·cm    | 19.9 kg·cm| 26.5 kg·cm|

**Result:** shoulder requirement (19.9-26.5 kg·cm) exceeds MG996R's rated
11-13 kg·cm even before safety factor is fully applied. Spec rejected —
see decision log.

## Revision 2: 32 cm reach, 100 g payload (adopted)

Link lengths: L1 = 14 cm, L2 = 11 cm, L3 = 7 cm

| Joint    | Static torque | ×1.5 SF   | ×2 SF     |
|----------|---------------|-----------|-----------|
| Wrist    | 1.0 kg·cm     | 1.5 kg·cm | 2.0 kg·cm |
| Elbow    | 3.0 kg·cm     | 4.5 kg·cm | 6.0 kg·cm |
| Shoulder | 6.5 kg·cm     | 9.8 kg·cm | 13.0 kg·cm|

**Result:** all three joints clear at 1.5x SF; shoulder clears exactly at
2x SF (MG996R rated 11-13 kg·cm). Adopted spec.

## Servo selection (final)

| Joint    | Servo   | Rated stall torque | Margin at adopted load |
|----------|---------|---------------------|--------------------------|
| Shoulder | MG996R  | ~11-13 kg·cm         | meets 2x SF (13.0 kg·cm) |
| Elbow    | MG996R  | ~11-13 kg·cm         | oversized (6.0 kg·cm needed) — downsize candidate |
| Wrist    | MG90S   | ~2.2 kg·cm           | meets 2x SF (2.0 kg·cm) — SG90 (~1.8) would not |
| Gripper  | SG90    | ~1.8 kg·cm           | minimal load, ample margin |
