# v2raya-openwrt

适用于 OpenWrt 用户的 v2rayA opkg 软件源。

[English](README.md)

## 安装方法

1. 导入 v2rayA 签名文件

   > 请确认软件包 `wget-ssl` 已经正确地安装在您的设备上

   ```sh
   wget https://osdn.net/projects/v2raya/storage/openwrt/v2raya.pub -O /etc/opkg/keys/94cc2a834fb0aa03
   ```

2. 添加 v2rayA 软件源

   ```sh
   echo "src/gz v2raya https://osdn.net/projects/v2raya/storage/openwrt/$(. /etc/openwrt_release && echo "$DISTRIB_ARCH")" | tee -a "/etc/opkg/customfeeds.conf"

   # 日本镜像
   # echo "src/gz v2raya https://ftp.jaist.ac.jp/pub/sourceforge.jp/storage/g/v/v2/v2raya/openwrt/$(. /etc/openwrt_release && echo "$DISTRIB_ARCH")" | tee -a "/etc/opkg/customfeeds.conf"
   # 美国镜像
   # echo "src/gz v2raya https://mirrors.gigenet.com/OSDN/storage/g/v/v2/v2raya/openwrt/$(. /etc/openwrt_release && echo "$DISTRIB_ARCH")" | tee -a "/etc/opkg/customfeeds.conf"
   ```

3. 更新软件源

   ```sh
   opkg update
   ```

4. 安装 v2rayA 及其依赖

   ```sh
   # 使用 Xray 内核：
   opkg install v2raya

   # 使用 v2ray 内核：
   opkg install v2raya2

   # 注：不可同时安装 v2raya 和 v2raya2。
   #     由于 v2ray 内核的透明代理支持欠佳，目前更推荐使用 Xray 内核。

   # 可选
   # opkg install v2fly-geoip v2fly-geosite
   ```

## 使用方法

- 方法一：通过 LuCI 界面配置（仅适用于 __OpenWrt 21.02 或更高版本__）

   1. 安装 LuCI app
      ```sh
      opkg install luci-app-v2raya luci-i18n-v2raya-zh-cn
      ```

   2. 访问 `http://<your_router_ip>/cgi-bin/luci/admin/services/v2raya` 并完成配置。

- 方法二：通过命令行配置

   1. 配置 v2rayA

      ```sh
      # 详细配置请参见 /etc/config/v2raya
      uci set v2raya.config.enabled='1'
      uci commit v2raya
      ```

   2. 启动 v2rayA

      ```sh
      /etc/init.d/v2raya start
      ```

   3. 访问 v2rayA webUI 面板并完成设置

      `http://<your_router_ip>:2017`
