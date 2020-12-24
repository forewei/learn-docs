守护进程文件脚本位置  /lib/systemd/system/

刷新 systemctl daemon-reload
启动  systemctl start xxxx
开机启动 systemctl enable

脚本demo:
[unit]
Description=frps
After=network.target

[Service]
Type=simple
ExecStart=/home/forewei/frp/frps -c /home/forewei/frp/frps.ini

[Install]
WantedBy=multi-user.target
