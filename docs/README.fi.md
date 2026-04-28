# Project Planner — AI-taito OpenCodelle

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** on OpenCode Agent -taito, joka edellyttää ammattimaista projektisuunnitteluprosessia ennen koodin tuottamista, varmistaen selkeän vaatimusanalyysin, arkkitehtuurisuunnittelun, tehtävien jakamisen ja edistymisen seurannan.

## Ominaisuudet

- **Pakollinen suunnittelu** — jokaisen koodin tuottamistehtävän on ensin käytävä läpi suunnittelu, ellei käyttäjä nimenomaisesti ohita sitä
- **Alueen luokittelu** — projektityypin automaattinen tunnistus (Web/CLI/Library/Mobile) ja vastaavien parhaiden käytäntöjen soveltaminen
- **Vaatimusanalyysi** — 14 ulottuvuutta vaatimusten selkeyttämiseen + kolme prioriteettitasoa (P0/P1/P2)
- **Riskien arviointi** — 6 riskiluokan tunnistaminen, luokittelu ja lieventämisstrategiat
- **Arkkitehtuurisuunnittelu** — ASCII-kerroskaavio + tietomalli + API-sopimukset
- **Tehtävien jakaminen** — riippuvuusgraafi + kriittinen polku + aika-arvio
- **Edistymisen seuranta** — kunkin vaiheen kirjaus + virstanpylväiden yhteenveto
- **Ei konflikteja** — ei muuta muiden IDE-lisäosien asetustiedostoja

## Asennus

### Tapa 1: Globaali asennus (suositeltu)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Tapa 2: Projektikohtainen asennus

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Asetukset

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "skill": {
      "project-planner": "allow"
    }
  }
}
```

## Työnkulku

Käyttäjän pyyntö → koodin tuottamistehtävän tunnistus → ohita suunnittelu? → alueen luokittelu → vaatimusanalyysi → tekninen suunnittelu → tehtävien jakaminen → tehtäväpohjainen suoritus

Tuotokset: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Yhteensopivuus

Ei muuta muiden lisäosien `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` asetustiedostoja.

## Lisenssi

MIT
