# Application d'apprentissage de vocabulaire

## Objectif
Application web full stack permettant :
- l'inscription et la connexion des utilisateurs,
- la gestion de mots français ↔ anglais,
- la révision via des quiz et un mode apprentissage.

## Stack technique
- **Frontend** : React + TypeScript (TSX)
- **Backend** : .NET 8 Web API (C#)
- **Base de données** : MongoDB
- **Auth** : JWT + Bcrypt
- **Communication** : API REST (fetch côté client)

## Architecture générale
React (frontend) ↔ .NET API (backend) ↔ MongoDB

## Dossier source
- `/client` : code React
- `/server` : API .NET
