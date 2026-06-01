# Imperial Fists — Chapter Site

> *"The time for speeches is done. They are coming. Kill them all."*
> — Rogal Dorn

Site communautaire dédié au chapitre des Imperial Fists issue de l'univers Warhammer 40k, VIIème Légion de l'Adeptus Astartes. Conçu comme un espace de lore et de fraternité pour les fans du chapitre.

---

## Structure du projet

```
DevWeb-1/
├── index.html          # Page d'accueil — hero, lore, citation
├── login.html          # Authentification (connexion / inscription)
├── profile.html        # Profil utilisateur
├── contacts.html       # Brotherhood — recherche et gestion des contacts
├── messages.html       # Messagerie privée entre membres
│
├── css/
│   └── style.css       # Styles globaux, variables CSS, composants partagés
│
├── js/
│   └── main.js         # Logique partagée (navbar, scroll, animations)
│
└── assets/
    └── images/         # Illustrations — hero, lore cards, backgrounds
```

---

## Pages

### `index.html` — Accueil
Page vitrine du chapitre. Composée d'une section hero plein écran avec l'emblème, d'une section lore en quatre cartes illustrées (Origines, Doctrine, Flotte, Successeurs), et d'une citation de Rogal Dorn. La navbar détecte la session et affiche dynamiquement les boutons Contacts et Profil si l'utilisateur est connecté.

### `login.html` — Authentification
Formulaire de connexion et d'inscription géré intégralement via Supabase Auth. À la connexion, redirige vers l'index. Crée une entrée dans la table `profiles` à l'inscription avec pseudo et discriminator générés aléatoirement.

### `profile.html` — Profil
Affiche les informations du membre connecté (pseudo, discriminator, avatar, email). Permet la mise à jour du profil et l'upload d'un avatar personnalisé stocké dans Supabase Storage.

### `contacts.html` — Brotherhood
Interface de gestion sociale en trois onglets : recherche de membres par pseudo, liste des contacts acceptés avec accès direct à la messagerie, et gestion des demandes d'amitié reçues.

### `messages.html` — Messagerie
Messagerie temps réel entre deux membres. Affiche la liste des conversations à gauche et le fil de messages à droite. Les messages sont synchronisés en direct via les Realtime Subscriptions de Supabase.

---

## Outils & technologies

| Outil | Usage |
|---|---|
| **HTML / CSS / JavaScript** | Stack frontend vanilla, sans framework |
| **Supabase** | Base de données PostgreSQL, authentification, storage, realtime |
| **Supabase Auth** | Gestion des sessions utilisateur |
| **Supabase Realtime** | Synchronisation en direct des messages |
| **Supabase Storage** | Hébergement des avatars uploadés |
| **Google Fonts** | Typographies — Cinzel, Cinzel Decorative, Crimson Text |
| **DiceBear API** | Génération d'avatars par défaut |

---

## Base de données

Deux tables principales dans Supabase :

**`profiles`** — Un enregistrement par utilisateur, lié à `auth.users`. Contient le pseudo, le discriminator (4 chiffres), et l'URL de l'avatar.

**`contacts`** — Gestion des relations entre membres. Un enregistrement par relation avec les champs `requester_id`, `addressee_id`, et `status` (`pending` ou `accepted`). Les policies RLS garantissent que chaque utilisateur ne peut voir et modifier que ses propres relations.

**`messages`** — Historique des messages privés. Chaque message est lié à un `sender_id` et un `receiver_id`. La souscription Realtime écoute les nouveaux messages entrants pour les afficher instantanément.

---

## Identité visuelle

Palette sombre centrée sur le noir `#0a0a0f` et l'or `#C9A84C`, en référence aux couleurs du chapitre. Typographie Cinzel pour les titres (évocation lapidaire, romaine), Crimson Text pour les corps de texte. Les illustrations de fond sont assombries par des overlays pour maintenir la lisibilité tout en préservant l'atmosphère.