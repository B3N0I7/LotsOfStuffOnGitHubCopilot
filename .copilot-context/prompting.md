# Instructions pour GitHub Copilot

## Quand j’écris du code dans :
- `/client/src/pages` → proposer des composants React TSX structurés avec hooks.
- `/client/src/services` → générer des appels `fetch` avec gestion des erreurs.
- `/server/Controllers` → générer des contrôleurs REST .NET.
- `/server/Repositories` → écrire du code MongoDB asynchrone avec filtre sur `UserId`.
- `/server/Services` → encapsuler la logique métier, ne pas exposer directement la base.

## Style attendu
- Code clair, bien typé, cohérent avec l’architecture définie.
- Utiliser les noms `WordService`, `UserRepository`, etc.
- Respecter les conventions du fichier `coding-style.md`.

## Exemple de demande typique
> "Ajoute un nouveau service React pour appeler /api/words avec token JWT et gère les erreurs 401."
