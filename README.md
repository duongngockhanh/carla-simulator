# Instruction for use of the CARLA
The version I use is CARLA 0.9.14 (stable and bug-free)

The official guide starts [here](https://carla.readthedocs.io/en/0.9.14/foundations/)

## 1. Foundations

### 1.1. World and client
Declare libraries
```
import carla
import random
from carla import Transform, Location, Rotation
```
Initialize a client
```
client = carla.Client('localhost', 2000)
```
Change map
```
client.load_world('Town07')
```
Declare world
```
world = client.get_world()
```
### 1.2. Synchronous and asynchronous mode
Use **asynchronous** mode if you are in **third-person** view. (By default, CARLA runs in asynchronous mode.)

Use **synchronous** mode if you are in **first-person** view.

### 1.3. Recorder
Start recording
```
client.start_recorder("/home/carla/recording01.log")
```
Stop recording
```
client.stop_recorder()
```
Simulation playback
```
client.replay_file("recording01.log", start, duration, camera)
```

## 2. Actors
Actors in CARLA includes:
- vehicles
- walkers
- sensors
- traffic signs
- traffic lights
- the spectator.

This section will cover spawning, destruction, types, and how to manage them.
