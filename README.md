# Sky2M-REPO

Data for the [Sky2M](https://github.com/2m3s/Sky2M-26.2) Hypixel SkyBlock mod. When Hypixel rewords a message or a
menu, the fix goes here instead of into a new mod version.

## How the mod uses it

- The mod reads `constants/<Name>.json` from the `live` branch:
  `https://raw.githubusercontent.com/2m3s/Sky2M-REPO/live/constants/<Name>.json`
- Each jar also ships a copy of these files, so features work offline and on the first start.
- Downloaded files are cached in `config/sky2m/repo-cache` and checked for changes every 12 hours, so a change
  reaches players within about 12 hours, or on their next start once the cache is older than that.
- A broken file (bad JSON, a missing field) is logged and ignored: players keep the last good copy.

## Rules for changing a file

- Every file has a `formatVersion`. Keep it the same while you only change values (wording, patterns, numbers).
- If you change a file's layout (rename, move or remove fields), raise `formatVersion` and update the mod to read the
  new layout. Older jars skip files with a `formatVersion` newer than they understand and keep their bundled copy.
- Patterns are Java regular expressions, matched against the text with colour codes removed.
- After changing a file here, copy it into the mod at `src/main/resources/assets/sky2m/repo/constants/` too, so the
  next jar ships it.

## Files

| File | Used for |
|---|---|
| `constants/Carnival.json` | Carnival goals (sentences, the COMPLETE line, menu title), the chat lines that start and end Zombie Shootout and Fruit Digging, Fruit Digging hints, board position, fruit values and head textures, the game NPCs for Quick Start |
