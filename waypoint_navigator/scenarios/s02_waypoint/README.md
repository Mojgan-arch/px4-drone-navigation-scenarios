# 02 — Waypoint Following

Fly a predefined list of waypoints, then return home.

**When you need it:** Survey lines, patrol circuits, repeatable test flights.

**Goal:** Fly a route that is fully known before takeoff, with no operator in the loop.

**Drone tasks:**

1. Take off and climb to cruise altitude.
2. Fly to each waypoint in the list, in order.
3. Count a waypoint as reached once inside the tolerance radius, then take the next.
4. Return to the launch point and land after the last one.

## Demo Video
https://github.com/user-attachments/assets/2be51080-975a-427e-af43-50178455549f


## Run it

```bash
# simulation, one command
./waypoint_navigator/scenarios/s02_waypoint/run.sh

# or launch it directly (this is what runs on hardware)
ros2 launch waypoint_navigator waypoint.launch.py
```

World: `worlds/walled_arena.sdf`

## What runs

| Node | Location |
|---|---|
| `waypoint_navigator_node.py` | in this folder |

This folder contains all the code unique to this scenario. The only other thing it needs is the vehicle interface in `waypoint_navigator/common/`, which every scenario uses.

## In this folder

- `__init__.py`
- `waypoint_navigator_node.py`  - the behaviour itself
- `waypoint.launch.py`  - how the scenario is launched
- `run.sh`  - one-command simulation demo

## How it works

The waypoint list is defined in the node. A waypoint counts as reached when the drone is within a tolerance radius, then the next one is taken.

## On real hardware

Adjust tolerance and cruise speed for your airframe. The defaults assume a small quadrotor in a 10 m arena.

Then read [the hardware checklist](../../../docs/hardware.md) before flying.

## Configuration

This scenario reads its topics and frames from the interface profile, like
every other one. Nothing here is hard-coded:

```bash
ros2 launch waypoint_navigator waypoint.launch.py \
    interface_config:=/path/to/my_vehicle.yaml
```

## Flight Verification Checklist

This checklist helps users evaluate Scenario 02, which demonstrates autonomous navigation along a preplanned route in PX4 SITL and Gazebo.

### Before running

- [ ] Confirm that the PX4 SITL environment is available.
- [ ] Confirm that the ROS 2 environment is sourced.
- [ ] Review the configured route and waypoint sequence.
- [ ] Confirm that the intended simulation world is selected.

### During simulation

- [ ] Observe the vehicle takeoff and initial flight behavior.
- [ ] Check whether the drone follows the configured waypoint sequence.
- [ ] Observe the vehicle trajectory in the simulation.
- [ ] Monitor the ROS 2 terminal for warnings or errors.
- [ ] Verify how the mission terminates.

### After simulation

Record the following observations:

| Item | Observation |
| --- | --- |
| Route completion | To be tested |
| Waypoint sequence | To be tested |
| Position tracking | To be tested |
| Mission termination | To be tested |
| ROS 2 errors | To be tested |

### Demo Video

A recorded simulation demonstration can be added after verification.
  
---

[← all scenarios](../../../README.md)
