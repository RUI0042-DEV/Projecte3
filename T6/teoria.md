# 🌐 Què és el DNS?

El **DNS (Domain Name System)** és un sistema que permet traduir noms de domini (com `www.google.com`) en adreces IP (com `142.250.184.196`). Això és necessari perquè els ordinadors i servidors d’Internet utilitzen adreces IP per comunicar-se entre ells, però les persones trobem molt més fàcil recordar noms que números.

## 🔁 Com funciona el DNS?

Quan escrius una adreça web al navegador, per exemple `www.google.com`, el teu dispositiu no sap automàticament a quin servidor ha d’anar. El que fa és demanar al sistema DNS que li digui quina IP correspon a aquest nom.

**Procés:**
1. El dispositiu envia una consulta DNS amb el nom del domini.
2. El sistema DNS busca la IP associada a aquest nom.
3. Quan la troba, la retorna al dispositiu.
4. El dispositiu utilitza aquesta IP per connectar-se al servidor web i carregar la pàgina.

**Exemple:**

| El que escrius       | El DNS busca       | El dispositiu rep     | Es connecta a         |
|----------------------|--------------------|------------------------|------------------------|
| `www.google.com`     | IP corresponent     | `142.250.184.196`      | servidor de Google     |

---

# 🌳 Estructura jeràrquica del DNS

El DNS està organitzat com un arbre jeràrquic:

- **Root (Arrel)**: El punt inicial. Coneix els servidors dels dominis de primer nivell.
- **TLD (Top-Level Domains)**: Són dominis com `.com`, `.org`, `.cat`, etc.
- **Domini de segon nivell**: Com `google.com`, `universitat.cat`.
- **Subdominis**: Com `mail.google.com`, `blog.universitat.cat`.

---

# 🔍 Tipus de consultes DNS

- **Consulta iterativa**: El dispositiu fa diverses consultes pas a pas fins trobar la IP.
- **Consulta recursiva**: El servidor DNS fa tot el procés per tu i et retorna la resposta final.

---

# 🗂️ Tipus de zones DNS

- **Zona directa**: Traducció de noms a IPs.
- **Zona inversa**: Traducció d’IPs a noms (utilitzada per verificacions).

També hi ha:
- **Zona primària**: Conté la base de dades principal.
- **Zona secundària**: Còpia de la primària, usada per redundància.

---

# 📄 Tipus de registres DNS

- **A**: Associa un nom amb una adreça IPv4.
- **CNAME**: Crea un alias d’un altre nom.
- **MX**: Defineix el servidor de correu.
- **NS**: Indica els servidors autoritatius d’una zona.
- **SRV**: Defineix serveis amb port i protocol.

---

# 🧠 Conceptes essencials

- **Resposta autoritativa**: Prové d’un servidor que té autoritat sobre el domini.
- **TTL (Time To Live)**: Temps que una resposta DNS pot estar en memòria cau.
- **SOA (Start of Authority)**: Registre que conté informació essencial sobre la gestió d’una zona DNS.

---

# 🔁 Reenviadors DNS

- **Condicionals**: Reenvien consultes només per a dominis específics.
- **Incondicionals**: Reenvien totes les consultes que no poden resoldre.

---

# 🖧 Resolució local i mDNS

- **Fitxer hosts**: Permet associar noms a IPs localment, sense servidor DNS.
- **mDNS (Multicast DNS)**: Utilitzat en xarxes locals per descobrir dispositius com impressores o altaveus, amb noms com `impresora.local`.
