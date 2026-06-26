# Genesis Boot for a Robot

## Core Idea

The ultimate test of the software is a GitHub repository that a tabula rasa robot can download.

Then the robot takes a picture of its environment and starts acting.

Not wildly, not magically, but with a small grounded loop:

```text
sense -> describe -> compare -> choose -> act -> observe difference -> log
```

The first milestone is not a complete robot brain. It is a first-contact protocol: a way for a minimal robot to wake up, perceive the world, form a small useful model, choose one safe action, and explain what happened.

## Cardboard Body, Augmented Mind

The physical prototype can begin as a cardboard box.

The box represents a robot cart. It gives the system a body, orientation, and a coordinate frame:

- front
- back
- left
- right
- top
- bottom

With AR glasses, the missing robotics hardware can be imagined and placed onto the box:

- motors
- grippers
- arms
- legs
- head
- cameras
- touch zones
- lidar or depth cones
- microphones
- force sensors

The cardboard body is the anchor. The AR layer is the possible robot. The log is the becoming robot.

## Process Layer

The robot should not only perceive components. It should also expose its internal processes:

- continual learning
- long-term reasoning
- memory
- problem solving
- uncertainty tracking
- safety checking
- affordance discovery

These processes can also be shown in AR as overlays:

| Process | AR / Software Representation |
|---|---|
| Perception | camera rays, object labels, unknown zones |
| Memory | remembered objects, places, failed actions |
| Reasoning | candidate goals, causal guesses, plans |
| Problem solving | obstacle, desired state, possible transform |
| Continual learning | before/after comparisons, updated rules |
| Safety | risk gates, blocked actions, confidence values |

## The Ultimate Test

The repo should be judged by one question:

**Can an unconfigured robot download it, look once at the world, form useful hypotheses, and perform one safe grounded action?**

That means the robot can:

1. Take a picture or sensor snapshot.
2. Identify candidate objects, spaces, obstacles, and affordances.
3. Convert perception into a tiny world model.
4. Select one low-risk goal.
5. Act through motors, actuators, or simulation.
6. Log what it saw, believed, chose, did, and learned.
7. Update memory from the difference between expectation and outcome.

## First Safe Actions

The first action should be humble.

Examples:

- turn the head toward the strongest light
- move forward 10 cm if the path seems clear
- stop when an obstacle is uncertain
- touch a nearby surface gently
- ask whether an object is safe to grasp
- point the camera at an uncertain object
- create a map cell such as `unknown obstacle at front-left`

## Minimal Repository Shape

```text
genesis_boot_for_a_robot/
  README.md
  boot.py

  perception/
    camera.py
    object_scan.py
    affordance_guess.py

  world_model/
    scene_graph.py
    memory.py
    uncertainty.py

  reasoning/
    goals.py
    rules.py
    problem_solver.py

  action/
    motor_interface.py
    gripper_interface.py
    safety_gate.py
    simulator.py

  logs/
    first_contact.csv

  examples/
    cardboard_cart/
    desktop_robot/
    simulated_room/
```

## Boot Script Intention

The crucial program is `boot.py`.

It should do roughly this:

```text
wake up
look around
build first scene
find safe action
act or ask
log everything
```

## Minimal World Model

The first world model can be very small:

| Field | Meaning |
|---|---|
| object | What seems to be present |
| position | Where it seems to be |
| affordance | What might be possible |
| risk | What could go wrong |
| confidence | How certain the robot is |
| action | What the robot may try |
| result | What changed after acting |

Example:

```csv
time,object,position,affordance,risk,confidence,action,result
001,light,front-right,turn_toward,low,0.82,rotate_head,light_centered
002,box,front,move_around,medium,0.61,stop_and_inspect,unknown_obstacle_logged
```

## Philosophical Test

The real question is:

**Can the robot go from pixels to "I am in a situation"?**

That is where grounding rules, logs, causal diagrams, memory, transforms, triangles, components, and problem solving meet.

The goal is not to begin with a giant ontology. The goal is to create a small loop that lets the robot touch the world carefully, compare before and after, and remember what happened.

## Project Sentence

Genesis Boot for a Robot is a first-contact software stack for a tabula rasa robot: it downloads the repo, looks at the world, builds a tiny grounded model, chooses one safe action, acts or asks, and logs the beginning of intelligence touching the world.
