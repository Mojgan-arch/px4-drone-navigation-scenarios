# 03 — Fly to a Clicked Goal

Fly to a goal published on /goal_pose - in RViz, the 2D Goal Pose tool.

**When you need it:** An operator picks a destination mid-flight, with no route planned in advance.

**Goal:** Let an operator redirect the drone mid-flight by clicking a destination, with no route prepared in advance.

**Drone tasks:**

1. Listen for a `PoseStamped` on `/goal_pose` — RViz's **2D Goal Pose** tool.
2. Substitute its own cruise altitude, since RViz publishes z = 0.
3. Fly toward the goal, correcting heading as it goes.
4. Hold position once inside the tolerance radius, ready for the next goal.

## Demo Video
https://github.com/user-attachments/assets/5c77f9d7-7a2c-4be5-9f7c-40549c306970

## Run it

```bash
# simulation, one command
./waypoint_navigator/scenarios/s03_goal/run.sh

# or launch it directly (this is what runs on hardware)
ros2 launch waypoint_navigator goal.launch.py
```

World: `worlds/walled_arena.sdf`

## What runs

| Node | Location |
|---|---|
| `goal_navigator_node.py` | in this folder |

This folder contains all the code unique to this scenario. The only other thing it needs is the vehicle interface in `waypoint_navigator/common/`, which every scenario uses.

## In this folder

- `__init__.py`
- `goal_navigator_node.py`  - the behaviour itself
- `goal.launch.py`  - how the scenario is launched
- `run.sh`  - one-command simulation demo

## How it works

RViz publishes a `PoseStamped` with z=0, so the node substitutes its own cruise altitude.

## On real hardware

Works unchanged. The goal can come from anything that publishes `PoseStamped` - a GCS, a script, another planner.

Then read [the hardware checklist](../../../docs/hardware.md) before flying.

## Configuration

This scenario reads its topics and frames from the interface profile, like
every other one. Nothing here is hard-coded:

```bash
ros2 launch waypoint_navigator goal.launch.py \
    interface_config:=/path/to/my_vehicle.yaml
```

## Goal Navigation Verification Checklist

This checklist helps users verify operator-selected goal navigation using the RViz 2D Goal Pose tool and the `/goal_pose` topic.

### Before running

- [ ] Confirm PX4 SITL and Gazebo are running.
- [ ] Confirm that the ROS 2 environment is sourced.
- [ ] Confirm RViz is available and configured.
- [ ] Review the configured cruise altitude and goal tolerance.

### During simulation

- [ ] Select a destination using RViz's 2D Goal Pose tool.
- [ ] Confirm that the goal is published on `/goal_pose` as `PoseStamped`.
- [ ] Observe whether the drone navigates toward the selected destination.
- [ ] Check that the drone uses its configured cruise altitude instead of RViz's z=0.
- [ ] Observe heading corrections during navigation.
- [ ] Verify that the drone holds position after reaching the goal tolerance radius.
- [ ] Select another goal and verify that the drone responds.

### Test Results

| Verification Item | Observation |
| --- | --- |
| Goal message received | To be tested |
| Goal navigation | To be tested |
| Cruise altitude handling | To be tested |
| Heading correction | To be tested |
| Position hold at goal | To be tested |
| Subsequent goal response | To be tested |

### Demo Video

The simulation demonstration is available in the Demo Video section above.
  
---

[← all scenarios](../../../README.md)
