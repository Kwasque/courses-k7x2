# Courses — installation

## 1. Mettre l'appli en ligne (GitHub Pages, gratuit) — depuis un ordinateur

1. Crée un compte sur https://github.com (si tu n'en as pas).
2. En haut à droite : **+ → New repository**.
   - Nom : quelque chose de peu devinable, ex. `courses-k7x2`
   - Visibilité : **Public**
   - Clique **Create repository**.
3. Sur la page du dépôt, clique **uploading an existing file**, puis glisse-dépose
   **le contenu** du dossier `courses` : `index.html`, `manifest.webmanifest`, `sw.js` et le dossier `icons`.
   (Tu peux ignorer ce fichier LISEZMOI.) Clique **Commit changes**.
4. Va dans **Settings → Pages**. Sous *Build and deployment* :
   Source = **Deploy from a branch**, Branch = **main** / **(root)** → **Save**.
5. Attends 1 à 2 minutes et recharge la page : l'adresse s'affiche, du type
   `https://ton-pseudo.github.io/courses-k7x2/`

## 2. L'installer sur l'iPhone

1. Ouvre cette adresse dans **Safari** (pas Chrome).
2. Bouton **Partager** → **Sur l'écran d'accueil** → **Ajouter**.
3. Utilise toujours l'appli depuis l'icône : ses données sont séparées de celles de l'onglet Safari.

## Bon à savoir

- Tes listes sont stockées **uniquement sur ton iPhone**. Rien n'est envoyé sur GitHub.
  Si tu supprimes l'appli de l'écran d'accueil, l'historique est effacé.
- **Photos automatiques** : l'appli cherche elle-même une photo à partir du nom :
  Open Food Facts pour les articles, Wikimedia Commons puis Wikipédia pour les recettes.
  Le premier affichage d'une nouvelle liste peut prendre 1 à 2 minutes (Open Food Facts limite le nombre de recherches),
  ensuite l'adresse de chaque photo est mémorisée. En attendant, ou si rien n'est trouvé, un emoji s'affiche.
  Sans réseau, les emojis restent et la liste est utilisable. Menu « ⋯ » → *Rechercher à nouveau les photos* pour tout relancer.
- **Articles cochés** : une minute après le dernier article coché, si tu ne touches plus l'appli
  (ni défilement, ni appui), ils sont rangés dans la section « Déjà pris » en bas de la liste.
  Touche ce titre pour l'ouvrir ; décocher un article le remet dans « À acheter ».
- **Recettes faites** : dans une recette, bouton « Marquer comme faite ». Elle passe en fin de grille avec un badge « Faite ».
- **Mettre à jour l'appli** : remplace les fichiers sur GitHub, en changeant `courses-v12` en `courses-v13`
  (etc.) en haut de `sw.js`. Ferme et rouvre l'appli deux fois pour voir la nouvelle version,
  ou menu « ⋯ » → *Forcer la mise à jour de l'appli* (les listes sont conservées).
  La version installée est affichée en bas de ce menu.

## Format du JSON

```json
{
  "titre": "Courses semaine 41",
  "date": "2026-10-03",
  "recettes": [
    {
      "id": "curry",
      "nom": "Curry de pois chiches",
      "emoji": "🍛",
      "photo_recherche": "chickpea curry",
      "temps": "30 min",
      "portions": 2,
      "source": "https://…",
      "ingredients": [
        { "article": "pois-chiches", "quantite": "1 boîte" },
        { "nom": "Huile d'olive", "quantite": "1 c. à s.", "article": null }
      ],
      "etapes": ["Étape 1…", "Étape 2…"]
    }
  ],
  "articles": [
    {
      "id": "pois-chiches",
      "nom": "Pois chiches",
      "quantite": "2 boîtes",
      "rayon": "Épicerie",
      "emoji": "🥫",
      "photo_recherche": "pois chiches",
      "recettes": ["curry"]
    }
  ]
}
```

- `ingredients[].article` = l'`id` d'un article à acheter. `null` = déjà à la maison (pas dans la liste).
- Rayons reconnus (dans l'ordre du magasin) : Fruits & légumes, Boulangerie, Boucherie, Poissonnerie,
  Traiteur, Frais, Crèmerie, Fromage, Épicerie, Épicerie salée, Épicerie sucrée, Conserves, Surgelés,
  Boissons, Hygiène, Entretien, Maison, Autre. Un autre nom marche aussi (placé avant « Autre »).
- `photo_recherche` : mots-clés pour trouver la photo (sinon le `nom` est utilisé).
  Articles : **en français** (Open Food Facts). Recettes : **en anglais** (Wikimedia Commons, meilleurs résultats).
- `emoji` : affiché en attendant la photo ou si aucune n'est trouvée.
- `photo` : une adresse d'image précise, si tu en as une (prioritaire sur la recherche automatique).
- Seuls `nom` (et `id` pour les liens) sont obligatoires ; le reste est optionnel.
