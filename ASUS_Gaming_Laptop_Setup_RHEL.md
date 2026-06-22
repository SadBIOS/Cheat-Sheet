# Enable dGPU Switching Capabilities in Modern Asus

### 1. Enable ASUS Linux COPR and RPM Fusion (for NVIDIA)
```bash
sudo dnf copr enable lukenukem/asus-linux -y
```
```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm -y
```
```bash
sudo dnf update --refresh
```
---

### 2. Install NVIDIA Proprietary Drivers and CUDA runtime
```bash
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda -y
```
---

### 3. Install ASUS Linux tools
```bash
sudo dnf install asusctl supergfxctl rog-control-center -y
```
---

### 4. Reload and enable ASUS services
```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl enable --now asusd.service
```
```bash
sudo systemctl enable --now supergfxd.service
```
---

### 5. Configure initramfs and kernel parameters for NVIDIA
```bash
echo 'add_drivers+=" nvidia nvidia_modeset nvidia_uvm nvidia_drm "' | sudo tee /etc/dracut.conf.d/nvidia.conf
```
```bash
sudo dracut --force
```
```bash
sudo grubby --update-kernel=ALL --args="nvidia-drm.modeset=1 nvidia-drm.fbdev=1"
```