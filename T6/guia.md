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

Anàlisi:
- IP de resposta: 83.247.151.214
- TTL: 3180 segons
- Servidor que ha respost: 127.0.0.53
- Estat: NOERROR
---
### 2. Consulta de Servidors de Noms (NS)

Comanda:

```bash
dig tecnocampus.cat NS
```
<img width="648" height="432" alt="image" src="https://github.com/user-attachments/assets/85aae03f-a24e-4316-ab2f-80b106caa039" />

Anàlisi:
- ns-130.awsdns-16.com
- ns-1689.awsdns-19.co.uk
- ns-535.awsdns-02.net
- ns-1071.awsdns-05.org

### 3. Consulta Detallada SOA

```bash
dig escolapia.cat SOA
```
