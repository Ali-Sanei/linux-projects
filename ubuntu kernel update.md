### Compile the ubuntu Kernel 5.15.0 to 6.1.7 


## curent kernel versio
```bash
uname -r
# 5.15.0-89-generic
```
## compatible version for upgrade is 6.1.7
 
 ## Download kernel 
 
 ```bash
 cd /usr/srrc
 wget https://mirrors.edge.kernel.org/pub/linux/kernel/v6.x/linux-6.1.7.tar.xz
 ```
 ## Decompress Downloaded file

 ```bash
 tar -Jvxf linux-6.1.7.tar.xz 
 ```
 ## link the decompressed directory
 
 ```bash
 ln -s linux-6.1.7 linux

 ``` 

 ## install tools 
 
 ```bash
 apt install -y build-essential dwarves python3 libncurses-dev flex bison libssl-dev bc libelf-dev zstd gnupg2

 ``` 
 
## change directory to the extracted directory (linux or linux-6.1.7) 

```bash
cd /usr/src/linux

```
## For Enable or Disable Kernel Moduls

```bash

make menuconfig 
# make nconfig
# make config

```

# if you want to delet configs use "make clean" , "make mrproper" 

# disable the SYSTEM_REVOCATION_KEYS

```bash

scripts/config --disable SYSTEM_REVOCATION_KEYS

```

## Before Compile the Kernel you must create a bz image (the new kernel installing whit this image) 

```bash

make bzImage

```

# An error occurs while creating the image, error make[1]: *** No rule to make target 'debian/canonical-revoked-certs.pem' , needed by certs/x509_revocation_list'. STOP. make: ***[Makefile:1851:certs] Error 2 to fix it :

```bash
vim .config
#
# Certificates for signature checking
#
CONFIG_MODULE_SIG_KEY="certs/signing_key.pem"
CONFIG_MODULE_SIG_KEY_TYPE_RSA=y
CONFIG_MODULE_SIG_KEY_TYPE_ECDSA=y
CONFIG_SYSTEM_TRUSTED_KEYRING=y
CONFIG_SYSTEM_TRUSTED_KEYS="/usr/local/src/debian/canonical-certs.pem"
CONFIG_SYSTEM_EXTRA_CERTIFICATE=y
CONFIG_SYSTEM_EXTRA_CERTIFICATE_SIZE=4096
CONFIG_SECONDARY_TRUSTED_KEYRING=y
CONFIG_SYSTEM_BLACKLIST_KEYRING=y
CONFIG_SYSTEM_BLACKLIST_HASH_LIST=""
CONFIG_SYSTEM_REVOCATION_LIST=y
CONFIG_SYSTEM_REVOCATION_KEYS="/usr/local/src/debian/canonical-revoked-certs.pem"
# end of Certificates for signature checking
# write and quite
```
# Then

```bash

sudo mkdir -p /usr/local/src/debian
sudo apt install linux-source
sudo cp -v /usr/src/linux-source-*/debian/canonical-*.pem /usr/local/src/debian/
sudo apt purge linux-source*

```
## Now Run again 

```bash

make bzImage

```
## intall the kernel modules

```bash

make modules
make modules_install

```

## install the Linux Kernel 6.1.7 

```bash

make install

```

## verify the newly installed kernel at /boot directory

```bash

# vmlinuz-6.1.7
# initrd.img-6.1.7

```

## Update Grub Boot Loader 

```bash

update-grub

```

## restart your system to boot from the newly installed kernel

```bash

reboot

```

##  verify your system Kernel

```bash

uname -a
# Linux ubuntu 6.1.7 #1 SMP PREEMPT_DYNAMIC Thu Nov 23 21:52:42 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux

```


