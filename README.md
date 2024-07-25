# Tutoriel Spring Boot: Gestion des Produits et Clients

## Introduction

Ce tutoriel vous guidera étape par étape pour créer une API RESTful avec Spring Boot afin de gérer des produits et des clients. Vous utiliserez MongoDB comme base de données. Un client pourra commander un produit et ajouter des produits à son panier en utilisant cette API.

## Prérequis

- Java Development Kit (JDK) 17 ou supérieur
- Maven 3.2+
- Un IDE comme IntelliJ IDEA ou Eclipse
- MongoDB installé localement

## Étape 1: Créer un Projet Spring Boot

1. Allez sur votre IDE et initialiser un projet Spring
2. Configurez votre projet:
    - **Project**: Maven Project
    - **Language**: Java
    - **Spring Boot**: 3.2.0 (ou la version stable la plus récente)
    - **Group**: com.example
    - **Artifact**: product-client-api
    - **Name**: ProductClientApi
    - **Packaging**: Jar
    - **Java**: 17 (ou votre version JDK)
3. Ajouter les dépendances:
    - **Spring Web**
    - **Spring Data MongoDB**
    - **Lombok** (facultatif pour réduire le code boilerplate)
4.  **Generate le projet** dans votre IDE.

## Étape 2: Configurer l'Application

Vérifiez que votre fichier `application.properties` contient les configurations pour MongoDB. Ajoutez les lignes suivantes dans `src/main/resources/application.properties`:

```properties
spring.data.mongodb.host=localhost
spring.data.mongodb.port=27017
spring.data.mongodb.database=product-client-api
```
## Étape 3: Configurer MongoDB

Assurez-vous que MongoDB est en cours d'exécution sur votre machine. Par défaut, Spring Boot se connectera à MongoDB sur `mongodb://localhost:27017`.

## Étape 4: Créer les Entités

Nous allons créer deux entités: `Product` et `Client`.

### Product

#### Attributs de l'entité `Product`:
- `id`: String
- `name`: String
- `description`: String
- `price`: double
- `quantity`: int

#### Tâches à effectuer:
1. Créez un package `model` dans votre projet.
2. Dans ce package, créez une classe `Product`.
3. Ajoutez les attributs ci-dessus à cette classe.
4. Annoter la classe pour qu'elle soit reconnue comme un document MongoDB.

### Client

#### Attributs de l'entité `Client`:
- `id`: String
- `name`: String
- `email`: String
- `cart`: List<String> (une liste d'IDs de produits)

#### Tâches à effectuer:
1. Dans le même package `model`, créez une classe `Client`.
2. Ajoutez les attributs ci-dessus à cette classe.
3. Annoter la classe pour qu'elle soit reconnue comme un document MongoDB.

## Étape 5: Créer les Repositories

Nous allons créer des repositories pour interagir avec MongoDB.

### ProductRepository

#### Tâches à effectuer:
1. Créez un package `repository` dans votre projet.
2. Dans ce package, créez une interface `ProductRepository` qui étend `MongoRepository<Product, String>`.

### ClientRepository

#### Tâches à effectuer:
1. Dans le même package `repository`, créez une interface `ClientRepository` qui étend `MongoRepository<Client, String>`.

## Étape 6: Créer les Services

Nous allons créer des services pour la logique métier.

### ProductService

#### Méthodes à inclure:
- `getAllProducts()`: Retourne la liste de tous les produits.
- `getProductById(String id)`: Retourne un produit par son ID.
- `saveProduct(Product product)`: Enregistre un produit.
- `deleteProduct(String id)`: Supprime un produit par son ID.

#### Tâches à effectuer:
1. Créez un package `service` dans votre projet.
2. Dans ce package, créez une classe `ProductService`.
3. Injectez `ProductRepository` dans `ProductService`.
4. Implémentez les méthodes ci-dessus.

### ClientService

#### Méthodes à inclure:
- `getAllClients()`: Retourne la liste de tous les clients.
- `getClientById(String id)`: Retourne un client par son ID.
- `saveClient(Client client)`: Enregistre un client.
- `deleteClient(String id)`: Supprime un client par son ID.
- `addProductToCart(String clientId, String productId)`: Ajoute un produit au panier d'un client.

#### Tâches à effectuer:
1. Dans le même package `service`, créez une classe `ClientService`.
2. Injectez `ClientRepository` dans `ClientService`.
3. Implémentez les méthodes ci-dessus.

## Étape 7: Créer les Contrôleurs

Nous allons créer des contrôleurs pour exposer les endpoints REST.

### ProductController

#### Endpoints à inclure:
- `GET /api/products`: Retourne la liste de tous les produits.
- `GET /api/products/{id}`: Retourne un produit par son ID.
- `POST /api/products`: Crée un nouveau produit.
- `PUT /api/products/{id}`: Met à jour un produit existant.
- `DELETE /api/products/{id}`: Supprime un produit par son ID.

#### Tâches à effectuer:
1. Créez un package `controller` dans votre projet.
2. Dans ce package, créez une classe `ProductController`.
3. Injectez `ProductService` dans `ProductController`.
4. Implémentez les endpoints ci-dessus.

### ClientController

#### Endpoints à inclure:
- `GET /api/clients`: Retourne la liste de tous les clients.
- `GET /api/clients/{id}`: Retourne un client par son ID.
- `POST /api/clients`: Crée un nouveau client.
- `PUT /api/clients/{id}`: Met à jour un client existant.
- `DELETE /api/clients/{id}`: Supprime un client par son ID.
- `POST /api/clients/{id}/cart`: Ajoute un produit au panier d'un client.

#### Tâches à effectuer:
1. Dans le même package `controller`, créez une classe `ClientController`.
2. Injectez `ClientService` dans `ClientController`.
3. Implémentez les endpoints ci-dessus.
