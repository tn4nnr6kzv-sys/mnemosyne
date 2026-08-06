# Mnémosyne — ma bibliothèque

Gestionnaire de bibliothèque personnelle, **100 % côté client**, hors-ligne, installable en application sur iPhone (PWA), avec **import Goodreads**.

- Aucune base de données serveur, aucun compte, aucune donnée envoyée ailleurs.
- Les livres sont stockés **sur l'appareil** (IndexedDB du navigateur).
- Couvertures récupérées automatiquement via Open Library (quand il y a un ISBN et une connexion).

---

## 1. Mettre en ligne sur GitHub Pages

1. Crée un dépôt GitHub, par exemple `mnemosyne` (public).
2. Dépose **tous ces fichiers à la racine du dépôt** (glisser-déposer sur github.com, ou `git push`) :
   ```
   index.html
   manifest.webmanifest
   sw.js
   icons/
   README.md
   ```
3. Dans le dépôt : **Settings → Pages**.
4. *Build and deployment → Source* : choisis **Deploy from a branch**, branche `main`, dossier `/ (root)`, puis **Save**.
5. Attends ~1 minute. L'adresse s'affiche en haut de la page Pages :
   `https://TON-PSEUDO.github.io/mnemosyne/`

> Les chemins de l'application sont **relatifs**, donc ça fonctionne aussi bien à la racine d'un domaine qu'à l'adresse `…github.io/mnemosyne/`. Rien à configurer.

---

## 2. Installer sur iPhone (PWA)

1. Ouvre l'adresse `https://TON-PSEUDO.github.io/mnemosyne/` **dans Safari** (l'installation ne marche pas depuis Chrome iOS).
2. Bouton **Partager** (carré avec la flèche) → **Sur l'écran d'accueil**.
3. L'icône « Mnémosyne » apparaît. Lancée depuis l'écran d'accueil, l'app s'ouvre **en plein écran** et **fonctionne hors-ligne**.

Sur Android/desktop (Chrome, Edge) : une invite « Installer l'application » apparaît, ou via le menu ⋮ → *Installer*.

---

## 3. Importer depuis Goodreads

1. Sur **goodreads.com** (version web) : *My Books* → menu de gauche **Import and export** → bouton **Export Library**. Goodreads prépare un fichier `.csv` (le lien apparaît sur la même page après quelques secondes).
2. Dans Mnémosyne : bouton **Données** (icône en haut à droite) → **Importer depuis Goodreads** → choisis le `.csv`.
3. Les doublons (même ISBN, ou même titre + auteur) sont automatiquement ignorés — tu peux réimporter sans créer de doublons.

Colonnes reprises : titre, auteur(s), ISBN/ISBN13, ma note, éditeur, pages, année, dates (ajout / lecture), étagères, étagère principale (lu / en cours / à lire), avis, notes privées.

---

## 4. Sauvegarde (important)

Les données vivent dans le navigateur de l'appareil. iOS peut effacer le stockage d'un site **peu utilisé** ; une fois l'app **ajoutée à l'écran d'accueil**, c'est bien plus durable, mais **fais des sauvegardes** :

- **Données → Exporter (.json)** : sauvegarde complète de toute la bibliothèque. Garde ce fichier (iCloud, mail, etc.).
- **Données → Restaurer (.json)** : réinjecte une sauvegarde (fusion sans doublons). Pratique aussi pour **passer d'un appareil à un autre**.
- **Données → Exporter au format Goodreads (.csv)** : ressort un CSV compatible pour aller ailleurs.

---

## 5. Bon à savoir

- **Couvertures** : cherchées via `covers.openlibrary.org` à partir de l'ISBN. Sans ISBN, sans couverture connue, ou hors-ligne, une couverture « toile » colorée est générée à partir du titre.
- **Confidentialité** : rien ne quitte l'appareil, sauf la requête d'image de couverture vers Open Library (uniquement l'ISBN).
- **Ajouter / modifier** : bouton **+**, ou clic sur un livre. Note en cliquant les étoiles (reclique la même étoile pour remettre à zéro).
- **Étagères et tags** : l'**étagère** (Lu / En cours / À lire) est le statut de lecture ; les **tags** (genre, type, thème… champ « Tags » de la fiche) sont libres. La barre de tags sous les filtres permet de les combiner avec l'étagère (un livre doit porter tous les tags cochés). Le bouton **⚙ Gérer** ouvre le gestionnaire pour renommer, fusionner ou supprimer un tag sur l'ensemble des livres.
- **Scanner un livre** : bouton **code-barres** (en haut). Vise l'ISBN au dos du livre, **prends-en une photo** (le plus fiable sur iPhone installé), ou saisis-le à la main. Si le livre est déjà enregistré, sa fiche s'ouvre ; sinon ses informations sont récupérées en ligne et la fiche d'ajout est pré-remplie. La caméra nécessite HTTPS (assuré par GitHub Pages) et l'autorisation d'accès ; la recherche des métadonnées nécessite une connexion. Le décodeur fonctionne hors-ligne une fois l'app chargée.
- **Profils** : le nom en haut à gauche (sous le titre) est le **profil actif** ; clique dessus pour ouvrir la fenêtre **Profils**. Chaque profil a sa propre bibliothèque. Pour retrouver **toutes tes bibliothèques sur un autre appareil**, utilise **Profils → « Configurer / synchroniser… »** (synchro du **compte** : un seul fichier GitHub regroupe toutes les bibliothèques ; sur un nouvel appareil, **Récupérer** les recrée toutes). Un profil n'est pas protégé par mot de passe (données lisibles sur l'appareil).
- **Suivi de lecture** : pour un livre « en cours », renseigne la **page actuelle** (dans la fiche, ou via le carrousel « En cours de lecture » → **Actualiser**). La progression s'affiche en jauge ; « **J'ai terminé** » bascule le livre en « Lu ». Le lien **Statistiques →** (sur le bandeau de chiffres) ouvre les statistiques de lecture.
- **Mises à jour** : quand tu déploies une nouvelle version sur GitHub, un bandeau **« Nouvelle version disponible — Actualiser »** apparaît au lancement suivant. Tu peux aussi forcer la vérification dans **Données → Application & mises à jour**, et, en dernier recours, **Forcer le rafraîchissement** (vide le cache et recharge la dernière version ; livres et réglages conservés).
- **Tout est un seul fichier** (`index.html`) : facile à bidouiller. Le nom, les couleurs (variables CSS en haut du `<style>`) et les libellés se changent en deux minutes.

---

## 6. Accéder à sa bibliothèque sur tous ses appareils (synchro GitHub)

Par défaut, Mnémosyne stocke tout **localement** sur chaque appareil. Pour retrouver la même bibliothèque partout, active la **synchronisation GitHub** : la bibliothèque est enregistrée dans un fichier `.json` d'un dépôt **privé** à toi, que chaque appareil lit et écrit. Aucun serveur à héberger.

**Mise en place (une seule fois)**
1. Crée un dépôt **privé** sur GitHub, par exemple `mnemosyne-data` (vide, sans README). *(C'est un dépôt distinct de celui qui héberge l'app.)*
2. github.com → photo de profil → **Settings** → tout en bas **Developer settings** → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
3. *Repository access* : **Only select repositories** → choisis `mnemosyne-data`.
4. *Permissions* → **Repository permissions** → **Contents** : **Read and write**.
5. **Generate token**, copie-le (il commence par `github_pat_`).
6. Dans Mnémosyne : bouton **nuage** (en haut) → colle le jeton, ton pseudo (*propriétaire*) et `mnemosyne-data` (*dépôt*) → **Enregistrer** → **Tester la connexion** → **Envoyer**. Le fichier est créé.

**Sur un autre appareil**
Ouvre l'app, bouton **nuage**, saisis les mêmes réglages + le même jeton (ou un second jeton dédié), puis **Récupérer**.

**Automatique**
Active *Synchroniser automatiquement* : récupération-fusion au lancement, et envoi après chaque modification.

**À savoir**
- Le jeton reste **sur l'appareil** (stockage local du navigateur) et n'est envoyé qu'à `api.github.com` en HTTPS. Utilise un jeton *fine-grained* limité à ce seul dépôt ; tu peux le révoquer à tout moment depuis GitHub.
- Modèle **« dernier qui écrit gagne »** au niveau du fichier ; la récupération en mode **Fusionner** réunit les livres des deux côtés (la fiche la plus récente l'emporte). Pour propager une **suppression**, utilise **Récupérer → Remplacer** sur les autres appareils, ou envoie depuis l'appareil où tu as supprimé.
- Chaque envoi crée un **commit daté** : tu disposes gratuitement d'un historique de sauvegardes dans le dépôt.

---

## 7. Versionnage

Mnémosyne suit le format **MAJEURE.MINEURE.PATCH** :

- **PATCH** (1.0.**x**) : corrections, ajustements sans nouvelle fonctionnalité.
- **MINEURE** (1.**x**.0) : nouvelle fonctionnalité rétro-compatible.
- **MAJEURE** (**x**.0.0) : évolution structurante ; **chaque version majeure porte un nom** (une Muse).

La version courante est affichée sous le titre et dans **Données → à propos**. Elle est définie à un seul endroit dans `index.html` :

```js
const APP_VERSION = "1.7.1";
const APP_CODENAME = "Clio";
```

Le nom du cache hors-ligne (`sw.js`) reprend le numéro de version, de sorte que chaque release remplace proprement l'ancien cache. L'historique complet est dans **`CHANGELOG.md`**.

Version actuelle : **1.7.1 « Clio »** (Clio, Muse de l'Histoire).

L'historique complet est dans **`CHANGELOG.md`**.

---

## Structure

| Fichier | Rôle |
|---|---|
| `index.html` | L'application entière (HTML + CSS + JS, stockage IndexedDB) |
| `manifest.webmanifest` | Métadonnées PWA (nom, icônes, couleurs) |
| `sw.js` | Service worker : met l'app en cache pour le hors-ligne |
| `icons/` | Icônes (écran d'accueil, favicon, maskable) |
| `vendor/zxing.min.js` | Décodeur de code-barres [ZXing](https://github.com/zxing-js/library) (Apache-2.0) |

Licence : usage personnel libre. Inclut ZXing (`@zxing/library`), sous licence Apache-2.0.
