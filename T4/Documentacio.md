
# 🛠️ Guia d'Implementació OpenLDAP per Innovatech

## 🔐 Connexió al servidor via SSH

Abans de començar qualsevol tasca, connecta't al servidor Ubuntu Server mitjançant SSH des de la màquina física o client.

```bash
ssh usuari@IP_del_servidor
```
Substitueix usuari pel nom d'usuari del servidor i IP_del_servidor per la seva IP a la xarxa Host-Only.

<img width="472" height="53" alt="image" src="https://github.com/user-attachments/assets/a6b709b1-517b-49f7-bef5-2b04b3b3f577" />

Si no saps quina IP té l’adaptador Host-Only, pots executar:
```bash
ip a
```
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/2a8f8dca-801f-445b-90d8-b78c86772341" />

---
## 🧾 Configuració del hostname i /etc/hosts abans de començar

###  Canviar el hostname del servidor:
```bash
sudo hostnamectl set-hostname server.innovatechXX.test
```
 Afegir el hostname al fitxer /etc/hosts:
Substitueix XX pel teu número de llista (exemple: server.innovatech11.test).
```bash
sudo nano /etc/hosts
```
<img width="405" height="51" alt="image" src="https://github.com/user-attachments/assets/e06d59e5-6f7a-4cb9-9072-21a0b314fd07" />

Afegeix una línia amb la IP del servidor i el hostname.
```bash
127.0.1.1   server.innovatechXX.test server
```
Substitueix XX pel teu número de llista
<img width="800" height="213" alt="image" src="https://github.com/user-attachments/assets/5cc95155-281e-4812-9f63-1fedda0092fb" />
3. Comprovar el hostname:
```bash
hostname
hostname -f
```
- El primer mostra el nom curt (server)
- El segon mostra el FQDN (server.innovatechXX.test)
<img width="288" height="77" alt="image" src="https://github.com/user-attachments/assets/a7b76af2-bca7-457f-80f6-2c7f5e2e4d38" />

---
## 🔧 1. Preparació de la Infraestructura

- Nom de màquina del servidor: `server.innovatechXX.test`
- Xarxa NAT per accés a Internet
- Xarxa Host-Only per comunicació amb el client ("*Adaptador de nómes l'amfitrió*")
> 📌 **Important**: Substitueix `XX` pel teu número de llista.  
> Exemple: Si ets el número **11**, el domini serà `innovatech11.test`.
<img width="616" height="295" alt="image" src="https://github.com/user-attachments/assets/d9636b01-5d45-41a5-b627-08d17c560bb0" />

<img width="613" height="294" alt="image" src="https://github.com/user-attachments/assets/2745dd06-bc88-4d9d-9603-59d5f2db474e" />


---
## 📦 2. Instal·lació del Servei OpenLDAP
```bash
sudo apt update
sudo apt install slapd ldap-utils
```
<img width="553" height="40" alt="Captura de pantalla 2025-10-21 170839" src="https://github.com/user-attachments/assets/03f1e537-26c8-4f60-be87-c9b25c95d213" />

`Contrasenya admin: p@ssw0rd`

Comprovació:

```bash
sudo systemctl status slaqd
```
<img width="1104" height="420" alt="image" src="https://github.com/user-attachments/assets/b81d924e-fbdf-4da3-b993-5b532ba04a48" />


# 🏗️ 3. Configuració del Directori

### 3.1. Crear fitxers LDIF per a les OUs

Primer, crea un fitxer per a **Usuaris**:
```bash
sudo nano OU_Usuaris.ldif
```
Contingut:

```bash
dn: ou=Usuaris,dc=innovatechXX,dc=test
ou: Usuaris
objectClass: top
objectClass: organizationalUnit
```
<img width="800" height="581" alt="image" src="https://github.com/user-attachments/assets/679b22fa-401c-4f16-8df1-ba6208127eb2" />

Després, crea un fitxer per a Grups:

```bash
sudo nano OU_Grups.ldif
```
Contingut:

```bash
dn: ou=Grups,dc=innovatechXX,dc=test
ou: Grups
objectClass: top
objectClass: organizationalUnit
```
<img width="800" height="575" alt="image" src="https://github.com/user-attachments/assets/db7b008a-3fdf-47c5-95e5-e1b6b3a7e740" />


3.2. Afegir les OUs al directori

Executa:
```bash
ldapadd -x -D "cn=admin,dc=innovatechXX,dc=test" -W -f OU_Usuaris.ldif
ldapadd -x -D "cn=admin,dc=innovatechXX,dc=test" -W -f OU_Grups.ldif
```

3.3. Comprovar la configuració

Utilitza:

```bash
sudo slapcat
```
Això mostrarà el contingut actual de la base de dades LDAP, incloent les OUs creades.

---
## 👥 4.Instal·lació i Configuració de LAM

### 4.1 Instal·lació del Gestor d'Usuaris LDAP (LAM)

```bash
sudo apt update
sudo apt install ldap-account-manager
```
<img width="1000" height="439" alt="image" src="https://github.com/user-attachments/assets/05f6c673-ee39-47db-9452-b441dc69266b" />

### 4.2 Accés Remot i Configuració

Descripció: Connectar a LAM des de la màquina física utilitzant la IP de la interfície Host-Only.

Passos:

- 1- Obre el navegador a la màquina física.
- 2- Introdueix l’adreça:

``Accés: http://<IP Host-Only>/lam``

<img width="378" height="34" alt="image" src="https://github.com/user-attachments/assets/16f7424e-4c60-4eac-9b86-c8c6d0265195" />

Si no saps quina IP té l’adaptador Host-Only, pots executar utilitzant el comanda:

```bash
ip a
```
### 4.3 Configuració per defecte

Passos:

1-Accedeix a LAM com a administrador.

2-Ves a Configuració > Configuració del servidor.

Ajustaments generals:
- 1- Preferències del servidor:

```
cn=admin,dc=innovatechXX,dc=test
```
- 2-Configuració de l'idioma:
<img width="1035" height="170" alt="image" src="https://github.com/user-attachments/assets/522f4639-1159-4a0d-a537-27e77bf4ad25" />

- 3-Ajustaments de ferramentes:
<img width="1066" height="318" alt="image" src="https://github.com/user-attachments/assets/1ccd13ca-238b-456e-acf5-e1dbb4657ddf" />

- 4-tipus de comptes (abaix de tot):
```
  Usuaris: ou=users,dc=innovatechXX,dc=test
  Grups: ou=groups,dc=innovatechXX,dc=test
```
<img width="1226" height="511" alt="image" src="https://github.com/user-attachments/assets/bc535442-12cd-494c-a36f-6eaae54db30e" />

- 5-Un cop acabat desar els canvis.

### 4.4 Creació de Grups i Usuaris

Abans de crear els grups haurem d'anar a l'inici del lam i iniciarem sessió la contrasenya és el ldap que has posat
<img width="861" height="395" alt="image" src="https://github.com/user-attachments/assets/e84f0518-61d0-41ca-953b-02623f6948ef" />

Passos:

- 1-anar en comptes
- 2-fer clic en grups
- 3-nou grup
- 4-poses nom del grup i ho guardes

<img width="1918" height="398" alt="image" src="https://github.com/user-attachments/assets/baafde72-5492-47a7-aec4-bf69506ab3d8" />

i per crear usuari el mateix, però al nom de l'usuari tindràs posar on posen en cognoms

<img width="1919" height="540" alt="image" src="https://github.com/user-attachments/assets/4fcc72ae-5150-4549-86ad-dda8fb85bb36" />

Un cop ja poseu el nom de l'usuari ires on posa unix i posar el grup primari conresponent i desesar

<img width="1878" height="521" alt="image" src="https://github.com/user-attachments/assets/00baed12-441e-4665-9b31-00181062d238" />

# 5.Integració de Client (Client Ubuntu Desktop)
### 5.1 Instal·lació del Client

Passos:
- Instal·la Ubuntu Desktop en una màquina virtual(Zorin).
- Configura la interfície de xarxa com a Host-Only.
- Comprova la connexió amb el servidor fent un ping a la seva IP.

### 5.2 Resolució de Noms

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

### 5.3 Instalació de dels moduls necessaris
