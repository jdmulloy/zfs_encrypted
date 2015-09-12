# zfs_encrypted
FreeBSD rc script for running a ZFS pool on top of GELI encrypted disks without
prompting for a password at boot. Suitable for servers where your OS volume is
unencrypted and you want to login via SSH to mount the encrypted ZFS Pool.

# Configuration (rc.conf)

## Enable Service
    zfs_encrypted_enable="YES"
This will enable the service, however it will not mount anything at boot since
you need to enter passwords which would stop boot.

## List the name of the pool(s) to mount
    zfs_encrypted_zpools="data"

## Geli Flags
    zfs_encrypted_data_geli_flags="-k /root/data.key"
Optionally pass extra flags to geli, variable name is zfs_encrypted_${pool}_geli_flags

## Geli devices
    zfs_encrypted_data_geli_devices="/dev/gpt/disk2 /dev/gpt/disk3 /dev/gpt/disk4 /dev/gpt/disk5"
List raw devices that are encrypted by geli. Variable name is zfs_encrypted_${pool}_geli_devices

# Usage
    service zfs_encrypted start
Geli mounts volumes and then imports/starts the zpool.
