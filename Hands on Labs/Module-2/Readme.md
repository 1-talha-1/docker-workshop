# Docker Installation & Configuration Deep Dive
## Comprehensive Technical Manual

*Prepared by: Choudhry Shehryar, MLOps Engineer*

## Introduction

This manual provides comprehensive instructions for installing and configuring Docker in various enterprise environments. Docker provides container virtualization, allowing applications to run in isolated environments with consistent behavior across development, testing, and production.

## Docker Architecture Overview

Before installation, it's important to understand Docker's architectural components:

- **Docker Engine**: The core runtime that builds and runs containers
  - **dockerd**: The Docker daemon that manages Docker objects
  - **Docker REST API**: API interface for interacting with the daemon
  - **Docker CLI**: Command line interface for sending commands
  
- **containerd**: Container runtime that manages container lifecycle
- **runc**: Low-level container runtime (OCI compliant)

![Docker Architecture](https://k21academy.com/wp-content/uploads/2020/05/2020-05-12-16_36_49-PowerPoint-Slide-Show-Azure_AZ104_M01_Compute_ed1-1.png)

### For windows users only.
```bash
Install using Command Prompt
Step 1: Start CMD with administrative privileges.
Step 2:Execute "wsl --install" command.
Step 3:Run "wsl -l -o" to list other Linux releases.
Step 4:You can install your favorite Linux distribution, use "wsl --install -d NameofLinuxDistro."
```
### Docker Desktop installation
https://docs.docker.com/get-started/get-docker/

### DOcker Engine installation
https://docs.docker.com/engine/install/

## Post-Installation Configuration

## Docker Daemon Configuration

### Configuration File

The Docker daemon configuration file location varies by platform:

- **Linux**: `/etc/docker/daemon.json`
- **Windows Server**: `C:\ProgramData\docker\config\daemon.json`
- **Docker Desktop**: Settings/Preferences -> Docker Engine

Create a basic configuration file:

```bash
# Linux
sudo tee /etc/docker/daemon.json <<EOF
{
  "data-root": "/var/lib/docker",
  "storage-driver": "overlay2",
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
EOF

# Apply changes
sudo systemctl restart docker
```

```powershell
# Windows Server
New-Item -Path "C:\ProgramData\docker\config\daemon.json" -Force -Value @"
{
  "data-root": "C:\\ProgramData\\docker\\data",
  "storage-driver": "windowsfilter",
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
"@

# Apply changes
Restart-Service Docker
```

### Storage Driver Configuration

Select the appropriate storage driver for your environment:

| Driver | Platform | Notes |
|--------|----------|-------|
| overlay2 | Linux (modern) | Recommended for most Linux distributions |
| devicemapper | Linux (older) | Use direct-lvm mode for production |
| btrfs | Linux w/Btrfs | Good for high I/O, requires Btrfs filesystem |
| zfs | Linux w/ZFS | Good for high I/O, requires ZFS filesystem |
| windowsfilter | Windows | Default for Windows containers |

Example overlay2 configuration:
```json
{
  "storage-driver": "overlay2",
  "storage-opts": [
    "overlay2.override_kernel_check=true"
  ]
}
```

Example devicemapper configuration (direct-lvm):
```json
{
  "storage-driver": "devicemapper",
  "storage-opts": [
    "dm.directlvm_device=/dev/xvdf",
    "dm.thinp_percent=95",
    "dm.thinp_metapercent=1",
    "dm.thinp_autoextend_threshold=80",
    "dm.thinp_autoextend_percent=20",
    "dm.directlvm_device_force=false"
  ]
}
```

### Logging Configuration

Configure logging for containers:

```json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3",
    "labels": "production_status",
    "env": "os,customer"
  }
}
```

Alternative log drivers:
- `syslog`: Logs to syslog
- `journald`: Logs to journald
- `fluentd`: Logs to fluentd
- `splunk`: Logs to splunk
- `awslogs`: Logs to Amazon CloudWatch

## Registry Configuration

### Private Registry Authentication

Create or update `~/.docker/config.json` (Linux/Mac) or `%USERPROFILE%\.docker\config.json` (Windows):

```json
{
  "auths": {
    "registry.example.com": {
      "auth": "dXNlcm5hbWU6cGFzc3dvcmQ="
    }
  }
}
```

The `auth` value is Base64 encoded `username:password`.

You can login to a registry using the Docker CLI:
```bash
docker login registry.example.com
```

### Registry Mirrors

Configure registry mirrors to improve pull performance:

```json
{
  "registry-mirrors": [
    "https://mirror.gcr.io",
    "https://registry-1.docker.io"
  ]
}
```

### Insecure Registries

For testing purposes or internal registries without HTTPS:

```json
{
  "insecure-registries": [
    "10.10.10.10:5000",
    "registry.internal:5000"
  ]
}
```

⚠️ **Warning**: Only use insecure registries in testing environments or isolated networks.

## Performance Tuning

### Resource Limits

Configure default resource limits for containers:

```json
{
  "default-shm-size": "64M",
  "default-ulimits": {
    "nofile": {
      "Name": "nofile",
      "Hard": 64000,
      "Soft": 32000
    },
    "memlock": {
      "Name": "memlock",
      "Hard": -1,
      "Soft": -1
    }
  }
}
```

### Linux Kernel Parameters

For high-performance Docker environments, adjust these sysctl settings:

```bash
# Create a sysctl configuration file
sudo tee /etc/sysctl.d/99-docker.conf <<EOF
# Network settings
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1

# File descriptor limits
fs.file-max = 1000000

# Memory settings
vm.max_map_count = 262144
vm.swappiness = 1
EOF

# Apply settings
sudo sysctl -p /etc/sysctl.d/99-docker.conf
```

### CPU and Memory Allocation (Docker Desktop)

For Docker Desktop, allocate resources through the UI:
1. Open Docker Desktop
2. Go to Settings/Preferences -> Resources
3. Adjust CPUs, Memory, Swap, and Disk image size

### DNS Configuration

If experiencing DNS issues, configure DNS settings:

```json
{
  "dns": ["8.8.8.8", "8.8.4.4"],
  "dns-opts": ["timeout:2", "attempts:3"],
  "dns-search": ["example.com", "test.example.com"]
}
```

## Installation Verification

### Basic Verification

Check Docker version and info:
```bash
docker --version
docker version
docker info
```

Run a test container:
```bash
docker run hello-world
```

### Advanced Verification

Check system-wide information:
```bash
docker system info
```

Verify Docker API works:
```bash
curl --unix-socket /var/run/docker.sock http://localhost/version
```

Monitor Docker daemon status:
```bash
# Linux
sudo systemctl status docker

# Windows
Get-Service Docker
```

Verify networking:
```bash
docker network ls
docker run --rm alpine ping -c 4 google.com
```

### Docker Components Verification

Verify Docker Compose installation:
```bash
docker compose version
```

Test container runtime:
```bash
# Create a persistent volume
docker volume create test-volume

# Create and access a container with the volume
docker run -it --rm -v test-volume:/data alpine sh -c "echo 'It works!' > /data/test.txt"
docker run -it --rm -v test-volume:/data alpine cat /data/test.txt

# Clean up
docker volume rm test-volume
```

## Troubleshooting Guide

### Common Installation Issues

#### Permission Denied Errors

```bash
# Add user to docker group
sudo usermod -aG docker $USER

# Apply without logout
newgrp docker
```

#### Daemon Not Starting

```bash
# Check Docker daemon logs
sudo journalctl -u docker.service

# Check for configuration errors
sudo dockerd --validate

# Start daemon manually to see errors
sudo dockerd
```

#### Port Conflicts

```bash
# Check for port usage
sudo netstat -tulpn | grep LISTEN

# Change Docker daemon port
sudo tee /etc/docker/daemon.json <<EOF
{
  "hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"]
}
EOF
```

#### Registry Connectivity Issues

```bash
# Test registry connectivity
curl -v https://registry-1.docker.io/v2/

# Configure proxy if needed
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo tee /etc/systemd/system/docker.service.d/http-proxy.conf <<EOF
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:8080"
Environment="HTTPS_PROXY=http://proxy.example.com:8080"
Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```

### Log Analysis

#### Docker Daemon Logs

```bash
# Linux
sudo journalctl -u docker.service --since "1 hour ago"

# Windows
Get-EventLog -LogName Application -Source Docker -After (Get-Date).AddHours(-1)
```

#### Container Logs

```bash
# View logs for a container
docker logs <container_id>

# Follow logs in real-time
docker logs -f <container_id>
```

### Restart Procedures

```bash
# Linux
sudo systemctl restart docker

# Windows
Restart-Service Docker
```

## Security Configuration

### Rootless Mode

Run Docker daemon as a non-root user:

```bash
# Install dependencies
sudo apt-get install -y uidmap

# Install Docker in rootless mode
curl -fsSL https://get.docker.com/rootless | sh

# Add to shell configuration
echo "export PATH=/home/$USER/bin:$PATH" >> ~/.bashrc
echo "export DOCKER_HOST=unix:///run/user/$(id -u)/docker.sock" >> ~/.bashrc
source ~/.bashrc
```

### TLS Configuration

Secure Docker daemon with TLS:

1. Create certificates:
```bash
# Create a directory for certificates
mkdir -p ~/.docker/certs

# Generate CA key and certificate
openssl genrsa -out ~/.docker/certs/ca-key.pem 4096
openssl req -new -x509 -days 365 -key ~/.docker/certs/ca-key.pem -sha256 -out ~/.docker/certs/ca.pem

# Create server key and CSR
openssl genrsa -out ~/.docker/certs/server-key.pem 4096
openssl req -subj "/CN=docker-server" -sha256 -new -key ~/.docker/certs/server-key.pem -out ~/.docker/certs/server.csr

# Sign server certificate
openssl x509 -req -days 365 -sha256 -in ~/.docker/certs/server.csr -CA ~/.docker/certs/ca.pem -CAkey ~/.docker/certs/ca-key.pem -CAcreateserial -out ~/.docker/certs/server-cert.pem

# Create client key and CSR
openssl genrsa -out ~/.docker/certs/client-key.pem 4096
openssl req -subj "/CN=docker-client" -new -key ~/.docker/certs/client-key.pem -out ~/.docker/certs/client.csr

# Sign client certificate
openssl x509 -req -days 365 -sha256 -in ~/.docker/certs/client.csr -CA ~/.docker/certs/ca.pem -CAkey ~/.docker/certs/ca-key.pem -CAcreateserial -out ~/.docker/certs/client-cert.pem
```

2. Configure Docker daemon:
```json
{
  "tls": true,
  "tlscacert": "/etc/docker/certs/ca.pem",
  "tlscert": "/etc/docker/certs/server-cert.pem",
  "tlskey": "/etc/docker/certs/server-key.pem",
  "tlsverify": true
}
```

3. Use client with TLS:
```bash
docker --tlsverify \
  --tlscacert=~/.docker/certs/ca.pem \
  --tlscert=~/.docker/certs/client-cert.pem \
  --tlskey=~/.docker/certs/client-key.pem \
  -H tcp://docker-server:2376 \
  version
```

### Content Trust

Enable Docker Content Trust for image verification:

```bash
# Enable Docker Content Trust
export DOCKER_CONTENT_TRUST=1

# Pull signed images
docker pull docker/trusttest:latest
```

## Hands-On Exercises

### Exercise 1: Basic Docker Installation and Verification

1. Install Docker using your platform's appropriate method
2. Verify installation with `docker version` and `docker info`
3. Run a test container with `docker run hello-world`
4. Identify where Docker is storing data using `docker info`

### Exercise 2: Docker Daemon Configuration

1. Create a basic `daemon.json` file with:
   - Specified log driver (json-file)
   - Log rotation configuration
   - Storage driver specification

2. Restart Docker and verify configuration took effect

3. Test container logs with:
```bash
docker run --name logtest alpine sh -c "while true; do echo 'Test log message'; sleep 1; done"
# In another terminal
docker logs logtest
# Cleanup
docker stop logtest
docker rm logtest
```

### Exercise 3: Registry Configuration

1. Set up authentication for Docker Hub:
```bash
docker login
```

2. Create a `daemon.json` with registry mirror configuration (if available)

3. Test pulling an image:
```bash
docker pull nginx:latest
```

### Exercise 4: Troubleshooting Practice

1. Intentionally create an error in `daemon.json`
2. Attempt to restart Docker
3. Examine the error logs
4. Fix the configuration and restart Docker

### Exercise 5: Security Configuration

1. Configure Docker to run with limited capabilities
2. Add your user to the docker group
3. Verify you can run Docker commands without sudo
4. Test container isolation

## References

- [Official Docker Installation Documentation](https://docs.docker.com/engine/install/)
- [Docker Daemon Configuration](https://docs.docker.com/engine/reference/commandline/dockerd/)
- [Docker Security Best Practices](https://docs.docker.com/engine/security/)
- [Docker Storage Drivers](https://docs.docker.com/storage/storagedriver/select-storage-driver/)
- [Docker Registry Configuration](https://docs.docker.com/registry/configuration/)