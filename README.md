# LeRobot-SO-ARM101-Pro
Building and training LeRobot SO-ARM101 Pro

Useful information:
https://huggingface.co/docs/lerobot/so101

# Setup for mac
[this is a summary for https://huggingface.co/docs/lerobot/installation]
brew install svt-av1
brew install ffmpeg
ffmpeg -encoders | grep svt   # Verify libsvtav1 is enabled
python3.13 -m venv venv
source venv/bin/activate

pip install 'lerobot[feetech]'   # (no need for pip install -e ".[feetech]")

## follower arm
1. connect the power to one motor board and run
lerobot-find-port
2. get the last part of the e.g. "tty.usbmodem5AE60750641"
3. connect the 12v power to the board and connect the gripper motor
lerobot-setup-motors \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem5AE60750641  # <- paste here the port found at previous step
4. hit enter and connect next motor, until all motors are done

## leader arm:
1. connect the power to the other motor board and run
lerobot-find-port
2. get the last part of the e.g. "tty.usbmodem5AE70447401"
3. connect the 5v power to the board and connect the gripper motor
lerobot-setup-motors \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem5AE70447401
4. hit enter and connect next motor, until all motors are done

## Calibration
lerobot-calibrate \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem5AE60750641 \ # The port of your follower arm
    --robot.id=my_awesome_follower_arm # Give the robot a unique name

lerobot-calibrate \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem5AE70447401 \
    --teleop.id=my_awesome_leader_arm

    
# Teleoperate

lerobot-teleoperate \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem5AE60750641 \
    --robot.id=my_awesome_follower_arm \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem5AE70447401 \
    --teleop.id=my_awesome_leader_arm \
    --display_data=true
