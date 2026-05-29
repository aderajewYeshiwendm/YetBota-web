# YetBota-web
<div align="center">

![Yet Bota](https://img.shields.io/badge/Yet%20Bota-Community%20Powered-22C55E?style=for-the-badge&logo=mapbox&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-15-black?style=for-the-badge&logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-v4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Go](https://img.shields.io/badge/Backend-Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)

**A community-powered digital address and local discovery platform built for Ethiopia.**

[Live Demo](#) · [Report Bug](#) · [Request Feature](#)

</div>

---

## Overview

Yet Bota bridges the gap between traditional landmarks and modern digital navigation — letting users find, contribute, and explore local spots using familiar names, Amharic addresses, and community-verified locations across Ethiopia.

> Aligned with **Ethiopia's Digital 2030** strategy, contributing to the digital transformation of local commerce and navigation infrastructure.

---

## Features

- **Local Discovery** — Browse curated and community-contributed places: coffee houses, hidden markets, local parks, and more
- **Digital Addressing** — Assign and find precise digital addresses for everyday spots that don't appear on standard maps
- **AI Assistant** — Ask Yet Bota AI about local events, trending spots, and community insights in natural language
- **Community Q&A** — Ask and answer hyperlocal questions verified by people who actually live there
- **Gamified Contributions** — Earn XP, unlock badges, and climb leaderboards by adding and verifying locations
- **User Profiles** — Track your contributions, reputation level, and earned achievements
- **Bilingual Support** — Full English and Amharic (አማርኛ) language support

---

## Tech Stack

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| [Next.js](https://nextjs.org) | 15 (App Router) | Framework |
| [TypeScript](https://typescriptlang.org) | 5 | Type safety |
| [Tailwind CSS](https://tailwindcss.com) | v4 | Styling |
| [shadcn/ui](https://ui.shadcn.com) | Latest | UI components |
| [Redux Toolkit](https://redux-toolkit.js.org) | Latest | State management |
| [RTK Query](https://redux-toolkit.js.org/rtk-query/overview) | Latest | API data fetching |
| [Lucide React](https://lucide.dev) | Latest | Icons |

### Backend
| Technology | Purpose |
|---|---|
| [Go](https://golang.org) | REST API *(in progress)* |

---

## Project Structure

```
src/
├── app/
│   ├── (auth)/
│   │   ├── signin/          # Sign in page
│   │   ├── signup/          # Sign up page
│   │   └── phone/           # Phone OTP page
│   ├── assistant/           # AI Assistant chat page
│   ├── profile/             # User profile page
│   ├── notifications/       # Notifications page
│   ├── layout.tsx           # Root layout
│   └── page.tsx             # Landing page
│
├── components/
│   ├── landing/             # Landing page sections
│   │   ├── Navbar.tsx
│   │   ├── HeroSection.tsx
│   │   ├── DiscoverySection.tsx
│   │   ├── AssistantSection.tsx
│   │   ├── NavigationSection.tsx
│   │   ├── AccuracySection.tsx
│   │   ├── GamificationSection.tsx
│   │   ├── PrinciplesSection.tsx
│   │   ├── ChampionsSection.tsx
│   │   └── Footer.tsx
│   ├── auth/                # Auth shared components
│   │   ├── AuthCard.tsx
│   │   └── AuthInput.tsx
│   ├── assistant/           # AI Assistant components
│   │   ├── AssistantSidebar.tsx
│   │   ├── ChatBubble.tsx
│   │   ├── ChatInput.tsx
│   │   ├── AssistantPlaceCard.tsx
│   │   └── QuickActions.tsx
│   ├── profile/             # Profile page components
│   │   ├── ProfileSidebar.tsx
│   │   ├── ProfileHeader.tsx
│   │   ├── ReputationCard.tsx
│   │   ├── BadgesCard.tsx
│   │   ├── RecentActivityCard.tsx
│   │   └── ContributionsGrid.tsx
│   ├── notifications/       # Notifications components
│   └── shared/
│       └── AppSidebar.tsx   # Shared sidebar (reusable)
│
├── store/
│   ├── index.ts             # Redux store
│   ├── localeSlice.ts       # EN/AM language toggle
│   ├── api.ts               # RTK Query API endpoints
│   └── hooks.ts             # Typed Redux hooks
│
├── lib/
│   ├── i18n.ts              # Locale helper
│   ├── useContent.ts        # i18n hook
│   ├── utils.ts             # cn() helper
│   ├── dummyData.ts         # Landing page mock data
│   ├── assistantMockData.ts # AI assistant mock data
│   └── profileMockData.ts   # Profile mock data
│
├── content/
│   ├── en.json              # English strings
│   └── am.json              # Amharic strings
│
└── types/
    ├── landing.ts           # Landing page types
    └── css.d.ts             # CSS module declarations
```

---

## Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/yetbota.git
cd yetbota

# Install dependencies
npm install

# Copy environment variables
cp .env.local.example .env.local

# Run development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Environment Variables

```env
# Go backend base URL — RTK Query uses this for all API calls
NEXT_PUBLIC_API_URL=http://localhost:8080/api/v1
```

---

## Pages

| Route | Description |
|---|---|
| `/` | Landing page |
| `/signin` | Sign in with email/password |
| `/signup` | Create a new account |
| `/phone` | Sign in with Ethiopian phone (+251) |
| `/assistant` | AI Assistant chat interface |
| `/profile` | User profile and contributions |
| `/notifications` | User notifications |

---

## i18n — Bilingual Support

Language is toggled globally via Redux and persists across all pages.

```tsx
// Switch language anywhere in the app
import { setLocale } from "@/store/localeSlice";
dispatch(setLocale("am")); // Switch to Amharic
dispatch(setLocale("en")); // Switch to English
```

All strings live in `src/content/en.json` and `src/content/am.json`.

---

## Backend Integration

All components currently use mock data from `src/lib/dummyData.ts`. RTK Query endpoints are defined and ready in `src/store/api.ts`. To connect to the Go backend, simply uncomment the RTK Query hooks in each component:

```tsx
// Before (mock data)
import { COFFEE_HOUSES } from "@/lib/dummyData";

// After (live API)
const { data, isLoading } = useGetPlacesByCategoryQuery("coffee");
const COFFEE_HOUSES = data?.data ?? [];
```

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <strong>Yet Bota &copy; 2024 — Empowering Communities</strong><br/>
  Alignment: Ethiopia Digital 2030
</div>
