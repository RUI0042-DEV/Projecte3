# 📦 1.Instal·lació del Servei OpenLDAP

##  1.1 Preparació de la Infraestructura

- Nom de màquina del servidor: `server.innovatechXX.test`
- Xarxa NAT per accés a Internet
- Xarxa Host-Only per comunicació amb el client ("*Adaptador de nómes l'amfitrió*")
> 📌 **Important**: Substitueix `XX` pel teu número de llista.  
> Exemple: Si ets el número **11**, el domini serà `innovatech11.test`.
<img width="616" height="295" alt="image" src="https://github.com/user-attachments/assets/d9636b01-5d45-41a5-b627-08d17c560bb0" />

<img width="613" height="294" alt="image" src="https://github.com/user-attachments/assets/2745dd06-bc88-4d9d-9603-59d5f2db474e" />

## 🔐 1.2 Connexió al servidor via SSH

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
## 🧾 1.3 Configuració del hostname i /etc/hosts abans de començar

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
- El segon mostra el domini (server.innovatechXX.test)
<img width="288" height="77" alt="image" src="https://github.com/user-attachments/assets/a7b76af2-bca7-457f-80f6-2c7f5e2e4d38" />

---
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


### 1.4 Instalació instal·lació OpenLDAP

Per instal·lar el ldap farem servir la comanda:
```bash
sudo apt install slapd ldap-utils -y
```
<img width="553" height="40" alt="image" src="https://github.com/user-attachments/assets/5fa38e2c-65b1-4d19-8487-06167f70f57d" />

i ens demanarà una contrasenya i posarem:
``
p@ssw0rd
``

Farem una comprovació
```bash
sudo systemctl slapd
```
<img width="974" height="214" alt="image" src="https://github.com/user-attachments/assets/9f61a6cc-6912-452c-a49d-0c77242d8aae" />

Comanda:
```bash
sudo slapcat
```
<img width="801" height="275" alt="image" src="https://github.com/user-attachments/assets/a855d5b8-2d29-4ee0-a8cd-0f232a58bc2f" />


## 🏗️  Configuració del Directori

### 1.5 Crear fitxers LDIF per a les OUs

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


### 1.6 Afegir les OUs al directori

Executa:
```bash
ldapadd -x -D "cn=admin,dc=innovatechXX,dc=test" -W -f OU_Usuaris.ldif
ldapadd -x -D "cn=admin,dc=innovatechXX,dc=test" -W -f OU_Grups.ldif
```

### 1.7 Comprovar la configuració

Utilitza:

```bash
sudo slapcat
```
Això mostrarà el contingut actual de la base de dades LDAP, incloent les OUs creades.

---
[Tornar enrere](Documentacio.md)
