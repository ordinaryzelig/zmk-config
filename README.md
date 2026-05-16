## Installation

### First time

- https://zmk.dev/docs/user-setup.
- Select cradio, nice!nano.

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

## Keymap config

- Edit config.cradio.keymap.
- Push to github.
- Action will automatically run.
- If successful, download the resulting zip file.
- Unzip and flash.

## Build locally

### Podman

- Follow podman directions in https://v0-3-branch.zmk.dev/docs/development/local-toolchain/setup/container?container=podman.
- Run container with `podman run -it --rm --security-opt label=disable --workdir /workspaces/zmk -v /Users/ningja/dev/projects/zmk:/workspaces/zmk -v /Users/ningja/dev/projects/zmk-config:/workspaces/zmk-config -p 3000:3000 zmk /bin/bash`
  - `west build -b nice_nano -- -DSHIELD=cradio_left`.
  - Copy zmk.uf2 to local dir: `cp /workspaces/zmk/app/build/zephyr/zmk.uf2 /workspaces/zmk/zmk_left.uf2`.
  - Repeat for right.
- Flash files to controllers (see Re-setup above).

### Native

#### Install

- Follow instructions at https://v0-3-branch.zmk.dev/docs/development/local-toolchain/setup/native?operating-systems=mac.
- Zephyr SDK notes:
  - Requires `wget` (install via homebrew).
  - Move tar to `.local` before extracting.

### Rebuilding

- `west build -d build/left -p always -s app -b nice_nano -- -DSHIELD=cradio_left -DZMK_CONFIG="/Users/ningja/dev/projects/zmk-config/config"`.
- `west build -d build/right -p always -s app -b nice_nano -- -DSHIELD=cradio_right -DZMK_CONFIG="/Users/ningja/dev/projects/zmk-config/config"`.
- `zmk.uf2` files will be in `build/<left|right>/zephyr`.
- Flash each to each side.

## Troubleshooting

### Device shows up in bluetooth settings, but won't connect.

- From bluetooth settings: find device, click "Forget this device".
- Clear BT on keyboards: (default) tri-layer: BT_CLR.
- Connect again.
