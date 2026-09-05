# Kota Student Guide

## Overview

Full-stack student location discovery web app for Kota, Rajasthan. Helps JEE/NEET aspirants find essential services — PGs, coaching institutes, food, transport, hospitals, parks, and more — with a map-based interface, reviews, and AI recommendations.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React 19 + Vite + Tailwind CSS
- **Map**: Leaflet + react-leaflet
- **AI**: OpenAI via Replit AI Integrations (for `/api/ai/recommend`)

## Artifacts

- **`artifacts/kota-guide`** — React + Vite frontend at `/` (port 23915)
- **`artifacts/api-server`** — Express API server at `/api` (port 8080)

## Key Features

1. **Map view** — Leaflet map with Kota-centered tiles, place markers, search, category filter chips
2. **Explore page** — Filter by category, price range, rating, sort by distance/rating/price
3. **Place detail** — 3-metric reviews (Owner Behaviour, Cleanliness, Price Value), add-review form, Google Maps navigation
4. **AI Guide** — Natural language recommendations (e.g. "best PG under ₹5000 near me")

## Categories

Stationery, Cafes, Restaurants, PGs, Libraries, Grocery, Mobile/Laptop, Temples, Parks, Coaching, Transport, Hospitals, Gyms, Hotels, Petrol Pumps, Laundry, EV Charging, Tourist Places

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)

## Database Schema

- `places` — name, category, address, lat, lng, phone, website, priceMin, priceMax, description, imageUrl, isOpen, openTime, closeTime
- `reviews` — placeId (FK), reviewerName, ownerBehaviour (1-5), cleanliness (1-5), priceValue (1-5), comment

## API Routes

- `GET /api/places` — list with filters (category, search, minRating, maxPrice, lat/lng, radius, sortBy)
- `POST /api/places` — create place
- `GET /api/places/:id` — place detail with reviews
- `GET /api/places/nearby` — nearby places with distance
- `GET /api/places/stats` — dashboard stats
- `GET /api/places/top-rated` — top rated places
- `GET /api/reviews?placeId=` — reviews for a place
- `POST /api/reviews` — add review
- `GET /api/categories` — categories with counts
- `POST /api/ai/recommend` — AI natural language search

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
