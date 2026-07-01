# 🚀 Lab d'Administration Système & Analyse Réseau
> **Titre :** Minilab 
> **Auteur :** Evan Bonnal, Natalia Giraldo, Ludovic Dos Santos    
> **Formation :**  Bachelor IT en Cyber     
> **Période :** 15 juin 2026 – 3 juillet 2026 (3 semaine)  
> **Établissement :** La Plateforme_


---

# 🛡️ Infrastructure Sécurisée : LDAP / NFS / MFA & Réseau Cisco

![Debian](https://img.shields.io/badge/OS-Debian%20Linux-A81D33?style=for-the-badge&logo=debian)
![Security](https://img.shields.io/badge/Security-MFA%20%2F%20TOTP-4CAF50?style=for-the-badge&logo=security)
![Network](https://img.shields.io/badge/Network-NFS%20%2F%20LDAP-00599C?style=for-the-badge)
![Cisco](https://img.shields.io/badge/Hardware-Cisco%20Aironet-1BA0D7?style=for-the-badge&logo=cisco)

## 📝 Contexte du Projet

Ce dépôt documente la conception, le déploiement et la sécurisation d'une infrastructure réseau d'entreprise complète. L'objectif principal est de fournir une gestion centralisée des identités et du stockage, tout en imposant un niveau de sécurité maximal (Zero Trust partiel) via l'Authentification Multi-Facteurs (MFA) sur tous les points d'entrée critiques (SSH, Webmin).

Ce projet a été réalisé dans le cadre de mon cursus à **LaPlateforme.io** 

## 🏗️ Architecture du Laboratoire

L'environnement est virtualisé et segmenté pour reproduire une architecture de production :

* **Passerelle (.254) :** Point d'entrée réseau, serveur NFS (Stockage des clés de sécurité).
* **Master (.253):** Serveur d'annuaire LDAP principal.
* **Slave (.252) / Client (.101) :** Machines clientes liées à l'annuaire et au stockage partagé.


## 🔑 Fonctionnalités Principales & Sécurité

### 1. Gestion Centralisée (LDAP & NFS)
* Déploiement d'un annuaire LDAP (`nslcd`, `libpam-ldapd`) pour l'authentification unifiée.
* Partage réseau NFSv3/NFSv4 avec gestion stricte des privilèges (`no_root_squash`) et droits de traversée (`chmod 755`).

### 2. Durcissement de l'Authentification (MFA / TOTP)
* **SSH & PAM :** Configuration du démon OpenSSH en mode `keyboard-interactive` pour forcer l'usage du module `pam_google_authenticator.so`.
* **Isolation des privilèges :** Délégation de la lecture/écriture des secrets TOTP à l'utilisateur `root` au travers du réseau NFS pour éviter les conflits d'UID LDAP.
* **Webmin :** Sécurisation de l'interface d'administration web via TOTP Authenticator.

## 🚀 Évolutions Envisagées

Afin d'améliorer la résilience et les services de cette infrastructure, les axes d'évolution suivants sont documentés :
1.  **Serveur d'impression centralisé :** Déploiement de CUPS interfacé avec LDAP pour la gestion des quotas utilisateurs.
2.  **Infrastructure as Code (IaC) & Backups :** Sauvegarde des configurations critiques (`/etc/`) via Etckeeper et automatisation par scripts Bash/Python.
3.  **Haute Disponibilité & PRA :** Duplication des données NFS critiques vers un NAS local via `rsync` et externalisation Cloud chiffrée via `rclone`.

## 🛠️ Stack Technique

* **Système :** Debian GNU/Linux
* **Services :** OpenLDAP, NFS-Kernel-Server, OpenSSH, Webmin,
* **Sécurité :** PAM (Pluggable Authentication Modules), Google Authenticator (TOTP), iptables
* **Scripting :** Bash

---

## 🤝 Équipe

<table>
  <thead>
    <tr>
      <th>Avatar</th>
      <th>Membre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
         <img src="https://github.com/evanbonnal.png?size=32" alt="Evan Bonnal" style="width:40px; height:40px; border-radius:4px;" />
      </td>
      <td><strong><a href="https://github.com/evanbonnal">Evan Bonnal</a></strong></td>
    </tr>
    <tr>
      <td align="center">
        <img src="https://github.com/Natalia-Giraldo.png?size=32" alt="Natalia Giraldo" style="width:40px; height:40px; border-radius:4px;" />
      </td>
      <td><strong><a href="https://github.com/Natalia-Giraldo">Natalia Giraldo</a></strong></td>
    </tr>
    <tr>
      <td align="center">
        <img src="https://github.com/ludovicdos-santos-io.png?size=32" alt="Alexandre Berdejo" style="width:40px; height:40px; border-radius:4px;" />
      </td>
      <td><strong><a href="https://github.com/ludovicdos-santos-io">Ludovic Dos Santos</a></strong></td>
    </tr>
    <tr>
  </tbody>
</table>
