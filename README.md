## Installation

### First time

- https://zmk.dev/docs/user-setup

### Re-setup

- Pick compiled firmware from https://github.com/ordinaryzelig/zmk-config/actions.
- Flash to controllers:
  - Connect via USB-C while power is off.
  - Double press reset on controller.
  - For each side
    - Copy `.uf2` file to controller mounted drive.
    - Controller will auto-restart (you may get warning from OS that disk was not ejected properly).
  - For left side only
    - Switch controller on.
    - It should be detectable by bluetooth. Connect like any bluetooth device.
    - Right should automatically connect to left.
