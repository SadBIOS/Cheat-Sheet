# Offline Setup Procedure for Official STM32 Development Suite for Debian

### 1. Prepare the System

> [!TIP]
> Updating the package manager is recommended (as of now, please check for issues during installation). You can also run a full system upgrade (this is at your degression).

```bash  
sudo apt install unzip p7zip-full libusb-1.0-0 libusb-1.0-0-dev udev zenity default-jre build-essential gcc g++ make gdb gdb-multiarch pkg-config libncurses6 libtinfo6 libwebkit2gtk-4.1-0 python3 python3-pip desktop-file-utils psmisc usbutils
```

---

### 2. Gather Binaries

> [!WARNING]  
> STMicroelectronics NV **REQUIRES** an account (email address) to download their software/toolchains. I know they are an European corporation with better privacy rules than the USA but give them your data at your own risk.

#### Download Links 

> * [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) (select **Debian Linux** from the download options)
> * [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) (select **Generic Linux** from the download options avoid ***STM32CubeMX2*** if you want to live)
> * [STM32CubeProg](https://www.st.com/en/development-tools/stm32cubeprog.html) (select **STM32CubePrg-Lin** from download options)

---

### 3. Installation

> [!NOTE]
> * During the whole process I used ```~/Downloads``` as the root directory
> * All package names were preserved for clarity 

> [!TIP]
> Downloading files from **STEP 2** and **STEP ???????** beforehand is required for **Air-gapped** deployments.

#### Create the following directories

> ```bash
> mkdir -p stm32_installers/cubemx
> ```
> ```bash
> mkdir -p stm32_installers/cubeprg
> ```
> ```bash
> mkdir -p stm32_installers/cubeide
> ```
#### Unzip the downloaded files
> ```bash
> unzip SetupSTM32CubeProgrammer_linux_64.zip -d stm32_installers/cubeprg
> ```
> ```bash
> unzip stm32cubemx-lin-v6-17-0.zip -d stm32_installers/cubemx
> ```
> ```bash
> unzip st-stm32cubeide_2.1.1_28236_20260312_0043_amd64.deb_bundle.sh.zip -d stm32_installers/cubeide
> ```
#### Change execution permissions of extracted files for installation

CubeMX

> ```bash
> cd stm32_installers/cubemx
> ```
> ```bash
> chmod +x SetupSTM32CubeMX*
> ```
> ```bash
> ./SetupSTM32CubeMX
> ```
<br>
CubeProg

> ```bash
> cd stm32_installers/cubeprg
> ```
> ```bash
> chmod +x SetupSTM32CubeProgrammer*.linux
> ```
> ```bash
> ./SetupSTM32CubeProgrammer*.linux
> ```
<br>
CubeIDE

> ```bash
> cd stm32_installers/cubeide
> ```
> ```bash
> chmod +x st-stm32cubeide_*_amd64.deb_bundle.sh
> ```
> ```bash
> sudo ./st-stm32cubeide_*_amd64.deb_bundle.sh
> ```
---
### 4. Adding Firmware Packages
#### Collect all firmware packages

> [!WARNING]  
> * There are **TWO** firmware package, one called **STM32CubeXX** and **Patch_CubeXX** (where XX stands for the core, which in my case are thee F1, F4, F7, G4 and H7)
> * Check CubeMX's package manager (inside ```Help > Manage embedded software packages```) for the latest supported package version before downloading. As anything newer will not show up there and will cause problems

#### Download Links 
The download links are for the controllers that I own

> * [STM32F1xx](https://www.st.com/en/embedded-software/stm32cubef1.html)
> * [STM32F4xx](https://www.st.com/en/embedded-software/stm32cubef4.html)
> * [STM32F7xx](https://www.st.com/en/embedded-software/stm32cubef7.html)
> * [STM32G4xx](https://www.st.com/en/embedded-software/stm32cubeg4.html)
> * [STM32H7xx](https://www.st.com/en/embedded-software/stm32cubeh7.html)
#### Create the root directory for CubeMX
```bash
mkdir -p ~/STM32Cube/Repository
```
#### Unzip all 
> ```bash
> unzip stm32cubef1.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubef1-v1-8-7.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubef4-v1-28-0.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubef4-v1-28-3.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubef7_v1-17-0.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubef7-v1-17-4.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubeg4-v1-6-0.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubeg4-v1-6-2.zip -d ~/STM32Cube/Repository/
> ```
> ```bash
> unzip stm32cubeh7-v1-13-0.zip -d ~/STM32Cube/Repository/
> ```

---

> [!NOTE]
> ### If stm32cubeide for some reason does not show up/launch
> Edit this file with superuser persmissions
> ```bash
> sudo micro /usr/share/applications/st-stm32cubeide-2.1.1.desktop
> ```
> ---
> Change
> ```bash 
> Exec=/opt/st/stm32cubeide_2.1.1/stm32cubeide_wayland %F
> ```
> To
> ```bash
> Exec=/opt/st/stm32cubeide_2.1.1/stm32cubeide %F
>```
> ---
> Finally Run
> ```bash
> sudo update-desktop-database
> ```
> ```bash
> xfdesktop --reload
> ```

> [!IMPORTANT]  
> * This project has been tested for kernel **6.12.94+deb13** (Debian 13.5 "*Trixie*") running **XFCE4**
> * As of writing, **Wayland** support is unknown
