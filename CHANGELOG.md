# Journal des versions — Mnémosyne

Format : **MAJEURE.MINEURE.PATCH**. Les versions majeures portent un nom (une Muse).

- **MAJEURE** (`x.0.0`) : évolution structurante, changement de nom.
- **MINEURE** (`1.x.0`) : nouvelle fonctionnalité rétro-compatible.
- **PATCH** (`1.0.x`) : correction ou ajustement.

---

## 1.5.0 « Clio » — 2026-08-06

### Ajouté
- **Suivi de lecture** pour les livres « en cours » :
  - Champ **page actuelle** dans la fiche, avec **jauge de progression** (page / total, %).
  - **Jauge sur les cartes** des livres en cours (à la place des étoiles).
  - **Carrousel « En cours de lecture »** en haut de la bibliothèque (vue par défaut), avec couverture, progression et bouton **Actualiser**.
  - Éditeur rapide **« Où j'en suis »** : saisie de la page (curseur + boutons ±1 / ±10), total de pages modifiable, pages restantes, et bouton **« J'ai terminé »** qui bascule le livre en « Lu » (avec date de lecture du jour).
- **Statistiques de lecture** (lien « Statistiques → » sur le bandeau de chiffres) : chiffres clés (livres, lus, en cours, à lire, pages lues, note moyenne, lus cette année / ce mois, pages/livre), répartition par étagère, progression moyenne des lectures en cours, histogramme des notes, lectures par année, top genres/tags, et repères (livre le plus long / le plus court).

### Note
- Nouveau champ `currentPage` par livre (synchronisé). Le cache hors-ligne passe à `mnemosyne-1.5.0`.

---

## 1.4.0 « Clio » — 2026-08-05

### Ajouté
- **Profils (bibliothèques séparées, locales)** : plusieurs « comptes » sur l'app, chacun avec sa **propre bibliothèque** et sa **propre configuration de synchronisation** GitHub.
  - Le nom du profil actif s'affiche dans l'en-tête ; un clic ouvre la fenêtre **Profils** (créer, activer, renommer, supprimer, avec le nombre de livres par profil).
  - Chaque profil utilise une **base IndexedDB distincte** (isolation complète des données sur l'appareil) et un **espace de réglages de synchro distinct** — un profil peut donc suivre son utilisateur sur ses appareils via **son propre** fichier GitHub, indépendamment des autres.
  - Idéal pour séparer perso / pro, ou partager un appareil entre plusieurs personnes.
- Migration transparente : l'ancienne bibliothèque et sa synchro deviennent le profil par défaut « Ma bibliothèque » ; « Vider la bibliothèque » ne concerne désormais que le profil actif.

### Note
- Un profil n'est **pas** protégé par mot de passe (les données restent lisibles sur l'appareil). Pour un verrou d'accès (PIN / Face ID) ou de vrais comptes serveur, voir les évolutions futures.
- Le cache hors-ligne passe à `mnemosyne-1.4.0`.

---

## 1.3.0 « Clio » — 2026-08-05

### Ajouté
- **Scanner de code-barres** (bouton code-barres, en haut) pour **retrouver ou ajouter** un livre via son ISBN :
  - Lecture par la **caméra arrière** (décodage EAN-13 / ISBN embarqué, hors-ligne, via ZXing), avec **saisie manuelle de l'ISBN** en repli (utile sur ordinateur ou si la caméra est indisponible).
  - Si l'ISBN correspond à un livre déjà enregistré → sa fiche s'ouvre. Sinon → les **métadonnées** (titre, auteur, pages, éditeur, année, catégories) sont récupérées automatiquement (Google Books, puis Open Library en repli) et la fiche d'ajout est pré-remplie.
  - Vibration légère à la lecture réussie ; couverture pré-affichée quand l'ISBN est reconnu.

### Technique
- Décodeur **ZXing** (`@zxing/library`, Apache-2.0) embarqué dans `vendor/zxing.min.js`, chargé à la demande et mis en cache pour le hors-ligne.
- Le cache hors-ligne passe à `mnemosyne-1.3.0`.

---

## 1.2.0 « Clio » — 2026-08-04

### Ajouté
- **Tags personnalisables** pour organiser les livres au-delà de l'étagère de lecture (Lu / En cours / À lire) : genre, type, thème… tout est libre.
  - **Barre de tags** sous les filtres : chaque tag est cliquable et se combine avec l'étagère et la recherche (logique « ET » : un livre doit porter tous les tags sélectionnés). Bouton pour effacer la sélection.
  - **Gestionnaire de tags** (⚙ Gérer) : liste tous les tags avec leur nombre de livres, permet de **renommer** (fusionne si le nom existe déjà), **filtrer** et **supprimer** un tag ; toute modification se propage à l'ensemble des livres et se synchronise.
  - **Saisie assistée** dans la fiche : champ « Tags » avec autocomplétion (datalist) et puces des tags existants à ajouter d'un clic (limite les doublons).
  - Couleur attribuée automatiquement à chaque tag (déterministe, cohérente partout).
- Les tags réutilisent le champ `shelves` déjà présent (compatible import/export Goodreads et synchronisation, sans migration).

### Note
- Le cache hors-ligne passe à `mnemosyne-1.2.0`.

---

## 1.1.0 « Clio » — 2026-08-04

### Ajouté
- **Synchronisation multi-appareils via GitHub** : la bibliothèque peut être stockée dans un fichier `.json` d'un dépôt GitHub privé, lu et écrit depuis n'importe quel appareil avec un jeton d'accès personnel (fine-grained). Aucun serveur à héberger, données chez soi, chaque envoi crée un commit daté (historique de sauvegardes).
  - Nouvel écran **Synchronisation** (bouton nuage) : jeton, propriétaire, dépôt, fichier, branche.
  - Boutons **Tester la connexion**, **Envoyer**, **Récupérer** (modes **Fusionner** ou **Remplacer**).
  - **Synchro automatique** optionnelle : récupération-fusion au lancement, envoi (différé) après chaque ajout / modification / suppression / import.
  - Fusion au niveau du livre (par identifiant, la modification la plus récente l'emporte) ; modèle « dernier qui écrit gagne » au niveau du fichier.
  - Jeton conservé uniquement sur l'appareil (localStorage), transmis seulement à `api.github.com` en HTTPS.

### Note
- Le cache hors-ligne passe à `mnemosyne-1.1.0`.

---

## 1.0.0 « Clio » — 2026-08-04

Première version nommée.

### Fonctionnalités
- Bibliothèque personnelle 100 % côté client, stockage local (IndexedDB), fonctionnement hors-ligne.
- Application installable (PWA) : manifeste, service worker, icônes, chemins relatifs (compatible GitHub Pages en sous-dossier).
- Import Goodreads (`.csv`) : parseur tolérant (guillemets, virgules et retours à la ligne dans les avis, format ISBN `="…"`), dédoublonnage automatique (ISBN, sinon titre + auteur).
- Fiche livre façon carton de catalogue : ajout, édition, suppression, note en étoiles.
- Navigation : recherche (titre / auteur / étagère), filtres par étagère, tris (ajout, titre, auteur, note, lecture, année), statistiques (livres, lus, en cours, à lire, pages lues, note moyenne).
- Couvertures via Open Library (par ISBN) avec repli « toile » générée à partir du titre.
- Sauvegarde / restauration en `.json`, export au format Goodreads (`.csv`), effacement complet.
- Affichage de la version dans l'en-tête et dans « Données → à propos ».

*Codename : Clio, Muse de l'Histoire.*
