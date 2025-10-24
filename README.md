# 🧠 Gensyn Node Setup Guide

## 🌐 About Gensyn

**Gensyn** is a decentralized compute network designed to train AI models efficiently by leveraging distributed nodes.  
The **Gensyn Testnet** is currently live, training reasoning models on the *reasoning-gym swarm datasets*.  
By running a node, you contribute your compute resources to help power decentralized AI training.

---

## ⚙️ Hardware Requirements

The swarm currently supports the following models:

- `Gensyn/Qwen2.5-0.5B-Instruct`  
- `Qwen/Qwen3-0.6B`  
- `nvidia/AceInstruct-1.5B`  
- `dnotitia/Smoothie-Qwen3-1.7B`  
- `Gensyn/Qwen2.5-1.5B-Instruct`

### Recommended Hardware

| Type | Minimum | Recommended |
|------|----------|-------------|
| **CPU-only** | arm64 or x86 CPU, 32GB RAM | 64GB+ RAM if multitasking |
| **GPU** | ≥12.4 CUDA driver | RTX 3090 / 4090 / 5090 / A100 / H100 |
| **vRAM** | ≥12GB supported | ≥24GB preferred |

> 💡 Users with lower-end hardware should use smaller models (e.g., Qwen2.5-0.5B or Qwen3-0.6B).  
> More powerful hardware can handle larger models efficiently.



## 🧩 1. Install Dependencies

> ⚠️ **Quickpod users:** Remove `sudo` from all commands.

### Step 1 — Update System Packages
```bash
sudo apt update && sudo apt upgrade -y

### Step 2 — Install Utilities and Build Tools
sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y

### Step 3 — Install Python
sudo apt install python3 python3-pip python3-venv python3-dev -y

### Step 4 — Install Node.js and Yarn
sudo apt update
curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
sudo apt-get install -y nodejs
node -v
npm install -g yarn
yarn -v

### Step 5 — (Optional) Install Yarn via Script
curl -o- -L https://yarnpkg.com/install.sh | bash
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
source ~/.bashrc
## 🧬 2. Clone the Repository
git clone https://github.com/gensyn-ai/rl-swarm/

## 🚀 3. Run the Swarm Node

🧾 If you're an existing user, ensure your swarm.pem file is in the rl-swarm directory before starting.
If lost, follow Gensyn’s recovery guide to restore it.

### Step 1 — Open a Screen Session
screen -S swarm

### Step 2 — Enter the Directory
cd rl-swarm

### Step 3 — Create and Activate a Python Virtual Environment
python3 -m venv .venv
source .venv/bin/activate
# if above fails:
. .venv/bin/activate

### Step 4 — Run the Swarm
./run_rl_swarm.sh


Once you see the initialization image, detach the screen:

<img width="623" height="169" alt="workspaces can" src="https://github.com/user-attachments/assets/82857dd6-008a-4c81-9485-820dc2fe851b" />

Ctrl + A + D



## 🌍 4. Set Up Ngrok

Ngrok is used to tunnel your local node for external communication.

### Step 1 — Install Ngrok
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-stable-linux-amd64.zip
unzip ngrok-stable-linux-amd64.zip
mkdir -p ~/.local/bin
mv ngrok ~/.local/bin/
chmod +x ~/.local/bin/ngrok
echo 'export PATH=$PATH:$HOME/.local/bin' >> ~/.profile
. ~/.profile

### Step 2 — Add Your Auth Token

Go to Ngrok Dashboard

Sign up and copy your AuthToken
<img width="819" height="223" alt="Your Authtoken" src="https://github.com/user-attachments/assets/68548475-b73a-4c09-beb4-ee268149a4df" />

Then run:

screen -S NGROK
ngrok config add-authtoken YOUR_AUTHTOKEN
ngrok http 3000


A new link will appear — open it in your browser, submit your email, and log in.
<img width="1479" height="723" alt="Screenshot 2025-10-22 at 6 18 32 PM" src="https://github.com/user-attachments/assets/cffebcba-3328-49c6-929f-b60410df38a4" />

## 🧠 5. Return to the Swarm Screen

Reattach your swarm screen:

screen -r swarm


Then follow the prompts:
<img width="917" height="146" alt="Screenshot 2025-10-24 at 8 16 47 AM" src="https://github.com/user-attachments/assets/b58d2452-3bf0-4a2d-bf93-b623a46f5a89" />

First: N

Second: Press Enter

Third: Y (judge)

🎉 Your Gensyn node is now live!

## 🧾 6. Backup Your Node Credentials

It’s critical to back up your node credentials for recovery.

### Step 1 — Save swarm.pem

Ensure your swarm.pem file is located here:

/root/rl-swarm/

### Step 2 — Backup User Data

Run:

cd
cat rl-swarm/modal-login/temp-data/userData.json
cat rl-swarm/modal-login/temp-data/userApiKey.json


Copy and securely store these JSON outputs — they contain your node’s API credentials and identity.
