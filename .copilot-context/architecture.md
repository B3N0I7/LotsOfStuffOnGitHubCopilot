# Architecture du projet

## Frontend (React TypeScript)
- `src/components` : composants réutilisables (Header, Footer, Menu, etc.)
- `src/pages` : pages principales (Register, Login, AddWord, ListWords, QuizWord, LearningWords)
- `src/services` : appels API via `fetch`
- `src/context` : état global (React Context API)
- `src/hooks` : hooks personnalisés
- `src/types` : types et interfaces partagées

## Backend (.NET)
- `Controllers` : endpoints REST
- `Models` : entités MongoDB
- `DTOs` : objets de transfert
- `Repositories` : couche d’accès aux données
- `Services` : logique métier
- `Auth` : génération et validation des JWT
- `Program.cs` : configuration de l’application

## Base de données
MongoDB héberge les collections suivantes :
- `Users`
- `Words`

### Exemple de flux de données
Login.tsx → fetch('/api/auth/login') → AuthController → UserService → MongoDB
