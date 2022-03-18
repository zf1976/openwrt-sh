<p align="center">
  <strong>README</strong> | <a href="https://github.com/zf1976/packages/blob/main/README-R4S.md">R4S</a> | <a href="https://github.com/zf1976/packages/blob/main/README-360v6.md">360v6</a>
</p>

# Openwrt packages
所有插件都为网上收集的开源仓库插件
- R4S适用于固件项目：https://github.com/QiuSimons/YAOF
- 360V6适用于lean固件 v22.3.8


### 安装基本工具包
> 含：`vim`、`cfdisk`、`rsync`、`git`、`git-http`、`usbutils`、`pciutils`、`lsof`、`coreutils-nohup`
```shell
wget https://raw.githubusercontent.com/zf1976/packages/main/base.sh && sh base.sh && rm base.sh
```

### 安装开发工具包
> 含：`golang`、 `erlang`、`rust`

```shell
wget https://raw.githubusercontent.com/zf1976/packages/main/dev.sh && sh dev.sh && rm dev.sh
```

### 安装zsh、oh-my-zsh、插件
- 安装zsh
```shell
wget https://raw.githubusercontent.com/zf1976/packages/main/zsh.sh && sh zsh.sh && rm zsh.sh
```
- 安装oh-my-zsh、zsh插件
```shell
# oh-my-zsh
wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh && sh install.sh && rm install.sh
# plugins
wget https://raw.githubusercontent.com/zf1976/packages/main/zsh-plugins.sh && sh zsh-plugins.sh && rm zsh-plugins.sh
```

> 提示类似符号”)“等报错，请删除`plugins(git)`行 

## 工具脚本
- acme
```shell
curl https://get.acme.sh | sh
```

-DDNSTO
```shel
sh -c "$(curl -sSL http://fw.koolcenter.com/binary/ddnsto/openwrt/install_ddnsto.sh)"
```

## 小提示
> 如果你路由空间不算大，建议把包安装在外置磁盘空间
```shell
echo "dest usb /mnt/opkg" >> /etc/opkg.conf
# 重启shell会重置，把下面这条放在`/etc/profile` 就可以保存了
# 注意`$PATH`是原来的变量值
export PATH=$PATH:/mnt/opkg/usr/bin:/mnt/opkg/usr/sbin

# 安装package时指定安装目录
opkg install git -d usb
```
> 直接扩容根分区`/`，根目录准备，确保使用以下命令来复制根文件系统
```shell
mkdir -p /tmp/introot
mkdir -p /tmp/extroot
mount --bind / /tmp/introot
mount /dev/sda1 /tmp/extroot
tar -C /tmp/introot -cvf - . | tar -C /tmp/extroot -xf -
umount /tmp/introot
umount /tmp/extroot
```
其中`/dev/sda1` 是挂载分区，注意格式化为ext4，执行完上面操作好，去挂载点保存好分区挂载配置后重启
