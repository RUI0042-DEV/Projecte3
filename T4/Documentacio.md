
# 🛠️ Guia d'Implementació OpenLDAP per Innovatech

## 🔧 1. Preparació de la Infraestructura

- Nom de màquina del servidor: `server.innovatechXX.test`
- Xarxa NAT per accés a Internet
- Xarxa Host-Only per comunicació amb el client ("*Adaptador de nómes l'amfitrió*")
> 📌 **Important**: Substitueix `XX` pel teu número de llista.  
> Exemple: Si ets el número **11**, el domini serà `innovatech11.test`.
<img width="616" height="295" alt="image" src="https://github.com/user-attachments/assets/d9636b01-5d45-41a5-b627-08d17c560bb0" />

<img width="613" height="294" alt="image" src="https://github.com/user-attachments/assets/2745dd06-bc88-4d9d-9603-59d5f2db474e" />

---

## 🔐2. Connexió al servidor via SSH

Abans de començar qualsevol tasca, connecta't al servidor Ubuntu Server mitjançant SSH des de la màquina física o client.

```bash
ssh usuari@IP_del_servidor

---
## 📦 3. Instal·lació del Servei OpenLDAP
```bash
sudo apt update
sudo apt install slapd ldap-utils
