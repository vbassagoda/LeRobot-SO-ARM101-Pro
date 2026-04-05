# LeRobot-SO-ARM101-Pro
Building and training LeRobot SO-ARM101 Pro

Useful information:
https://huggingface.co/docs/lerobot/so101

# Setup for mac
brew install svt-av1
brew install ffmpeg
ffmpeg -encoders | grep svt   # Verify libsvtav1 is enabled
python3.13 -m venv venv
source venv/bin/activate
