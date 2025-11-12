# 📦 Instal·lació del Servei OpenLDAP
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
- El segon mostra el domini (server.innovatechXX.test)
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
