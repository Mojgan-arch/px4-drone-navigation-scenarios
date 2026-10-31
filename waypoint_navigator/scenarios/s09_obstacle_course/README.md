# 09 — Obstacle Course Traversal

Cross the pillar slalom from one end to the other.

**When you need it:** Warehouses, forests, construction sites, urban canyons.

**Goal:** Cross a cluttered space from one end to the other without a prior map.

**Drone tasks:**

1. Take the next goal from the course mission.
2. Head toward it while the avoidance behaviour steers around the pillars.
3. Advance to the following goal once the current one is reached.
4. Repeat until it reaches the far end of the course.

## Demo Video

https://github.com/user-attachments/assets/405be361-a0e8-441d-ade4-fc0801728f04


## Run it

```bash
# simulation, one command
./waypoint_navigator/scenarios/s09_obstacle_course/run.sh

# or launch it directly (this is what runs on hardware)
ros2 launch waypoint_navigator obstacle_course.launch.py
```

World: `worlds/obstacle_course.sdf`

## What runs

| Node | Location |
|---|---|
| `obstacle_course_mission_node.py` | in this folder |
| `obstacle_avoidance_node.py` | `waypoint_navigator/common/` |

This folder contains the code that is unique to this scenario. It also uses shared nodes from `waypoint_navigator/common/` - see the table above - and the vehicle interface (`common/px4_offboard_interface_node.py`), which every scenario needs.

## In this folder

- `__init__.py`
- `obstacle_course_mission_node.py`  - the behaviour itself
- `obstacle_course.launch.py`  - how the scenario is launched
- `run.sh`  - one-command simulation demo

## How it works

Combines the reactive avoidance behaviour with a mission that feeds it successive goals across the course.

## On real hardware

A good demonstration. Not a good first hardware flight.

Then read [the hardware checklist](../../../docs/hardware.md) before flying.

## Configuration

This scenario reads its topics and frames from the interface profile, like
every other one. Nothing here is hard-coded:

```bash
ros2 launch waypoint_navigator obstacle_course.launch.py \
    interface_config:=/path/to/my_vehicle.yaml
```

---

[← all scenarios](../../../README.md)
