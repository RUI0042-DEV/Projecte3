## 👥 2. Instal·lació i Configuració de LAM

### 2.1 Instal·lació del Gestor d'Usuaris LDAP (LAM)

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
### 2.3 Configuració per defecte

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

### 2.4 Creació de Grups i Usuaris

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

---
[Tornar enrere](Documentacio.md)
