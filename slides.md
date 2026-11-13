---
marp: true
theme: default
style: |
  section {background-color: #121114}
  h1,h2,h3 {color: #8393f0}
  p,ul,li,td,th {color: #ccc}
  section table {font-size: 0.85em}
  section table td {background-color: #121114}
  section table th {background-color: #272133; font-weight: bolder}
  pre {background-color: #17151a; color: #ccc}
  blockquote {border: 2px green solid; border-left-width: 15px; padding: 0.5em 15px;font-style: italic }
paginate: true
header: "Active Directory, DNS et DHCP"
footer: "![height:20px](https://raw.githubusercontent.com/DiginamicInternal/PublicAssets/refs/heads/main/Logo-diginamic-color-blk.png)"
---

# Active Directory, DNS et DHCP

### Les trois services socles du réseau d'entreprise

Nicolas SAHUC

---

## 🎯 Objectifs pédagogiques

1. Expliquer le rôle d'Active Directory et d'un annuaire
2. Décrire le contrôleur de domaine
3. Présenter LDAP
4. Expliquer la résolution de noms, de NetBIOS à DNS
5. Décrire l'échange DHCP et le bail

---

## Au démarrage d'un poste

1. **DHCP** : « quelle est ma configuration IP ? »
2. **DNS** : « où est mon contrôleur de domaine ? »
3. **AD** : « voici qui je suis » → accès accordé

> Sans ces trois services, rien ne fonctionne.

---

# 1. Active Directory

---

## Un annuaire LDAP pour Windows

- Ancien nom : **NTDS** (*NT Directory Services*)
- Créé par Microsoft en 1996, livré avec Windows Server depuis 2000
- Identification et authentification **centralisées**
- Centralise **ressources**, **utilisateurs** et **services**

---

## Intérêts d'un annuaire

- Administration **centralisée** et simplifiée
- Authentification **unifiée**
- **Identification** unique de chaque objet
- **Référencement** des utilisateurs, groupes et ordinateurs

---

## Le contrôleur de domaine

Authentifie utilisateurs et postes, valide leurs accès.

| ✔ | ✘ |
|---|---|
| Gestion centralisée | Cible privilégiée des attaques |
| Partage de ressources | Réseau dépendant de sa disponibilité |
| Redondance si plusieurs DC | Exigences matérielles |

> Toujours au moins **deux** DC.

---

## LDAP

- Protocole standard d'accès aux annuaires
- **389/TCP** (LDAP) · **636/TCP** (LDAPS, chiffré)
- Contenu : UO, utilisateurs, ordinateurs, groupes, DC, serveurs, imprimantes, GPO
- Chaque objet porte des **attributs** et leurs valeurs

---

# 2. DNS

---

## Pourquoi résoudre des noms ?

On ne retient pas des adresses IP : on retient des **noms**.

| | NetBIOS | DNS |
|---|---|---|
| Structure | plate | hiérarchique |
| Résolution | broadcast | serveur |
| Portée | LAN | Internet |
| Noms | 16 caractères | 253 caractères |

---

## Comment fonctionne DNS

1. Le client demande au serveur DNS l'IP de `google.fr`
2. Le serveur répond avec l'adresse
3. Le client contacte directement cette adresse

Composants : un **serveur** DNS, un **client** DNS

> Diagnostic : `nslookup google.fr`

---

# 3. DHCP

---

## L'échange DORA

1. **D**iscover — le client crie en broadcast
2. **O**ffer — le serveur propose une configuration
3. **R**equest — le client l'accepte
4. **A**ck — le serveur la réserve

IP, masque, passerelle, DNS : tout arrive automatiquement.

---

## Le bail

- La configuration est réservée pour une **durée** fixée sur le serveur
- Le client la renouvelle avant échéance
- `ipconfig /release` puis `ipconfig /renew` pour rejouer DORA

---

# Des questions ?

Pour toute question [adressez-vous au service pédagogie](mailto:pedagogie@diginamic.fr)
