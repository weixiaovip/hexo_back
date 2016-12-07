---
title: raspberry pi3安装chromium和flash插件
date: 2016-11-13 14:14:33
tags: [raspberry,pi3,chrome,chromium,flash]
---
### 说明
- chromium是chorme浏览器的开源版本
- 由于官方的把chromuim的apt-get包删了，所以没法直接通过apt-get的方式安装了，
- 49以上的版本需要依赖新的库，比较麻烦，所以我们安装48版本
### 安装chromium
~~~
wget http://ports.ubuntu.com/pool/universe/c/chromium-browser/chromium-browser-l10n_48.0.2564.82-0ubuntu0.15.04.1.1193_all.deb
wget http://ports.ubuntu.com/pool/universe/c/chromium-browser/chromium-browser_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
wget http://ports.ubuntu.com/pool/universe/c/chromium-browser/chromium-codecs-ffmpeg-extra_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
sudo dpkg -i chromium-codecs-ffmpeg-extra_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
sudo dpkg -i chromium-browser-l10n_48.0.2564.82-0ubuntu0.15.04.1.1193_all.deb chromium-browser_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
~~~

### 安装flash插件
- 安装以下步骤操作
~~~
wget http://odroidxu.leeharris.me.uk/repo/chromium-pepper-flash-12-12.0.0.77-1-armv7h.pkg.tar.xz
xz chromium-pepper-flash-12-12.0.0.77-1-armv7h.pkg.tar.xz -d
tar -xvf chromium-pepper-flash-12-12.0.0.77-1-armv7h.pkg.tar
cd./usr/lib/PepperFlash
chmod +x *
sudo cp * /usr/lib/chromium-browser/plugins
sudo nano /etc/chromium-browser/default
~~~
- 将打开文件中的最后一句改为：
CHROMIUM_FLAGS="--ppapi-flash-path=/usr/lib/chromium-browser/plugins/libpepflashplayer.so --ppapi-flash-version=12.0.0.77 -password-store=detect -user-data-dir"

- 然后打开chromium，在网址栏中输入chrome://plugins
如果看到插件栏中有“Flash(2Files)-Version=12.0.0.77”等则安装成功。

###### ps：这样看视频，cpu占用很高的，注意散热哦