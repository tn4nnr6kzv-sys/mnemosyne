# Journal des versions — Mnémosyne

Format : **MAJEURE.MINEURE.PATCH**. Les versions majeures portent un nom (une Muse).

- **MAJEURE** (`x.0.0`) : évolution structurante, changement de nom.
- **MINEURE** (`1.x.0`) : nouvelle fonctionnalité rétro-compatible.
- **PATCH** (`1.0.x`) : correction ou ajustement.

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
