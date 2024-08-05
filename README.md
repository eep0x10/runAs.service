# Run anything in background as a service (Linux)

(Example: Run Responder (https://github.com/camopants/igandx-Responder) as a Service to collect hashes)

## Create service file:

`sudo nano /etc/systemd/system/responder.service`

## Content:
```
[Unit]
Description=Responder Service
After=network.target

[Service]
ExecStart=/usr/bin/python3 /usr/share/responder/Responder.py -I wlan0 -Q
WorkingDirectory=/usr/share/responder
StandardOutput=syslog
StandardError=syslog
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

## 

`sudo systemctl enable responder`

`sudo service responder start`

* If change enything in file, run: `sudo systemctl daemon-reload`
* Change network interface wlan0 to target
