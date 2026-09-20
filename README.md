# Fomo

### Find Out More Often

<p align="center">
  <img src="https://github.com/user-attachments/assets/f5b235a2-1827-4c0b-911a-8a052b133f4d" alt="Discover nearby events on the Fomo map" width="30%" />
  <img src="https://github.com/user-attachments/assets/acbd5db3-64c0-4b41-abea-126e0ecb4541" alt="Browse posts and top moments from an event" width="30%" />
  <img src="https://github.com/user-attachments/assets/9ffa9189-6369-4069-a59d-3b59138c9d99" alt="Create a post for an event" width="30%" />
</p>

### Try Fomo

- [Download on the App Store](https://apps.apple.com/us/app/fomo-find-out-more-often/id6765584105)
- [Use Fomo on the web](https://fomo-app.dev/links)

## Built with

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Expo](https://img.shields.io/badge/Expo-000020?style=for-the-badge&logo=expo&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![Turborepo](https://img.shields.io/badge/Turborepo-EF4444?style=for-the-badge&logo=turborepo&logoColor=white)
<br />
![Convex](https://img.shields.io/badge/Convex-EE342F?style=for-the-badge&logo=convex&logoColor=white)
![Clerk](https://img.shields.io/badge/Clerk-6C47FF?style=for-the-badge&logo=clerk&logoColor=white)
![Mapbox](https://img.shields.io/badge/Mapbox-000000?style=for-the-badge&logo=mapbox&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)

Fomo is a social map for local events. Browse what's happening nearby, see
which events your friends plan to attend, RSVP, and share photos or videos.

#### 🏆 Fomo won [1st Place in Computer Science](https://www.unlv.edu/announcement/howard-r-hughes-college-engineering/unlv-engineering-celebrates-winning-student) at UNLV's Spring 2026 Senior Design Competition

### Project materials

- [Poster](https://docs.google.com/presentation/d/e/2PACX-1vQfSpEVJoLUrZtYGTrTMBm5VBiXEIKGnLJVlZuufyXZk-h887Up-kEuOHfO2RERyGpGXEJcNrKcJaU5/pub?start=false&loop=false&delayms=3000&slide=id.g3dec73974a2_0_0)
- [Presentation slides](https://docs.google.com/presentation/d/e/2PACX-1vRSQbP5SJb4Ld6oV1tgnjmFWFk2lx4lzT45iqu6D_xrujqNrqd7GyncG6O31XqG8l1zV6bzfbJ2bE8v/pub?start=false&loop=false&delayms=3000)

## How it works

1. Browse nearby events on the map or search by place, event, or tag.
2. RSVP as going or interested and choose which updates you want to receive.
3. Post photos, videos, and comments before, during, or after an event.
4. See friends' profiles, event posts, and top moments.

## Features

### Event discovery

- Mapbox maps on mobile and web
- Markers that cluster when events overlap and spread apart when selected
- Ticketmaster events alongside events created in Fomo
- Text and voice search, tag filters, and directions in installed map apps

### Recommendations

- PyTorch two-tower model that scores user activity against event tags, time, and price
- Reranking based on friends attending, preferred days and times, event diversity, and newly added events
- Collaborative filtering for friend suggestions based on shared attendance and tags

### Event activity

- Going, interested, and not interested RSVPs
- Notification preferences for each event
- Photo and video posts with reactions, comments, and replies
- Top moments, attendee lists, and past events on profiles

### Social and account tools

- Profiles, friend requests, and friends-only posts
- Camera and gallery uploads with draggable media ordering
- Email, Google, and Apple sign-in through Clerk
- Password changes, connected accounts, device history, and remote sign-out
- Post reports, user blocking, and account deletion

## Architecture

Fomo is a pnpm and Turborepo monorepo. The Expo app and the Next.js app share a
Convex backend, typed environment configuration, and design tokens.

| Path               | Purpose                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------- |
| `apps/mobile`      | Expo app for maps, media capture, event activity, and notifications                         |
| `apps/web`         | Next.js landing site and browser app for maps, event discovery, and profiles                |
| `packages/backend` | Convex data model and APIs for auth, events, feeds, friends, moderation, and data ingestion |
| `packages/data_ml` | PyTorch event ranking and reranking plus collaborative friend recommendations               |
| `packages/theme`   | Shared palette and design tokens for native and web                                         |
| `packages/env`     | Typed environment validation for the backend, mobile app, and web app                       |

## Development

### Requirements

- Node.js 20 or newer
- pnpm 10.33.0
- Python 3.14 and `uv` for recommendation development
- Xcode for iOS development or Android Studio and JDK 17 for Android development

### Install

```bash
git clone https://github.com/Fomo-Find-Out-More-Often/fomo.git
cd fomo
pnpm install
```

### Configure environment variables

Copy each required `.env.example` file to `.env.local`, then add the values for
the application you want to run.

| Location                        | Used by                            |
| ------------------------------- | ---------------------------------- |
| `apps/web/.env.example`         | Next.js, Clerk, Convex, and Mapbox |
| `apps/mobile/.env.example`      | Expo, Clerk, Convex, and Mapbox    |
| `packages/backend/.env.example` | Convex, Clerk, and Ticketmaster    |

The applications validate required environment variables at startup.

### Run the web app

```bash
pnpm dev:web
```

This starts the Next.js app and the Convex backend.

### Run the mobile app

Fomo uses Expo development builds because it depends on native modules. Build
and install the app once for your platform:

```bash
pnpm dev:ios
# or
pnpm dev:android
```

After the development build is installed, start Metro and the Convex backend:

```bash
pnpm dev:mobile
```

Use `pnpm dev` to run the full monorepo development workflow.

<details>
<summary>Mobile setup and troubleshooting</summary>

Fomo does not run in Expo Go. If Metro reports that no development build is
installed, run `pnpm dev:ios` or `pnpm dev:android` before starting Metro again.

iOS development requires macOS and Xcode. Android development requires Android
Studio, an Android SDK, and JDK 17. If the Android tooling cannot find the SDK,
set its location in your shell configuration:

```bash
export ANDROID_HOME="/path/to/Android/sdk"
export PATH="$PATH:$ANDROID_HOME/emulator"
export PATH="$PATH:$ANDROID_HOME/platform-tools"
```

</details>

### Run the recommendation system

The recommendation package uses Python 3.14 and `uv`. Install its dependencies
and run the tests from `packages/data_ml`:

```bash
cd packages/data_ml
uv sync
uv run pytest
```

Generate the training dataset and train the event recommendation model from
`packages/data_ml/event_rec`:

```bash
cd packages/data_ml/event_rec
uv run python data/generate_training_data.py
uv run python training/trainEventRec.py
```

The friend and event recommendation jobs connect to Convex through
`CONVEX_SITE_URL` and `CRON_SECRET`:

```bash
cd packages/data_ml
uv run friendRec/friendRecs.py
uv run event_rec/recommendEvent.py
```

Both jobs update recommendation rows in Convex. Point them at a development
deployment unless you intend to update production data.

### Run the backend only

Set the required Convex deployment variables from `packages/backend`:

```bash
pnpm exec convex env set VARIABLE_NAME value
```

Then, from the repository root, start Convex in development mode. It watches
the backend functions for changes.

```bash
pnpm dev:backend
```
