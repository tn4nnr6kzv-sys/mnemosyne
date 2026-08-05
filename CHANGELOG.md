# Journal des versions — Mnémosyne

Format : **MAJEURE.MINEURE.PATCH**. Les versions majeures portent un nom (une Muse).

- **MAJEURE** (`x.0.0`) : évolution structurante, changement de nom.
- **MINEURE** (`1.x.0`) : nouvelle fonctionnalité rétro-compatible.
- **PATCH** (`1.0.x`) : correction ou ajustement.

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
