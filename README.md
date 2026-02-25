#!/bin/bash

# 1. تحديث النظام وتثبيت الأدوات الأساسية
echo "--- تحديث المستودعات وتثبيت الأدوات الأساسية ---"
sudo apt update && sudo apt install -y zsh git curl fzf vlc-bin neofetch htop bat exa

# 2. تثبيت Oh My Zsh
echo "--- تثبيت Oh My Zsh ---"
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# 3. تثبيت الإضافات (التكملة التلقائية وتلوين الأوامر)
echo "--- إضافة Plugins الذكاء الاصطناعي للتيرمينال ---"
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# 4. تثبيت ثيم Powerlevel10k (الأكثر فخامة)
echo "--- تثبيت ثيم Powerlevel10k ---"
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# 5. ضبط الإعدادات في ملف .zshrc
echo "--- ضبط إعدادات الواجهة ---"
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc
sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting fzf)/' ~/.zshrc

# إضافة Neofetch عند الدخول و Aliases للأدوات الجديدة
echo "neofetch" >> ~/.zshrc
echo "alias ls='exa -l --icons'" >> ~/.zshrc
echo "alias cat='batcat --paging=never'" >> ~/.zshrc

# 6. تغيير التيرمينال الافتراضي إلى Zsh
sudo chsh -s $(which zsh) $USER

echo "--- تم التثبيت بنجاح! يرجى تسجيل الخروج والعودة (Logout/Login) لتفعيل التغييرات ---"
