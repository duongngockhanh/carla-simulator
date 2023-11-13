# Instruction for use of the CARLA
The version I use is CARLA 0.9.14 (stable and bug-free)

The official guide starts [here](https://carla.readthedocs.io/en/0.9.14/foundations/)

Traffic Manager: [here](https://carla.readthedocs.io/en/docs-preview/adv_traffic_manager/)

## 0. Run
```
/bin/bash ./CarlaUE4.sh
```

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

### 2.1. Bluerprint library
```
blueprint_library = world.get_blueprint_library()
```

### 2.2. Single Vehicle
2.2.1. Create a set of locations on the map where vehicles can be placed.
```
spawn_points = world.get_map().get_spawn_points()
```

2.2.2. Spawn a car
```
vehicle_bp = blueprint_library.find('vehicle.lincoln.mkz_2020')
vehicle = world.try_spawn_actor(vehicle_bp, random.choice(spawn_points))
print(vehicle)
```

2.2.3. Set the sight position relative to the vehicle.
```
spectator = world.get_spectator()
transform = carla.Transform(vehicle.get_transform().transform(Location(x=-4, z=2.5)), vehicle.get_transform().rotation)
spectator.set_transform(transform)
```

2.2.4. Turn on autopilot mode
```
vehicle.set_autopilot(True)
```

2.2.5. **Optinal**: Set up vehicle controls. In the following code, apply_control() is used to send control signals to the vehicle. In this example, the speed is set to 1.0 (maximum), the steering angle is set to 0.0, no brake, no handbrake, and no reverse.
```
control = carla.VehicleControl(throttle=0.0, steer=0.0, brake=0.0, hand_brake=False, reverse=False)
vehicle.apply_control(control)
```

### 2.3. Sensors
This example spawns a camera sensor, attaches it to a vehicle, and tells the camera to save the images generated to disk.
```
camera_bp = blueprint_library.find('sensor.camera.rgb')
camera = world.spawn_actor(camera_bp, relative_transform, attach_to=my_vehicle)
camera.listen(lambda image: image.save_to_disk('output/%06d.png' % image.frame))
```
