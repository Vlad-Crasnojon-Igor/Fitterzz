# Fitterz — AI Virtual Wardrobe

A virtual wardrobe app: upload photos of your clothes, let AI identify them,
and get daily outfit suggestions based on the weather. It started as my
university thesis and I rebuilt it into a containerized, tested application.

> Source is private — available on request. This repository is the showcase.

## How it works

1. You upload a photo of a clothing item.
2. Gemini 2.5 Flash identifies it: category, colors, materials, style,
   warmth. If the API fails or returns junk, a Fashion-CLIP zero-shot
   classifier takes over, and YOLOS-Fashionpedia detections are deduplicated
   by IoU so one garment never appears three times.
3. The app checks the weather (Open-Meteo) and builds outfit suggestions
   from what you already own.
4. AI work runs in Celery/Redis workers, so the interface never blocks.

## Under the hood

- Django 4.2 + DRF, PostgreSQL 15, JWT auth with httpOnly refresh cookies
- Celery + Redis for async AI analysis
- Angular 21 + TailwindCSS PWA — installable, bilingual (EN/RO), dark/light
- 5-service Docker Compose: Nginx, Gunicorn (gevent), PostgreSQL, Redis,
  Celery worker
- Asset splicing: extracting individual items from full-outfit photos

## Testing

50 automated tests over API views, Celery tasks, and the asset splicer,
run by GitHub Actions on every push.

## Stack

Django 4.2 · DRF · PostgreSQL 15 · Celery · Redis · Angular 21 ·
TailwindCSS · Google Gemini 2.5 Flash · Fashion-CLIP · YOLOS-Fashionpedia ·
Open-Meteo · Docker Compose · Nginx · Gunicorn · GitHub Actions
