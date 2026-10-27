# Rapport d'analyse de menace : le groupe ChimeraZ

**Analyse d'une cyberattaque contre une armurerie française et mesures de protection pour une entreprise du même secteur**

*Motivation et démarche de l'attaquant · Mécanismes (MITRE ATT&CK) · Impacts · Recommandations*

| | |
|---|---|
| **Mise en situation** | Data analyst d'une armurerie concurrente, rapport destiné au RSSI |
| **Rédigé par** | Stella Ngalagou |
| **Date** | 9 octobre 2026 |
| **Cadre** | Projet académique, Mastère Spécialisé Expert Big Data (UTT) |

> Le nom et la localisation de l'entreprise victime ont été retirés de cette version publique. L'analyse s'appuie uniquement sur des informations rendues publiques au moment de la revendication.

## Contexte

### Qui a été attaqué ?

La victime est une armurerie française spécialisée dans la chasse et le tir sportif. Elle vend des armes, des munitions et des équipements destinés aux chasseurs et aux tireurs sportifs. Elle s'adresse donc à la même clientèle que notre entreprise et a le même profil d'activité, ce qui fait d'elle un concurrent direct. Elle est soumise aux mêmes obligations réglementaires : elle doit vérifier l'identité de ses clients ainsi que leurs titres et autorisations avant toute vente d'arme, ce qui l'oblige à collecter et conserver des documents particulièrement sensibles.

### Où l'attaque a-t-elle eu lieu ?

Sur le plan géographique, l'entreprise exploite deux points de vente en France ainsi qu'un site marchand.

Sur le plan technique, on ne sait pas encore quel système a été compromis. Plusieurs points d'entrée sont envisagés :

- **le site marchand**, exposé sur Internet et susceptible de contenir des failles ;

- **un espace documentaire** où les clients déposent ou consultent leurs justificatifs ;

- **un compte compromis**, celui d'un salarié ou d'un administrateur, obtenu par hameçonnage ou par réutilisation de mot de passe ;

- **un autre système interne**, comme un serveur de fichiers, une messagerie ou un logiciel de gestion.

La nature des fichiers volés (essentiellement des PDF et des images, et non une base clients structurée) laisse penser que l'attaquant a eu accès à **un espace de stockage de documents**, plutôt qu'à la seule base de données du site marchand.

### Quand l'attaque a-t-elle eu lieu ?

La revendication de ChimeraZ a été rendue publique le **6 octobre 2026**. La date réelle de l'intrusion reste inconnue. Il faut distinguer trois moments :

- **l'intrusion**, c'est-à-dire l'accès initial aux systèmes ;

- **le vol des données** c'est-à-dire la copie des 4,65 Go de données, qui a pu s'étaler dans le temps ;

- **la publication**, c'est-à-dire la mise en vente publique.

Dans ce type d'attaque, il s'écoule souvent plusieurs jours, voire plusieurs semaines, entre l'intrusion et la publication. L'armurerie n'a, à ce stade, ni confirmé l'incident ni communiqué de chronologie.

### Comment l'attaque a-t-elle été menée ?

La méthode d'intrusion n'a pas été rendue publique. Seule la suite de l'attaque est connue : le vol de 7 546 fichiers, publication d'un inventaire détaillé, diffusion de 200 documents comme preuve, puis mise en vente du lot. L'absence de chiffrement des systèmes et de demande de rançon indique qu'il ne s'agit pas d'un ransomware, mais d'un vol de données destinées à la revente.

### Pourquoi cet incident nous concerne directement

Cette attaque visait un acteur de notre secteur, qui détient le même type de données que nous : pièces d'identité, passeports, licences FFTir, documents SIA, décisions préfectorales, justificatifs de domicile et RIB. Ce sont précisément ces documents qui donnent de la valeur au lot volé. Des groupes cybercriminels comme ChimeraZ pourraient donc considérer les armureries comme des **cibles rentables**, d'autant que ces structures sont souvent de petite taille et disposent de moyens de sécurité limités. Cet incident doit nous amener à vérifier sans attendre :

- où et comment nous stockons les documents de nos clients ;

- combien de temps nous les conservons ;

- qui peut y accéder ;

- quel est le niveau de protection de notre site marchand et de nos comptes.

## Le groupe attaquant

### Une motivation essentiellement financière

Tout indique que ChimeraZ agit dans un but lucratif. Le groupe ne cherche ni à défendre une cause ni à faire passer un message : il propose les données volées à la vente. Plusieurs éléments écartent l'hypothèse de l'hacktivisme. Aucune revendication idéologique n'accompagne l'attaque. Les données ne sont pas diffusées gratuitement pour dénoncer la victime. Enfin, la cible, une petite armurerie locale, ne présente pas de dimension symbolique particulière.

L'intérêt du groupe se porte sur la valeur marchande des fichiers. Le lot contient des documents très recherchés sur les marchés cybercriminels, notamment environ 1 200 cartes d'identité, 200 passeports, 300 justificatifs de domicile et RIB, ainsi que 1 900 licences FFTir et documents liés au Système d'information sur les armes (SIA). Ce lot permet de croiser l'identité, l'adresse et la qualité de détenteur d'armes d'une même personne. Il peut donc servir à l'usurpation d'identité et à la fraude bancaire, mais aussi exposer les victimes à un risque physique, par exemple des cambriolages ciblés.

### Une démarche en plusieurs étapes

La démarche de ChimeraZ suit le schéma classique des vendeurs de données volées :

1.  **L'intrusion** : le groupe a obtenu un accès aux systèmes de l'armurerie. La méthode reste inconnue. Il peut s'agir du site marchand, d'un espace documentaire, d'un compte compromis ou d'un autre système.

2.  **Le vol de données** : il a copié un volume important de documents sensibles que l'armurerie conservait pour respecter ses obligations réglementaires de vérification d'identité et d'autorisation de détention d'armes.

3.  **La publication**: il a publié une description détaillée du contenu, avec des volumes par catégorie de documents, pour mettre en avant la valeur du lot auprès d'acheteurs potentiels.

4.  **La preuve** : il a diffusé un échantillon de 200 fichiers afin d'établir la crédibilité de sa revendication.

5.  **La monétisation** : il met en vente l'ensemble des données.

## Mécanismes d'attaque

Voici les mécanismes de l'attaque, phase par phase.

| Phase                    | Mécanisme                                                                                                                                                                                           | Tactique MITRE ATT&CK                                                                            |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| 1\. Accès initial        | Entrée dans les systèmes de l'armurerie, par l'une de ces voies possibles : faille du site marchand ; espace documentaire mal protégé ; compte compromis (phishing, mot de passe réutilisé ou volé) | Initial Access : T1190 (faille d'application exposée), T1078 (comptes valides), T1566 (phishing) |
| 2\. Repérage des données | Identification de l'endroit où sont stockés les documents clients (PDF, images)                                                                                                                     | Discovery : T1083 (recherche de fichiers et répertoires)                                         |
| 3\. Collecte             | Rassemblement de 7 546 fichiers : pièces d'identité, licences FFTir, documents SIA, décisions préfectorales, RIB…                                                                                   | Collection : T1005 (données du système local) ou T1213 (dépôts de documents)                     |
| 4\. Vol des données      | Copie de 4,65 Go vers l'extérieur                                                                                                                                                                   | Exfiltration (TA0010)                                                                            |
| 5\. Inventaire et preuve | Publication d'une liste chiffrée du contenu et diffusion de 200 fichiers comme échantillon                                                                                                          | C’est une étape de **monétisation**                                                              |
| 6\. Monétisation         | Mise en vente du lot complet                                                                                                                                                                        |                                                                                                  |

## Impacts de l'attaque

Voici les impacts de l'attaque, classés selon qui les subit.

**1. Pour les clients de l'armurerie (les premières victimes)**

| Impact                   | Explication                                                                                                                                                                   |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Risque physique          | Leur identité, leur adresse et le fait qu'ils détiennent des armes sont associés. Leur domicile peut donc être ciblé, notamment par des cambrioleurs qui cherchent des armes. |
| Usurpation d'identité    | Les copies de cartes d'identité, de passeports et de justificatifs de domicile permettent d'ouvrir des comptes ou de faire des démarches au nom des victimes.                 |
| Fraude bancaire          | Les RIB et les documents liés aux cartes bancaires peuvent servir à des prélèvements frauduleux.                                                                              |
| Phishing ciblé           | Les escrocs peuvent envoyer des emails très crédibles, par exemple en se faisant passer pour l'armurerie ou la préfecture.                                                    |
| Atteinte à la vie privée | Des informations sur les armes détenues (nombre, motif, autorisation) sont exposées.                                                                                          |
| Inquiétude durable       | Des documents d'identité ne se « changent » pas facilement, contrairement à un mot de passe.                                                                                  |

**2. Pour l'armurerie victime**

| Impact                     | Explication                                                                                                    |
|----------------------------|----------------------------------------------------------------------------------------------------------------|
| Atteinte à la réputation   | La perte de confiance des clients profite aux concurrents.                                                     |
| Obligations légales (RGPD) | L'armurerie doit notifier la CNIL sous 72 h et informer les personnes concernées, puisque le risque est élevé. |
| Sanctions possibles        | La CNIL peut prononcer une amende si les mesures de sécurité étaient insuffisantes (art. 32 du RGPD).          |
| Recours des victimes       | Les clients lésés peuvent demander des dommages et intérêts.                                                   |
| Coûts directs              | Enquête technique, sécurisation des systèmes, accompagnement des clients.                                      |
| Attention des autorités    | Le dossier touche aux données SIA, donc au ministère de l'Intérieur et à la préfecture.                        |

**3. Pour notre entreprise (concurrent du même secteur)**

| Impact                     | Explication                                                                                                                    |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Menace sur tout le secteur | Les armureries apparaissent comme des cibles rentables. Le même groupe ou d'autres pourraient s'attaquer à d'autres enseignes. |
| Méfiance des clients       | Les clients peuvent hésiter à transmettre leurs documents à n'importe quelle armurerie.                                        |
| Opportunité commerciale    | Des clients inquiets peuvent se tourner vers une enseigne qui montre qu'elle protège sérieusement leurs données.               |
| Contrôles renforcés        | Les autorités pourraient renforcer leurs exigences de sécurité pour toute la profession.                                       |

## Mesures de protection contre des attaques similaires

**1. Garder moins de documents**

Moins on en garde, moins il y a à voler.

- Ne demander aux clients que les documents vraiment obligatoires.

- Regarder une pièce d'identité sans forcément la photocopier, quand la loi ne l'exige pas.

- Décider combien de temps on garde chaque document, puis le supprimer passé ce délai.

> <https://www.cnil.fr/fr/passer-laction/les-durees-de-conservation-des-donnees>

- Faire le tri dans les vieux dossiers et supprimer ce qui ne sert plus.

- Ne pas ranger au même endroit le nom du client, son adresse et les armes qu'il possède.

- Prendre le temps d'évaluer les risques que ces données font courir aux clients.  
  <https://www.cnil.fr/fr/RGPD-analyse-impact-protection-des-donnees-aipd>

**2. Bien protéger les documents qu'on garde**

- Les rendre illisibles pour qui n'a pas la clé (c'est ce qu'on appelle le chiffrement). Même volés, ils seront inutilisables.

- Ne pas laisser les documents des clients sur le site internet. Les ranger dans un espace à part.

- Ne donner l'accès qu'aux employés qui en ont vraiment besoin.

- Demander aux prestataires (hébergeur du site, informaticien) de s'engager par écrit à protéger les données.  
  **<https://www.cnil.fr/fr/guide-de-la-securite-des-donnees-personnelles>**

**3. Empêcher les pirates d'entrer**

- Ajouter une deuxième vérification à la connexion, par exemple un code reçu sur le téléphone en plus du mot de passe. Un mot de passe volé ne suffit alors plus à entrer.  
  <https://d3fend.mitre.org/technique/d3f:Multi-factorAuthentication/>

- Utiliser un mot de passe différent et solide pour chaque compte.

- Faire les mises à jour du site et des ordinateurs dès qu'elles sont proposées.  
  <https://messervices.cyber.gouv.fr/guides/guide-dhygiene-informatique>

**4. Apprendre aux employés à repérer les faux emails**

Un email est suspect quand :

- Le nom de l'expéditeur ne correspond pas à son adresse ;

- Il presse d'agir vite (« votre compte va être bloqué ») ;

- Il contient une pièce jointe ou un lien inattendu ;

- Il demande de se connecter ou de donner un mot de passe.

Avant de cliquer sur un lien douteux, vérifier où il mène.

### À faire en priorité

1.  **Faire le tri dans les documents et ne garder que le nécessaire.**

2.  **Ajouter la deuxième vérification à la connexion sur tous les comptes.**

3.  **Rendre illisibles les documents des clients et les sortir du site internet.**
