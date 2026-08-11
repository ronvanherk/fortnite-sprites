# Fortnite Sprites — data voor Sprite Tracker

Deze map wordt door GitHub Pages geserveerd en voedt de Android-app **Sprite Tracker**.

| Bestand | Rol |
|---|---|
| `sprites.json` | De lijst met sprites en varianten. `version` is een hash van de inhoud; verandert die niet, dan doet de app niets. |
| `images/` | Eén WebP per variant, 256 px. Bestandsnaam is de `id` uit `sprites.json`. |
| `index.html` | Galerij met alles erin — de publieke pagina van deze site. |

## Bijwerken

Nieuwe sprite of variant erbij:

1. Zet de afbeelding in `images/` als `<id>.webp`.
2. Voeg de variant toe aan de juiste sprite in `sprites.json`.
3. Wijzig `version` in iets nieuws (elke andere waarde volstaat).
4. Committen en pushen. De app pikt het bij de eerstvolgende start op.

De APK hoeft hiervoor niet opnieuw gebouwd te worden. Alleen als de app zelf verandert.

Sprites zijn eigendom van Epic Games; deze verzameling is voor persoonlijk gebruik.
