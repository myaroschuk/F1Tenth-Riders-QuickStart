# The F1TENTH - Riders

Sample project for the [Trinity College F1Tenth Challenge](https://riders.ai/challenge/40). 

## Installation

### Local Development with F1Tenth Gym

First clone this repository:

```bash
git clone https://gitlab.com/acrome-colab/riders-poc/f1tenth-riders-quickstart --config core.autocrlf=input
cd f1tenth-gym-quickstart
pip install --user -e gym
```

### Testing with Docker

First build required image:

```bash
docker-compose build agent
```

Create an `.env` file at the root of the project with following contents:

```bash
RACE_MAP_PATH=/catkin_ws/src/f1tenth_gym_ros/maps/SILVERSTONE.yaml
RACE_MAP_IMG_EXT=.png
F1TENTH_AGENT_NAME=a1
F1TENTH_AGENT_IMAGE=a1
RIDERS_CHALLENGE_ID=40
RIDERS_API_HOST=https://api.riders.ai
RIDERS_F1TENTH_HOST=https://f1tenth.riders.ai
```

Start ROSCore & F1Tenth ROS Bridge:

```bash
docker-compose up --force-recreate roscore-dev bridge-dev
```

Go to http://localhost:6080 , if everything worked properly until now, you should see simulator window. 
Finally, launch agent:   

```bash
docker-compose up --force-recreate agent-dev
``` 

You should see your agent moving in a single direction and crashing to wall in ~2.9 seconds.

### Changing Driver

To add a new Driver, paste it into the file [pkg/src/pkg/drivers.py](./pkg/src/pkg/drivers.py)

To select your new driver, replace it in the file [pkg/nodes/f1tenth_ros_agent.py](./pkg/nodes/f1tenth_ros_agent.py) as shown below, where we select GapFollower:

```python
from pkg.drivers import GapFollower as Driver
```
