# 在命令行中使用 Shadowsocks

Shadowsocks 的代理支持 Socks5 协议. 很多使用 Http 协议的软件都无法使用.

通过简单的配置就可以使 Zsh 使用 Shadowsocks. 方法来自:[Mac OSX终端走shadowsocks代理](https://github.com/mrduli/blog/issues/18)

只需要使用命令: export all_proxy=socks5://127.0.0.1:1080
取消使用 unset all_proxy