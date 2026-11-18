# Studio d'affiches · Pharmacie Al Fatiha

Générateur d'affiches pour les réseaux sociaux d'une petite pharmacie (statuts WhatsApp, posts Facebook/Instagram).
Projet offert à la pharmacie : **coût zéro**, site 100 % statique, aucun serveur, aucune clé API.

## Fichiers

- `index.html` : toute l'application (HTML + CSS + JS, sans dépendance ni build). Les affiches sont dessinées sur un `<canvas>` 1080 px de large.
- `config.js` : infos par défaut de la pharmacie (nom, slogan, téléphone/WhatsApp, repère, logo). Pas de couleurs ni de police : la charte est fixe.
- `photos/` : photos prêtes à l'emploi (façade, pharmacien·nes, produits), sources dans `photos/CREDITS.md`. Listées dans `LIB` (avec le point de cadrage `x`/`y`).
- `manifest.json`, `icon-*.png` : installation sur l'écran d'accueil du téléphone.
- `README.md` : mise en ligne gratuite (Netlify Drop, GitHub Pages).
- `example/` : références visuelles (pas à mettre en ligne).

## Charte (à respecter dans tout nouveau modèle)

- Couleurs `CH` : vert enseigne `#2E9B3E`, vert profond `#0E4B22`, jaune `#F2C200` (un seul mot ou chiffre par affiche), vert pâle `#EEF6EC`. Seule exception : la couleur symbole d'une journée mondiale (`CALENDAR[].color`).
- Titres en Bricolage Grotesque, texte en Inter. Pas de police manuscrite.
- Trois éléments fixes : `header()` (logo en haut à gauche, version pastille blanche sur photo), `footer()` (vague verte + bandeau contact), `macaron()` (« Disponible » sur les produits). Le surligneur jaune vient de `*mot*`.
- Deux fonds par modèle : clair (`light`: white/pale) ou vert (`dark`: green/deep), choix via `choose`.

## Architecture de index.html

- Tout est dessiné dans un repère de 540 px de large, mis à l'échelle ×2 (`K`). Hauteurs : 960 (9:16), 675 (4:5), 540 (1:1) ; `compact` = 4:5 et carré.
- `TYPES` : les 11 modèles (champs, fond par défaut, `pic` = photo par défaut). `VARIANTS` : 3 mises en page par modèle (`TYPES[x].v`), chacune avec un cadre `f` (`own` = dessin propre au modèle, `full` plein cadre photo, `top` photo en haut, `medal` photo ronde centrée, `center` centré, `band` bandeau santé), `photo` (need/option) et `st` (affiche un sticker). Choix mémorisé dans `state.variant[type]` ; les 3 aperçus sont redessinés par `renderThumbs()`.
- Textes tout prêts : `IDEAS[type]` = liste `{n, d}` (les champs absents reprennent le texte par défaut du modèle) ; `IDEAS.mois` est généré pour les 12 mois à venir depuis `MONTHS`. La journée santé utilise `CALENDAR`. `applyIdea()` garde une copie pour « Annuler ».
- Stickers : `STICKERS` (illustrations vectorielles 100×100, clé couleur `m` = couleur de la journée), `drawSticker()` (pastille blanche découpée). `state.sticker[type]` = id, `emo:…` (emoji) ou `img:…` (image importée, `localStorage` clé `stickers`). Sticker proposé : `CALENDAR[].sticker` (via `DAY_STICKER`) ou `STICKER_DEFAULT`.
- `ALIGN` (left/center) : alignement par défaut de `put()`/`placeBox()`/`checklist()`, fixé par le cadre. `c.frame` = cadre courant.
- `BUILD[type](d, c)` : renvoie une pile de blocs `{h, draw(y)}` et d'espacements `gap(px, flex)`. `c.s` = échelle, réduite par `fit()` jusqu'à ce que tout tienne. `LX`/`LW` = colonne de texte ; `c.colW`, `c.titleW`, `c.lowW` la rétrécissent quand une photo occupe une partie de l'affiche.
- `draw()` : fond, partie photo propre au modèle (produit, garde avec façade, ouverts en arche, un conseil, promo), en-tête, pile de texte, puis la vague contact en dernier.
- Texte : `textBlock()` (retour à la ligne, ajustement, limite de lignes) ; `*mot*` = surligné (`richBlock`), dans les titres comme dans le texte.
- Photos : `state.photo[type]` mémorise la photo de chaque modèle ; `lib:…` = photo de `photos/`, sinon IndexedDB. `blurFill()` fait le fond flouté (sans `ctx.filter`, pour Safari).
- Persistance : `localStorage` (clé `state4`, réglages, textes) et IndexedDB (photothèque). Rien ne part sur un serveur.
- Export : PNG via `canvas.toBlob`, `navigator.share` sur mobile. En `file://`, les photos de `photos/` bloquent l'export : tester avec `python3 -m http.server` (config `.claude/launch.json`).

## Règles

- Rester sans dépendance payante ni backend.
- Tester chaque modèle, dans ses 3 mises en page, dans les 3 formats (1920, 1350, 1080 px de haut) et avec les deux fonds après une modification de mise en page.
- Nouveau sticker : rester dans la charte (vert, jaune, blanc + couleur de la journée), forme simple lisible en petit.
- Textes santé : conseils généraux uniquement, à faire relire par la pharmacienne.
