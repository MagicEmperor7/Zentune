🔧 Tech Stack
Language: C
Build System: CMake
Dependencies:
libpci (for accessing PCI devices)
Optionally: ryzen_smu kernel module (for more secure and reliable access)
Platforms: Linux and Windows

🛠️ How to Build (Linux)
1. Install Dependencies
On Debian/Ubuntu
Bash: sudo apt install build-essential cmake libpci-dev
On Fedora
Bash: sudo dnf install cmake gcc-c++ pciutils-devel
On Arch
Bash: sudo pacman -S base-devel pciutils cmake

2. Clone and Build RyzenAdj
Bash:
git clone https://github.com/FlyGoat/RyzenAdj
cd RyzenAdj
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make

3. (Optional) Install
Bash: sudo cp ryzenadj /usr/local/bin/

⚙️ How to Use RyzenAdj
You must run it as root (Linux) or administrator (Windows).
Basic Syntax:
Bash: sudo ./ryzenadj [options]
Example: Set all power limits to 45W and Tctl to 90°C
Bash: sudo ./ryzenadj --stapm-limit=45000 --fast-limit=45000 --slow-limit=45000 --tctl-temp=90

📜 Common Options (All in milliwatts (mW), milliamps (mA), MHz, or degrees C)
| Option                          | Description                            |
| ------------------------------- | -------------------------------------- |
| `--stapm-limit`                 | Sustained power limit (e.g., 45000 mW) |
| `--fast-limit`                  | Fast (short burst) power limit         |
| `--slow-limit`                  | Slow (long-term average) power limit   |
| `--tctl-temp`                   | CPU temperature limit in °C            |
| `--vrm-current`                 | VRM VDD current limit (mA)             |
| `--vrmsoc-current`              | VRM SoC current limit (mA)             |
| `--vrmmax-current`              | VRM max current (EDC)                  |
| `--max-gfxclk` / `--min-gfxclk` | GPU core frequency (MHz)               |
| `--max-lclk` / `--min-lclk`     | Memory controller frequency            |
| `--max-vcn` / `--min-vcn`       | Video encoding engine frequency        |
| `--power-saving`                | Enables power saving preset            |
| `--max-performance`             | Enables performance preset             |

🧪 Info & Debug
--info         # Show power metrics after applying changes
--dump-table   # Show full table of power settings before/after

⚠️ Important Notes
Changes are not persistent across reboots. You can automate it via a shell script or systemd service.
Requires root/admin access.
Be careful: setting values too high/low can cause overheating, instability, or shutdowns.
