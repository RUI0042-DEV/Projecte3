# T03: Gestió flexible de discos (LVM i Espais d’emmagatzematge)
## Part Linux – LVM amb Zorin OS
<img width="175" height="150" alt="image" src="https://github.com/user-attachments/assets/6b811809-f7df-421b-b039-95253fcd5455" />


Discos necessaris:

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
pvcreate /dev/sdb 
```
<img width="493" height="124" alt="image" src="https://github.com/user-attachments/assets/0422e2bd-a786-449e-a388-74163e203407" />

### Crear grup de volums (executar una sola vegada)
```bash
vgcreate volgrup /dev/sdb /dev/sdc
```
<img width="538" height="59" alt="image" src="https://github.com/user-attachments/assets/db0f4499-007f-4ec6-bb81-01f386eb58bd" />

### Afegir un disc més al grup (executar quan s'afegeix el tercer disc)
```bash
vgextend volgrup /dev/sdd
```
<img width="524" height="59" alt="image" src="https://github.com/user-attachments/assets/c04e9e71-ea27-4c3c-a41b-6d54def3fdea" />

### Mostrant els VG
```bash
vgdisplay
```
<img width="569" height="382" alt="image" src="https://github.com/user-attachments/assets/e33232da-c2fb-4d27-a66f-7089b5d9efe8" />

### Crear volum lògic (primer LV)
```bash
lvcreate -L 100M -n lv01 volgrup
```
<img width="590" height="45" alt="image" src="https://github.com/user-attachments/assets/c70baafb-c3a2-488d-8dc9-bb5bfbb6c744" />

### Formatar i muntar (executar per cada LV creat)
```bash
mkdir /mnt/lv01
mkfs.ext4 /dev/volgrup/lv01
mount /dev/volgrup/lv01 /mnt/lv01
```
<img width="651" height="219" alt="image" src="https://github.com/user-attachments/assets/e1037edb-16a3-4559-be48-50396deb333e" />

### Afegir a /etc/fstab per muntatge automàtic
Fem un:
```bash
sudo nano /etc/fstab
```
I afegim:

<img width="944" height="468" alt="image" src="https://github.com/user-attachments/assets/18fd3e76-f4c1-4ba4-95d0-dc46a64a9348" />

## 2. Comprovacions
```
pvs    # Mostra volums físics
vgs    # Mostra grups de volums
lvs    # Mostra volums lògics
```
<img width="814" height="210" alt="image" src="https://github.com/user-attachments/assets/aa031b38-a252-4851-b6ad-c2d8974d0af9" />

## 3. Snapshot

### Crear snapshot 
```bash
lvcreate -L 100M -s -n copialv01 /dev/volgrup/lv01
```
<img width="677" height="37" alt="image" src="https://github.com/user-attachments/assets/f55793ef-2aa1-4281-ada3-c534e6dec9fa" />

### Muntar snapshot 
```bash
mkdir /mnt/copia
mount /dev/volgrup/copialv01 /mnt/copia
```
<img width="599" height="78" alt="image" src="https://github.com/user-attachments/assets/0331cf7d-b3e9-41f2-9651-369b6cde3f06" />

## 4. Mirroring
### Crear volum amb mirall (executar una vegada)
```bash
lvcreate -L 90M -m1 -n mirrorlv volgrup
```
<img width="579" height="151" alt="image" src="https://github.com/user-attachments/assets/a0e65669-c19d-42cf-9b8d-458bde8329c3" />

### Formatar i muntar el volum amb mirall
```bash
mkdir /mnt/mirror
mkfs.ext4 /dev/volgrup/mirrorlv
mount /dev/volgrup/mirrorlv /mnt/mirror
```
<img width="687" height="240" alt="image" src="https://github.com/user-attachments/assets/074eda12-b16c-4a03-8622-16479f1a605b" />

# 5. Eliminació d’un LV
```bash
umount /mnt/lv01
lvremove /dev/volgrup/lv01
```
<img width="936" height="112" alt="image" src="https://github.com/user-attachments/assets/e800860f-0b4b-4570-9339-a02a11098c57" />


### Eliminar la línia corresponent a aquest LV de /etc/fstab
```bash
nano /etc/fstab
```
Esborra la línia:
``
/dev/volgrup/lv01 /mnt/lv01 ext4 defaults 0 0
``
<img width="950" height="482" alt="image" src="https://github.com/user-attachments/assets/3224c407-2fa4-4739-97c0-eb2ce0762226" />

## 6. Comprovació final
```bash
pvs
vgs
lvs
```
<img width="771" height="240" alt="image" src="https://github.com/user-attachments/assets/cf9cecf6-8b0d-43ac-a1ae-2f71a890ed68" />

---
[Tornar enrere](README.md)
