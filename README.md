#### SWAP
```bash
fallocate -l 8G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo '/swapfile none swap defaults 0 0' | tee -a /etc/fstab
echo 'vm.swappiness=10' | tee /etc/sysctl.d/99-swappiness.conf
sysctl -p /etc/sysctl.d/99-swappiness.conf
```

#### SSD
```bash
lsblk
parted /dev/sdX --script mklabel gpt mkpart primary ext4 0% 100%
mkfs.ext4 -m 0 -L "ronflex" /dev/sdX1
blkid /dev/sdX1 # get UUID
mkdir -p /mnt/ronflex
chown -R $USER:$USER /mnt/ronflex
vim /etc/fstab
```
```
UUID=<ID> /mnt/ronflex ext4 defaults,nofail 0 2
```
```bash
mount -a
```

#### VPN
```bash
apt install wireguard resolvconf iptables-persistent -y
```
```bash
mv /chemin/vers/votre_fichier.conf /etc/wireguard/wg0.conf
chmod 600 /etc/wireguard/wg0.conf
systemctl enable --now wg-quick@wg0
```
