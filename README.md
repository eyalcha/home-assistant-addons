# Home Assistant Addons

- [Deepstack](https://github.com/johnolafenwa/DeepStack)
- [CompreFace](https://github.com/exadel-inc/CompreFace)
- [Frigate]()
- [Double-Take]()
- [Samba]()

## LXC Template

Template for home assistant lxc addons

### Resources

Resource|Size
---|---
Template | ubuntu-22.04-standard_22.04-1_amd64.tar.zst
Disk | 2G
Memory | 512Mb

### Install

Install packages
```
apt update
apt install curl git zsh
```

Install docker 
```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

Install docker compose
```
apt install docker-compose
```

Install oh-my-zsh
```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Create Template

Stop container and backup as gzip

Run in pve
```
mv /mnt/<shared>/dump/<backup>.tar.gz /var/lib/vz/template/cache/ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
```

## LXC NVR

Resource|Size
---|---
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 
Memory |

### Configure

Check usb devices
```
lsusb
```

Add to pve lxc conf (/etc/pve/lxc/<id>.conf)
```
lxc.mount.entry: /dev/bus/usb/002/ dev/bus/usb/002/ none bind,optional,create=dir 0,0
lxc.cgroup2.devices.allow: c 189:* rwm
lxc.apparmor.profile: unconfined
lxc.cgroup2.devices.allow: a
lxc.cap.drop: 
lxc.mount.auto: cgroup:rw
```
  
Share drive with lxc, Run in pve
```
pct set <id> -mp0 /mnt/ext1/share,mp=/share
```

## LXC Samaba

### Resources
  
Resource|Size
---|---
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 2G
Memory | 512Mb
  
### Configure

Mount share to container
```
pct set <id> -mp0 /mnt/ext1/share,mp=/share
```

Remove security profile, add to pve lxc conf (/etc/pve/lxc/<id>.conf)
```
lxc.apparmor.profile: unconfined
```

Share drive with lxc, Run in pve
```
pct set <id> -mp0 /mnt/ext1/share,mp=/share
```




