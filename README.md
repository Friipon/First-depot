# First-depot
Premier dépôt GitHub

Ceci est un test README sur GitHub

## Configuration


Cybersphère Services — Infrastructure virtualisée sur Hyper-V

Projet annuel de deuxième année de Bachelor Cybersécurité, parcours Administration systèmes et réseaux, réalisé par **Christophe Trouvé** à **Nexa Digital School** (2025–2026).

Le projet porte sur la conception d’une infrastructure informatique locale pour Cybersphère Services, une entreprise de services numériques fictive. La maquette centralise la gestion des comptes et des fichiers, héberge un annuaire interne et prévoit la supervision des services essentiels.

## Architecture cible

La maquette repose sur six machines virtuelles hébergées sur **Microsoft Hyper-V**. Le pare-feu **pfSense** assure le routage, le NAT et le filtrage entre le WAN, le LAN (`192.168.50.0/24`) et la DMZ (`192.168.200.0/24`).

| Machine | Système | Zone | Rôle |
| --- | --- | --- | --- |
| pfSense | pfSense | WAN, LAN, DMZ | Pare-feu, routage et NAT |
| `SRV-AD-01` | Windows Server | LAN | Active Directory, DNS, DHCP et partages de fichiers |
| `WEB-SRV` | Windows Server | DMZ | Hébergement de l’intranet avec IIS et PHP |
| `DB-SRV` | Debian | LAN | Base de données MariaDB |
| `CLI-WIN10` | Windows 10 | LAN | Poste client joint au domaine `b2.cyber.local` |
| `KALI-SRV` | Debian | LAN | Supervision des hôtes et services avec Zabbix |

Dans l’architecture cible, le poste client accède à l’intranet dans la DMZ. Le serveur web dispose d’une règle de pare-feu dédiée pour interroger MariaDB. Les autres connexions initiées depuis la DMZ vers le LAN sont bloquées par défaut.

## Intranet et administration

- **Annuaire interne** — Une page PHP lit la table `employes` dans la base MariaDB `intranet_cs` et affiche le nom, le prénom, le service et l’adresse e-mail. Le compte SQL de l’application dispose uniquement des droits de lecture nécessaires.
- **Gestion des accès** — Active Directory organise les utilisateurs par service. Les groupes de sécurité gèrent les droits d’accès aux partages, et les stratégies de groupe (GPO) appliquent les paramètres aux postes du domaine.
- **Sauvegardes** — Un script PowerShell automatise la copie horodatée des partages et journalise les opérations. Le scénario prévoit une exécution via le Planificateur de tâches Windows.
- **Supervision et maintenance** — Zabbix suit la disponibilité des hôtes et services, ainsi que l’utilisation du processeur, de la mémoire et de l’espace disque. Le plan de maintenance couvre la revue des alertes, les mises à jour et les tests de restauration.

## État du projet

Le déploiement est resté partiel à la remise du dossier en raison de l’instabilité de certaines machines virtuelles et de dysfonctionnements logiciels. Le rapport présente les choix de conception et les vérifications fonctionnelles, notamment la connexion au domaine, la résolution DNS, l’accès aux partages et la consultation de l’intranet. Certaines captures illustrent le résultat attendu à partir d’environnements de démonstration.
