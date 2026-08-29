# Autonomous Underwater Mapping Vehicle

## System Requirements — Version 0.1

**Project:** SDU Underwater Mapping AUV
**Version:** 0.1
**Date:** 29 August 2026
**Status:** Initial research requirements

---

## 1. Project Goal

The long-term goal of the project is to develop a low-cost autonomous underwater vehicle capable of surveying coastal underwater environments and generating bathymetric maps of the seabed.

The system should eventually be capable of performing a predefined survey mission with minimal operator intervention.

The initial development environment will focus on shallow-water operation in controlled environments and coastal waters near Sønderborg, Denmark.

The project will be developed incrementally:

1. Software simulation
2. Tethered manually controlled ROV
3. Stabilized ROV
4. Sonar-equipped mapping ROV
5. Underwater localization system
6. Autonomous underwater vehicle
7. Autonomous bathymetric mapping

---

# 2. Primary Mission

The final prototype shall be capable of performing the following mission:

1. Start at the water surface.
2. Determine its initial position using GPS.
3. Receive a predefined survey area.
4. Dive to the required operating depth.
5. Navigate toward the survey area.
6. Follow a predefined survey pattern.
7. Measure the seabed using sonar.
8. Record vehicle position, orientation, depth and sonar measurements.
9. Complete the survey.
10. Return toward the recovery position.
11. Surface automatically.
12. Provide the recorded data for generation of a bathymetric map.

A typical survey pattern will be a lawnmower pattern.

Example:

```text
START

A ─────────────────→ B
                     │
C ←──────────────────┘
│
└──────────────────→ D
                     │
E ←──────────────────┘
│
└──────────────────→ F

SURVEY COMPLETE
```

---

# 3. Initial Operating Environment

The vehicle is intended primarily for shallow-water coastal operation.

Initial target environment:

* Baltic Sea coastal waters near Sønderborg
* Lakes
* Harbours
* Swimming pools or controlled test basins during development

The system shall be designed with the expectation of:

* low underwater visibility;
* suspended particles;
* moderate water currents;
* salt or brackish water;
* vegetation;
* uneven seabed;
* low underwater lighting.

The vehicle shall therefore **not depend on visual camera data to successfully complete its mapping mission**.

---

# 4. Initial Performance Requirements

These values are preliminary and may be modified following research and simulation.

| Parameter                       |          Initial Requirement |
| ------------------------------- | ---------------------------: |
| Normal operating depth          |                        0–5 m |
| Design/test depth               |                         10 m |
| Initial survey area             |                  ≥ 20 × 20 m |
| Typical vehicle speed           |                  0.3–0.7 m/s |
| Minimum mission duration        |                       30 min |
| Minimum controlled ROV duration |             45 min preferred |
| Survey pattern                  | Lawn-mower / parallel tracks |
| Initial track spacing           |                        1–2 m |
| Mapping method                  |          Acoustic bathymetry |
| Initial control method          |                     Tethered |
| Final control method            |                   Autonomous |
| Surface positioning             |                     GNSS/GPS |
| Underwater positioning          |                Sensor fusion |
| Recovery state                  |  Positive buoyancy / surface |

Exact positioning and mapping accuracy requirements are currently **TBD** and will be defined after studying available sensors and mapping methods.

---

# 5. Vehicle Degrees of Freedom

The vehicle operates with six degrees of freedom.

### Translation

* **Surge:** forward/backward
* **Sway:** left/right
* **Heave:** up/down

### Rotation

* **Roll**
* **Pitch**
* **Yaw**

The propulsion system shall eventually provide sufficient control authority for:

* forward/backward movement;
* vertical movement;
* heading control;
* controlled turning;
* roll/pitch stabilization.

Direct sway control is desirable but is not mandatory for the first physical prototype.

---

# 6. Buoyancy Requirements

The vehicle shall have approximately neutral buoyancy during normal operation.

For safety, the final vehicle should preferably have **slightly positive buoyancy**.

This means:

$$
F_B > F_G
$$

where

$$
F_B = \rho Vg
$$

and

$$
F_G = mg
$$

The difference should be small enough that the vertical thrusters can easily maintain depth.

In the event of complete power loss, the preferred behaviour is:

```text
POWER FAILURE
      ↓
thrusters stop
      ↓
vehicle slowly rises
      ↓
vehicle reaches surface
```

Ballast and buoyancy material shall be adjustable during development.

---

# 7. Static Stability Requirements

The vehicle shall be mechanically designed so that:

$$
CoB_z > CoM_z
$$

where:

* CoB = Centre of Buoyancy
* CoM = Centre of Mass

The centre of buoyancy should be located above the centre of mass.

This arrangement shall produce a passive restoring moment when the vehicle experiences roll or pitch disturbances.

The vehicle should therefore naturally attempt to return toward a level orientation.

The mechanical design should provide adjustable locations for:

* battery;
* ballast;
* buoyancy foam;
* heavy electronics.

This will allow the centre of mass and centre of buoyancy to be tuned experimentally.

---

# 8. Propulsion Requirements

The first complete ROV should use approximately **six independently controlled thrusters**.

Target configuration:

* four horizontal thrusters;
* two vertical thrusters.

The horizontal thrusters should provide:

* surge;
* yaw;
* preferably sway capability depending on configuration.

The vertical thrusters should provide:

* heave;
* pitch/roll correction when possible.

The exact thruster configuration will be selected after simulation.

Each thruster shall be individually controllable through an electronic speed controller.

The propulsion system should support bidirectional thrust.

---

# 9. Pressure Housing Requirements

All electronics requiring protection from water shall be enclosed in waterproof pressure housings.

Initial design pressure:

$$
P=P_0+\rho gh
$$

At a design depth of 10 m, the housing should withstand approximately two atmospheres of absolute pressure.

The housing system shall include:

* appropriate O-ring seals;
* removable endcaps;
* waterproof electrical penetrators;
* pressure/vacuum testing capability;
* internal leak detection.

The pressure housing shall be tested without electronics before underwater operation.

---

# 10. Required Sensors

## Essential Sensors

### IMU

Used to estimate:

* roll;
* pitch;
* yaw rate;
* acceleration.

---

### Pressure Sensor

Used to calculate vehicle depth.

The pressure sensor shall provide sufficient resolution for stable depth control.

---

### Magnetometer / Compass

Used for heading estimation.

---

### Leak Sensor

Used to detect water inside the electronics enclosure.

Detection of a leak shall eventually trigger an emergency recovery procedure.

---

### Battery Monitoring

The system shall monitor:

* battery voltage;
* preferably current;
* preferably consumed energy.

---

# 11. Navigation Sensors

## GPS / GNSS

GPS shall be used when the vehicle is at or near the water surface.

GPS shall provide:

* initial mission position;
* final recovery position;
* surface tracking.

GPS shall **not** be considered available while the vehicle is submerged.

---

## Doppler Velocity Log — Future Requirement

A DVL may eventually be used to estimate:

* velocity relative to the seabed;
* altitude above seabed.

A DVL is not required for the first ROV prototype due to cost.

---

# 12. Mapping Sensors

## Initial Mapping Sensor

The first mapping prototype should use a downward-looking acoustic range sensor or single-beam sonar.

The sensor shall measure approximately:

$$
h=\text{distance between vehicle and seabed}
$$

When combined with vehicle depth:

$$
z_{bottom}=z_{vehicle}+h
$$

subject to the chosen coordinate convention.

The resulting measurements can be combined with vehicle position:

$$
(x,y,z_{bottom})
$$

to form a basic bathymetric point cloud.

---

## Future Mapping Sensors

Future versions may investigate:

* mechanical scanning sonar;
* side-scan sonar;
* multibeam echosounder.

A multibeam system is considered an advanced-stage capability rather than a requirement for the first prototype.

---

# 13. Camera Requirements

A camera is **not required for the primary mapping function**.

Poor visibility is expected in Baltic coastal waters.

The vehicle shall therefore be capable of operating when the camera provides little or no useful information.

A camera may nevertheless be installed for:

* vehicle inspection;
* identifying obstacles;
* debugging;
* observing the seabed;
* identifying objects detected by sonar;
* recording missions;
* public demonstrations;
* future visual navigation research.

Artificial lighting may be installed.

Lighting should preferably be positioned away from the optical axis of the camera to reduce backscatter from suspended particles.

---

# 14. Main Control System

The vehicle should use a dedicated autopilot/flight controller for low-level control.

The initial candidate software platform is:

**ArduPilot / ArduSub**

The autopilot shall eventually handle:

* IMU processing;
* attitude estimation;
* thruster mixing;
* depth control;
* heading control;
* low-level vehicle stabilization;
* basic failsafes.

---

# 15. Companion Computer

A separate onboard computer may eventually be used for high-level autonomous functions.

Possible platform:

* Raspberry Pi;
* equivalent ARM computer;
* other suitable single-board computer.

It may perform:

* sonar processing;
* mission planning;
* mapping;
* data logging;
* ROS 2 nodes;
* sensor fusion;
* SLAM;
* object recognition.

Communication between the companion computer and the autopilot shall preferably use **MAVLink**.

---

# 16. Software Architecture

Initial intended architecture:

```text
                    Mission planner
                         ROS 2
                           │
                           │
                        MAVLink
                           │
                           ▼
                     ┌──────────┐
                     │ ArduSub  │
                     └────┬─────┘
                          │
                    Thruster mixer
                          │
             ┌────────────┼─────────────┐
             ▼            ▼             ▼
          Thruster 1   Thruster 2     ...

Sensors:

IMU ──────────────→ ArduSub

Pressure ─────────→ ArduSub

Compass ──────────→ ArduSub

Leak sensor ──────→ Safety system


Sonar ─────────────→ Companion computer

DVL ───────────────→ Companion computer

Camera ────────────→ Companion computer

GPS ───────────────→ Navigation system
```

---

# 17. Mapping Architecture

The eventual mapping pipeline shall follow approximately:

```text
IMU ────────┐
            │
Depth ──────┤
            │
DVL ────────┼──→ State estimation ───→ Vehicle pose
            │
GPS ────────┘        when available
                                      │
                                      │
Sonar ────────────────────────────────┤
                                      ▼
                             Coordinate transform
                                      │
                                      ▼
                                 X,Y,Z points
                                      │
                                      ▼
                            Filtering / interpolation
                                      │
                                      ▼
                               Bathymetric map
```

---

# 18. Communications

During early development, the vehicle shall operate using a tether.

The tether may carry:

* Ethernet;
* serial communication;
* power depending on architecture;
* emergency recovery line.

The final autonomous system shall not depend upon continuous communication with the surface.

---

# 19. Data Logging

The vehicle shall log all mission-critical information with timestamps.

The minimum logged data should eventually include:

* time;
* depth;
* pressure;
* roll;
* pitch;
* yaw;
* vehicle state;
* thruster commands;
* battery voltage;
* battery current if available;
* sonar distance;
* estimated position;
* GPS position when available;
* mission mode;
* error/failsafe events.

The system should use synchronized timestamps so sensor data can be combined after the mission.

---

# 20. Safety Requirements

Safety and recovery shall be considered from the beginning of the project.

The eventual autonomous vehicle shall provide failsafe responses for at least:

### Leak detected

```text
LEAK
 ↓
ABORT MISSION
 ↓
SURFACE
```

### Low battery

```text
LOW BATTERY
 ↓
ABORT MISSION
 ↓
RETURN / SURFACE
```

### Navigation failure

```text
POSITION INVALID
 ↓
ABORT MISSION
 ↓
SURFACE
```

### Mission timeout

```text
TIME LIMIT EXCEEDED
 ↓
ABORT
 ↓
SURFACE
```

### Companion computer failure

Low-level autopilot safety functions should continue operating even if the companion computer fails.

### Complete power failure

Positive buoyancy should cause the vehicle to rise slowly toward the surface.

---

# 21. Mechanical Design Requirements

The first vehicle should prioritize modularity over hydrodynamic efficiency.

The design should allow easy repositioning of:

* thrusters;
* battery;
* sensors;
* ballast;
* buoyancy material;
* sonar;
* camera.

The initial vehicle should therefore use an open-frame ROV architecture rather than a streamlined torpedo-shaped body.

Siemens NX will be used as the primary CAD environment.

---

# 22. Modularity Requirement

Subsystems should be designed as separate modules wherever practical.

Possible modules:

```text
Propulsion module
Power module
Autopilot module
Companion computer module
Navigation module
Sonar module
Camera module
Communication module
Safety/recovery module
```

This should allow individual systems to be replaced or upgraded without redesigning the entire vehicle.

---

# 23. Development Strategy

Development shall follow the sequence:

### Stage 1

Software research and simulation

### Stage 2

Bench electronics

### Stage 3

Mechanical frame and waterproof housing

### Stage 4

Tethered manual ROV

### Stage 5

Depth and attitude stabilization

### Stage 6

Tethered sonar mapping

### Stage 7

Underwater localization

### Stage 8

Untethered autonomous operation

### Stage 9

Advanced bathymetric mapping

A stage shall not progress merely because a planned date has been reached.

Each stage should have defined validation tests before progression.

---

# 24. First Physical Prototype Success Criteria

The first ROV shall be considered successful when it can repeatedly:

1. Enter the water.
2. Remain waterproof.
3. Communicate reliably with the operator.
4. Submerge under controlled power.
5. Maintain approximately constant depth.
6. Move forward and backward.
7. Change heading.
8. Stop safely.
9. Return to the surface.
10. Be recovered without damage.

Autonomy and mapping are **not requirements for Prototype 1**.

---

# 25. First Mapping Prototype Success Criteria

The mapping prototype shall be considered successful when it can:

1. Measure vehicle depth.
2. Measure distance to the seabed.
3. Associate each sonar measurement with an estimated vehicle position.
4. Perform a controlled survey pattern.
5. Record synchronized sensor data.
6. Generate a basic seabed elevation map from the recorded data.

The first mapping mission may remain tethered.

---

# 26. Final Prototype Success Criteria

The long-term prototype should be capable of:

1. Receiving a survey area.
2. Determining its initial GPS position.
3. Diving autonomously.
4. Navigating underwater.
5. Following a survey trajectory.
6. Recording bathymetric measurements.
7. Detecting major faults.
8. Aborting safely when required.
9. Returning toward its deployment position.
10. Surfacing autonomously.
11. Producing a bathymetric representation of the surveyed seabed.

---

# 27. Open Research Questions

The following questions remain intentionally unresolved in Version 0.1:

* Which thrusters should be used?
* What exact thruster configuration should be selected?
* What autopilot hardware should be used?
* What companion computer should be used?
* What battery chemistry and voltage should be used?
* How much battery capacity is required?
* What pressure vessel dimensions are required?
* Which sonar should be used for Prototype 1?
* What mapping resolution is realistically achievable?
* What absolute mapping accuracy is required?
* How accurately can the ROV be localized while tethered?
* Is a DVL financially achievable?
* Which localization method should be used before purchasing a DVL?
* Which ROS 2 architecture should be used?
* Which simulator should be used alongside ArduSub SITL?
* What maximum current speed should the vehicle tolerate?
* What legal/operational restrictions apply to autonomous testing near Sønderborg?
* What university equipment can be accessed?
* What equipment may be available through SDU research groups?

These questions shall be progressively answered through research, simulation and testing.

---

# 28. Immediate Development Objective

The immediate objective is **not to build the physical vehicle**.

The first engineering milestone is:

> Create a simulated underwater vehicle using ArduSub/SITL that can receive commands, report telemetry and eventually perform a simple predefined survey trajectory.

The next work package therefore focuses on:

1. ArduSub architecture
2. SITL
3. MAVLink
4. Basic underwater vehicle dynamics
5. Simulation
