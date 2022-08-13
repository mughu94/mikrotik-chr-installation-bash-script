# mikrotik-chr-installation-bash-script
Instalasi Mikrotik CHR Menggunakan Script Sederhana

check storage filesystem vda/sda atau yg lain dengan perintah "df -h"

## Jika FIlesystem /dev/vda
wget -4 https://download.mikrotik.com/routeros/6.47.10/chr-6.47.10.img.zip -O chr.img.zip && \
gunzip -c chr.img.zip > chr.img && rm -f chr.img.zip && \
mount -o loop,offset=512 chr.img /mnt && \
ADDRESS=`ip addr show eth0 | grep global | cut -d' ' -f 6 | head -n 1` && \
GATEWAY=`ip route list | grep default | cut -d' ' -f 3` && \
echo "/ip address add address=$ADDRESS interface=[/interface ethernet find where name=ether1]
/ip route add gateway=$GATEWAY
" > /mnt/rw/autorun.scr && \
umount /mnt && \
echo u > /proc/sysrq-trigger && \
dd if=chr.img bs=1024 of=/dev/vda

## Jika FIlesystem /dev/sda
wget -4 https://download.mikrotik.com/routeros/6.47.10/chr-6.47.10.img.zip -O chr.img.zip && \
gunzip -c chr.img.zip > chr.img && rm -f chr.img.zip && \
mount -o loop,offset=512 chr.img /mnt && \
ADDRESS=`ip addr show eth0 | grep global | cut -d' ' -f 6 | head -n 1` && \
GATEWAY=`ip route list | grep default | cut -d' ' -f 3` && \
echo "/ip address add address=$ADDRESS interface=[/interface ethernet find where name=ether1]
/ip route add gateway=$GATEWAY
" > /mnt/rw/autorun.scr && \
umount /mnt && \
echo u > /proc/sysrq-trigger && \
dd if=chr.img bs=1024 of=/dev/sda
