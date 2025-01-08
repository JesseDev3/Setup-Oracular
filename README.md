# Ubuntu - Docker Desktop

#Docker desktop runs a vm that requires KVM support
modprobe kvm
modprobe kvm_intel  # Intel processors
modprobe kvm_amd    # AMD processors
kvm-ok              # View the diagnostics
lsmod | grep kvm    # Check if the KVM modules are enabled
ls -al /dev/kvm     # Check ownership
sudo usermod -aG kvm $USER # Add your user to group

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Docker packages:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Verify the installation:
sudo docker run hello-world

# Download latest deb package
# https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64&_gl=1*kkt779*_gcl_au*MTg3OTA0NTQ4NS4xNzM2Mjg3OTc2*_ga*MTIyNzg5ODA4Mi4xNzM2Mjg3OTc3*_ga_XJWPQMJYHQ*MTczNjI4Nzk3Ni4xLjEuMTczNjI4OTI2OS40OS4wLjA.

# Install the package with apt as follows:
sudo apt-get update
sudo apt-get install ./docker-desktop-amd64.deb
# At the end of the installation process, apt displays an error due to installing a downloaded package. You can ignore this error message.
# N: Download is performed unsandboxed as root, as file '/home/user/Downloads/docker-desktop.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)

# Check versions of binaries
$ docker compose version
Docker Compose version v2.29.1

$ docker --version
Docker version 27.1.1, build 6312585

$ docker version
Client: 
 Version:           23.0.5
 API version:       1.42
 Go version:        go1.21.12
<...>

# Initialize pass by using a gpg key
gpg --generate-key # Follow the prompts
pass init <your_generated_gpg-id_public_key>

# Launch Docker Desktop:
systemctl start docker
systemctl --user start docker-desktop

# Quit Docker Desktop
systemctl --user stop docker-desktop

# Enable Docker Desktop to start on sign in
# Open Docker Desktop and go to Settings > General, then select Start Docker Desktop when you log in or:
systemctl --user enable docker-desktop

# Update Docker Desktop
sudo apt-get install ./docker-desktop-<arch>.deb # Replace <arch> with the architecture of your system
