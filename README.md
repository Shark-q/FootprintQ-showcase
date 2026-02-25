# 🌍 FootprintQ 

![Next.js](https://img.shields.io/badge/Next.js-16-black?style=flat-square&logo=next.js)
![React](https://img.shields.io/badge/React-19-blue?style=flat-square&logo=react)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-v4-38B2AC?style=flat-square&logo=tailwind-css)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-PostGIS-336791?style=flat-square&logo=postgresql)

Welcome to **FootprintQ** (My 3D Footprint) — A stunning, interactive 3D footprint map application designed to visualize your travel journeys, automatically parse photo locations, and transform your memories into cinematic stories and beautiful annual reports.

> **👇 Live Interactive Map Demo (Story Mode & Explore Mode)**
> 
> *The following is an actual recording of the interactive 3D globe in action:*
> 
> ![FootprintQ Interactive Demo](./demo_preview.webp)

## ✨ Features

- 🗺️ **Interactive 3D Globe & Maps**: Experience your travels on a fully interactive 3D globe powered by **Mapbox GL JS**. Toggle between customized map textures (Satellite, Carto basemaps) and smooth fly-to animations.
- 📸 **Smart Photo Parsing & Batch Upload**: Upload images via drag-and-drop to automatically extract EXIF GPS data and map your footprint.
- 📱 **Cross-Device Uploading via QR Code**: Easily scan a QR code on your PC screen to securely trigger uploads directly from your mobile device into your active session.
- 🤖 **AI-Powered Travel Diaries**: Integrated with **Dashscope (Qwen-VL-Max)** to automatically polish your photo notes and generate context-aware, poetic travel stories.
- 🎬 **Story & Explore Modes**: 
  - **Story Mode**: Sit back and watch a cinematic, auto-panning journey through your geographical footprint with custom camera movements.
  - **Explore Mode**: Focus on your map markers with an atmospheric desaturated basemap and glowing active state indicators.
- 📊 **Annual Reports & Travel Posters**: Generate dynamic, shareable travel posters and map snapshots summarizing your footprint stats (Memories, Cities, Countries crossed).
- 💎 **Modern UI & Responsive Design**: A beautiful, glassmorphism-inspired interface powered by **Tailwind CSS v4**. Works flawlessly across desktop and mobile, implementing silky-smooth bottom sheets (`vaul`) for touch interactions.
- 🌐 **Internationalization (i18n)**: Seamless language switching (English / 简体中文) via Next-intl.

## 🛠️ Tech Stack

- **Core Framework**: [Next.js 16](https://nextjs.org/) (App Router), React 19
- **Geomorphology & Mapping**: Mapbox GL JS, Turf.js
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/)
- **Database Architecture**: PostgreSQL + **PostGIS** for spatial queries
- **ORM**: [Prisma 5.22.0](https://www.prisma.io/)
- **Asset Storage**: [Supabase Storage](https://supabase.com/)
- **Authentication**: [Clerk](https://clerk.com/)
- **AI Capabilities**: Aliyun Dashscope API

## 🧩 Project Architecture

FootprintQ utilizes a modern, decoupled architecture to ensure smooth performance for rendering 3D maps and handling media uploads.

```mermaid
graph TD
    subgraph Frontend [Next.js Client]
        UI[UI Components]
        Map[Mapbox GL JS]
        Store[Zustand State]
        UI <--> Store
        Store <--> Map
    end

    subgraph Backend [Next.js API Routes]
        Auth[Clerk Auth]
        Upload[Upload Sessions API]
        Data[Prisma ORM]
    end

    subgraph External Services
        DB[(PostgreSQL + PostGIS)]
        Storage[Supabase Storage]
        AI[Aliyun Dashscope API]
    end

    Frontend -- REST API --> Backend
    Backend -- DB Connections --> DB
    Frontend -- Direct Upload --> Storage
    Backend -- AI Generation --> AI
    Frontend -- Map Tiles & Geocoding --> Map
```

## 🚀 Getting Started

Follow these steps to set up the project locally:

### 1. Prerequisites
- **Node.js**: v18.17+ or v20+
- **PostgreSQL**: Must have the `postgis` extension installed and enabled locally or via a cloud provider (e.g., Supabase / Vercel Postgres).

### 2. Clone the repository
```bash
git clone https://github.com/Shark-q/my-3d-footprint.git
cd my-3d-footprint
```

### 3. Install dependencies
```bash
npm install
```

### 4. Environment Variables Setup
Create a `.env` file in the root directory. You can copy the structure below and fill in your keys:

| Variable | Description | Required Services |
| :--- | :--- | :--- |
| `DATABASE_URL` | PostgreSQL connection string (transactional) | Your Postgres DB + PostGIS |
| `DIRECT_URL` | Direct connection string for Prisma migrations | Your Postgres DB |
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Clerk public key for client-side auth | [Clerk](https://clerk.com/) |
| `CLERK_SECRET_KEY` | Clerk secret key for backend actions | Clerk |
| `NEXT_PUBLIC_MAPBOX_ACCESS_TOKEN` | Token for rendering the 3D map | [Mapbox](https://account.mapbox.com/) |
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL for storage | [Supabase](https://supabase.com/) |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous key | Supabase |
| `DASHSCOPE_API_KEY` | API Key for Qwen-VL-Max | [Aliyun Dashscope](https://dashscope.aliyun.com/) |

### 5. Database Initialization
Generate your Prisma client and push the schema (with PostGIS extensions) to your database:
```bash
npx prisma generate
npx prisma migrate dev
```

### 6. Run the Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) with your browser to experience FootprintQ.

## 📁 Core Directory Structure

- `src/app/`: Next.js App Router pages (Landing, Login, APIs).
- `src/app/api/`: Backend REST routes covering upload sessions, geocoding reverse lookups, and AI proxying.
- `src/components/`: Modular UI building blocks. `MapboxView.tsx` serves as the heavy-lifting core for map initialization and state management.
- `src/lib/`: Core utilities including Prisma/Supabase clients and the advanced `story-engine/`.
- `public/geojson/`: Boundary data parsing for region mapping.
- `prisma/schema.prisma`: The central truth for our Database Models (`User`, `Journey`, `PhotoNode`, and `UploadSession`).

## 👨‍💻 Developer Notes
- **Styling Rules**: This project uses a CSS-first configuration via `globals.css` with Tailwind CSS v4. No legacy `tailwind.config.js` is utilized.
- **Geocoding Context**: We rely on Amap APIs for domestic (China) geocoding and standard Mapbox geocoding for international locations to handle boundary precision.

## 📜 License
*Project primarily for portfolio and showcase purposes.*