# Marketing Strategy Agent - Slack x LinkedIn

Agent IA construit avec **n8n** qui aide à concevoir des stratégies marketing directement depuis Slack, et qui peut publier un post sur LinkedIn **uniquement après validation explicite** de l'utilisateur.

## Fonctionnement

```
Slack (mention du bot)
   -> Webhook n8n
   -> Code JS (nettoyage du message + anti-boucle bot)
   -> AI Agent (OpenAI + mémoire + outils)
        |- Read_Formations : lit un catalogue de formations via API
        |- Post_LinkedIn   : publie un post texte via l'API LinkedIn
   -> Réponse envoyée dans un channel Slack
```

## Fonctionnalités

- Conseils marketing professionnels en réponse aux messages Slack
- Accès à un catalogue de formations (API REST) pour contextualiser les stratégies
- Publication LinkedIn sécurisée : demande de validation avant tout post
- Mémoire de conversation (Simple Memory)
- Protection contre les boucles : les messages du bot lui-même sont ignorés

## Prérequis

- Une instance n8n (cloud ou self-hosted)
- Une app Slack avec Event Subscriptions (événement `app_mention`) et un bot token
- Une clé API OpenAI
- Une app LinkedIn avec OAuth2 et le scope `w_member_social`
- (Optionnel) Une API de catalogue de formations

## Installation

1. Dans n8n : **Workflows > Import from file** et choisir `workflow.json`
2. Configurer les credentials :
   - **OpenAI** sur le node `OpenAI Chat Model`
   - **Slack** sur le node `Send a message`
   - **OAuth2 LinkedIn** sur le node `Post_LinkedIn`
3. Remplacer les placeholders :
   - `YOUR_LINKEDIN_PERSON_ID` dans le prompt de l'AI Agent (ton ID LinkedIn)
   - `YOUR_SLACK_CHANNEL_ID` dans le node `Send a message`
   - `YOUR_FORMATIONS_API_URL` dans le node `Read_Formations`
4. Copier l'URL de production du node `Slack Webhook` dans Slack (Event Subscriptions > Request URL)
5. Activer le workflow

## Sécurité

- Aucune clé API ni token n'est stocké dans ce repo
- Toutes les credentials sont gérées par n8n
- Le post LinkedIn n'est déclenché qu'après demande explicite et validation

## Stack

n8n - OpenAI - Slack API - LinkedIn API - JavaScript

## Auteur

Nombré Alidou Salim

## Licence

MIT
