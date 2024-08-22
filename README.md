# Run anything in background as a service

(Example: Run Responder (https://github.com/camopants/igandx-Responder) as a service to collect hashes)

`!!!CHECK RESPONDER INTERFACE!!!`

## Create service file:

`sudo nano /etc/systemd/system/responder.service`

## Content:
```
[Unit]
Description=Responder Service
After=network.target

[Service]
ExecStart=/usr/bin/python3 /usr/share/responder/Responder.py -I eth0 -wFdQ
WorkingDirectory=/usr/share/responder
StandardOutput=syslog
StandardError=syslog
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

## Start Service

`sudo systemctl enable responder`

`sudo service responder start`

* If change enything in file, run: `sudo systemctl daemon-reload`
* Change network interface wlan0 to target
