# Cartographie des menaces sur le secteur aérien avec MITRE ATT&CK

**Windows est la cible commune aux 7 groupes étudiés ; les équipements de bordure (VPN, appliances réseau) sont le deuxième vecteur, exploité par 4 d'entre eux.**

Étude des groupes d'attaquants recensés par MITRE ATT&CK qui ciblent l'aviation ou l'aérospatial et sont actifs depuis au moins 2013 : plateformes visées à partir de leurs techniques et outils documentés, puis méthodes de remédiation proposées par MITRE D3FEND.

## Groupes étudiés

| Groupe | Identifiant MITRE |
|---|---|
| [Dragonfly](https://attack.mitre.org/groups/G0035/) | G0035 |
| [Leviathan](https://attack.mitre.org/groups/G0065/) | G0065 |
| [APT33](https://attack.mitre.org/groups/G0064/) | G0064 |
| [menuPass](https://attack.mitre.org/groups/G0045/) | G0045 |
| [APT5](https://attack.mitre.org/groups/G1023/) | G1023 |
| [Axiom](https://attack.mitre.org/groups/G0001/) | G0001 |
| [Threat Group-3390](https://attack.mitre.org/groups/G0027/) | G0027 |

## Plateformes ciblées

✓ = usage observé · (✓) = usage indirect ou non confirmé · vide = aucun usage documenté

| Plateforme | Dragonfly | Leviathan | APT33 | menuPass | APT5 | Axiom | TG-3390 |
|---|---|---|---|---|---|---|---|
| Windows | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Linux / Unix | | ✓ (SSH) | | | ✓ (appliances, cron) | (✓) | ✓ (SysUpdate) |
| Équipements réseau / VPN | ✓ (Citrix, Fortinet) | ✓ (appliances, routeurs SOHO) | | ✓ (Pulse Secure) | ✓ (Pulse Secure, Citrix ADC) | | |
| Hyperviseur ESXi | | | | | ✓ | | |
| Cloud / SaaS (Microsoft 365) | | (✓) | ✓ | | ✓ | | |
| Serveurs Exchange / SharePoint | ✓ (OWA) | | ✓ (Ruler) | | | | ✓ (OwaAuth, CVE SharePoint/Exchange) |
| ICS (systèmes industriels) | ✓ | | ✓ | | | | |
| macOS / mobile | | | | | | | |

Le tableau complet, avec les décomptes calculés par formules, est dans [`plateformes_groupes_aviation.xlsx`](plateformes_groupes_aviation.xlsx).

## Points clés

- **Windows** est la cible commune aux 7 groupes.
- Les **équipements de bordure** (VPN, appliances) sont le deuxième vecteur : 4 groupes, avec APT5 en tête.
- Seuls **Dragonfly et APT33** utilisent des techniques de la matrice **ICS**, ce qui est cohérent avec leur ciblage de l'énergie et de l'aviation.
- **APT5** a la surface d'attaque la plus large : Windows, Linux, VPN, ESXi et Microsoft 365.
- Aucun groupe n'a d'usage documenté contre **macOS ou le mobile** ; seuls certains de leurs outils en ont la capacité.

## Méthode

Les plateformes sont déduites des usages décrits dans les techniques et les logiciels des pages MITRE ATT&CK de chaque groupe (version v19, consultée le 8 octobre 2026). MITRE ne publie pas directement de liste de plateformes ciblées par groupe ; pour une vue officielle, on peut utiliser ATT&CK Navigator en filtrant la couche de chaque groupe par plateforme.

Les méthodes de remédiation ont ensuite été identifiées dans **MITRE D3FEND**, dans les tactiques *Evict* (expulser l'attaquant) et *Restore* (restaurer les systèmes).

## Sources

- [MITRE ATT&CK — Groups](https://attack.mitre.org/groups/)
- [MITRE D3FEND](https://d3fend.mitre.org/)
