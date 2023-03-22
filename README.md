## 我們組的 Raspberry 連線資訊
- 固定 IP : 172.16.13.38
- 主機名稱 : raspberryTeam1.local
- 帳號 : pi
- 密碼 : raspberry

## Google Meet
- https://meet.google.com/aco-ayih-hct

## 老師的 Github
- https://github.com/roberthsu2003/raspberry

## 上課影片
- 2023_03_04

	https://youtube.com/live/wfbY49CFn28
- 2023_03_11_早上

	https://youtube.com/live/pPcIeDhzeq8
- 2023_03_11_下午

	https://youtube.com/live/0c3dF0orcsk
- 2023_03_18_早上

	https://youtube.com/live/MozOJf65pAI
## 使用 VS Code 的 remote SSH 跟 Raspberry 連線

- 因為VNC只能一人遠端桌面控制，無法同時 5 人以上使用，所以我們使用 SSH 連線到 raspberry 操作。
- 需要知道 raspberry 的 IP 或主機名稱。
- 安裝 remote SSH，透過 SSH 跟 raspberry 連線，即可在 VS Code 直接編輯 raspberry 上的檔案。

## 將 raspberry 設定為固定 IP
- 我們希望上課可以用學校的內部網路，這樣每個人都可以自己連線到 raspberry，而學校的內部網路是固定IP，所以我們要把它設成固定IP。
- 修改之前，先查一下目前的IP是多少，用 ipconfig 或 ifconfig。
- 參考 Digital Guide IONOS 網站的說明

	https://www.ionos.com/digitalguide/server/configuration/provide-raspberry-pi-with-a-static-ip-address/
	


```

Assign a static private IP address to Raspberry Pi with DHCPCD

1 確認 DHCPCD 是否已啟動

sudo service dhcpcd status

2 如果沒有，啟動它

sudo service dhcpcd start
sudo systemctl enable dhcpcd

3 編輯 DHCPCD 的 config

sudo nano /etc/dhcpcd.conf

4 修改以下欄位, ip arddress 就改目前的 ip，router 就是 Getway，
domain name server 打 8.8.8.8，這是 google 的 domain name serer

interface eth0
static ip_address=192.168.0.4/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1

5 重新開機

sudo reboot

6 檢查有沒有成功，用 ping 檢查

ping raspberryTeam1.local

```
