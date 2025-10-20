# 🔐 Informe Tècnic: Gestió de Contrasenyes

## 1. 🛡️ Justificació

Les contrasenyes febles o reutilitzades exposen l’empresa a atacs com el diccionari o el credential stuffing. Un gestor de contrasenyes permet generar claus fortes, evitar reutilitzacions i emmagatzemar-les de forma segura, reduint el risc humà.

## 2. 📊 Comparativa Tècnica

| Característica         | Bitwarden (Online ☁️)                        | KeePassXC (Offline 💻)                      |
|------------------------|----------------------------------------------|--------------------------------------------|
| Seguretat              | Xifratge end-to-end 🔒                       | Xifratge local (fitxer KDBX) 🔐             |
| Emmagatzematge         | Núvol                                        | Local                                       |
| Sincronització         | Automàtica 🔄                                 | Manual 🧍                                   |
| Accés                  | Web, mòbil, escriptori 📱🖥️                  | Escriptori 🖥️                               |
| Cost                   | Gratuït amb opcions de pagament 💳           | Totalment gratuït 🆓                        |
| Open Source            | Sí 🧑‍💻                                       | Sí 🧑‍💻                                     |
| Portabilitat           | Alta via núvol                               | Alta via fitxer                            |

## 3. ⚖️ Pros i Contres

**Bitwarden**  
Avantatges:  
– Fàcil d’utilitzar i accessible des de qualsevol dispositiu.  
– Sincronització automàtica molt útil per equips en mobilitat.  
– Possibilitat d’autohosting per més control intern.

Inconvenients:  
– Requereix connexió a Internet per sincronitzar.  
– Algunes funcions avançades són de pagament.

**KeePassXC**  
Avantatges:  
– Control total de les dades, sense dependència externa.  
– Ideal per entorns amb polítiques de seguretat estrictes.  
– Compatible amb sistemes de còpia local o sincronització privada.

Inconvenients:  
– Sincronització manual, menys pràctica per a equips.  
– Interfície menys intuïtiva per a usuaris no tècnics.  
– Risc de pèrdua si no es fan còpies del fitxer.

## 4. ✅ Recomanació

Es recomana **Bitwarden** per al personal tècnic, ja que ofereix una bona combinació de **seguretat, comoditat i escalabilitat**. KeePassXC pot complementar en entorns molt restringits, però Bitwarden és més pràctic per al dia a dia.
