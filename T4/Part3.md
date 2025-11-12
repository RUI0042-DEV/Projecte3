# 5.Integració de Client (Client Ubuntu Desktop)
### 3.1 Instal·lació del Client

Passos:
- Instal·la Ubuntu Desktop en una màquina virtual(Zorin).
- Configura la interfície de xarxa com a Host-Only.
- Comprova la connexió amb el servidor fent un ping a la seva IP.

### 3.2 Resolució de Noms

1-Editar el arxiu
```
sudo nano /etc/hosts
```
2-Afegeix la linea
```
<IP-del-servidor> server.innovatechXX.test
```
<img width="598" height="190" alt="image" src="https://github.com/user-attachments/assets/81869044-3418-47eb-9b32-0419e1368b9c" />

3-Desa i tanca, i fer el comanda:

```
sudo hostnamectl set-hostname client
```
<img width="653" height="55" alt="image" src="https://github.com/user-attachments/assets/1b154022-6efe-447f-bc4d-c839d3259ed4" />

4-Comprovació
```bash
Hostaname -f
```
<img width="376" height="43" alt="image" src="https://github.com/user-attachments/assets/56e267a0-59fc-4214-91a4-bf732150939d" />

```bash
dig server.innovatechXX.test
```
<img width="636" height="377" alt="image" src="https://github.com/user-attachments/assets/7b0d4763-366b-491a-a969-12cbc4641300" />

```bash
ping server.innovatechXX.test
```
<img width="647" height="135" alt="image" src="https://github.com/user-attachments/assets/691742fa-6b3a-49e0-a020-2a8690758f41" />

### 3.3 Instalació de dels moduls necessaris

Ara instal·larem els mòduls necessaris per poder utilitzar libpam i nss.

Comanda:
```bash
sudo apt install libnss-ldap libpam-ldap ldap-utils nscd -y
```

1-

<img width="643" height="473" alt="image" src="https://github.com/user-attachments/assets/3156ae22-3426-4fff-889a-ed46cf0bc794" />

2-

<img width="643" height="358" alt="image" src="https://github.com/user-attachments/assets/9de52fb3-01f7-40f2-84ae-947b67fe3a74" />

3-

<img width="635" height="311" alt="image" src="https://github.com/user-attachments/assets/bffe305e-11a6-46d3-a01b-3b19c05956f0" />


4-

<img width="639" height="373" alt="image" src="https://github.com/user-attachments/assets/97c73a86-455a-46ff-9a25-c3ab864c2e44" />

5-

<img width="632" height="317" alt="image" src="https://github.com/user-attachments/assets/81c8f6cf-f361-4821-956c-65dd8a2b4f8f" />

6-

<img width="636" height="361" alt="image" src="https://github.com/user-attachments/assets/e752706a-b272-45ea-90bb-6698fa7d15e6" />

7-

<img width="639" height="369" alt="image" src="https://github.com/user-attachments/assets/19907d3c-2734-4c27-9ada-c710617f7e54" />

### 5.4 Compravació connexió

```bash
ldapsearch -x -D 'cn=admin,dc=innovatechXX,dc=test' -W -H ldap://server.innovatechXX.test -b 'dc=innovatechXX,dc=test' objectClass=posixAccount uid'
```

<img width="661" height="477" alt="image" src="https://github.com/user-attachments/assets/ae45ccb7-9ad3-49b8-af8d-b896967d6d2b" />

### Configuracions

Comanda:
```bash
sudo nano /etc/nsswitch.conf
```

<img width="666" height="482" alt="image" src="https://github.com/user-attachments/assets/5a5f61ad-4e84-43b0-9bbf-d9596f453365" />

Comanda:
```bash
sudo nano /etc/pam.d/common-password
```
Eliminarem la línea del terme use_authtok

<img width="922" height="484" alt="image" src="https://github.com/user-attachments/assets/647e4177-aa7c-431b-a2fd-0710b56b2b54" />

Comanda:
```bash
sudo nano /etc/pam.d/common-session
```
<img width="923" height="482" alt="image" src="https://github.com/user-attachments/assets/9da83ea6-eddf-4e81-9e06-2ce26968a601" />

Afegim la línea indicada per crear els perfils

Ara reniciarem el servei

Comanda:
```bash
sudo systemctl restart nscd
```
<img width="464" height="21" alt="image" src="https://github.com/user-attachments/assets/013237a9-99cd-42a6-a819-6b8647bd4a0d" />


Comprovarem que ara es pugui veure els usuaris usant la comanda:
```bash
sudo getent passwd | tail
```
<img width="646" height="252" alt="image" src="https://github.com/user-attachments/assets/478933e8-9150-45ac-8197-3fe8782954a5" />

Per finalitzar editarem l'arxiu indicat perquè ens permetés l'inici de sessió gràfica

```bash
sudo nano /etc/pam.d/gdm-launch-environment
```

### Comprovacions

Ara reniciarem la nostra màquina i iniciarem sessió amb el compte ("tech01")

<img width="1275" height="778" alt="image" src="https://github.com/user-attachments/assets/ffadaaaa-dcbf-4ed1-b04b-46d9ec130200" />


Un cop ja iniciat sessió al compte anirem a terminal i posarem la comanda:
```bash
id
```

<img width="654" height="134" alt="image" src="https://github.com/user-attachments/assets/ce9184db-60ad-413d-8c63-829de5e55f4a" />

