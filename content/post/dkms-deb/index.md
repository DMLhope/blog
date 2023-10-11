---
title: dkms 内核模块打包 deb
description: dkms 内核模块打包 deb
date: 2021-08-08 00:00:00+0000
categories: 
  - note
tags: 
  - dkms
image: 20210808.jpg
---

## 安装环境 :
``` 
sudo apt-get install dkms
sudo apt-get install dh-make
```

## 文件 :
### hello.c
```c
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/module.h>

static int hello_init(void)
{
  pr_info("Hello world.\n");
  return 0;
}
static void hello_exit(void)
{
  pr_info("Goodbye world.\n");
}

module_init(hello_init);
module_exit(hello_exit);
```

### Makefile
```makefile 
ifneq ($(KERNELRELEASE),)
obj-m := hello.o
else
KVERSION:= $(shell uname -r)
all:
  $(MAKE) -C /lib/modules/$(KVERSION)/build M=$(PWD) modules
clean:
  $(MAKE) -C /lib/modules/$(KVERSION)/build M=$(PWD) clean
endif
```

### dkms.conf
```conf
PACKAGE_NAME="hello"
PACKAGE_VERSION="0.1"
BUILT_MODULE_NAME[0]="hello"
DEST_MODULE_LOCATION[0]="/updates"
AUTOINSTALL="yes"
```

模块需要在 /usr/src 下建立文件夹，命名方式为 < 模块名称 >-< 版本号 >, 如 :hello-0.1

路径 :/usr/src/hello-0.1
```shell 
.
├── dkms.conf
├── hello.c
└── Makefile
```

## 命令 :
`dkms status 、add、build、install、uninstall 和 remove`

状态 : `dkms status`

添加模块 :`sudo dkms add -m hello -v 0.1`

编译驱动 :`sudo dkms build -m hello -v 0.1`

安装模块 :`sudo dkms install -m hello -v 0.1`

移除模块 :`sudo dkms remove -m hello -v 0.1 --all`

模块打包 :`sudo dkms mkdeb -m hello -v 0.1`

deb 产出 :`/var/lib/dkms/hello/0.1/deb/`
