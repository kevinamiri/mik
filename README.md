
## Step 1: Download RouterOS CHR Image

Choose one of the following RouterOS images:

```bash
# Version 7.19.1
wget https://raw.githubusercontent.com/kevinamiri/mik/refs/heads/main/install-image-7.19.1.img.tar.gz

# Version 7.13
wget https://github.com/kevinamiri/mik/raw/main/chr-7.13.img.tar.gz
```

Before proceeding, identify your server's main disk:

```bash
lsblk
```

Common disk names:
- `/dev/sda` - Traditional naming
- `/dev/vda` - Virtual disk naming

If you see `/dev/vda` in the output, use it. If you see `/dev/sda`, use it.



## Step 2: Extract and Install RouterOS

```bash
tar -xzvf install-image-7.19.1.img.tar.gz
sudo dd if=install-image-7.19.1.img of=/dev/vda
```

For 7.13:

```bash
tar -xzvf chr-7.13.img.tar.gz
sudo dd if=chr-7.13.img.tar.gz of=/dev/vda
```


## Step 5: Sync and Reboot

Ensure all data is written to disk before rebooting:

```bash
sync
sudo reboot
```

## Step 6: Post-Installation Access


### Initial Configuration
```bash
# Via SSH (once you know the IP)
ssh admin@<router-ip>

# Set admin password
/user set admin password=your-secure-password

# Configure basic network settings
/ip address add address=<router-ip>/24 interface=ether1
/ip route add gateway=<router-gateway> (offen ends with `.1`)
```
