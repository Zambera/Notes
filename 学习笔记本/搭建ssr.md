# SSR搭建代码记录

## SSR安装脚本

```bash
//root
sudo -i

//逗比SSR脚本
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/ssrmu.sh && chmod +x ssrmu.sh && bash ssrmu.sh

//安装ssr
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh && chmod +x shadowsocksR.sh

//打开
./shadowsocksR.sh
```

## 开启BBR

~~~~bash
//BBR加速
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

//BBR开启
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh &&  chmod +x bbr.sh &&./bbr.sh

//魔改BBR
wget --no-check-certificate -qO 'BBR.sh' 'https://moeclub.org/attachment/LinuxShell/BBR.sh' && chmod a+x BBR.sh && bash BBR.sh -f

chmod +x shadowsocksR.sh
~~~~



## Shell登录服务器

~~~~bash
//修改服务器root密码
passwd

//修改sshd配置文件
vim /etc/ssh/sshd_config
//修改如下参数
PermitRootLogin yes 
PasswordAuthentication yes

//重启ssh服务
systemctl restart sshd.service
~~~~



## SSR配置信息



> Your Server IP        :  34.92.55.237 
> Your Server Port      :  23333 
> Your Password         :  genilless.club 
> Your Protocol         :  origin 
> Your obfs             :  plain 
> Your Encryption Method:  rc4-md5 