# T03: Gestió flexible de discos (LVM i Espais d’emmagatzematge)
## Part Linux – LVM amb Zorin OS

✅ Discos necessaris

Sistema operatiu: 1 disc (ja existent).
Discos addicionals: 3 discos de 10 GB.
<img width="962" height="560" alt="image" src="https://github.com/user-attachments/assets/797fd2e6-9acc-4c6f-b7d3-175c38798d9e" />


Es faran servir per crear el grup de volums, el volum lògic, el snapshot i el mirroring.

## 1. Configuració inicial

Crear un grup de volums (VG) i un volum lògic (LV) amb els discos afegits.

Abans de executar els comandes farem un:
```bash
sudo su
```
Fem això per estar en *root* per executar les comandes sense cap problema
### Instalacio fdisk
```bash
sudo apt install fdisk
```
### Comprovar discos
```bash
sudo fdisk -l
```
<img width="648" height="413" alt="image" src="https://github.com/user-attachments/assets/9f5887a7-6c43-44c5-9577-2f6fe301acdf" />
### Instalació lvm2
```bash
sudo apt install lvm2
```

### Inicialitzar volums físics (executar una sola vegada amb tots els discos)
```bash
pvcreate /dev/sdb /dev/sdc /dev/sdd
```
### Crear grup de volums (executar una sola vegada)
```bash
vgcreate volgrup /dev/sdb /dev/sdc
```
### Afegir un disc més al grup (executar quan s'afegeix el tercer disc)
```bash
vgextend volgrup /dev/sdd
```
### Crear volum lògic (primer LV)
```bash
lvcreate -L 100M -n lv01 volgrup
```
### Formatar i muntar (executar per cada LV creat)
```bash
mkfs.ext4 /dev/volgrup/lv01
mkdir /mnt/lv01
mount /dev/volgrup/lv01 /mnt/lv01
````
### Afegir a /etc/fstab per muntatge automàtic
```bash
echo "/dev/volgrup/lv01 /mnt/lv01 ext4 defaults 0 0" >> /etc/fstab
```
## 2. Comprovacions
``
pvs    # Mostra volums físics
vgs    # Mostra grups de volums
lvs    # Mostra volums lògics
``
## 3. Snapshot

### Crear snapshot (executar una vegada)
```bash
lvcreate -L 100M -s -n copialv01 /dev/volgrup/lv01
```
### Muntar snapshot (executar una vegada)
```bash
mkdir /mnt/copia
mount /dev/volgrup/copialv01 /mnt/copia
```
## 4. Mirroring
### Crear volum amb mirall (executar una vegada)
```bash
lvcreate -L 90M -m1 -n mirrorlv volgrup
```
### Formatar i muntar el volum amb mirall
```bash
mkfs.ext4 /dev/volgrup/mirrorlv
mkdir /mnt/mirror
mount /dev/volgrup/mirrorlv /mnt/mirror
```
# 5. Eliminació d’un LV
```bash
umount /mnt/lv01
lvremove /dev/volgrup/lv01
```
# Si hi ha entrada a /etc/fstab, eliminar-la

## 6. Comprovació final
```bash
pvs
vgs
lvs
```

