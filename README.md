# Fortnite Sprites — data voor Sprite Tracker

Deze map wordt door GitHub Pages geserveerd en voedt de Android-app **Sprite Tracker**.

| Bestand | Rol |
|---|---|
| `sprites.json` | De lijst met sprites en varianten. `version` is een hash van de inhoud; verandert die niet, dan doet de app niets. |
| `images/` | Eén WebP per variant, 256 px. Bestandsnaam is de `id` uit `sprites.json`. |
| `index.html` | Galerij met alles erin — de publieke pagina van deze site. |

Stand: **48 sprites, 264 varianten**, waarvan 218 uitgebracht en 46 nog niet. Verdeeld over twee
seizoenen: Runners (Chapter 7 Season 3) 25 sprites / 161 varianten, Override (Season 4) 23 / 103.

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
- `api/releases.php` overrult de `unreleased`-vlaggen uit de datafile. Lang stond die leeg, maar
  sinds 26 september 2026 niet meer: Birthday werd daar vrijgegeven zonder dat de datafile
  veranderde. Altijd meenemen dus.

De mtimes op `spriteimg/` zijn geen betrouwbaar signaal: op 16 september 2026 kreeg de hele map in
één klap een nieuwe `Last-Modified`, terwijl 176 van de 225 bestaande afbeeldingen ongewijzigd
bleken. Gebruik ze om te zien *waar je moet kijken*, en vergelijk daarna de bytes.

Afbeeldingen worden geschaald naar 256×256 (LANCZOS) en opgeslagen als WebP met `quality=88` en
`method=6`. Met diezelfde instellingen levert een hercodering van de bron bytegelijke bestanden op,
dus zo controleer je ook of de art hier nog bij is.

**De art komt niet van fnsprites.** Die levert ingezoomde renders op een dichte achtergrond; alle
264 tegels hier zijn transparante uitsnedes van de hele sprite. Bron daarvoor is
`spritelocker.com/sprites/c7s4/<upstream-id>.webp` (512), met
`spritechecklist.org/sprites/s4_<upstream-id>.webp` (256) als achtervang voor sprites die
spritelocker nog niet heeft.

Sprites zijn eigendom van Epic Games; deze verzameling is voor persoonlijk gebruik.
