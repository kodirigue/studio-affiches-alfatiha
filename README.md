# Studio d'affiches · Pharmacie Al Fatiha

Site 100 % statique : aucun serveur, aucune clé API, aucun abonnement. Coût : 0 F.

**En ligne :** https://kodirigue.github.io/studio-affiches-alfatiha/ (GitHub Pages, dépôt `kodirigue/studio-affiches-alfatiha`). Pour mettre à jour : `git push` sur `main`, le site se met à jour en une minute environ.

## Ce qu'il fait

- **Une charte fixe** : vert enseigne, vert profond, jaune ; titres en Bricolage Grotesque, texte en Inter. Sur chaque affiche : le logo en haut à gauche et la vague contact (téléphone, WhatsApp, repère) en bas.
- **Ma pharmacie** (une seule fois) : nom, slogan, téléphone/WhatsApp, repère, logo.
- **11 modèles** : Produit, Promotion, Ouverts, De garde, Journée santé, Le saviez-vous ?, Vrai ou faux ?, Un conseil ?, Bon mois, Fêtes, Annonce. **3 mises en page par modèle** (aperçus cliquables), deux fonds possibles (clair ou vert) selon le modèle. Mettre un mot entre *étoiles* le surligne en jaune.
- **Textes tout prêts** : près de 70 textes à adapter (produits, promos, gardes, conseils santé, vrai ou faux, fêtes dont Ramadan et Tabaski, annonces, et les 12 mois), en un clic avec « Annuler ». Dates, horaires et prix sont des exemples à vérifier ; les textes santé sont à faire relire par la pharmacienne.
- **Calendrier santé** : 12 journées et mois de sensibilisation avec textes déjà rédigés et un sticker proposé pour chacune (cœur, ruban, moustique…). On peut le changer : 28 stickers dessinés, des emojis, ou sa propre image.
- **Photos prêtes à l'emploi** dans `photos/` (façade, pharmaciennes et pharmaciens, produits ; voir `photos/CREDITS.md`), plus la photothèque personnelle enregistrée sur le téléphone.
- **Formats** : statut WhatsApp 9:16, publication 4:5, carré 1:1. Chaque modèle se recale tout seul. Téléchargement PNG et bouton « Partager » sur mobile.

Tout est enregistré dans le navigateur de l'appareil (localStorage + IndexedDB).

## Avant la mise en ligne

Vérifie `config.js` : ce sont les valeurs affichées à la première ouverture, sur n'importe quel appareil.
Pour un vrai logo : dépose `logo.png` dans ce dossier et mets `logo: "logo.png"`.

À mettre en ligne : `index.html`, `config.js`, `manifest.json`, les `icon-*.png` et le dossier `photos/`.
Inutile d'envoyer `example/` ni les captures `IMG_*.PNG`.

Pour tester sur l'ordinateur, lance un petit serveur (`python3 -m http.server`) plutôt que d'ouvrir le fichier
en double-cliquant : sinon le navigateur bloque le téléchargement des affiches qui contiennent une photo.

## Mise en ligne gratuite (au choix)

**Netlify Drop (le plus rapide, sans compte Git)**
1. Va sur app.netlify.com/drop
2. Glisse le dossier entier dans la page → tu obtiens une adresse en `.netlify.app`
3. Crée un compte gratuit pour garder le site et renommer l'adresse (ex. `affiches-alfatiha.netlify.app`)

**GitHub Pages**
1. Crée un dépôt, pousse ces fichiers à la racine
2. Settings → Pages → Branch `main` / `root` → Save

**Vercel / Cloudflare Pages** : importe le dossier comme site statique, sans commande de build.

## Pour la pharmacienne

Ouvre le lien sur son téléphone, puis menu du navigateur → « Ajouter à l'écran d'accueil » :
l'outil s'ouvre ensuite comme une application.
