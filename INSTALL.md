# Carla Simulator Installation Instruction for Ubuntu

Official website: [Here](https://carla.org/)

Installation instruction website: [Here](https://carla.readthedocs.io/en/latest/start_quickstart/)

## 1. Getting Started
Firstly, download Ubuntu **CARLA_0.9.14.tar.gz**: [Here](https://github.com/carla-simulator/carla/releases/tag/0.9.14/)

Secondly, extract it.

Then, install **carla** and **libomp5**.
```
pip install carla
sudo apt install libomp5
```

## 2. Run

At root, run this commands.
```
/bin/bash ./CarlaUE4.sh
```

## 3. Create Actors
Install some necessary libraries.
```
cd PythonAPI/examples
pip install -r requirements.txt
```
Generate 30 vehicles and 10 walkers.
```
python generate_traffic.py
```
Press Ctrl + C to exit.
