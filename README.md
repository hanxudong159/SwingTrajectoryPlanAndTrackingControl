# SwingTrajectoryPlanAndTrackingControl

In this project, we focus on the planning and control for the swing trajectories.

The codes are based on: <https://xbpeng.github.io/projects/Robotic_Imitation/index.html>

## Getting Started

We use this repository with Python 3.7 or Python 3.8 on Ubuntu, MacOS and Windows.

- Install MPC extension (Optional) `python3 setup.py install --user`

Install dependencies:

- Install MPI: `sudo apt install libopenmpi-dev`
- Install requirements: `pip3 install -r requirements.txt`

You can run `mpc_controller/my_swing_example.py` to get a quickstart.

Here are the definitions of the importtant varibles in `mpc_controller/my_swing_example.py`:

`_RECORD_VIDEO`: `True` or `False` to record a video of the simulation process or not, which requires ffmpeg in the path.

`_MAX_TIME_SECONDS`: the maximum running time (seconds) of the simulatioin process.

`_NUM_BULLET_SOLVER_ITERATIONS`: the number of iterations of the bullet solver.

`_SIMULATION_TIME_STEP`: the time step of the simulation.

`_ROBOT_BASE_HEIGHT`: the fixed height of the robot base.

`_WITH_OBSTACLE`: `True` or `False` to show an obstacle or not.

`_OBSTACLE_HALF_SIZE`: the half size of the obstacle.

`_OBSTACLE_POS`: the position of the obstacle.

`_MAX_CLEARANCE`: the maximum clearance of the foot path to the ground.

`_PHASE_NUM`: the number of the phases of the swing trajectory.

`_WITH_OPTIMIZATION`: `True` or `False` to use the optimization method or not.

`_FOOT_STEP_DISP`: the displacement matrix (4x3) of the 4 foot steps.

`_PARAMETERS`: collection of the parameters of the swing trajectory to be saved as the name of the result file.

`_SAVE_PATH`: the path to save the result file.

## Finding a feasible trajectory connecting the initial and final positions

We give a method to find a feasible swing trajectory when given an initial and final position of the foot tip. And we also design a tracking controller to track the planned trajectory. To simplify, we only consider the single FR leg and fixed the robot base at a certain height defined by `_ROBOT_BASE_HEIGHT`.

In `mpc_controller/my_swing_example.py`, the initial position of the foot is (0, 0, 0), and the final position is based on `_FOOT_STEP_DISP` which is a 4x3 matrix describing all 4 foot displacements. We can change `_FOOT_STEP_DISP` to give different swing path.

## Finding a collision-free trajectory when there are known obstacles

In the presence of known obstacles, a swing trajectory can also be generated by the proposed method with a collision avoidence module. We tested the trajectory generating method with obtacles of different height of 0.02, 0.04, 0.06, and 0.08 mm. All the tests were successful, which means that the method is avalible.

In `mpc_controller/my_swing_example.py`, to show an obstacle, `_WITH_OBSTACLE` need to be `True`. `_OBSTACLE_HALF_SIZE` and `_OBSTACLE_POS` define the size and position of the obstacle.
