# First Assignment of the rt2
## Action Package:

This module facilitates 'got to point' behavior-based robot control in the gazebo environment. The robot then positions itself in relation to a randomly created target. It sets the linear speed to move to the desired position, and once there, it makes the necessary adjustments to get the desired angular position. The procedure will loop if the robot is not stopped, creating new goal destinations and poses. The robot can be preempted, stopped at any moment, and restarted when the new target is reached because its "go to point" is built as an action server.

Two nodes are implemented as python scripts:
- go_to_point: the node GoToPoint, which implements a service to drive a robot toward a point in the gazebo environment.This node publishes on the topics /cmd_vel the velocity of the robot and read its position by subscribing the topic '/odom'.
- user_interface: the UserInterface, which asks the user to start/stop the robot, and calls the service implemented in the Finite State Machine node.

Other two nodes are implemented in C++:
- position_server: the node PositionServer, which implements a random position service.The service implemented in the Position Server node replies with random values for x, y, and theta, where x and y should be limited between some minimum and maximum values.
- state_machine: The service implemented in the Robot FSM node gives the possibility to start or stop the robot behaviour.it monitors the request of a new goal pose when needed, sending it as a goal to 'go_to_point' action server.

## Command for Running the package:
A launch file has been provided to generate the Gazebo simulation and run all the nodes required for the control of the non-holonomic robot:

- sim.launch: this launch file is used to launch all the nodes and to start the gazebo simulation.

```
roslaunch rt2_assignment1 sim.launch
```


