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
- **Tout est un seul fichier** (`index.html`) : facile à bidouiller. Le nom, les couleurs (variables CSS en haut du `<style>`) et les libellés se changent en deux minutes.

---

## 6. Versionnage

Mnémosyne suit le format **MAJEURE.MINEURE.PATCH** :

- **PATCH** (1.0.**x**) : corrections, ajustements sans nouvelle fonctionnalité.
- **MINEURE** (1.**x**.0) : nouvelle fonctionnalité rétro-compatible.
- **MAJEURE** (**x**.0.0) : évolution structurante ; **chaque version majeure porte un nom** (une Muse).

La version courante est affichée sous le titre et dans **Données → à propos**. Elle est définie à un seul endroit dans `index.html` :

```js
const APP_VERSION = "1.0.0";
const APP_CODENAME = "Clio";
```

Le nom du cache hors-ligne (`sw.js`) reprend le numéro de version, de sorte que chaque release remplace proprement l'ancien cache. L'historique complet est dans **`CHANGELOG.md`**.

Version actuelle : **1.0.0 « Clio »** (Clio, Muse de l'Histoire).

---

## Structure

| Fichier | Rôle |
|---|---|
| `index.html` | L'application entière (HTML + CSS + JS, stockage IndexedDB) |
| `manifest.webmanifest` | Métadonnées PWA (nom, icônes, couleurs) |
| `sw.js` | Service worker : met l'app en cache pour le hors-ligne |
| `icons/` | Icônes (écran d'accueil, favicon, maskable) |

Licence : usage personnel libre.
