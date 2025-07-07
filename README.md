# This file helps in understanding the Full_Potential_Steering_auto.py script.

## Import
  - rospy
  - time
  - copy
  - queue
  - ros msgs like sensor_msg and std_msg
  - traversal (custom package)
  - add (from operators; equivalent to '+')

## Control Flow
1. Initialization:
   - `Drive` class is instantiated.
   - Subscribed to the neccessary ROS topics.
2. 

## Subscribers
  - `/joy`: Joystick input
  - `/enc_auto`: Encoder angles for steering feedback (`Float32MultiArray`)
  - `/motion`: Provides autonomous commands through linear and angular velocity msgs
  - `/rot`: Rotation mode integer

## Publishers
  - `motor_pwm`: Sends motor drive and steer PWM signals.
  - `state`: Publishes current mode (manual/autonomous)

## Attributes
  - `enc_callback()`: It reads steering encoder values and stores them in `self.enc_data` based on the correct wheel number and sign conventions. It gets this data from `msg.data` which is a list of 6 float values
  - `rotinplace_callback()`: It receives msg through `msg.data` which is a single integer that tells whether the wheel should rotate in place or move forward.
  - `autonomous_motion_callback()`: It firstly checks whether the motion is in autonomous mode. If true, it sets the desired linear and angular velocities and crab mode.
  - `joyCallback()`: It checks whether the motion is in manual mode. If true, it processes the joystick input to update the drive, steering and control mode states. Finally, it processes switching between autonomous and manual mode irrespective of previous mode.
  - `spin()`: It is the main publisher loop that runs at 10Hz. It keeps running till the ROS node is shutdown. It gives a pause while running to publish the pwm values to `motor_pwm`.
  - `main()`: It is the main loop that calls for steering, driving and autonomous control functions.
  - 
