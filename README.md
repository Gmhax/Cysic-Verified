# Cysic-Verifier

Cysic is a ZK-hardware acceleration project focused on developing advanced ASIC chips to expedite the generation of ZK proofs for zk-based systems. Leveraging its expertise in ASIC design and GPU engineering, Cysic aims to address this hurdle by offering enterprise-grade ZK compute-as-a-service to an array of ZK projects.

- Before installation, don’t forget to reserve 0.5 CYS.
<img width="1356" height="572" alt="image" src="https://github.com/user-attachments/assets/a8c2ea2b-b16a-45b2-a531-815beb2cc6d8" />


# Installation 
## Step 1 — Redownload & Setup
```
curl -L https://github.com/cysic-labs/cysic-phase3/releases/download/v1.0.0/setup_linux.sh > ~/setup_linux.sh
bash ~/setup_linux.sh 0x-YOUR-REWARD-ADDRESS
```
- Replace 0x-YOUR-REWARD-ADDRESS with your own reward address.

Step 2 — Test Manually (before systemd)
```
cd /root/cysic-verifier
bash start.sh
```
- If you see “start sync data from server it means the program is alive and running.
- Press CTRL+C to stop it before continuing.

Step 3 — Create a Systemd Service
Paste:
```
sudo tee /etc/systemd/system/cysic-verifier.service > /dev/null <<EOF
[Unit]
Description=Cysic Verifier
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/cysic-verifier
ExecStart=/bin/bash /root/cysic-verifier/start.sh
Restart=always
RestartSec=10
TimeoutStartSec=120
LimitNOFILE=65536
Environment=HOME=/root
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
EOF
```

Step 4 — Enable & Start the Service
```
sudo systemctl daemon-reload
sudo systemctl enable --now cysic-verifier.service
```

Step 5 — Check Logs
```
systemctl status -l cysic-verifier
journalctl -u cysic-verifier -f
```

<img width="1616" height="784" alt="image" src="https://github.com/user-attachments/assets/6ade84b6-c0db-4666-9df3-22244d2e8859" />


# Done ✅



