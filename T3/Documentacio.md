# T03: Gestió flexible de discos (LVM i Espais d’emmagatzematge)
## Part Linux – LVM amb Zorin OS

✅ Discos necessaris

Sistema operatiu: 1 disc (ja existent).
Discos addicionals: 3 discos de 10 GB (segons la demo de la presentació).

Es faran servir per crear el grup de volums, el volum lògic, el snapshot i el mirroring.

## 1. Configuració inicial

Crear un grup de volums (VG) i un volum lògic (LV) amb els discos afegits.

### Comprovar discos
```
fdisk -l
```
### Inicialitzar volums físics (executar una sola vegada amb tots els discos)
```
pvcreate /dev/sdb /dev/sdc /dev/sdd
```
### Crear grup de volums (executar una sola vegada)
```
vgcreate volgrup /dev/sdb /dev/sdc
```
### Afegir un disc més al grup (executar quan s'afegeix el tercer disc)
```
vgextend volgrup /dev/sdd
```
### Crear volum lògic (primer LV)
```
lvcreate -L 100M -n lv01 volgrup
```
### Formatar i muntar (executar per cada LV creat)
```
mkfs.ext4 /dev/volgrup/lv01
mkdir /mnt/lv01
mount /dev/volgrup/lv01 /mnt/lv01
````
### Afegir a /etc/fstab per muntatge automàtic
```
echo "/dev/volgrup/lv01 /mnt/lv01 ext4 defaults 0 0" >> /etc/fstab
```
