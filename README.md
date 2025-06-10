# 🚀 Gensyn Node Setup Guide  
By [@eliteairdroops](https://x.com/eliteairdroops)

Easily set up & run your Gensyn RL-Swarm node on **Linux/WSL** or **Mac**  
**All commands are ready to copy-paste!**

---

## 🔧 1. Prerequisites

### 🐧 Linux/WSL
```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof
```

### 🍏 For Mac
```bash
brew install python
```

---

## 🐍 2. Check Python
```bash
python3 --version
```

---

## 🟩 3. Install Node.js

### Linux/WSL:
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt update && sudo apt install -y nodejs
```

### Mac:
```bash
brew install node
corepack enable
npm install -g yarn
```

---

## 🧶 4. Install Yarn

### Linux/WSL:
```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list > /dev/null
sudo apt update && sudo apt install -y yarn
```

### Mac:
```bash
npm install -g yarn
```

---

## 📦 5. Install Cloudflared
```bash
yes | sudo apt install ufw -y && sudo ufw allow 22 && sudo ufw allow 3000/tcp && yes | sudo ufw enable && wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb && sudo dpkg -i cloudflared-linux-amd64.deb
```

---

## 📁 6. Clone Gensyn RL-Swarm
```bash
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
```

---

## 💻 7. Create Screen (VPS only)
```bash
screen -S gensyn
```

---

## 🧪 8. Virtual Environment
```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

## 🚀 9. Run Node
```bash
./run_rl_swarm.sh
```

### Answer Prompts:
- Join Testnet? → `Y`  
- Swarm A or B? → `a`  
- Parameters? → `7`

---

## 🌐 10. Login

### 🖥️ Local PC:
Login at [http://localhost:3000](http://localhost:3000)

### VPS:
```bash
cloudflared tunnel --url http://localhost:3000
```

Open the link it gives, login, then return to terminal.

---

## 🆔 11. Save Peer ID & Username  
It shows after login — **save them** somewhere safe! ( eg . 🐱 Hello 🐈 [apple bmw cat] 🦮 [QmADf8JRCLEfLx4ubBomzYJ......]! )

---

## 🖥️ 12. VPS: Keep Node Running
```bash
Ctrl + A + D
```

To return:
```bash
screen -r gensyn
```

---

## 🛡️ 13. Backup Credentials
```bash
[ -f backup.sh ] && rm backup.sh; curl -sSL -O https://raw.githubusercontent.com/zunxbt/gensyn-testnet/main/backup.sh && chmod +x backup.sh && ./backup.sh
```

Open the 3 links it gives and save the info.

---

## 🔄 14. Restart Node (Next Day)
```bash
cd rl-swarm
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```


## 🆘 Troubleshooting & Fixes

---

### ❌ Reset Gensyn Node
```bash
cd ~
sudo rm -rf ~/rl-swarm
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

---

### 🛠️ Fix Minor Errors
```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/eliteairdroops/Gensyn_Guide_with_all_solutions/main/solutions_file/fixall.sh)"
```

---

### 🔧 Fix Bootstrap/DHT Error
```bash
perl -i -pe '
  if (/hivemind\.DHT\(start=True, startup_timeout=30/) {
    @matches = /ensure_bootstrap_success=[^,)\s]+/g;
    if (@matches > 1) {
      s/(,?\s*ensure_bootstrap_success=[^,)\s]+)+//g;
      s/(hivemind\.DHT\(start=True, startup_timeout=30, )/$1$matches[0], /;
    } elsif (@matches == 0) {
      s/(hivemind\.DHT\(start=True, startup_timeout=30, )/$1ensure_bootstrap_success=False, /;
    }
  }
' ~/rl-swarm/hivemind_exp/runner/grpo_runner.py
```

---

### 🧩 Identity Conflict
```bash
pkill -f swarm.pem
```

---

### ⬇️ Downgrade RL-Swarm (if new version causes problems)
```bash
cd ~
bash -c "$(curl -fsSL https://raw.githubusercontent.com/eliteairdroops/Gensyn_Guide_with_all_solutions/main/solutions_file/Downgrade.sh)"
cd rl-swarm
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

---

## ⚠️ Important Note  
If your EOA shows as `0x0000000000000000000000000000000000000000`,  
your rewards won’t count!  
👉 Delete `swarm.pem` and restart with a new email.

---

## 🤝 Support

- 🧑‍🏫 **Need help? DM us at** [@eliteairdroops](https://x.com/eliteairdroops)
