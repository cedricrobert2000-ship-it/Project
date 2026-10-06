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

## Structure

- `index.html` — toute l'app (HTML, CSS, JS vanilla).
  - **Programme** : `LIFTS` (6 mouvements de force), `WAVE` (cycle de 4 semaines : 5×5 à 80 %, 5×4 à 85 %, 4×3 à 90 %, décharge), `HYP` (exercices de volume en double progression), `SESSIONS`, `SCHEDULE` (planning lundi → dimanche), `WODS` (Hyrox).
  - **Prescriptions** : `forcePresc`, `hypPresc`, `runPresc`, `ergoPresc`.
  - **Moteur de progression** : `finish()` ajuste les training max (Epley + AMRAP), les charges de volume, l'allure 10 km et la base rameur 2000 m ; réenregistrer une séance annule puis réapplique le delta.
  - **Vues** : Aujourd'hui, Semaine, Progrès, Réglages, onboarding.
- `design/forerunner-965/` — maquettes de l'app montre Garmin Forerunner 965 (454×454, rond) pour une séance de force : séance du jour, exercice en cours, reps réalisées, repos, fin de séance. Format `.dc.html` du canvas Design claude.ai, `canvas.json` = index.
