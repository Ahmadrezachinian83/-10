#!/bin/bash

# به‌روزرسانی و ارتقاء سیستم
echo "Updating system..."
sudo apt update && sudo apt upgrade -y

# نصب برنامه‌های ضروری
echo "Installing essential applications..."
sudo apt install -y 
    vlc                # پخش‌کننده رسانه
    gimp               # ویرایشگر تصویر
    git                # سیستم کنترل نسخه
    htop               # مانیتورینگ سیستم
    curl               # ابزار خط فرمان برای انتقال داده
    neofetch          # نمایش اطلاعات سیستم
    build-essential    # ابزارهای توسعه
    python3-pip       # مدیریت بسته‌های پایتون

# نصب مرورگر Google Chrome
echo "Installing Google Chrome..."
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install -y ./google-chrome-stable_current_amd64.deb
rm google-chrome-stable_current_amd64.deb

# نصب Visual Studio Code
echo "Installing Visual Studio Code..."
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /usr/share/keyrings/microsoft.gpg > /dev/null
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
sudo apt update
sudo apt install -y code

# نصب Zsh و Oh My Zsh
echo "Installing Zsh and Oh My Zsh..."
sudo apt install -y zsh
chsh -s $(which zsh)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# نصب فونت‌های اضافی (مثلاً Nerd Fonts)
echo "Installing Nerd Fonts..."
mkdir -p ~/.local/share/fonts
wget -O ~/.local/share/fonts/FiraCode.zip https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FiraCode.zip
unzip ~/.local/share/fonts/FiraCode.zip -d ~/.local/share/fonts/
fc-cache -fv

# نصب Docker (اختیاری)
echo "Installing Docker..."
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce

# افزودن کاربر به گروه Docker
sudo usermod -aG docker $USER

# نصب Flatpak و Flathub (اختیاری)
echo "Installing Flatpak..."
sudo apt install -y flatpak
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# پایان نصب
echo "Installation completed successfully!"
echo "Please log out and log back in to apply changes."
