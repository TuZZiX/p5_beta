# p5_beta

Assignment on trajectory planning for PS5 and PS6.  It
demonstrates the following behaviors:

+ graceful halt from LIDAR alarm
+ graceful recovery from LIDAR alarm
+ graceful recovery from wireless E-stop
+ ability to execute open-loop control corresponding to a prescribed
  polyline path
+ ability to append subgoal poses to a prescribed path plan
+ ability to flush a path plan and replace it

Also included in this submission is three videos, one of the Gazebo
simulation, one of the robot running on ruler, the other of the robot trundling from the lab hallway to the vending machine.

## Example usage

### General

To send the emergency stop, run `rosservice call /estop_service`.  A
more complete listing of available service calls can be seen below:

```
/clear_estop_service
/estop_service
/flush_path_queue_service
```

In addition to these three trigger-based services, there is also a
fourth that requires an argument.  `/append_path_queue_service` can be
called from a node.  That node, `append_path_client`, accepts as
arguments `stop`, `clear`, `flush`, or `append x y th`, where the last three
arguments are the desired X, Y, and yaw values.  Multiple such
triplets can be specified at once, in `x1 y1 th1 x2 y2 th2 ...` order.
If no arguments beyond the initial `append` are provided, a default
path tracing out a square will be assumed. `stop` and `clear` are provided as easy mnemonics for the estop services, and `flush` will clear paths that have not yet been executed.

### Gazebo Specific

Executing the following Gazebo-based launch file will bring up an
instance of Gazebo complete with a mobot, a LIDAR obstacle detector,
and an open-loop controller.  The second command will allow one to use
the included services, detailed in the General section. The robot will move 5 meters forward and 5 meters backward.

```
$ roslaunch p5_beta load_world_and_controller.launch
$ rosrun p5_beta des_state_publisher
```


### Jinx Specific

Executing the following launch file will start the jinx open-loop controller, a LIDAR obstacle detector, and topic re-mapping. The second command will allow one to use the included services, detailed in the General section. The robot will move from the elevator to the vending machine.

```
$ roslaunch p5_beta jinx_controller.launch
$ rosrun p5_beta des_state_publisher jinx
```


