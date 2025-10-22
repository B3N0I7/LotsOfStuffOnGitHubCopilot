# Entités principales

## User
| Champ | Type | Description |
|--------|------|--------------|
| Id | ObjectId | Identifiant Mongo |
| Username | string | Nom d'utilisateur unique |
| PasswordHash | string | Hash Bcrypt du mot de passe |

## Word
| Champ | Type | Description |
|--------|------|-------------|
| Id | ObjectId | Identifiant Mongo |
| French | string | Mot en français |
| English | string | Traduction anglaise |
| UserId | ObjectId | Référence à l'utilisateur propriétaire |

## QuizWord
| Champ | Type | Description |
|--------|------|-------------|
| WordId | ObjectId | Référence au mot |
| Correct | bool | Résultat du quiz |
| Date | DateTime | Date du test |
