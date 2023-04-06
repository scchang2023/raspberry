### 我們組的 raspberry 連線資訊
- 固定 IP : 172.16.13.38
- 主機名稱 : raspberryTeam1.local
- 帳號 : pi
- 密碼 : raspberry

### Google Meet
- https://meet.google.com/aco-ayih-hct

### 老師的 Github
- https://github.com/roberthsu2003/raspberry

### 上課影片
- 2023_03_04

	https://youtube.com/live/wfbY49CFn28
- 2023_03_11_早上

	https://youtube.com/live/pPcIeDhzeq8
- 2023_03_11_下午

	https://youtube.com/live/0c3dF0orcsk
- 2023_03_18_早上

	https://youtube.com/live/MozOJf65pAI

---
### 使用 VS Code 的 remote SSH 跟 raspberry 連線

- 因為VNC只能一人遠端桌面控制，無法同時 5 人以上使用，所以我們使用 SSH 連線到raspberry 操作。
- 需要知道 raspberry 的 IP 或主機名稱。
- 如果使用 command 方式登入，如下：

		ssh pi@192.168.1.72
- 安裝 remote SSH，透過 SSH 跟 raspberry 連線，即可在 VS Code 直接編輯 raspberry 上的檔案。
- 過程如下：

	[圖1](./images/remote_ssh_01.png)
	[圖2](./images/remote_ssh_02.png)
	[圖3](./images/remote_ssh_03.png)
	[圖4](./images/remote_ssh_04.png)
	[圖5](./images/remote_ssh_05.png)
	[圖6](./images/remote_ssh_06.png)
	[圖7](./images/remote_ssh_07.png)
	[圖8](./images/remote_ssh_08.png)
	[圖9](./images/remote_ssh_09.png)
	[圖10](./images/remote_ssh_10.png)

### 將 raspberry 設定為固定 IP
- 我們希望上課可以用學校的內部網路，這樣每個人都可以自己連線到 raspberry，而學校的內部網路是固定 IP，所以我們要把它設成固定 IP。
- 修改之前，先用 ipconfig 或是 ifconfig 查一下目前內網的 IP 是多少，記錄下來。
- 參考 Digital Guide IONOS 的說明

	https://www.ionos.com/digitalguide/server/configuration/provide-raspberry-pi-with-a-static-ip-address/
	



		
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

### GitHub 裡面有東西，要如何下載下來。
		1. Git 先 config，只需要做一次就行了

		git config --global user.name "roberthsu2003"
		git config --global user.email roberthsu2003@gmail.com

		2. 至GitHub將要clone的repositiry的url複制下來。

		gh repo clone https://github.com/roberthsu2003/raspberry.git
### Python 的 tkinter

- Lesson1.py

		import tkinter as tk
		class Window(tk.Tk):
	    	def __init__(self):
	        	super().__init__()
	        	self.title("Hello Tkinter")
	
	        	label = tk.Label(self, text="Hello World!")
	        	label.pack(fill=tk.BOTH, expand=1, padx=100, pady=50)
	
		def main():
	   		window = Window()
	    	window.mainloop()
	    
		if __name__ == "__main__":
	    	main()
	

	py 是由上而下執行的

	py 檔內有很多工具箱，tkinter 是其中一個，是專門用來做視窗的

	每支 py 檔要寫視窗，都要 import tkinter

	as tk 代表之後我們用 tk 代表 tkinter

	讀了 window，還沒執行

	讀了 main，知道你有一個 function 叫 main

	繼承 tk.Tk class Window(tk.Tk)

	method 一定要有 (self)

	super().__init__() 執行父類別的初始化function

	tkinter 的每個視窗元件有什麼屬性可以設定，要自己上網頁看文件


- Lesson2.py

		import tkinter as tk
		import RPi.GPIO as GPIO
	
		class Window(tk.Tk):
		    def __init__(self):
		        super().__init__()
		        self.title("按鈕")
		        open_button = tk.Button(self, text="開啟電燈", command=self.open, padx=30,pady=30)
		        open_button.pack(side=tk.LEFT, padx=20, pady=20)
		
		        close_button = tk.Button(self, text="關閉電燈", command=self.close, padx=30,pady=30)
		        close_button.pack(side=tk.LEFT, padx=20, pady=20)
		
		    def open(self):
		        print("開燈")
		        GPIO.output(25, GPIO.HIGH)
		
		    def close(self):
		        print("關燈")
		        GPIO.output(25, GPIO.LOW)
		
		
		def main():
		    GPIO.setmode(GPIO.BCM)
		    GPIO.setwarnings(False)
		    GPIO.setup(25,GPIO.OUT)
		    window = Window()
		    window.mainloop()
		    
		if __name__ == "__main__":
		    main()
	raspberry pi的configuration的 interface要全開
	
	GPIO有套件可以使用，不是內建，要另外下載
		
		pip install RPI.GPIO

	告訴程式要使用 GPIO PIN，而不是實體 PIN

		GPIO.setmode(GPIO.BCM)

	不要出現警告

		GPIO.setwarnings(False)

	告訴程式說，25 PIN 要輸出
		
		GPIO.setup(25,GPIO.OUT)

	實際控制【開】

		GPIO.output(25, GPIO.HIGH)

	實際控制【關】

		GPIO.output(25, GPIO.LOW)

### Linux 基本常用指令
		pwd			檢查現有目錄
		~			使用者根目錄
		/			OS根目錄
		cd			進入指定路徑
		ls			查看目前目錄底下的所有資料夾及檔案
		ls -a		顯示隱藏檔案跟資料夾
		ls -l		顯示細節
		ls -al		顯示隱藏檔案 + 細節
		.			現有目錄
		..			上一層目錄
		./home/pi	上一層目錄
		../home/pi	上一層目錄
		/home/pi	根目錄的絕對路徑
		~home/pi	個人目錄的絕對路徑
		mkdir		建立目錄（後面要加目錄名稱）
		clear		清除 Terminal 畫面中的內容

		※ 路徑大小寫有差
		
		touch 		建立檔案（後面要加路徑跟檔案名稱）
		touch 		~/Documents/a1/a1a.txt
		nano		編輯純文字（後面要加路徑跟檔案名稱）
		^			代表 Ctrl
		^x			退出（會提示要不要存檔）
		cat			檢查文字檔內容（後面要加路徑跟檔案名稱）
		cat 	會將檔案內容輸出到 Terminal 視窗當中
		nano 	後面的檔名如果不存在就會直接建立檔案
		cp		複製 (要加 來源 + 目標)
		cp ~/Documents/a1/a1a.txt ~/Documents/a2/a2b.txt
		cp 可複製目錄
		mv	移動 or 改名　(要加 來源 + 目標)
		mv ~/Documents/a1/a1a.txt ~/Documents/a2/a2b.txt
		rm	移除
		-r	recursive：跟目錄有關都要用這個引數
		-f	force:強制執行
### Git 是做什麼用的？
		git 可以針對一個資料夾做管理

		要先輸入 email、username

		git --version
		git config --global user.name "roberthsu"
		git config --global user.email roberthsu2003@gmail.com
		git config -l
		git config --list

		git 是對資料夾做版本管理的工具，所以使用前要先建資料夾，讓它管理

		資料夾建議建立在 Documents

		git init	進入資料夾後要輸入這個【初始化】指令，資料夾就會被納入 git 管理

		ls -al	在 git 管理的資料夾中要檢查有沒有成功管理，就看有沒有出現 .git 資料夾就好

		rm		可以取消 git 管理
### GitHub
		後面都會用 github 上傳打完的程式
		要先安裝 github 的 command line
		搜尋 github cli
		找到 our Debian and RPM repositories

		Official sources
		Debian, Ubuntu Linux, Raspberry Pi OS (apt)
		Install:

		type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
		curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
		&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
		&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
		&& sudo apt update \
		&& sudo apt install gh -y

		gh --version 看版本，就知道有沒有安裝成功了
		


