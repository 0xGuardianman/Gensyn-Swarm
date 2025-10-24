# 🧠 Gensyn Node Setup Guide

<img width="302" height="183" alt="Screenshot 2025-10-24 at 8 51 21 AM" src="https://github.com/user-attachments/assets/80001869-8366-4413-979a-f949d95f38ce" />

Welcome to the **Gensyn Node Installation Guide** — this document will help you set up and run your Gensyn Testnet node step-by-step.  
Gensyn is a **decentralized compute network** designed to train AI models collaboratively by distributing workloads across nodes like yours.  

---

## ⚙️ Hardware Requirements

Currently, the Gensyn Testnet swarm supports these models:

- `Gensyn/Qwen2.5-0.5B-Instruct`
- `Qwen/Qwen3-0.6B`
- `nvidia/AceInstruct-1.5B`
- `dnotitia/Smoothie-Qwen3-1.7B`
- `Gensyn/Qwen2.5-1.5B-Instruct`

### 💡 Choosing a Model
- **Lower-end hardware:** choose smaller models like `Qwen2.5-0.5B` or `Qwen3-0.6B`
- **High-end hardware:** can handle larger models like `Qwen2.5-1.5B-Instruct`

### 🧰 Minimum Requirements
| Type | Requirement |
|------|--------------|
| **CPU-only** | arm64 or x86 CPU with at least **32GB RAM** |
| **GPU** | RTX 3090 / 4090 / 5090 / A100 / H100 |
| **vRAM** | Recommended ≥ 24GB (supports <24GB too) |
| **CUDA** | Version ≥ 12.4 |

---

# 🧩 Step 1 — Install Dependencies

> ⚠️ **Quickpod users:** Remove `sudo` from all commands.

---

## 🪄 Step 1.1 — Update System Packages

Use this command:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 🔧 Step 1.2 — Install Utilities and Build Tools

Use this command:

```bash
sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```

---

## 🐍 Step 1.3 — Install Python

Use this command:

```bash
sudo apt install python3 python3-pip python3-venv python3-dev -y
```

---

## 🧱 Step 1.4 — Install Node.js and Yarn

Run these commands one by one:

```bash
sudo apt update
curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
sudo apt-get install -y nodejs
node -v
npm install -g yarn
yarn -v
```

---

## 🎀 Step 1.5 — (Optional) Install Yarn via Script

If you want to install Yarn using the official script:

```bash
curl -o- -L https://yarnpkg.com/install.sh | bash
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
source ~/.bashrc
```

---

# 📂 Step 2 — Clone the Repository

Clone the Gensyn swarm repository:

```bash
git clone https://github.com/gensyn-ai/rl-swarm/
```

---

# 🚀 Step 3 — Run the Swarm Node

> 🧾 If you're an existing user, make sure your `swarm.pem` file is in the `rl-swarm` directory.  
> If it’s missing, follow the Gensyn recovery guide to restore it.

---

## 🖥️ Step 3.1 — Start a Screen Session

This lets your node keep running even if you close the terminal:

```bash
screen -S swarm
```

---

## 📁 Step 3.2 — Navigate to the Directory

Move into the project folder:

```bash
cd rl-swarm
```

---

## 🧬 Step 3.3 — Create and Activate a Python Environment

Set up a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
# If the above doesn't work, try:
. .venv/bin/activate
```

---

## ⚙️ Step 3.4 — Run the Swarm

Start the swarm node:

```bash
./run_rl_swarm.sh
```

When you see the swarm initialization screen, **detach** it by pressing:
<img width="623" height="169" alt="workspaces can" src="https://github.com/user-attachments/assets/649cf755-c53d-4235-81a4-4c262e0193f0" />

```
Ctrl + A + D
```

---

# 🌐 Step 4 — Set Up Ngrok

Ngrok allows your node to communicate externally.

---

## 🔽 Step 4.1 — Install Ngrok

Run these commands:

```bash
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-stable-linux-amd64.zip
unzip ngrok-stable-linux-amd64.zip
mkdir -p ~/.local/bin
mv ngrok ~/.local/bin/
chmod +x ~/.local/bin/ngrok
echo 'export PATH=$PATH:$HOME/.local/bin' >> ~/.profile
. ~/.profile
```

---

## 🔑 Step 4.2 — Add Your Auth Token

1. Visit [Ngrok Dashboard](https://dashboard.ngrok.com/get-started/your-authtoken)  
2. Sign up and copy your **AuthToken**  
<img width="819" height="223" alt="Your Authtoken" src="https://github.com/user-attachments/assets/bdc28e4b-28c9-498f-a878-8a3feecf2898" />

3. Run the following commands:

```bash
screen -S NGROK
ngrok config add-authtoken YOUR_AUTHTOKEN
ngrok http 3000
```

A link will appear — open it in your browser, submit your email, and log in.
![Uploading Screenshot 2025-10-22 at 6.18.32 PM.png…]()

---

# 🔄 Step 5 — Reconnect and Complete Setup

Reattach to your swarm screen:

```bash
screen -r swarm
```

When prompted, answer the following:
<img width="917" height="146" alt="Screenshot 2025-10-24 at 8 16 47 AM" src="https://github.com/user-attachments/assets/4983255c-16f5-4b16-a3ec-89fd3b447e3d" />


- First: `N`
- Second: *(Press Enter)*
- Third: `Y` (judge)

🎉 **Your Gensyn node is now live and operational!**

---

# 💾 Step 6 — Backup Important Files

### 🧠 Save the following file:
```
/root/rl-swarm/swarm.pem
```

### 🔐 Also back up these credential files:
```bash
cat ~/rl-swarm/modal-login/temp-data/userData.json
cat ~/rl-swarm/modal-login/temp-data/userApiKey.json
```

Store these files securely — they are required to recover your node.


---

**Contribute to decentralized AI — power the future with your compute! ⚡**
