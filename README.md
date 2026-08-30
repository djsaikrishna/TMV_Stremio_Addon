# InMax - TamilMV Stremio Addon

A high-performance Stremio addon for trending Indian movies with multi-language streams (Tamil, Malayalam, Telugu, Kannada, Hindi), built with Node.js and TypeScript.

Featuring automated GitHub Actions background scraping, real-time UDP torrent tracker health checks, IMDb metadata enrichment, and a zero-database Static CDN / In-Memory caching architecture.

---

## Features

- **Multi-Language Streams**: Scrapes latest releases with audio tracks for Tamil, Malayalam, Telugu, Kannada, Hindi, and Multi-Audio.
- **Ultra-Fast & Zero-Cost Architecture**:
  - Catalog data is cached in static JSON and loaded directly into Node.js RAM for sub-millisecond response times.
  - No database server required (works without Redis; Redis supported as optional fallback).
- **Automated Background Scraping**: GitHub Actions workflow automatically scrapes TamilMV twice daily and syncs fresh stream links.
- **Real-Time Torrent Health**: Scrapes UDP/HTTP trackers for live seeder/leecher counts.
- **Tracker Injection**: Automatically injects 30+ high-performance public trackers to accelerate peer discovery and streaming speed in Stremio.
- **IMDb & Cinemeta Enrichment**: Enriches titles with posters, ratings, genres, and synopses.
- **Resilient Mirror Failover**: Automatically rotates through active TamilMV mirror domains to bypass blocks and Cloudflare protections.

---

## Prerequisites

- **Node.js**: v20+ recommended (v18+ supported)
- **npm**: v9+

---

## Setup & Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/saraV97/TMV_Stremio_Addon.git
   cd TMV_Stremio_Addon
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure Environment Variables:**
   Create a `.env` file in the root directory:
   ```env
   PORT=7000
   TAMILMV_BASE_URL=https://www.1tamilmv.fi/
   MAX_SCRAPE_LIMIT=500
   
   # Optional IMDb API key for richer metadata (falls back to Cinemeta)
   IMDB_API_KEY=your_omdb_key_here

   # Static CDN / Data Source URL (Optional, defaults to local data/movies.json)
   DATA_URL=https://raw.githubusercontent.com/saraV97/TMV_Stremio_Addon/main/data/movies.json
   DATA_REFRESH_MINUTES=15

   # Optional Redis URL (if you prefer using Redis)
   # REDIS_URL=redis://default:...
   ```

4. **Run in development mode:**
   ```bash
   npm run dev
   ```

5. **Build for production:**
   ```bash
   npm run build
   ```

6. **Start production server:**
   ```bash
   npm start
   ```

---

## Available Scripts

| Command | Description |
| :--- | :--- |
| `npm run dev` | Starts development server with live reload (`ts-node-dev`). |
| `npm run build` | Compiles TypeScript into JavaScript (`dist/`). |
| `npm start` | Runs the compiled production server (`dist/index.js`). |
| `npm run scrape:once` | Executes a single TamilMV scrape, metadata enrichment, and torrent health check via `tsx`. |

---

## Automated Background Scraping (GitHub Actions)

This repository includes a scheduled GitHub Actions workflow in [`.github/workflows/scrape.yml`](.github/workflows/scrape.yml):
- **Schedule**: Automatically runs twice daily at `03:00 UTC` and `15:00 UTC`.
- **Manual Trigger**: Can be manually run anytime via the **Actions** tab on GitHub (**Daily TamilMV Scraper** -> **Run workflow**).
- **Auto-Sync**: Automatically commits updated [`data/movies.json`](data/movies.json) back to the repository.

---

## Deployment

### Render.com
A [`render.yaml`](render.yaml) blueprint is included for 1-click deployment on Render:
1. Connect your repository to Render.
2. Deploy as a **Web Service** using the blueprint.
3. Your addon manifest will be live at `https://<your-service-name>.onrender.com/manifest.json`.

---

## License

This project is licensed under the ISC License. See the [LICENSE](LICENSE) file for details.
