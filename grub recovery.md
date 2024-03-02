# Ubuntu Grub Recovery
## grub>

```bash

grub > set root=(hd0,gpt2)
grub > linux /vmlinuz-5.15.0-88-generic root=/dev/mapper/ubuntu--vg-ubuntu--lv
grub > initrd /initrd.img-5.15.0-88-generic
grub > boot

``` 
### after login 

```bash

grub-mkconfig -o /boot/grub/grub.cfg

```

