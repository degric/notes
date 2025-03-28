# Configurar netplan

netplan es una herramienta para asignar ip de manera estatica, o confiugrar adaptadores de red. Archivo de configuraacio: `/etc/netplan/01-netcdfg.yaml`
```yaml
network:
  version: 2
  ethernets:
  enp0s3:
    addresses: [192.168.1.1/ 24]
    dhcp4: no
    namerservers: 
      addresse: 8.8.8.8
network:
enp0s8
  version: 2
  ethernets:
    dhcp4: yes
```
De esta manera estamos configurando el adaptador de red `enp0s3` y `enp0s8`

Despues de esto tenemos que configurar el `ip_forward`, el cual permite la retrasnmision de paquetes entre adaptadores. 
para esto tenemos el archivo de `/proc/sys/net/ipv4/ip_forward`, el cual es un solo bit, cero si no acetpta  y uno si acetta. 
- POdemos cambiar esta configuracion manualmente editando el archivo, sin embargo esto volveria a su estado original una vez reiniciado el equipo, asi que para hacerlo permanetne, editamos el archivo: `/etc/systctl.conf`, en este buscamos la linea: `net.ipv4.ip_forward=1` y la descomentamos.
- Una vez esto falta hacer los cambios efectiovos con el comando: `sudo sysctl -p /etc/sysctl.conf`, ahora si vemos el arcvio de /proc veremos que tiene una valor de 1.



# configurar iptables

Ya tenemos todo casi listo, solo nos falta la ultima configuracion, y esta est la de `iptables`.
1. Vemos la configuracion de iptables con : `iptables -L`
2. Vemos la configuracion de nat con : `iptables -L -nv -t nat`
3. Finalmente permitimos el nat con: `iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`
4. Para quitar los cambios es con: `sudo iptables -F`
5. `sudo iptables -t nat -F`
6. Para guardar los cambio se necesita el paquete "iptables-persistent" y despues para guardar cxxambios es: `netfilter-persistent save`






