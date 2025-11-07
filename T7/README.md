# T07: Instal·lant un servidor de noms 🖧🔧

## Breu descripció

Després de l’exitosa experiència a nivell de formació, els clients de **Digicore** estan tan satisfets amb la nostra feina que ens encarreguen la **implantació des de zero dels seus serveis de DNS interns**.

Actualment, l'agència fa servir **adreces IP** per accedir als seus servidors de desenvolupament, bases de dades i eines de gestió interna. Aquest mètode és:

- ❌ Ineficient
- ❌ Propens a errors
- ❌ Poc professional

### Problemes detectats

- **Usabilitat deficient**: Els empleats han de memoritzar IPs com `192.168.10.25`.
- **Manteniment feixuc**: Canvis d’IP requereixen actualitzacions manuals.
- **Manca de professionalitat**: Els serveis haurien de ser accessibles amb noms clars com `bbdd.digicore.lan`.

---

## 🎯 Objectiu

Implementar un **Sistema de Noms de Domini (DNS)** intern robust amb **BIND9** en Linux.

Els serveis i aplicacions de l’agència han de ser accessibles mitjançant **noms de domini amigables**, com:

- `bbdd.digicore.lan`
- `wiki.digicore.lan`

---

## 🔨 El vostre repte

Instal·lar i configurar un **servidor DNS primari (màster)** amb BIND9 en un sistema Linux.

### Domini de prova

Utilitzeu el domini: `digicore-XX.test`  
(on `XX` és el vostre número de llista)

---

## 🖥️ Pas previ

- Configurar una màquina virtual **Ubuntu Server** amb:
  - 4 GB de RAM
  - 20 GB de disc
  - Interfície en **adaptador pont** i una altra en **host-only**
- Instal·lar:
  - `bind9`
  - Servei `ssh` per exportar arxius al vostre repositori GitHub

---

## 📋 Accions a realitzar

1. **named.conf.options**  
   - Acceptar consultes recursives de la xarxa local  
   - Usar com reenviador la IP `8.8.8.8`  
   - Mostrar captura i estat del servei

2. **Client Zorin OS**  
   - Canviar adaptador a **pont**  
   - Configurar DNS amb la IP del servidor  
   - Comprovar resolució a Internet (`dig google.com`)

3. **named.conf.local**  
   - Definir dues zones:
     - Zona directa: `digicore-XX.test`
     - Zona inversa: xarxa local

4. **Zona directa**  
   - Crear carpeta `/etc/bind/zones`  
   - Crear arxiu copiant `db.local`  
   - Configurar amb:
     - SOA
     - NS
     - Registre A: `server` amb IP del servidor
     - Registre A: `dbserver` amb IP del client
     - CNAME: `data` apuntant a `dbserver`

5. **Zona inversa**  
   - Crear arxiu copiant `db.127`  
   - Configurar amb:
     - SOA i NS
     - Registres PTR per `server` i `dbserver`

6. **Comprovacions**  
   - Reiniciar servei  
   - Fer consultes directes i inverses des del client

7. **Transferència de zona**  
   - Permetre transferència de la zona directa  
   - Configurar zona secundària del domini d’un company  
   - Forçar transferència i comprovar funcionament

---

## 🧪 Activitat d’avaluació

Per demostrar la vostra competència tècnica:

- Superar una **avaluació pràctica** al final del repte
- Només podreu usar un **full manuscrit** amb anotacions pròpies
- El full s’haurà de **lliurar** en finalitzar la prova

---
[Tornar a la pagina principal](../README.md)
