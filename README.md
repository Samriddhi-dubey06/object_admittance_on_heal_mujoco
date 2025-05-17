# 🤖 Object Admittance Control for Dual-Arm Robot in MuJoCo

This project implements **object admittance control** for a dual-arm robotic system in a MuJoCo simulation. The robot collaboratively lifts an object (like a box) using sensor feedback, dynamic control, and intelligent coordination between both arms.

---

## 📽️ Demonstration

[![Watch on YouTube](https://img.shields.io/badge/▶️%20Watch%20Demo%20Video-blue)]([https://youtu.be/1Zh8jDSsFWA](https://youtu.be/-an-89Gh3lk?feature=shared))

---

## 🚀 Key Features

- **Cartesian Admittance Control:** Allows compliant interaction with the environment by responding to external forces.
- **Force-Based Lifting:** The robot adjusts its lifting motion based on sensed wrenches from both arms.
- **Dual-Arm Coordination:** Combines control of two robot arms to stably grasp and move the object.
- **Fallback Logic:** Intelligent recovery when contact is lost or force thresholds are not met.
- **Real-Time MuJoCo Simulation:** Accurate dynamics-based control loop running at high frequency.

---

## 🧠 Core Concepts

### ✳️ Admittance Control Equation

The object motion is governed by:

\[
\dot{x}_o^* = \dot{x}_o + D^{-1}(W - W^* - K(x_o^* - x_o))
\]

Where:
- \( \dot{x}_o^* \): Desired object velocity
- \( \dot{x}_o \): Current object velocity
- \( W \): Actual sensed wrench (force/torque)
- \( W^* \): Desired wrench
- \( x_o^* \): Desired object position
- \( x_o \): Current object position
- \( D \): Damping matrix
- \( K \): Stiffness matrix

This equation ensures **compliant yet controlled motion** in response to external disturbances or contacts.

---

## 🔧 Code Breakdown

### 1. **Imports & Initialization**
- Loads MuJoCo XML model
- Initializes custom velocity controller for each robot arm
- Sets gains for stiffness and damping

### 2. **Contact Wrench Detection**
- Function: `get_contact_wrenches`
- Detects contact between robot and box
- Extracts forces & torques (wrenches) from both arms

### 3. **Admittance Control**
- Function: `compute_object_admittance_control`
- Applies admittance control law to compute desired motion
- Adjusts movement dynamically based on external force

### 4. **Velocity Mapping**
- Converts Cartesian object velocity → joint velocity
- Uses Jacobians of both arms
- Applies velocity limits for safety

### 5. **Control State Machine**
#### States:
- `reaching_first_target`: Move to pre-grasp pose
- `reaching_second_target`: Move to grasp pose
- `reading_sensors`: Read force/torque
- `lifting_object`: Activate admittance control
- `maintaining_position`: Hold object in air

---

## 🔁 Simulation Loop

- Step physics in MuJoCo
- Visualize state using viewer (if enabled)
- Transition through phases based on robot progress
- Reacts in real-time to changes (e.g., contact loss)
- Uses fallback strategies when issues occur

---

## 🧪 Robustness Strategies

- Retry grasping if contact fails
- Update grasp positions slightly for better alignment
- Fall back to simple joint-space control if impedance fails
- Continuously print debug info (optional)

---

## 🛠️ How to Use

1. Clone the repository:
   ```bash
   git clone https://github.com/Samriddhi-dubey06/object_admittance_on_heal_mujoco.git
   cd object_admittance_on_heal_mujoco
