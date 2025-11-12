# 🛠️ Guia d'Implementació OpenLDAP per Innovatech

## Introducció
Aquesta guia proporciona un recorregut complet per a la implementació d’un entorn LDAP en sistemes Linux, ideal per a pràctiques de xarxes i administració de sistemes. L’objectiu és desplegar un servidor OpenLDAP en Ubuntu Server, configurar-lo correctament i integrar-lo amb un client Ubuntu Desktop (o derivats com Zorin OS), permetent l’autenticació centralitzada d’usuaris.
Durant el procés aprendràs a:

Instal·lar i configurar OpenLDAP en un servidor Ubuntu, incloent la definició del hostname, la configuració de xarxes i la creació d’unitats organitzatives (OUs).
Integrar LDAP amb LAM (LDAP Account Manager) per gestionar usuaris i grups de manera gràfica.
Configurar un client Linux perquè utilitzi LDAP per a l’autenticació, mitjançant mòduls PAM i NSS.
Realitzar comprovacions per assegurar la correcta comunicació entre servidor i client.

Aquest document està pensat per a entorns virtualitzats amb xarxes NAT (per accés a Internet) i Host-Only (per comunicació interna). Cada pas inclou comandes, captures i indicacions pràctiques per facilitar la implementació.
