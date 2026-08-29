# Prototype 1 — Thruster Requirements

**Project:** SDU Underwater Mapping AUV  
**Subsystem:** Propulsion  
**Status:** Preliminary requirements  
**Date:** 29 August 2026

## 1. Purpose

This document defines the preliminary requirements for the thrusters used on Prototype 1 of the underwater mapping vehicle.

Prototype 1 is currently planned as a tubular vehicle using four thrusters:

- 2 horizontal thrusters for surge and yaw
- 2 vertical thrusters for heave and pitch

The purpose of these requirements is to guide future component research and comparison. They do not yet specify a final thruster model.

---

## 2. Thruster Configuration

Prototype 1 shall initially use four independently controlled underwater thrusters.

The preferred configuration is:

- H1 — horizontal left
- H2 — horizontal right
- V1 — vertical front
- V2 — vertical rear

The horizontal pair shall provide:

- forward/reverse motion
- differential yaw control

The vertical pair shall provide:

- vertical motion
- depth control
- differential pitch control

Roll stability shall primarily be achieved through passive mechanical stability using the separation between the center of buoyancy and center of mass.

Direct sway actuation is not required for Prototype 1.

---

## 3. Thruster Type

Candidate thrusters should preferably:

- use a brushless DC motor
- be designed specifically for submerged operation
- use a flooded or otherwise underwater-compatible motor design
- avoid rotating shaft seals where practical
- operate in both forward and reverse
- be suitable for repeated operation in fresh, brackish, and salt water

Standard aerial drone motors that are merely capable of spinning underwater should not be considered sufficient without evidence of corrosion resistance and long-term submerged suitability.

---

## 4. Preliminary Thrust Range

The current working vehicle mass estimate is approximately:

5–7 kg

The expected survey speed is approximately:

0.3–0.7 m/s

Based on preliminary drag estimates, individual thrusters in approximately the following range should initially be investigated:

1–3 kgf maximum thrust per thruster

Equivalent force:

1 kgf ≈ 9.81 N

Therefore:

1–3 kgf ≈ 10–30 N

This range is preliminary and shall be revised after:

- vehicle dimensions are better known
- drag is modeled more accurately
- current disturbance requirements are defined
- actual thruster performance data is compared
- Prototype 1 mass is estimated more accurately

Maximum thrust alone shall not determine thruster selection.

---

## 5. Bidirectional Operation

All four thrusters shall support bidirectional operation.

The horizontal thrusters require reverse thrust for:

- reverse vehicle motion
- differential yaw control
- disturbance correction

The vertical thrusters require reverse thrust for:

- upward and downward motion
- depth control
- pitch control

Forward and reverse thrust shall not be assumed to be equal.

Candidate thruster data should include reverse thrust performance where available.

---

## 6. Counter-Rotating Propellers

Where possible, paired thrusters should use opposite propeller rotation directions.

Preferred arrangement:

- H1 — CW
- H2 — CCW
- V1 — CW
- V2 — CCW

The exact orientation may change with the final mechanical layout.

The objective is to reduce unwanted reaction torque from the propellers.

Candidate thrusters should therefore preferably have both clockwise and counter-clockwise propeller options available.

---

## 7. ESC Requirements

Each thruster shall be controlled by a reversible electronic speed controller (ESC).

The ESC shall:

- support bidirectional brushless motor operation
- support the operating voltage of the selected battery
- support the maximum expected thruster current with suitable safety margin
- accept a control method compatible with the selected autopilot / ArduSub system
- provide a neutral/stop command between forward and reverse operation

ESC current ratings shall include safety margin above the expected maximum motor current.

ESCs are initially expected to be located inside the dry pressure housing.

Thermal management inside the sealed housing shall therefore be considered during later design.

---

## 8. Electrical Requirements

The propulsion system should preferably operate from a practical low-voltage battery system suitable for Prototype 1.

Candidate systems around common 3S/4S lithium battery voltage ranges should initially be investigated.

The final voltage shall be selected based on:

- thruster efficiency
- ESC compatibility
- maximum current
- wiring losses
- battery availability
- power distribution
- electronics compatibility

Higher voltage may reduce current for a given power level, but unnecessarily high system voltage should be avoided for the first prototype.

---

## 9. Efficiency Requirements

Thrusters shall not be compared only by maximum thrust.

The most important comparison should be performance around the expected normal operating point.

Candidate data should preferably include:

- thrust versus command
- thrust versus current
- thrust versus electrical power
- forward thrust
- reverse thrust

A useful comparison quantity is:

thrust / electrical power

especially in the thrust range expected during normal survey operation.

Prototype 1 is expected to spend most of its operating time well below maximum thrust.

---

## 10. Environmental Requirements

Thrusters should be suitable for operation in:

- freshwater
- swimming pools
- brackish Baltic water
- coastal saltwater environments

Materials should resist corrosion caused by repeated submerged operation.

Particular attention shall be paid to:

- bearings or bushings
- motor laminations
- magnets
- exposed copper
- fasteners
- electrical cable
- connectors

Thrusters should be rinsed and maintained as required after salt/brackish-water testing.

---

## 11. Propeller Protection

A ducted or shrouded propeller is preferred for Prototype 1.

The shroud should provide:

- protection against accidental propeller contact
- some protection against external objects
- suitable low-speed/static thrust performance

The design should also consider possible ingestion of:

- seaweed
- grass
- fishing line
- plastic
- other debris

Thrusters should remain reasonably accessible for inspection and cleaning.

---

## 12. Mechanical Requirements

Candidate thrusters should:

- have a rigid and simple mounting method
- allow easy removal and replacement
- fit the modular Prototype 1 structure
- permit adjustment of thruster position during development where practical
- have known dimensions and mass

The horizontal thrusters will be laterally separated to generate yaw torque.

The vertical thrusters will be longitudinally separated to generate pitch torque.

Final moment arms shall be determined later.

---

## 13. Documentation Requirements

Preference shall be given to thrusters with good manufacturer documentation.

Useful documentation includes:

- voltage range
- current consumption
- maximum power
- forward thrust
- reverse thrust
- thrust-current curves
- thrust-power curves
- dimensions
- mass
- propeller type
- CW/CCW availability
- recommended ESC specifications
- environmental limitations

A low-cost thruster with little or no reliable performance data may require bench testing before it can be accepted for the vehicle.

---

## 14. Cost and Maintainability

Prototype 1 is intended to remain relatively low cost.

The preferred thruster should be affordable enough that:

- four thrusters can be purchased
- ideally one spare thruster can also be obtained
- replacement parts are reasonably accessible

Using four identical thrusters is preferred because this simplifies:

- purchasing
- spare parts
- ESC selection
- mechanical mounting
- software configuration
- maintenance

Different horizontal and vertical thrusters may be considered later if there is a significant performance, mass, or cost advantage.

---

## 15. Current Candidate Benchmark

The Blue Robotics T200 may be used as a reference benchmark when comparing lower-cost thrusters.

It is not currently selected for Prototype 1.

It provides useful published data for:

- thrust
- current
- voltage
- forward/reverse performance
- underwater construction

Prototype 1 may require substantially less maximum thrust than a T200-class propulsion system.

---

## 16. Parameters Still To Be Determined

The following values remain open:

- final required thrust per thruster
- final operating voltage
- final ESC current rating
- required continuous thrust
- required peak thrust
- minimum acceptable reverse thrust
- required efficiency
- exact horizontal thruster spacing
- exact vertical thruster spacing
- final vehicle mass
- final drag coefficient
- maximum design current
- tether drag
- acceptable cross-current disturbance
- final selected thruster model

These values shall be refined through simulation, component research, and physical testing.
