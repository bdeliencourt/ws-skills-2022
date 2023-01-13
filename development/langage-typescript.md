# TypeScript

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- l'intéret de TypeScript dans l'IDE ✔️
- les types de bases ✔️
- comment et pourquoi étendre une interface ✔️
- les classes et les decorators ✔️

## 💻 J'utilise

### Un exemple personnel commenté ✔️

### TypeScript
TypeScript transforms Javascript language in a typed language. While transpiling all .ts files to .js files, all variables types are checked and errors are notified to the user through the IDE. Typescript configuration is loaded from ``tsconfig.json``.

#### Types
##### Basic types
```
boolean, number, string, [], Array<type>, any, object
```
##### Complex array
```
Array<Array<number>>, number[][]
```


### Define Wilder interface

#### Interface
```javascript
interface Wilder {
  name: string;
  city?: string | null;
  bio?: string | null;
  avatarUrl?: string | null;
  skills?: ISkill[];
}

//?: The property is optional
```

#### Type
```javascript
type ISkill {
  id: number;
  name: string;
}
```

### Define a variable as Wilder
```javascript
  const [editedWilder, setEditedWilder] = useState<Wilder>({
    name: "",
    id: -1,
    skills: [],
    avatarUrl: undefined,
    city: undefined,
  });
```
Since ``editedWilder`` is typed as ``Wilder``, the default value provided in the useState() must follow the Wilder type definition. Otherwise the transpiling from TypeScript to JavaScript with ``ts-node-dev`` will trigger an error in the IDE.

### Inheritance with interface
Inherance can be used to extends interface : either with ``extends`` or ``&``

#### Extends
```javascript
interface ISkill {
  id: number;
  name: string;
}

interface ISkillWithScore extends ISkill{
  votes: number
}
```

### Overloading
Inherance can be used to extends interface.

#### & operator - for type
```javascript
type ISkill {
  id: number;
  name: string;
}

type ISkillWithScore = ISkill & { votes: number };
const mySkill : ISkill = { id : 1, name: "React"};

// The following lines are the same
const mySkill : ISkill & { votes: number } = { id : 1, name: "React", votes: 10 };
const mySkill : ISkillWithScore = { id : 1, name: "React", votes: 10 };

```

#### Extends - for interface
```javascript
interface ISkill {
  id: number;
  name: string;
}

interface ISkillWithScore extends ISkill{
  votes: number;
}

const mySkill : ISkillWithScore = { id : 1, name: "React", votes: 10 };
```

### Cast a variable 
```javascript
let myString : any = "word"
const stringLength = (myString as string).length
```

### Inference
At initialization, common types are inferred and doesn't need to be defined.
```javascript
const i = 3 // i is typed as a number
```

### Utilisation dans un projet ❌ / ✔️

[lien github](...)

Description :

### Utilisation en production si applicable❌ / ✔️

[lien du projet](...)

Description :

### Utilisation en environement professionnel ✔️

Description : At PixPay all back-ends are using TypeScript.

## 🌐 J'utilise des ressources

### Titre

- lien
- description

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
- J'ai fait une [présentation](...) ❌ / ✔️
