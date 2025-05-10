Problem Statement
A severe flood in a coastal town has left numerous residents stranded on rooftops, cut off from access to basic necessities like food, water, and medicine. Swift, autonomous aerial assistance is essential to locate and deliver supplies to survivors where ground access is not feasible.

To address the challenge, we propose a dual-drone system that includes:
1. Scout Drone (SD) – for real-time area surveillance, survivor detection, and geotagging.
2. Delivery Drone (DD) – for precision air-drop of 10 survival kits (200g each) to detected survivors.
Both drones are designed for autonomous operation, coordinated via a single Ground Control Station (GCS).

1. Scout Drone (SD)
Type: Quadrotor VTOL
Why:
Vertical takeoff/landing in flooded urban environments
Stable hover for high-resolution image/video capture
Payload:
RGB + thermal imaging camera
Onboard speaker for voice announcements
Functional Capabilities:
Autonomous area scanning
Survivor detection using OpenCV + YOLOv8
GPS geotagging
Real-time video feed to GCS

2. Delivery Drone (DD)
Type: Hexacopter VTOL
Why:
Enhanced lift capacity and redundancy (safer flight in case of motor failure)
Stable flight required for precise kit drops
Payload:
10 × 200g survival kits (2 kg total)
Servo-based release mechanism
Functional Capabilities:
Autonomous navigation to survivor coordinates
Descends to 20 ft for delivery
Drops kits with high accuracy (Zone A targeting)

 Autonomy and Vision System
Survivor Detection: Using YOLOv8 with RGB + thermal fusion for better accuracy in complex post-disaster visuals
Geotagging: GPS coordinates extracted upon detection
Drop Triggers: Activated only near verified survivor locations

 Command and Control
Software: QGroundControl with KML file mission planning
Features:
Real-time drone telemetry and video feed
Integrated mission timeline for scanning and drop sequence
Fail-safes:
Return-to-home on low battery or link loss
Geo-fencing and altitude locking
Emergency pause/resume with auto-recovery

Drone Type Justification

| Drone          | Type             | Justification                                                                 |
|----------------|------------------|-------------------------------------------------------------------------------|
| **Scout Drone**   | Quadrotor VTOL    | VTOL enables deployment in tight/flooded areas, hover for scanning, and real-time surveillance |
| **Delivery Drone**| Hexacopter VTOL   | Provides better lift for payloads, hover stability for accurate drops, and redundancy for safety |


 

Drone System Summary Table

| Component        | Scout Drone                                  | Delivery Drone                            |
|------------------|-----------------------------------------------|-------------------------------------------|
| **Main Controller** | Raspberry Pi 4                              | ESP32 / Teensy                             |
| **Camera**          | PiCamera + Thermal Module                   | N/A                                        |
| **Navigation**      | GPS Module                                   | GPS + Barometer + IMU                      |
| **Processing**      | Onboard YOLOv8 (OpenCV + Python)             | Waypoint & drop logic (C/C++/MicroPython)  |
| **Communication**   | Wi-Fi / Optional 4G LTE to GCS               | Wi-Fi or ESP-NOW (peer or GCS link)        |
| **Drop System**     | N/A                                          | Servo-based mechanism (10 survival kits)   |

