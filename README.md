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

## Triangles

A triangle is a small structured program for a situation: it names an activity, lists the states that can arise, pairs each state with a response, and ends when the goal is reached.

Triangles live in the `triangles/` folder as semicolon-delimited CSV files with eight columns:

```
description ; row_type ; subtype ; thing1 ; thing2 ; quality ; low_val ; high_val
```

Row types:

| Type | Meaning |
|------|---------|
| `c;activity` | Triangle header or goal line |
| `a;stat` | A situation the robot may find itself in |
| `c;mode` | The response action for that situation |

Quality vocabulary (drawn from grounding rules):

| Quality | Meaning |
|---------|---------|
| `stat empty` | nothing present, no model yet |
| `stat vapor` | present but unclear or ambiguous |
| `stat soft` | low resistance, low risk |
| `stat rough` | high resistance, increased pressure needed |
| `stat broken` | path blocked, structure failed, trust damaged |
| `stat hot` | overload, conflict, or excess activity |
| `stat cold` | underload, withdrawal, or dead silence |
| `stat heavy` | imbalance, fatigue, or shifted weight |
| `pattern` | structure detected, sequence possible |
| `problem` | explicit failure signal |

Each triangle follows this shape:

```
;;;;;;;;
[goal description];c;activity;[actor];[target];;[start];[end];
;;;;;;;;
[situation];a;stat;[thing1];[thing2];[quality];[low];[high];
;c;mode;[thing1];[thing2];[action];[low];[high];
;;;;;;;;
... more situation + response pairs ...
;;;;;;;;
[goal achieved];c;activity;[actor];[target];goal [type]+[type];[high];[high];
;;;;;;;;
```

Example — `triangles/triangle_first_contact.csv`:

```
;;;;;;;;
first contact — sense perceive choose act log;c;activity;robot;world;;20;40;
;;;;;;;;
scene unread, no prior model;a;stat;robot001;world001;stat empty;10;20;
;c;mode;robot001;world001;take_snapshot;15;25;
;;;;;;;;
objects detected, affordances unclear;a;stat;robot001;scene001;stat vapor;30;40;
;c;mode;robot001;scene001;label_candidates;35;45;
;;;;;;;;
path blocked, risk unknown;a;stat;robot001;path001;stat broken;20;30;
;c;mode;robot001;path001;stop_and_assess;25;35;
;;;;;;;;
safe target within reach;a;stat;robot001;object001;stat soft;50;60;
;c;mode;robot001;object001;reach_toward;55;65;
;;;;;;;;
first action complete, world model seeded;c;activity;robot;world;goal loc+bond;80;90;
;;;;;;;;
```

## Philosophical Test

The real question is:

**Can the robot go from pixels to "I am in a situation"?**

That is where grounding rules, logs, causal diagrams, memory, transforms, triangles, components, and problem solving meet.

The goal is not to begin with a giant ontology. The goal is to create a small loop that lets the robot touch the world carefully, compare before and after, and remember what happened.

## Project Sentence

Genesis Boot for a Robot is a first-contact software stack for a tabula rasa robot: it downloads the repo, looks at the world, builds a tiny grounded model, chooses one safe action, acts or asks, and logs the beginning of intelligence touching the world.
