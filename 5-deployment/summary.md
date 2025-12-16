# Deployment – Nijmeegse Straattaal Generator

Deze pagina beschrijft het deployment-artefact van mijn MADS project:
een NLP-applicatie die nieuwe Nijmeegse straattaalwoorden genereert.

## Live applicatie
De applicatie draait op een SURF VM en is bereikbaar via:
http://145.38.194.28

## Wat is gedeployed?
- FastAPI backend
- HTML/CSS frontend
- Character-level RNN (PyTorch)
- Docker image + docker-compose
- Automatische startup via `restart: unless-stopped`

## Technische implementatie
De volledige implementatie is te vinden in:
https://github.com/MischTrader/MADS-deployment/tree/main/2-frontend/straattaal

## Reproduceerbaarheid
- Modelconfiguratie: `slanggen.toml`
- Trained model: `artefacts/`
- Build & run: `Makefile`

[← Terug naar portfolio homepage](../README.md)

