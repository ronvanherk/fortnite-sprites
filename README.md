# Fortnite Sprites — data voor Sprite Tracker

Deze map wordt door GitHub Pages geserveerd en voedt de Android-app **Sprite Tracker**.

| Bestand | Rol |
|---|---|
| `sprites.json` | De lijst met sprites en varianten. `version` is een hash van de inhoud; verandert die niet, dan doet de app niets. |
| `images/` | Eén WebP per variant, 256 px. Bestandsnaam is de `id` uit `sprites.json`. |
| `index.html` | Galerij met alles erin — de publieke pagina van deze site. |

Stand: **48 sprites, 249 varianten**, waarvan 191 uitgebracht en 58 nog niet. Verdeeld over twee
seizoenen: Runners (Chapter 7 Season 3) 25 sprites / 161 varianten, Override (Season 4) 23 / 88.

## Bijwerken

Nieuwe sprite of variant erbij:

1. Zet de afbeelding in `images/` als `<id>.webp`.
2. Voeg de variant toe aan de juiste sprite in `sprites.json`.
3. Wijzig `version` in iets nieuws (elke andere waarde volstaat).
4. Committen en pushen. De app pikt het bij de eerstvolgende start op.

De APK hoeft hiervoor niet opnieuw gebouwd te worden. Alleen als de app zelf verandert.

## Waar de gegevens vandaan komen

Bron is [fnsprites.info](https://fnsprites.info/), met twee datafiles — `sprites-data.js` (Runners)
en `sprites-data-s4.js` (Override) — en de art als `spriteimg/<id>.png`.

Of er iets te doen is zie je aan `Last-Modified`:

```bash
curl -sSI https://fnsprites.info/sprites-data.js    | grep -i last-modified
curl -sSI https://fnsprites.info/sprites-data-s4.js | grep -i last-modified
```

Is die datum ouder dan de laatste commit hier, dan is er niets veranderd. Twee dingen om te weten
bij het vergelijken:

- De id's hier zijn korter dan upstream: `_cheatmaster` → `_cheat`, `_loothacker` → `_loot`,
  `_bountyhunter` → `_bounty`, `dumpsterdive` → `dumpster`. Zonder die mapping lijkt de halve
  lijst nieuw.
- `api/releases.php` kan de `unreleased`-vlaggen overrulen, maar staat bewust leeg. Staat er wél
  iets in, dan is dát de actuele releasestatus.

De mtimes op `spriteimg/` zijn geen betrouwbaar signaal: op 16 september 2026 kreeg de hele map in
één klap een nieuwe `Last-Modified`, terwijl 176 van de 225 bestaande afbeeldingen ongewijzigd
bleken. Gebruik ze om te zien *waar je moet kijken*, en vergelijk daarna de bytes.

Afbeeldingen worden geschaald naar 256×256 (LANCZOS) en opgeslagen als WebP met `quality=88` en
`method=6`. Met diezelfde instellingen levert een hercodering van de bron bytegelijke bestanden op,
dus zo controleer je ook of de art hier nog bij is.

Sprites zijn eigendom van Epic Games; deze verzameling is voor persoonlijk gebruik.
