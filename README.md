OpenWrt's ChinaDNS-C Makefile
===

 > 编译时默认从 [ChinaDNS-C][1] 下载最新源码

编译说明
---

 - OpenWrt 平台的编译, [预编译 IPK 下载][2]

 > ```
 > # 获取 Makefile
 > git clone https://github.com/aa65535/openwrt-chinadns.git package/network/chinadns
 > # 选择要编译的包 Network -> ChinaDNS-C
 > make menuconfig
 > # 开始编译 ChinaDNS-C
 > rm -f dl/master.zip && make package/network/chinadns/compile V=99
 > # 若上面语句编译出错 需要先使用下面语句编译出 Toolchain
 > make V=99
 > ```

配置说明
---

 - 默认 DNS 服务器为 `127.0.0.1` 端口 `53`

 - 可搭配路由器自带的 Dnsmasq 使用 借助其 DNS 缓存提升查询速度

 > 将 `/etc/init.d/chinadns` 内容修改为 [chinadns.masq][3]
 >
 > Dnsmasq 配置`(/etc/dnsmasq.conf)`如下
 > ```
 > no-resolv
 > server=127.0.0.1#5353
 > ```

 - [chnroute][4] 可以使用下面命令更新
    > ```
    > curl 'http://ftp.apnic.net/apnic/stats/apnic/delegated-apnic-latest' | awk -F\| '/CN\|ipv4/ { printf("%s/%d\n", $4, 32-log($5)/log(2)) }' > /etc/chinadns_chnroute.txt
    > ```

相关项目
---

 Name                     | Description
 -------------------------|-----------------------------------
 [openwrt-chinadns][5]    | OpenWrt's ChinaDNS-C Makefile
 [openwrt-dnsmasq][6]     | OpenWrt's Dnsmasq Patch & Makefile
 [openwrt-shadowsocks][7] | OpenWrt's ShadowSocks Makefile


  [1]: https://github.com/clowwindy/ChinaDNS-C
  [2]: https://sourceforge.net/projects/openwrt-dist/files/chinadns-c/
  [3]: https://github.com/aa65535/openwrt-chinadns/blob/master/files/chinadns.masq
  [4]: https://github.com/aa65535/openwrt-chinadns/blob/master/files/chinadns.route
  [5]: https://github.com/aa65535/openwrt-chinadns
  [6]: https://github.com/aa65535/openwrt-dnsmasq
  [7]: https://github.com/aa65535/openwrt-shadowsocks
