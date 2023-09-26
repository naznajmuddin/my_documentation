## Overview

Recommended steps to setup Zephyr RTOS.

More info: https://docs.zephyrproject.org/latest/develop/getting_started/index.html

**Recommended Operating System:**
* Ubuntu 20.04
***************************************

**1. Open terminal and Update OS**
```
sudo apt update
sudo apt upgrade
```

**2. Execute the Kitware archive script**

```
wget https://apt.kitware.com/kitware-archive.sh
sudo bash kitware-archive.sh
```

**3. Use apt to install the required dependencies:**
```
sudo apt install --no-install-recommends git cmake ninja-build gperf \
  ccache dfu-util device-tree-compiler wget \
  python3-dev python3-pip python3-setuptools python3-tk python3-wheel xz-utils file \
  make gcc gcc-multilib g++-multilib libsdl2-dev libmagic1
```

**4. Verify the versions of the main dependencies installed on your system by entering:**

* This is an optional step.
```
cmake --version
python3 --version
dtc --version
```
********************
### Get Zephyr and install Python dependencies
**1. Install west, and make sure ~/.local/bin is on your PATH environment variable:**
```
pip3 install --user -U west
echo 'export PATH=~/.local/bin:"$PATH"' >> ~/.bashrc
source ~/.bashrc
```
**2. Get the Zephyr source code**
```
west init ~/zephyrproject
cd ~/zephyrproject
west update
```

**3. Export a Zephyr CMake package.**
```
west zephyr-export
```

**4. Zephyr’s scripts/requirements.txt file declares additional Python dependencies. Install them with pip3.**
```
pip3 install --user -r ~/zephyrproject/zephyr/scripts/requirements.txt
```

********************
### Install Zephyr SDK
**1. Download and verify the Zephyr SDK bundle:**
```
cd ~
wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.1/zephyr-sdk-0.16.1_linux-x86_64.tar.xz
wget -O - https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.1/sha256.sum | shasum --check --ignore-missing
```

**2. Extract the Zephyr SDK bundle archive:**
```
tar xvf zephyr-sdk-0.16.1_linux-x86_64.tar.xz
```

**3. Run the Zephyr SDK bundle setup script:**
```
cd zephyr-sdk-0.16.1
./setup.sh
```

**4. Install udev rules, which allow you to flash most Zephyr boards as a regular user:**
```
sudo cp ~/zephyr-sdk-0.16.1/sysroots/x86_64-pokysdk-linux/usr/share/openocd/contrib/60-openocd.rules /etc/udev/rules.d
sudo udevadm control --reload
```

### Build your first Zephyr: Blinky Sample

**1. Build the Blinky sample, change `<your-board-name>` appropriately for your board:**

```
cd ~/zephyrproject/zephyr
west build -p always -b <your-board-name> samples/basic/blinky
```
**Example for STM32F411CEU6 Blackpill:**
```
cd ~/zephyrproject/zephyr
west build -p always -b blackpill_f411ce samples/basic/blinky
```
**Example for STM32 Nucleo H723ZG:**
```
cd ~/zephyrproject/zephyr
west build -p always -b nucleo_h723zg samples/basic/blinky
```

**2. Flash the sample**
```
west flash
```