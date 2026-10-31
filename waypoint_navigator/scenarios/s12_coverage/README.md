# 12 — Area Coverage Sweep

Sweep a rectangular area in a boustrophedon (lawnmower) pattern.

**When you need it:** Field survey, search sweep, photogrammetry, spraying.

**Goal:** Visit every part of an area, rather than a few points inside it.

**Drone tasks:**

1. Take the area bounds and the line spacing from parameters.
2. Generate a back-and-forth (boustrophedon) pattern that covers it.
3. Publish the pattern on `/coverage_pattern` so it can be checked before flight.
4. Fly the pattern end to end, then return home.

_Line spacing should follow from your sensor's ground footprint, not from the defaults here._

## Demo Video
https://github.com/user-attachments/assets/42563a6b-412b-4d9f-9ba8-6721f9b057b7

## Run it

```bash
# simulation, one command
./waypoint_navigator/scenarios/s12_coverage/run.sh

# or launch it directly (this is what runs on hardware)
ros2 launch waypoint_navigator coverage.launch.py
```

World: `worlds/walled_arena.sdf`

## What runs

| Node | Location |
|---|---|
| `coverage_planner_node.py` | in this folder |
| `state_machine_node.py` | `waypoint_navigator/common/` |

This folder contains the code that is unique to this scenario. It also uses shared nodes from `waypoint_navigator/common/` - see the table above - and the vehicle interface (`common/px4_offboard_interface_node.py`), which every scenario needs.

## In this folder

- `__init__.py`
- `coverage_planner_node.py`  - the behaviour itself
- `coverage.launch.py`  - how the scenario is launched
- `run.sh`  - one-command simulation demo

## How it works

The pattern is published as markers on `/coverage_pattern` before flight, so you can inspect the sweep before it starts.

## On real hardware

Line spacing should follow from your sensor's ground footprint, not from the defaults here.

Then read [the hardware checklist](../../../docs/hardware.md) before flying.

## Configuration

This scenario reads its topics and frames from the interface profile, like
every other one. Nothing here is hard-coded:

```bash
ros2 launch waypoint_navigator coverage.launch.py \
    interface_config:=/path/to/my_vehicle.yaml
```

---

[← all scenarios](../../../README.md)
