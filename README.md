# TP1 - Questy

## Questy, c'est quoi ?

Questy est une application Vue.js permettant de suivre ses tâches sous forme de quêtes, façon RPG. Chaque tâche devient une quête avec un niveau de difficulté (1 à 5 étoiles), et une date limite, organisée sur un tableau au thème pirate.

## Fonctionnalités

- Création de quêtes (nom, description, difficulté, date limite)
- Organisation en quatre colonnes : Disponibles, En cours, Terminées, Échouées
- Changement de statut d'une quête (Disponible → En cours → Terminée)
- Passage automatique en Échouée des quêtes dont la date limite est dépassée
- Suppression de quêtes
- Persistance des données en local (`localStorage`), sans backend

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

## Structure du projet

```
src/
├── App.vue              # Composant racine : état des quêtes, logique métier
├── Components/
│   ├── Board.vue         # Conteneur du tableau
│   ├── Column.vue        # Une colonne du tableau (Disponibles, En cours, ...)
│   ├── Card.vue          # Une carte de quête
│   └── Form.vue          # Formulaire d'ajout de quête
```

## Technologies

- Vue.js 3 (Options API)
- `localStorage` pour la persistance des données
- CSS thème pirate (polices Pirata One, IM Fell English, Cinzel) en grande partie fait par Claude