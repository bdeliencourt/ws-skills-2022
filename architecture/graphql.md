# GraphQL

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- la différence entre REST et GraphQL ✔️
- les besoins auxquels répond GraphQL ✔️
- la définition d'un schéma ✔️
- Query ✔️
- Mutation ✔️
- Subscription ❌

## 💻 J'utilise

### Un exemple personnel commenté ✔️

# Server side
## Type definition
### Without TypeGraphQL
```javascript 
typeDefs = gql `
  type Wilder {
    id: Int
    name: String
    bio: String
    city: String
    skills: [WilderSkill]
  }
  
  type WilderSkill {
    id: Int
    name: String
    votes: Int
  }
  
  type Query {
    wilders(): [Wilder]
  }
  
  type Mutation {
    addWilder(name: String!) : [Wilder]
  }
`
```
### Using TypeGraphQL
```javascript
// Define GraphQL Type : Type that will be exposed by Request and Mutations
@ObjectType()
class Wilder {
  
  @Field()
  id: number;

  @Field()
  name: string;

  @Field({ nullable: true })
  bio?: string;

  @Field({ nullable: true })
  city?: string;

  @Field({ nullable: true })
  avatarUrl?: string;

  @OneToMany(() => Grade, (g) => g.wilder)
  grades: Grade[];

  @Field(() => [WilderSkill])
  skills: WilderSkill[];
}

// Define GraphQL Input Type: Type that will be used as resolver parameters
@InputType()
export class WilderSkillInput {
  @Field()
  id: number;

  @Field()
  name: string;

  @Field()
  votes: number;
}
```

## Resolver definition
### Without TypeGraphQL
```javascript
const resolvers = {
  Query : {
    wilders : async () => // CODE
    },
  Mutation : {
    addWilder : async (_, args : { name : string } ) => // CODE
  }
```

### Using TypeGraphQL
```javascript
// Define Resolver for Wilder Type
@Resolver(Wilder)
export default class WilderResolver {
  // Define a query
  @Query(() => [Wilder])
  async wilders(): Promise<Wilder[]> {
    // CODE
  }
  
  // Define Mutation
  @Mutation(() => Wilder)
  async addWilder(@Arg("data") data: WilderInput): Promise<Wilder> {
    console.log({ data });
    const wilder = await db.getRepository(Wilder).save(data);
    return await this.wilder(wilder.id);
  }
```

## Apollo Server Instantiation


### Instantiate ApolloServer without TypeGraphQL
```javascript
const server = new ApolloServer({
    resolvers,
    typeDefs,
    csrfPrevention: true,
    cache: "bounded",
    /**
     * What's up with this embed: true option?
     * These are our recommended settings for using AS;
     * they aren't the defaults in AS3 for backwards-compatibility reasons but
     * will be the defaults in AS4. For production environments, use
     * ApolloServerPluginLandingPageProductionDefault instead.
     **/
    plugins: [ApolloServerPluginLandingPageLocalDefault({ embed: true })],
  });
```

### Instantiate ApolloServer with TypeGraphQL

#### Setting Resolver in ApolloServer with TypeGraphQL
```javascript
  const schema = await buildSchema({
    // Resolver classes - types are implicitly linked
    resolvers: [WilderResolver, SkillResolver],
  });
```


```javascript
const server = new ApolloServer({
    schema,
    csrfPrevention: true,
    cache: "bounded",
    /**
     * What's up with this embed: true option?
     * These are our recommended settings for using AS;
     * they aren't the defaults in AS3 for backwards-compatibility reasons but
     * will be the defaults in AS4. For production environments, use
     * ApolloServerPluginLandingPageProductionDefault instead.
     **/
    plugins: [ApolloServerPluginLandingPageLocalDefault({ embed: true })],
  });
```

#Client side

## Call a query
```javascript
query GetAdminRoleSAML($groups: [String!]!) {
    getCurrentAdminRolesFromSAML(groups : $groups)
}
```
### Utilisation dans un projet ❌

[lien github](...)

Description :

### Utilisation en production si applicable ❌

[lien du projet](...)

Description :

### Utilisation en environement professionnel ✔️

Description : At PixPay, GraphQL is highly used.

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
