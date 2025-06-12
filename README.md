# 📋 Feedback System – Web App (GraphQL + Node.js + MongoDB)

## 1. ✅ Solution proposée

### 🔍 Analyse du problème
Une entreprise SaaS souhaite recueillir les avis de ses utilisateurs pour améliorer ses produits. Aucun
 système automatisé n'est en place actuellement. Ce projet propose une API GraphQL permettant à un
 utilisateur de laisser une note et un commentaire sur un produit.
### 🧩 Identification des entités & relations
- **User** : peut donner un feedback
- **Product** : reçoit plusieurs feedbacks
- **Feedback** : lie un utilisateur à un produit par un commentaire et une note

Relations :
- Un `User` peut envoyer plusieurs `Feedback`
- Un `Product` peut recevoir plusieurs `Feedback`

### ⚙️ Liste des fonctionnalités (sous forme de services GraphQL)
- **Query :**
  - `users` : récupérer tous les utilisateurs
  - `products` : récupérer tous les produits
  - `feedbacks` : récupérer tous les feedbacks
  - `feedbacksByProduct(productName: String!)` : feedbacks liés à un produit

- **Mutation :**
  - `createUser(username, email)` : ajouter un utilisateur
  - `createProduct(name, description, version)` : ajouter un produit
  - `createFeedback(username, productName, rating, comment)` : ajouter un feedback

---

## 2. 🧾 Diagrammes

### 📦 Diagramme de classes (entités)


User
 -id: ID
 -username: String
 -email: String
 -createdAt: String

Product
 -id: ID
 -name: String
 -description: String
 -version: String
 -createdAt: String

Feedback
 -id: ID
 -username: String
 -productName: String
 -rating: Int
 -comment: String
 -createdAt: String

### 🔗 Schéma GraphQL 

type Query {
  users: [User!]!
  products: [Product!]!
  feedbacks: [Feedback!]!
  feedbacksByProduct(productName: String!): [Feedback!]!
}

type Mutation {
  createUser(username: String!, email: String!): User!
  createProduct(name: String!, description: String, version: String): Product!
  createFeedback(username: String!, productName: String!, rating: Int!, comment: String): Feedback!
}


# 🛠️ Implémentation technique

Web service : GraphQL via Apollo Server
Back-end : Node.js + Express
Base de données : MongoDB
Front-end : Interface simple HTML/JS pour soumettre et voir les feedbacks
Structure de projet propre et organisée :
models/: Schémas de données (MongoDB via Mongoose)
schemas/: Définition du schéma GraphQL (types + opérations)
resolvers/: Logique des requêtes GraphQL (Query + Mutation)
config.js/: Connexion à MongoDB avec Mongoose
index.js/: Point d'entrée de l'application (Apollo Server)

# 🧾 Documentation


 ### 📋 Types GraphQL

 type
 User {
 id: ID!
 username: String!
 email: String!
 createdAt: String
 }
 type
 Product {
 id: ID!
 name: String!
 description: String
 version: String
 createdAt: String
 }
 type
 Feedback {
 id: ID!
 username: String!
 productName: String!
 rating: Int!
 comment: String
 createdAt: String
 user: User
 product: Product
 }


# 🧪 Exemples d’utilisation

Créer un utilisateur :

mutation {
  createUser(username: "alice", email: "alice@mail.com") {
    id
    username
  }
}

Lister les feedbacks :

query {
  feedbacks {
    productName
    comment
    rating
  }
}

### ✍ Mutations (exemples)

 mutation {
 createUser(username: "alice", email: "alice@example.com") {
 id
 username
 }
 }
 mutation {
 createProduct(name: "SaaS Tool", description: "Outil cloud", version:
 "1.0") {
 id
 name
 }
 }
 mutation {
 createFeedback(username: "alice", productName: "SaaS Tool", rating: 5,
 comment: "Excellent") {
 id
 rating
 }
 }


