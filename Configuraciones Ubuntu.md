# Red

1. Crear el archivo de configracion 00

```bash
# This is the network config written by 'subiquity'
network:
  ethernets:
   enp0s3:
    dhcp4: true

   enp0s8:
    addresses: [192.168.10.12/24]
    gateway4: 192.168.10.1  -> deprecated
    nameservers:
     search: [redinterna.local]
     addresses: [192.168.10.10]
     routes:
     - to: default
       via: 172.13.8.1
version: 2
```

Para probar la configuracion: 

```bash
netplan try
```
y para cargbarla 

```bash
netplan apply
```

# Consola proxmox

```bash
sudo apt install -y xserver-xorg-video-qxl spice-vdagent
```

