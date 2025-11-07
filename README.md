![source](https://github.com/zhizhi1348/Gnesyn-CodeAssist/blob/main/Screenshot%202025-11-07%20155355.png)
# CodeAssist Setup Guide

This guide will help you install dependencies, download the code, and run CodeAssist.

Program is currently avaliable for Linux & MacOS. You can run it on local system or VPS.

### System Requirements
- 12 GB RAM minimum (32 GB recommended)
- Stable internet connection
- At least 10 GB of available storage (for overhead)
- Modern multi-core CPU (Intel, AMD, or Apple Silicon)

## 1. Install Dependencies

Update and upgrade your system:

```bash
sudo apt update && sudo apt upgrade -y
```
Install essential packages:
```bash
sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
sudo apt install python3 python3-pip python3-venv python3-dev -y
sudo apt update
```
Install Node.js and Yarn:
```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
sudo apt install -y nodejs
node -v

npm install -g yarn
yarn -v

curl -o- -L https://yarnpkg.com/install.sh | bash
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
source ~/.bashrc
```
Install Astral UV:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env
```
Install Docker:
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world
```

## 2. Download the Code
Clone the repository:
```bash
git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist
```
Run the application:
```bash
# This command spins up a local Docker environment and launches the web server at localhost:3000 which automatically opens in your device's default browser.
uv run run.py
```
Authentication:
1. Visit your [Hugging Face](https://huggingface.co/) profile > Settings > Access Tokens.
2. Generate a New Token with 'Write' access.
3. Copy the token string.
4. When starting CodeAssist, the application will prompt you for the token. Paste it into the terminal or web interface.

---
## Running on a VPS
If you are running assitant on a VPS, create an SSH tunnel from your local PC:
```bash
ssh -N -L 3000:localhost:3000 -L 8000:localhost:8000 -L 8008:localhost:8008 root@<your-vps-ip>
```
> After resolving any issues, go back to the terminal, press Ctrl+C, and wait for it to finish pushing the data.
