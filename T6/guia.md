# Diagnosi de Noms (Auditoria amb CLI) - Entorn Linux

## Entorn de treball
- Sistema operatiu: **Zorin OS (Linux)**
- Eines utilitzades: `dig`, `nslookup` (mode interactiu)

---

## A. Diagnosi Avançada amb `dig` (Linux)

### 1. Consulta Bàsica de Registre A
**Comanda:**
```bash
dig xtec.cat A
```
<img width="607" height="386" alt="image" src="https://github.com/user-attachments/assets/8e73d6b7-44a8-43ea-af33-d7cf7ce4de6d" />

Resultats:
- IP: 83.247.151.214
- TTL: 3180 segons
- Servidor: 127.0.0.53
- Estat: NOERROR

Anàlisi:

El domini xtec.cat té un registre A que apunta a la IP pública indicada. El TTL (3180 segons) indica que la resposta pot ser cachejada durant uns 53 minuts, cosa que ajuda a reduir càrrega en els servidors DNS. El servidor que ha respost és el DNS local (127.0.0.53), habitual en sistemes Linux amb systemd-resolved.

---
### 2. Consulta de Servidors de Noms (NS)

Comanda:

```bash
dig tecnocampus.cat NS
```
<img width="648" height="432" alt="image" src="https://github.com/user-attachments/assets/85aae03f-a24e-4316-ab2f-80b106caa039" />

Resultats:

- ns-130.awsdns-16.com
- ns-1689.awsdns-19.co.uk
- ns-535.awsdns-02.net
- ns-1071.awsdns-05.org
- TTL: 85881 segons

Anàlisi:

El domini tecnocampus.cat utilitza servidors autoritatius d’AWS Route 53. El TTL és molt alt (gairebé 24 hores), cosa que indica que la informació es manté estable i pot ser cachejada durant molt temps. Això és habitual en dominis amb infraestructura cloud.

### 3. Consulta Detallada SOA

```bash
dig escolapia.cat SOA
```
<img width="647" height="439" alt="image" src="https://github.com/user-attachments/assets/55e4174c-b44e-41ef-ad8f-09467cf0d26c" />

Resultats:

- Servidor SOA: dns1.nominalia.com
- Correu administrador: root.dns1.nominalia.com
- Número de sèrie: 1761028965
- TTL: 900 segons

Anàlisi:

El registre SOA indica el servidor principal de la zona i el correu de contacte per incidències. El número de sèrie serveix per controlar actualitzacions de la zona. El TTL és curt (900 segons), cosa que permet actualitzacions ràpides si hi ha canvis.

### 4. Consulta de Resolució Inversa

```bash
dig -x 147.83.2.135
```
<img width="647" height="409" alt="image" src="https://github.com/user-attachments/assets/3dcced44-e57a-47ca-acbf-b14b53e4c291" />

Anàlisi:
La IP 147.83.2.135 té múltiples registres PTR associats a dominis de la UPC. Això indica que és un servidor amb diversos serveis o webs. El TTL és d’una hora, cosa que és habitual per registres PTR.

## B. Comprovació amb nslookup

### 1. Consulta Bàsica no Autoritativa

```bash
nslookup
> set type=A
> tecnocampus.cat
```
<img width="344" height="288" alt="image" src="https://github.com/user-attachments/assets/b43ed551-e550-4d07-8451-a312dc0b35cd" />

Resultats:

Noms associats:

- www.upc.es
- masters.upc.edu
- edicioweb.produccio.upc.edu
- saladepensa.upc.edu
- barcelonatech.upc.edu
- barcelonatech-upc.eu
- upc.cat
- upc.edu


TTL: 3600 segons

Anàlisi:

La resposta és no autoritativa perquè prové d’un servidor DNS intermediari (normalment el DNS local o del proveïdor), no del servidor autoritatiu del domini.

### 2. Consulta Autoritativa
```bash
> server [IP del servidor NS]
> set type=A
> tecnocampus.cat
```
<img width="332" height="314" alt="image" src="https://github.com/user-attachments/assets/67f54b9d-19ab-470c-ac9e-8c58b96e24d1" />

Anàlisi:

La resposta és autoritativa perquè prové directament d’un servidor de noms autoritatiu. Això garanteix que la informació és oficial i actual.

## C. Resolucions Locals

Fitxer: /etc/hosts
Comanda:
```bash
sudo nano /etc/hosts
```
Exemple:

<img width="639" height="208" alt="image" src="https://github.com/user-attachments/assets/a3e17a00-c47a-42be-8a57-c30fa4622c11" />


``
127.0.0.1    servidorlocal.test
``
Comanda:

```bash
ping (Nom del teu server).test
```
Anàlisi:

El sistema resol correctament el nom sense consultar DNS externs, cosa útil en entorns locals o per proves de desenvolupament.
