# Autonomous Robotic Breast Ultrasound Screening

A research project to develop a robotic system that autonomously scans a patient's
chest region with an ultrasound probe, guided by 3D vision, for breast cancer screening.

> **Status:** Early development. Perception foundation working (single L515 camera
> streaming to Ubuntu via Python). See the roadmap below.

<!-- TODO: add your name, role, and (optionally) a project start date -->
**Author:** _TODO — your name / role_
**Institution:** University of Memphis

---

## Motivation

Conventional breast cancer screening depends on access to hospitals, trained
technicians, and expensive imaging equipment. This project targets two underserved
groups:

- **Women with denser breast tissue**, for whom some conventional screening is less
  effective.
- **Women in rural or low-resource areas** who cannot easily reach or afford a hospital.

The aim is an autonomous, lower-cost system that can perform a consistent ultrasound
scan with minimal operator expertise.

---

## How it works (system overview)

1. **Two 3D cameras** image the chest region from different viewpoints — one positioned
   **above** the patient's torso, one **alongside** it, in parallel.
2. The two depth scans are **fused into a single 3D model** of the surface to be scanned.
3. Using that model as a map, a **robotic arm** holding an **ultrasound probe** (on a
   custom mount) plans a path and scans the entire chest region, keeping the probe
   oriented to the skin and in gentle, controlled contact.
4. Ultrasound frames are captured and tied to the probe's position for later review.

The core engineering challenge throughout is **coordinate frames**: relating what each
camera sees, where the robot is, and where the probe tip is, in one consistent
reference system.

---

## Hardware

| Component | Part |
|---|---|
| Robot arm | Yaskawa Motoman **GP8** (industrial 6-axis) |
| Depth cameras | 2× Intel RealSense **L515** LiDAR cameras |
| Ultrasound | _TODO — confirm system (e.g. Verasonics Vantage) with Ultrasound Lab_ |
| Probe mount | Custom (to be designed; must accommodate a force/torque sensor) |

> **Safety note:** The GP8 is an industrial (not collaborative) arm with no built-in
> contact sensing. Safe patient contact — force limiting, compliant control, e-stop,
> and phantom-only testing before any human — is a core design requirement, not an
> afterthought.

---

## Software stack

- **OS:** Ubuntu 24.04 LTS (Noble Numbat)
- **Robot control:** ROS 2 **Jazzy** + Python (`rclpy`); Yaskawa **MotoROS2** driver;
  MoveIt 2 for motion planning
- **Camera:** librealsense **v2.54.2** (built from source — see setup) + `pyrealsense2`
- **Point clouds / fusion:** Open3D
- **Ultrasound acquisition:** MATLAB (isolated to the ultrasound host only; data bridged
  into the Python/ROS2 system)

---

## Setup

Getting the L515 cameras working on Ubuntu is version-sensitive (the L515 is
discontinued and needs a specific librealsense version). Full step-by-step instructions,
including troubleshooting, are in:

- [`L515-ubuntu-setup-runbook.md`](./L515-ubuntu-setup-runbook.md)

<!-- TODO: add a ROS2 / robot setup guide here as that work progresses -->

---

## Roadmap

- [x] Ubuntu 24.04 workstation set up
- [x] Single L515 camera streaming (Viewer + Python)
- [ ] Read camera data in custom Python code
- [ ] Drive the GP8 in simulation (RViz + MoveIt)
- [ ] Move the real GP8 safely on command
- [ ] Fuse both cameras into one torso model
- [ ] Hand-eye calibration (link camera space to robot space)
- [ ] Probe mount + force-limited contact
- [ ] Capture ultrasound tied to probe pose
- [ ] Full autonomous scan (phantom validation)

---

## Team

- **Rohith Rajeev** — project lead / developer
- **Dr. Kevin Berriso** — Automatic Identification Lab, University of Memphis
  (robotics, sensing, integration)
- **Dr. Carl Herickhoff** — Ultrasound Lab, University of Memphis
  (ultrasound imaging, clinical)

---

## Repository structure

<!-- TODO: update this as you add folders. Example: -->
```
.
├── README.md                        # this file
├── L515-ubuntu-setup-runbook.md     # camera setup guide
├── perception/                      # camera / point-cloud code (to come)
└── robot/   V                        # ROS2 packages (to come)
```