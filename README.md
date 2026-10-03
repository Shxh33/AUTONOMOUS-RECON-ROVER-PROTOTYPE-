# AUTONOMOUS-RECON-ROVER-PROTOTYPE-
# 🤖 Autonomous Recon Rover

A Raspberry Pi 3 powered, metal-chassis rover that drives itself, sees through a gimbal-mounted camera, detects motion and obstacles, tracks its position with GPS, and can pick things up with a 6 DOF gripper.

> Built for Hack Club. Status: **in progress** (see [JOURNAL.md](JOURNAL.md)).

![Recon Rover](docs/images/rover.jpg)

## What it does

- **Autonomous driving**: avoids obstacles using an ultrasonic sensor
- **Vision**: live camera stream from an OV5647 on a pan/tilt gimbal
- **Detection**: PIR sensor flags warm moving objects
- **Navigation**: GPS logging and waypoint following
- **Manipulation**: 6 DOF gripper for collecting or moving small objects
- **Remote control**: drive and view the camera over WiFi from a browser

## Hardware

| Part | Role |
|---|---|
| Raspberry Pi 3 | Main computer ("brain") |
| OV5647 camera | Vision, mounted on the gimbal |
| Pan/tilt gimbal | Aims the camera independently of the chassis |
| 6 DOF gripper | Picks up and carries objects |
| PIR sensor | Motion / heat detection |
| HC-SR04 (SR04) ultrasonic | Distance and obstacle sensing |
| WiFi module | Wireless link to the operator |
| GPS module | Position and speed |
| Metal chassis | Structure and drivetrain mount |
| 3D printed parts | Mounts, gimbal brackets, sensor housings |

Full list with quantities: [bom.csv](bom.csv)

## Repo layout

```
recon-rover/
├── README.md
├── bom.csv            # bill of materials
├── JOURNAL.md         # build log
├── docs/
│   ├── wiring.md      # pin map and power notes
│   └── images/        # photos, wiring diagram, renders
├── cad/               # STL / STEP files for 3D printed parts
├── firmware/          # code that runs on the Pi
└── LICENSE
```

## Software plan

- Raspberry Pi OS (Lite) + Python 3
- `picamera2` / `libcamera` for the OV5647 camera
- `gpiozero` for PIR, ultrasonic, motors
- `pyserial` + `gpsd` for GPS
- A small Flask web app for the control and video stream
- Servo control for the gimbal and gripper (see wiring notes)

## Getting started

```bash
git clone https://github.com/<your-username>/recon-rover.git
cd recon-rover/firmware
pip install -r requirements.txt
python main.py
```

## Known challenges

- GPS on the Pi 3 UART shares hardware with Bluetooth (details in [docs/wiring.md](docs/wiring.md))
- The ultrasonic echo pin outputs 5V, so it needs a voltage divider for the Pi's 3.3V GPIO
- Servos (gimbal and 6 gripper joints) need their own power supply, not the Pi's 5V pin

## Roadmap

- [ ] Chassis assembled and driving
- [ ] Camera streaming over WiFi
- [ ] Gimbal control
- [ ] Obstacle avoidance
- [ ] PIR detection alerts
- [ ] GPS logging
- [ ] Gripper control
- [ ] Autonomous patrol mode

## License

MIT, see [LICENSE](LICENSE).
