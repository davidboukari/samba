# samba

* See https://www.howtoforge.com/tutorial/samba-server-ubuntu-16-04/

```bash
#$ apt-get install -y samba samba-common python-glade2 system-config-samba
$ apt-get install -y samba samba-common system-config-samba

#**********************************************
#Add on /etc/samba/smb.conf
#**********************************************
[global]
workgroup = WORKGROUP
server string = Samba Server %v
netbios name = ubuntu
security = user
map to guest = bad user
dns proxy = no

[Anonymous]
path = /media/samba/anonymous
browsable =yes
writable = yes
guest ok = yes
read only = no
force user = nobody

#**********************************************
#* Creation des  partages
#**********************************************

mkdir -p /media/samba/anonymous
chmod 755 /media/samba/anonymous
chown -R nobody:nogroup  /media/samba/anonymous

# Check the sharing
smbtree -v

# Mount a sharing
mkdir -p /tmp/toto
mount -t cifs -o guest //myserver/Anonymous /tmp/toto
```
