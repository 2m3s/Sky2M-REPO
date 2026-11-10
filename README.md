# Sky2M-REPO

Data for the [Sky2M](https://github.com/2m3s/Sky2M-26.2) Hypixel SkyBlock mod. When Hypixel rewords a message, a menu
or an item, the fix goes here instead of into a new mod version.

## How the mod uses it

- The mod reads `constants/<Name>.json` from the `live` branch:
  `https://raw.githubusercontent.com/2m3s/Sky2M-REPO/live/constants/<Name>.json`
- Downloaded files are cached in `config/sky2m/repo-cache` and checked for changes every 12 hours, so a change
  reaches players within about 12 hours, or on their next start once the cache is older than that.
- A broken file or entry (bad JSON, a regex that doesn't compile, a table of the wrong shape) is logged and ignored:
  players keep what they had.
- Every file has a `formatVersion`. Keep it while you only change values. If a file's layout changes, raise it and
  update the mod; older jars skip files newer than they understand.

## Fixing a pattern (`constants/Regexes.json`)

Sky2M reads Hypixel's chat, menus, lore, tab list and scoreboard with about 700 named patterns. Their defaults are
built into the mod and listed in `reference/AllRegexes.json`, by key (`<package>.<Class>.<FIELD>`).

To replace one, copy its entry into `constants/Regexes.json` and change the regex:

```json
{
  "formatVersion": 1,
  "regexes": {
    "garden.PestTimer.PEST_SPAWN": "^\\w+! A \\S* ?Pest has appeared in Plot - (?<plot>.*)!"
  }
}
```

- Patterns are Java regular expressions, matched against the text with colour codes removed. In JSON, write every
  backslash twice (`\\d`, `\\.`).
- Keep the named groups (`(?<plot>...)`) the default has: the mod reads them by name.
- Only replaced patterns go in `Regexes.json`. Removing an entry brings back the default.
- Once a mod version ships the fix itself, remove the entry here.

## Fixing a table (`constants/Tables.json`)

Lists of Hypixel data (drops, NPC, mob and area names, Fetchur's and the Sphinx's answers, warps, fishing and garden
lists, slayer areas) work the same way. Defaults are in `reference/AllTables.json`. Copy a table into
`constants/Tables.json` and change it. A replaced table is used whole, so copy all of it, not just the changed line.
Maps are JSON objects; lists and sets are arrays.

## Other files

| File | Used for |
|---|---|
| `constants/Carnival.json` | Carnival goals (sentences, the COMPLETE line, menu title), the chat lines that start and end Zombie Shootout and Fruit Digging, Fruit Digging hints, board position, fruit values and head textures, the game NPCs for Quick Start. The mod ships a copy of this file; after changing it here, copy it into the mod at `src/main/resources/assets/sky2m/repo/constants/` too. |
| `reference/AllRegexes.json`, `reference/AllTables.json` | Every pattern and table key with its default. Not read by the mod. Regenerate them when the mod adds or changes patterns. |
