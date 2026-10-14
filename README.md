# Foodi

Save restaurants from TikTok and Maps, and remember exactly what to order when you get there.

Mobile app (React Native + Expo) for logging what you ate and how it was — dishes get a verdict
(Skip / Mid / Solid / Elite), restaurants get stars computed from those verdicts.

## Docs

- [`docs/PRD.md`](docs/PRD.md) — MVP product requirements (v2, Oct 14 2026)
- [`docs/DESIGN.md`](docs/DESIGN.md) — design system, v1 locked Oct 14 2026 (tokens, type scale, screen specs)

## Stack

Expo (React Native) · Supabase (Postgres, auth, storage) · Google Places API ·
react-native-maps with clustering · expo-media-library · expo-notifications

## Status

Pre-build. Design v1 locked; next step is Expo + Supabase setup and the thin slice
(map pins → restaurant page → log one dish).
