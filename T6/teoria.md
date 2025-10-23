# 🌐 Guia Formativa: Fonaments del Sistema de Noms de Domini (DNS)

### 🎯 Objectiu de la Sessió
Aquesta sessió té com a finalitat que els participants comprenguin el funcionament bàsic del DNS, la seva estructura jeràrquica, els tipus de consultes i registres, així com conceptes essencials relacionats amb la resolució de noms.

---

### 📚 Què és el DNS?
El **Sistema de Noms de Domini (DNS)** és com la "guia telefònica d'Internet". Tradueix noms de domini llegibles per humans (com `www.exemple.cat`) a adreces IP numèriques (com `192.168.1.1`) que entenen els ordinadors. Sense el DNS, hauríem de recordar números IP per accedir a cada lloc web! 🧠💭

---

### 🏗️ Jerarquia i Estructura del DNS
El DNS està organitzat de manera jeràrquica en forma d'arbre invertit:

**🌳 Arrel (Root ".")**
- Punt superior de l'estructura DNS
- Conté informació sobre tots els TLDs del món
- Gestionat pels 13 servidors arrel globals

**🏢 Dominis de Nivell Superior (TLDs)**
- **Genèrics**: `.com`, `.org`, `.net`, `.edu`
- **Geogràfics**: `.es`, `.cat`, `.fr`, `.uk`
- **Nous gTLDs**: `.tech`, `.shop`, `.barcelona`
- Cada TLD té els seus propis servidors autoritatius

**🏠 Segon Nivell i Subdominis**
- Noms registrats sota un TLD: `empresa.cat`, `google.com`
- Subdominis: `mail.empresa.cat`, `shop.empresa.cat`
- Gestionats pels propietaris del domini o els seus proveïdors

Aquesta jerarquia permet que el sistema sigui escalable i fàcilment administrable a nivell mundial. 🌍

### 🌳 Explicació de jerarquia i estructura del dns

1. **Root (Arrel)**  
   - No sap les adreces IP finals.  
   - Sap **quins servidors TLD** (els de l’extensió `.com`, `.cat`, `.es`...) poden tenir la resposta.  
   - Et diu a quin servidor preguntar després.

2. **TLD (Dominis de Nivell Superior)**  
   - Coneix **quins servidors autoritatius** gestionen cada domini concret.  
   - Per exemple, si busques `empresa.cat`, el servidor del `.cat` et diu quin servidor autoritatiu sap la informació per a `empresa.cat`.

3. **Servidor autoritatiu del domini**  
   - Aquest **sí que conté els registres amb les IPs reals** (A, MX, etc.) del domini.  
   - Retorna l’adreça IP exacta del nom que has buscat.

4. **Client o navegador**  
   - Rep la resposta final amb la IP.  
   - Ja pot connectar-se directament al servidor web corresponent i mostrar-te la pàgina. 🌐


---

### 🔍 Procés de Resolució
Quan un usuari escriu un nom de domini en un navegador, s'inicia un procés de resolució per trobar l'adreça IP associada:

**🔄 Consulta iterativa**
- El servidor DNS respon amb l'adreça d'un altre servidor fins que el client troba la resposta final
- El client fa múltiples peticions seguint les referències

**🎯 Consulta recursiva**
- El servidor DNS fa totes les consultes necessàries i retorna el resultat final al client
- Més còmoda per al client però més càrrega per al servidor

**🌐 Servidors d'arrel (Root Servers)**
- Contenen informació sobre els TLDs
- Dirigeixen les consultes cap als servidors corresponents
- Hi ha 13 servidors arrel distribuïts mundialment

**👑 Servidors autoritatius**
- Guarden els registres DNS oficials per a un domini concret
- Tenen la resposta definitiva per a les consultes del seu domini

### 🔍 Procés de Resolució explicat

El DNS funciona fent preguntes de manera **jeràrquica** fins a trobar la IP que busca:

1. Primer, el **servidor DNS** del client fa una consulta.  
2. Aquest **pregunta al servidor Root**, que no sap la IP, però sap **a quin TLD ha de preguntar**.  
3. Després, **el servidor TLD** (com `.cat`, `.com`, `.es`) indica **quin servidor autoritatiu** té la informació.  
4. A continuació, **el servidor autoritatiu** retorna **la IP exacta** del domini.  
5. Finalment, el client **rep la IP** i pot accedir a la pàgina web. 🌐


---

### 🗂️ Tipus de Zones DNS (explicat fàcil)

Una "zona" DNS és com un **conjunt d'informació sobre noms i adreces** que té un servidor específic. És una manera d'organitzar qui té l'autoritat sobre quina part del sistema DNS.

**Hi ha diferents tipus de zones:**

1. **Zona directa**
   - Serveix per traduir noms de domini a adreces IP.
   - Exemple: `www.empresa.cat` → `192.168.1.100`
   - Sempre que escrivim una web al navegador, consultem la "zona directa" per saber la IP.

2. **Zona inversa**
   - Serveix per traduir una adreça IP a un nom de domini.
   - Exemple: `192.168.1.100` → `www.empresa.cat`
   - És útil per validar que una IP correspon a un domini concret.

3. **Zona primària**
   - És **l'original**, on es fan i s'emmagatzemen els canvis de configuració.
   - El servidor que té la zona primària és qui 'mana' per aquella zona.

4. **Zona secundària**
   - És una **còpia de la zona primària**.
   - Serveix per seguretat o per repartir la càrrega.
   - Si un servidor cau, la zona secundària pot respondre igualment, així no es perd el servei.

---

### 📝 Tipus de Registres Clau (Records)
Cada domini conté diversos tipus de registres que defineixen el seu comportament dins la xarxa:

**🎯 A (Address)**
- Associa un nom de domini amb una adreça IPv4
- Exemple: `web.empresa.cat` → `192.168.1.50`

**🔗 CNAME (Canonical Name)**
- Defineix un àlies per a un altre nom de domini
- Exemple: `www.empresa.cat` apunta a `web.empresa.cat`

**📧 MX (Mail Exchange)**
- Indica els servidors de correu associats al domini
- Inclou prioritat per ordenar els servidors

**🌐 NS (Name Server)**
- Especifica quins servidors són autoritatius per a la zona
- Defineix qui té autoritat sobre el domini

**⚙️ SRV (Service)**
- Defineix serveis específics (VoIP, LDAP) i els seus ports
- Inclou prioritat, pes, port i servidor

---

### ⭐ Conceptes Essencials

**✅ Resposta autoritativa**
- Es dona quan la resposta prové directament d'un servidor autoritatiu
- És fiable i oficial, no provê de memòria cau

**⏰ Time To Live (TTL)**
- Indica quant temps pot una resposta ser desada en memòria cau
- Valor alt: millor rendiment, propagació més lenta
- Valor baix: propagació ràpida, més tràfic de xarxa

**👑 Start of Authority (SOA)**
- Conté informació essencial de la zona
- Inclou: servidor principal, correu del responsable, número de sèrie, intervals de refresc

**📡 Reenviadors**
- **Incondicionals**: Totes les consultes es reenvien a un servidor específic
- **Condicionals**: Només es reenvien consultes de certs dominis específics

**🏠 Resolució local (mDNS)**
- Permet que equips dins una mateixa xarxa es resolguin noms directament
- No necessita servidor DNS central
- Utilitza el protocol Multicast DNS per a xarxes locals

### 🏠 Resolució local (mDNS)

La **resolució local** és un mecanisme que permet als dispositius d’una mateixa xarxa trobar-se entre ells **sense utilitzar un servidor DNS extern**.

Això és especialment útil en xarxes petites (com les de casa o d’una oficina) on no hi ha un servidor DNS propi.

**Com funciona:**

- Cada equip envia un missatge a tota la xarxa local (amb el protocol *Multicast DNS* o **mDNS**).  
- Els altres equips responen si el nom coincideix amb el seu.
- D’aquesta manera, poden resoldre noms de dispositius com `impressora.local` o `portatil.local` sense necessitat d’un servidor DNS.

**Exemple pràctic:**  
Quan connectes una impressora Wi-Fi o un altaveu intel·ligent a la xarxa i pots escriure només `impressora.local`, el teu dispositiu l’està trobant gràcies al protocol mDNS. 🌐📡

