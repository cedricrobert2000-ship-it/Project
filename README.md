# APEX

Application d'entraînement hybride (force, volume, course, rameur, Hyrox) avec progression automatique des charges et des allures.

Récupérée depuis l'artifact claude.ai « APEX » pour être développée ici.

## Lancer

Fichier unique, sans build : ouvrir `index.html` dans un navigateur, ou servir le dossier :

```sh
python3 -m http.server 8000
# puis http://localhost:8000
```

Les données sont stockées dans `localStorage` (clé `apex3`). Publiée comme artifact claude.ai, l'app synchronise aussi l'état via `window.claude.use('db')` / `('user')` ; hors claude.ai ce bloc est ignoré.

## Installer sur iPhone

APEX est une PWA : elle s'installe depuis Safari et s'ouvre en plein écran, hors ligne.

1. Héberger le dépôt avec GitHub Pages : Settings → Pages → Source « Deploy from a branch », branche `claude/apex-musculation-app-15najw`, dossier `/ (root)`.
2. Sur l'iPhone, ouvrir `https://cedricrobert2000-ship-it.github.io/Snoop/` dans **Safari**.
3. Partager → « Sur l'écran d'accueil » → Ajouter.

Pour publier une mise à jour, pousser sur la branche puis incrémenter `VERSION` dans `sw.js` ; l'app se met à jour à l'ouverture suivante (réseau d'abord).

## Structure

- `index.html` — toute l'app (HTML, CSS, JS vanilla).
  - **Programme** : `LIFTS` (6 mouvements de force), `WAVE` (cycle de 4 semaines : 5×5 à 80 %, 5×4 à 85 %, 4×3 à 90 %, décharge), `HYP` (exercices de volume en double progression), `SESSIONS`, `SCHEDULE` (planning lundi → dimanche), `WODS` (Hyrox).
  - **Prescriptions** : `forcePresc`, `hypPresc`, `runPresc`, `ergoPresc`.
  - **Moteur de progression** : `finish()` ajuste les training max (Epley + AMRAP), les charges de volume, l'allure 10 km et la base rameur 2000 m ; réenregistrer une séance annule puis réapplique le delta.
  - **Vues** : Aujourd'hui, Semaine, Progrès, Réglages, onboarding.
- `manifest.webmanifest`, `sw.js`, `icons/` — installation PWA et cache hors ligne.
- `design/forerunner-965/` — maquettes de l'app montre Garmin Forerunner 965 (454×454, rond) pour une séance de force : séance du jour, exercice en cours, reps réalisées, repos, fin de séance. Format `.dc.html` du canvas Design claude.ai, `canvas.json` = index.
