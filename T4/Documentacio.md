# 🛠️ Guia d'Implementació OpenLDAP per Innovatech

## Introducció
Aquesta guia proporciona un recorregut complet per a la implementació d’un entorn LDAP en sistemes Linux, ideal per a pràctiques de xarxes i administració de sistemes. L’objectiu és desplegar un servidor OpenLDAP en Ubuntu Server, configurar-lo correctament i integrar-lo amb un client Ubuntu Desktop (o derivats com Zorin OS), permetent l’autenticació centralitzada d’usuaris.
Durant el procés aprendràs a:

Instal·lar i configurar OpenLDAP en un servidor Ubuntu, incloent la definició del hostname, la configuració de xarxes i la creació d’unitats organitzatives (OUs).
Integrar LDAP amb LAM (LDAP Account Manager) per gestionar usuaris i grups de manera gràfica.
Configurar un client Linux perquè utilitzi LDAP per a l’autenticació, mitjançant mòduls PAM i NSS.
Realitzar comprovacions per assegurar la correcta comunicació entre servidor i client.

Aquest document està pensat per a entorns virtualitzats amb xarxes NAT (per accés a Internet) i Host-Only (per comunicació interna). Cada pas inclou comandes, captures i indicacions pràctiques per facilitar la implementació.

## Índex:


### [1.Instal·lació del Servei OpenLDAP](Part1.md)
- 1.1 Preparació de la Infraestructura
- 1.2 Connexió al servidor via SSH
- 1.3 Configuració del hostname i /etc/hosts
- 1.4 Instal·lació d’OpenLDAP
- 1.5 Creació de fitxers LDIF per a les OUs
- 1.6 Afegir les OUs al directori
- 1.7 Comprovació de la configuració


### [2.Instal·lació i Configuració de LAM](Part2.md)
- 2.1 Instal·lació del Gestor d’Usuaris LDAP (LAM)
- 2.2 Accés remot i configuració inicial
- 2.3 Ajustaments generals i configuració per defecte
- 2.4 Creació de grups i usuaris


### [3.Integració de Client (Ubuntu Desktop)](Part3.md)
- 3.1 Instal·lació del client
- 3.2 Resolució de noms
- 3.3 Instal·lació dels mòduls necessaris (libpam, nss)
- 3.4 Comprovació de connexió LDAP
3.5 Configuració de PAM i NSS
3.6 Validació i inici de sessió amb usuaris LDAP
