# Autonomous Underwater Mapping Vehicle
## System Requirements — Version 0.2

**Project:** SDU Underwater Mapping AUV  
**Version:** 0.2  
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

The project is not intended initially for deep-sea operation, biological sampling, manipulation, pipeline inspection, fish identification, or photorealistic visual reconstruction.

The primary engineering objective is:

> **Determine the geometry of the seabed accurately and reproducibly using an underwater robotic platform.**

---

## 2. Primary Mission

The final prototype shall be capable of performing the following mission:

1. Start at the water surface.
2. Determine its initial position using GPS/GNSS.
3. Receive a predefined survey area.
4. Dive to the required operating depth.
5. Navigate toward the survey area.
6. Follow a predefined survey pattern.
7. Measure the seabed using acoustic sensors.
8. Record vehicle position, orientation, depth and sonar measurements.
9. Complete the survey.
10. Return toward the recovery position.
11. Surface automatically.
12. Provide the recorded data for generation of a bathymetric map.

A typical survey pattern will be a lawnmower or parallel-track pattern.

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

## 3. Primary Mapping Objective

The primary mapping objective is **bathymetric mapping**.

The system shall estimate seabed geometry in the form:

z = f(x,y)

where:

- x = horizontal position
- y = horizontal position
- z = seabed elevation or depth

The mapping system shall therefore generate a collection of seabed points:

```text
Pi = [xi, yi, zi]
```

These points may later be used to produce:

- a point cloud
- a gridded depth map
- a contour map
- a 3D seabed surface

The initial project does not require visual texture mapping or photogrammetry.

---

## 4. Mapping Accuracy Requirement

The mapping system shall provide a method for **quantitatively evaluating mapping accuracy against reference measurements**.

This requirement is considered more important than maximizing survey area during early development.

A small accurately validated map is preferred over a larger map of unknown accuracy.

Initial examples of possible validation methods include:

- surveying a known pool floor
- mapping known submerged objects
- comparing with manually measured depth points
- comparing with existing reference bathymetry where suitable

Exact acceptable mapping error is currently **TBD** and shall be established after sensor and localization research.

---

## 5. Development Vehicle Classes

The project shall use different requirements for different development stages.

### Prototype 1 — Development ROV

The first physical vehicle is intended primarily for:

- propulsion testing
- waterproofing testing
- control development
- sensor integration
- software integration

Target requirements:

| Requirement | Target |
|---|---|
| Operating depth | 0–3 m |
| Structural design depth | ≥10 m |
| Endurance | ≥30 min |
| Preferred endurance | ≥45 min |
| Control | Tethered/manual |
| Depth hold | Required |
| Heading hold | Required |
| Camera | Recommended |
| Mapping sonar | Not initially required |
| Underwater localization | Not initially required |
| Positive buoyancy | Required |
| Modular sensor mounting | Required |

### Prototype 2 — Mapping ROV

The mapping ROV shall be capable of creating basic bathymetric maps while still operating tethered.

Target requirements:

| Requirement | Target |
|---|---|
| Operating depth | ≤5 m initially |
| Structural design depth | ≥10 m |
| Survey area | ≥20 × 20 m target |
| Survey speed | 0.3–0.7 m/s |
| Endurance | ≥45 min preferred |
| Mapping sensor | Downward acoustic ranging |
| Survey pattern | Parallel/lawnmower |
| Track spacing | Adjustable |
| Depth hold | Required |
| Heading hold | Required |
| Data logging | Required |
| Localization | External, relative, or experimental |

### Final AUV

The operating depth of the final AUV shall remain:

> **TBD following use-case, sensor, pressure-system and environmental research.**

The final vehicle shall not be permanently constrained to the initial 5 m or 10 m figures simply because those values are convenient for early prototypes.

The final depth requirement shall be established later based on:

- intended Baltic Sea use cases
- pressure housing design
- sonar capability
- localization capability
- recovery risk
- cost
- available university equipment

---

## 6. Initial Operating Environment

The vehicle is intended primarily for shallow-water coastal operation.

Initial target environments include:

- Baltic Sea coastal waters near Sønderborg
- lakes
- harbours
- swimming pools
- controlled test basins

The system shall be designed with the expectation of:

- low underwater visibility
- suspended particles
- moderate water currents
- salt or brackish water
- vegetation
- uneven seabed
- low underwater lighting
- possible sediment disturbance close to the seabed

The vehicle shall therefore **not depend on visual camera data to successfully complete its primary mapping mission**.

---

## 7. Vehicle Degrees of Freedom

The vehicle operates with six degrees of freedom.

### Translation

- **Surge:** forward/backward
- **Sway:** left/right
- **Heave:** up/down

### Rotation

- **Roll**
- **Pitch**
- **Yaw**

The propulsion system shall eventually provide sufficient control authority for:

- forward/backward movement
- vertical movement
- heading control
- controlled turning
- roll/pitch stabilization

Direct sway control is desirable but is not mandatory for the first physical prototype.

---

## 8. Buoyancy Requirements

The vehicle shall have approximately neutral buoyancy during normal operation.

For safety, the vehicle should preferably have **slightly positive buoyancy**.

This means:

```text
FB > FG
```

where:

```text
FB = ρVg
FG = mg
```

The buoyancy difference should be small enough that the vertical thrusters can maintain depth without excessive continuous thrust.

In the event of complete power loss, the preferred vehicle behaviour shall be:

```text
POWER FAILURE
      ↓
Thrusters stop
      ↓
Vehicle slowly rises
      ↓
Vehicle reaches surface
```

Ballast and buoyancy material shall be adjustable during development.

---

## 9. Static Stability Requirements

The vehicle shall be mechanically designed so that:

```text
CoBz > CoMz
```

where:

- CoB = Centre of Buoyancy
- CoM = Centre of Mass

The centre of buoyancy should be located above the centre of mass.

This arrangement shall create a passive restoring moment when the vehicle experiences roll or pitch disturbances.

The vehicle should therefore naturally tend toward a level orientation.

The mechanical design should allow adjustment of:

- battery position
- ballast
- buoyancy foam
- heavy electronics
- sensor position where practical

This will allow the centre of mass and centre of buoyancy to be tuned experimentally.

---

## 10. Propulsion Requirements

The first complete ROV should use approximately **six independently controlled thrusters**, subject to later simulation and design validation.

An initial candidate configuration consists of:

- four horizontal thrusters
- two vertical thrusters

The horizontal thrusters should provide:

- surge
- yaw
- preferably sway depending on orientation

The vertical thrusters should provide:

- heave
- pitch and/or roll correction where possible

The exact thruster configuration shall not be finalized until simulation has been performed.

Each thruster shall be individually controllable.

The propulsion system should support bidirectional thrust.

---

## 11. Pressure Housing Requirements

All electronics requiring protection from water shall be enclosed in suitable waterproof pressure housings.

For Prototype 1, the structural design depth shall be at least:

```text
10 m
```

The housing pressure may be estimated using:

```text
P = P0 + ρgh
```

At approximately 10 m depth, the housing should withstand roughly two atmospheres of absolute pressure.

The housing system shall include:

- suitable O-ring seals
- removable endcaps
- waterproof electrical penetrators
- pressure or vacuum testing capability
- internal leak detection

The pressure housing shall be tested without critical electronics before underwater operation.

---

## 12. Required Sensors

### IMU

Used to estimate:

- roll
- pitch
- angular velocity
- linear acceleration
- attitude-related information

### Pressure Sensor

Used to calculate vehicle depth.

The pressure sensor shall provide sufficient resolution and update rate for stable depth control.

### Magnetometer / Compass

Used for heading estimation.

Possible magnetic interference from:

- thrusters
- power wiring
- batteries
- metal structures

shall be considered in sensor placement and calibration.

### Leak Sensor

Used to detect water inside protected electronics enclosures.

Leak detection shall eventually trigger an emergency recovery procedure.

### Battery Monitoring

The system shall monitor at minimum:

- battery voltage

Preferably it shall also monitor:

- current
- consumed energy
- estimated remaining energy

---

## 13. Navigation Sensors

### GPS / GNSS

GPS/GNSS shall be used when the vehicle is at or near the surface.

It may provide:

- initial mission position
- final recovery position
- surface tracking
- correction of accumulated localization drift

GPS/GNSS shall not be considered available during normal submerged operation.

### DVL — Future Candidate

A Doppler Velocity Log may eventually be used to estimate:

- velocity relative to the seabed
- altitude above seabed

A DVL is not required for the first physical prototype due to likely cost.

The project shall first investigate whether a DVL is necessary and whether one can be obtained through:

- SDU research equipment
- sponsorship
- project funding
- borrowing
- alternative low-cost localization methods

---

## 14. Mapping Sensors

### Initial Mapping Sensor

The first mapping prototype should use a downward-looking acoustic range sensor or single-beam sonar.

The sensor shall estimate:

```text
h = distance between vehicle and seabed
```

If vehicle depth is:

```text
z_vehicle
```

and measured seabed altitude is:

```text
h
```

then seabed depth can approximately be obtained from:

```text
z_bottom = z_vehicle + h
```

subject to the coordinate convention used.

When combined with vehicle horizontal position:

```text
x, y
```

the system can generate:

```text
(x, y, z_bottom)
```

measurements for bathymetric mapping.

### Future Mapping Sensors

Future versions may investigate:

- mechanically scanning sonar
- side-scan sonar
- multibeam echosounder

Advanced mapping sonar shall be considered a later-stage capability rather than a requirement for Prototype 1.

---

## 15. Camera Requirements

A camera is **not required for the primary bathymetric mapping function**.

Poor visibility is expected in Baltic coastal waters.

The vehicle shall therefore be capable of completing its mission when the camera provides little or no useful visual data.

A camera may nevertheless be installed for:

- vehicle inspection
- debugging
- identifying obstacles
- observing the seabed
- identifying objects detected acoustically
- mission recording
- public demonstrations
- future visual navigation research

Artificial lighting may be installed.

Lighting should preferably be positioned away from the camera optical axis in order to reduce backscatter from suspended particles.

---

## 16. Main Control System

The vehicle should use a dedicated autopilot or flight controller for low-level control.

The initial candidate software platform is:

**ArduPilot / ArduSub**

The autopilot shall eventually handle:

- IMU processing
- attitude estimation
- thruster mixing
- depth control
- heading control
- low-level stabilization
- basic failsafes

The project shall avoid placing mission-critical low-level stabilization exclusively on the companion computer.

---

## 17. Companion Computer

A separate onboard computer may eventually be used for high-level autonomous functions.

Possible platforms include:

- Raspberry Pi
- equivalent ARM-based computer
- other suitable single-board computer

The companion computer may perform:

- sonar processing
- mission planning
- mapping
- data logging
- ROS 2 nodes
- sensor fusion
- SLAM
- object recognition
- high-level autonomy

Communication between the companion computer and autopilot should preferably use **MAVLink**.

---

## 18. Software Architecture

Initial intended architecture:

```text
                    Mission planner
                         ROS 2
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

## 19. Mapping Architecture

The eventual mapping pipeline shall approximately follow:

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

The fundamental mapping problem can therefore be divided into three major tasks:

1. Determine where the vehicle is.
2. Determine where the seabed is relative to the vehicle.
3. Transform seabed measurements into a common world coordinate system.

---

## 20. Coordinate Transformation Requirement

The mapping system shall eventually transform sonar measurements from the sensor coordinate frame into a fixed world or map coordinate frame.

Conceptually:

```text
P_world = T_world_vehicle × T_vehicle_sensor × P_sensor
```

This transformation requires knowledge of:

- vehicle position
- vehicle orientation
- sensor position relative to vehicle
- sensor orientation relative to vehicle

Accurate sensor mounting geometry shall therefore be considered part of the mapping system.

---

## 21. Communications

During early development, the vehicle shall operate using a tether.

The tether may carry:

- Ethernet
- serial communication
- power depending on architecture
- emergency recovery capability

The final autonomous system shall not depend upon continuous communication with the surface.

---

## 22. Data Logging

The vehicle shall log all mission-critical information with timestamps.

Minimum logged information should eventually include:

- time
- depth
- pressure
- roll
- pitch
- yaw
- vehicle state
- thruster commands
- battery voltage
- battery current if available
- sonar distance
- estimated position
- GPS position when available
- mission mode
- error and failsafe events

The system shall use synchronized timestamps so that sensor measurements can be accurately combined after the mission.

---

## 23. Safety Requirements

Safety and recovery shall be considered from the beginning of the project.

The eventual autonomous vehicle shall provide failsafe responses for at least the following conditions.

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

## 24. Mechanical Design Requirements

The first physical vehicle should prioritize:

- modularity
- accessibility
- maintainability
- testability

over hydrodynamic efficiency.

The first vehicle should therefore use an open-frame ROV architecture rather than a highly streamlined torpedo-shaped body.

The mechanical design shall allow easy repositioning or replacement of:

- thrusters
- battery
- sensors
- ballast
- buoyancy material
- sonar
- camera
- electronics enclosures

**Siemens NX** shall be used as the primary CAD environment.

---

## 25. Modularity Requirement

Major sensing, computing and propulsion components should be replaceable without redesigning the complete vehicle.

This includes, where practical:

- mapping sonar
- navigation sensors
- companion computer
- autopilot
- camera
- thrusters
- communication hardware

The vehicle should provide standardized mounting locations or adaptable interfaces where practical.

Conceptually:

```text
                 VEHICLE
                    │
             Sensor interface
                    │
          ┌─────────┴─────────┐
          │                   │
 Initial low-cost sonar   Future sonar
                          or multibeam
```

This modularity is particularly important because future sensors may be obtained through:

- SDU research groups
- sponsorship
- competitions
- external funding

---

## 26. Major System Modules

Where practical, the vehicle shall be divided into separate functional modules.

Possible modules include:

```text
Propulsion module
Power module
Autopilot module
Companion computer module
Navigation module
Mapping sonar module
Camera module
Communication module
Safety/recovery module
Pressure housing module
```

Subsystems should be testable independently where practical.

---

## 27. Development Strategy

Development shall follow the approximate sequence:

### Stage 1
Requirements, research and software simulation

### Stage 2
Bench electronics and component testing

### Stage 3
Mechanical frame and waterproof housing

### Stage 4
Tethered manual ROV

### Stage 5
Depth, heading and attitude stabilization

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

## 28. Prototype 1 Success Criteria

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

## 29. First Mapping Prototype Success Criteria

The mapping prototype shall be considered successful when it can:

1. Measure vehicle depth.
2. Measure distance to the seabed.
3. Associate each sonar measurement with an estimated vehicle position.
4. Perform a controlled survey pattern.
5. Record synchronized sensor data.
6. Generate a basic seabed elevation map.
7. Compare the generated map against a reference.
8. Calculate or estimate mapping error.

The first mapping mission may remain tethered.

---

## 30. Final Prototype Success Criteria

The long-term prototype should be capable of:

1. Receiving a survey area.
2. Determining its initial GPS position.
3. Diving autonomously.
4. Navigating underwater.
5. Following a survey trajectory.
6. Recording acoustic bathymetric measurements.
7. Estimating its underwater position.
8. Detecting major faults.
9. Aborting safely when required.
10. Returning toward its deployment position.
11. Surfacing autonomously.
12. Producing a bathymetric representation of the surveyed seabed.
13. Providing an estimate of mapping accuracy.

---

## 31. Open Research Questions

The following questions remain intentionally unresolved in Version 0.2:

- What final operating depth is useful for Baltic Sea missions?
- Which thrusters should be used?
- What exact thruster configuration should be selected?
- Is direct sway control necessary?
- What autopilot hardware should be used?
- What companion computer should be used?
- What battery chemistry and voltage should be used?
- How much battery capacity is required?
- What pressure vessel dimensions are required?
- Which materials should be used for the frame and housings?
- Which sonar should be used for Prototype 2?
- What mapping resolution is realistically achievable?
- What vertical mapping accuracy is realistically achievable?
- What horizontal positioning accuracy is required?
- How accurately can the ROV be localized while tethered?
- Is a DVL financially achievable?
- Can a DVL be borrowed from SDU?
- Which localization method should be used before obtaining a DVL?
- Is acoustic positioning required?
- Which ROS 2 architecture should be used?
- Which simulator should be used alongside ArduSub SITL?
- Can Stonefish be used effectively through WSL2?
- What maximum current speed should the vehicle tolerate?
- What seabed altitude should be maintained during surveys?
- What survey line spacing should be used?
- What legal or operational restrictions apply to autonomous testing near Sønderborg?
- What university equipment can be accessed?
- What equipment may be available through SDU research groups?
- How should the system determine that localization has become unreliable?
- What recovery system should be used for untethered operation?

These questions shall be progressively answered through research, simulation and experimental testing.

---

## 32. Immediate Development Objective

The immediate objective is **not to build the physical vehicle**.

The first engineering milestone is:

> **Create a simulated underwater vehicle using ArduSub/SITL that can receive commands, report telemetry and eventually perform a simple predefined survey trajectory.**

Before beginning advanced simulation, the next research task is to understand the basic physical vehicle architecture.

The next work package shall therefore investigate:

1. Six-degree-of-freedom underwater vehicle motion
2. Required actively controlled degrees of freedom
3. Candidate thruster arrangements
4. Buoyancy
5. Centre of mass
6. Centre of buoyancy
7. Passive stability
8. Basic underwater drag
9. How these properties affect ArduSub control and thruster mixing
