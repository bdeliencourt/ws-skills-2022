# Langage Javascript

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- les `structures` de base du langage ✔️
- les normes `ecmascript` ✔️
- l'utilisation de l'`asynchrone` ✔️
- les spécifités du mot-clef `this` ✔️

## 💻 Je code en Javascript

### Un exemple de code commenté ✔️

```javascript
export default function ({
  events,
}: {
  events: EventWithCategory[];
}): string[] {
  // Contains unique categories
  let uniqueCategories: string[] = [];
  // Iterates on each event
  events.forEach(
    (event) =>
      // Append categories not already present in uniqueCategories
      (uniqueCategories = [
        ...uniqueCategories,
        ...event.categories.filter(
          (category) => !uniqueCategories.includes(category)
        ),
      ])
  );
  // Return sorted categories
  return uniqueCategories.sort();
}
```

### Utilisation dans un projet ✔️

#### Bloc-Kit API
Repository privé : me demander les accès :) 

Description : Server side de l'application Bloc-Kit. Il permet le traitement des requêtes du client, l'authentificaiton, l'interrogation à la base de données. ExpressJS, PassportJS, Mongoose, API REST.

#### Bloc-Kit APP
Repository privé : me demander les accès :) 

Description : Client de Bloc-Kit. Cette application web communautaire permet le partage et la création de voies d'escalades à partir de photo. L'utilisateur a la possibilité de voter pour les voies d'autres utilisateurs. Des voies pour s'améliorer et combler ses lacunes lui sont également proposées. Ses statistiques de grimpeur sont également affichées.

### J'ai utilisé ce langage en production ✔️

Bloc-Kit : https://blockit.bdeliencourt.com 
Disclaimer: L'application est hostée sur un RasberryPi. Ne pas hésiter à me soliciter s'il est down.

### J'ai utilisé ce langage en environement professionnel ❌ NOT YET

Description :

## 🌐 J'utilise des ressources

### Bootstrap

- https://getbootstrap.com
- Librarie de composants stylisés permettant la création d'applications mobile-first responsive.

### Passport
- https://www.passportjs.org/
- Middleware d'authentification permettant de définir différentes stratégies d'authentifications (auth0, local, google, facebook, JWT). Utilisation de hash et salt pour encryption des mots de passes 

### Mongoose
- https://mongoosejs.com/
- ODM permettant d'exploiter le SGBD MongoDB.

## 🚧 Je franchis les obstacles

### Point de blocage ❌ / ✔️

Description:

Plan d'action : (à valider par le formateur)

- action 1 ❌ / ✔️
- action 2 ❌ / ✔️
- ...

Résolution :

## 📽️ J'en fais la démonstration

- J'ai ecrit un [tutoriel](...) ❌ / ✔️
- J'ai fait une présentation sur Bootstrap ✔️

