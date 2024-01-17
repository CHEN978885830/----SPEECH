# 开启WSL

```linux
window功能中打开全部虚拟机相关功能
wsl --update 
wsl --set-default-version 2
wsl.exe --install Ubuntu-22.04
cd /etc/apt
sudo vim sources.list
复制Ubuntu清华源到list文件中
```

# 迁移
```linux
wsl --list
wsl --export Ubuntu-22.04 C:\ubuntu2204.tar
wsl --unregister Ubuntu-22.04
wsl --import Ubuntu-22.04 F:\wsl C:\ubuntu2204.tar --version 2
del C:\ubuntu2204.tar
ubuntu2204.exe config --default-user  # WindowsApps中查看<wsl>
```

# 安装图像界面
```linux
# 虚拟机方法
sudo apt clean all && sudo apt update
sudo apt-mark hold acpid acpi-support
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
sudo systemctl set-default multi-user.target # 命令行
sudo systemctl set-default graphical.target  # 图形用户界面
从图形界面切换回命令行：Ctrl+Alt+F7

#子系统方法
sudo apt-mark hold acpid acpi-support
sudo apt-get install ubuntu-deskto
sudo apt-get install gnome-tweak
git clone https://github.com/DamionGans/ubuntu-wsl2-systemd-script.git
cd ubuntu-wsl2-systemd-script/
bash ubuntu-wsl2-systemd-script.sh

进入PowerShell重启WSL
net stop LxssManager
net start LxssManager

安装xrdo并开启服务
sudo apt-get install xrdp
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
echo "gnome-session" > ~/.xsession
sudo systemctl restart xrdp
sudo service xrdp stop
sudo systemctl status xrdp

远程桌面进入3390端口
localhost:3390

# 中文
sudo apt install language-pack-zh-hans
sudo dpkg-reconfigure locales
选择 en_US.UTF-8 和 zh_CN.UTF-8
选择 zh_CN.UTF-8 为默认语言
```

# 安装CUDA
```linux
sudo apt-get install gcc -y
官网下载CUDA runfile版本 用完记得删 https://developer.nvidia.com/cuda-downloads
更新PATH 记得先检查路径
 > export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
 > export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

```

# python
```linux
python3 --version
sudo apt-get install python3-pip

pip install virtualenv
echo 'export PATH=/home/clq/.local/bin:$PATH' >>~/.bashrc
source ~/.bashrc
pip3 uninstall virtualenv
pip3 install virtualenv
```

# 创建虚拟环境
```linux
cd project_01
sudo chmod -R a+w /path/to/your/directory
virtualenv fish_speech_env
source venv/bin/activate
deactivate
rm -r venv
```