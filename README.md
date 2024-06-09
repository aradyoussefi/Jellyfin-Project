# Jellyfin Media Server Setup with Docker on Linux Mint

## Introduction

I have set up a Jellyfin media server using Docker on my Linux Mint machine. Jellyfin is an open-source media server that allows me to organize, manage, and stream my media files effortlessly.

## Prerequisites

- A Linux Mint-based machine
- An external HDD with media files (e.g., movies)
- Basic knowledge of Docker and Linux command line

## Installation Steps

### 1. Install Docker

First, I updated the package list and installed prerequisites:
```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
```

Next, I added Docker’s official GPG key:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Then, I added Docker's APT repository:
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

After updating the package list again, I installed Docker:
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Finally, I started and enabled Docker:
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. Run Jellyfin Container

I created directories for Jellyfin configuration and cache:
```bash
mkdir -p ~/jellyfin/config ~/jellyfin/cache
```

I ensured my external HDD was properly mounted. I checked with:
```bash
df -h
```

Then, I ran the Jellyfin container:
```bash
docker run -d \
  --name jellyfin \
  --user $(id -u):$(id -g) \
  --volume ~/jellyfin/config:/config \
  --volume ~/jellyfin/cache:/cache \
  --volume "/path to media" \
  --network host \
  --restart unless-stopped \
  jellyfin/jellyfin
```

### 3. Adding Media Libraries

I accessed Jellyfin via `http://localhost:8096`.

To add my media library:
1. I navigated to **Dashboard** > **Libraries**.
2. I clicked **Add Library**.
3. I chose the content type (e.g., Movies).
4. I set the path to `/media/movies`.
5. I saved the library settings.

### 4. Remote Access and Management

To connect to my server from any device, such as my laptop, and access or modify anything, I use:
- **NoMachine**: For remote desktop access to my Linux Mint machine.
- **NordVPN's Meshnet**: To securely connect to my server from anywhere.

## Verifying Setup

To verify Jellyfin is running and configured correctly:
```bash
docker ps
```

I also checked Jellyfin logs:
```bash
docker logs jellyfin
```

## Conclusion

I have successfully set up a fully functional Jellyfin media server on my Linux Mint machine using Docker. This setup allows me to enjoy a seamless media streaming experience and manage my server remotely with ease.



<img width="1920" alt="Screenshot 2024-05-14 at 18 14 47" src="https://github.com/aradyoussefi/Jellyfin-Server-Project/assets/66588311/705978d6-25bb-4351-8491-a28200fd397d">
