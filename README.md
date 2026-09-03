# mothership-firmware-releases

Public repo with mothership firmware releases. `manifest.json` is what each
deployed mothership actually checks (on boot, and every 24h) to decide
whether to self-update — treat edits to it as production changes to live
field hardware, not routine doc updates.

A firmware image only ever reads its own compiled-in `OTA_MANIFEST_KEY` — it
never looks at any other key in the manifest. Updating one farm's key is
structurally incapable of affecting another farm's deployment.

## Current manifest keys

| Key            | Farm                          | Status |
|----------------|--------------------------------|--------|
| `lilygo`       | F03 — Black Roots (Tatum, KY) | Legacy generic key that F03's original firmware happens to read. Kept in sync with `lilygo_f03`. New F03 builds should standardize on `lilygo_f03`. |
| `lilygo_f01`   | F01 — Milpa Caracol           | Independent of F03/Ghana — do not need to coordinate changes here with other keys. |
| `lilygo_f03`   | F03 — Black Roots (Tatum, KY) | Primary key for F03 going forward. |
| `lilygo_ghana` | F02 — Ghana                    | Deployment offline / hardware powered down on-site (professor who transported the hardware left it off; not a firmware issue). Ignore this key until the farm is physically back online — there is nothing here an OTA push can fix. |

For *why* a given version exists — root cause, what broke, what the fix
actually was — see the mothership firmware source repo's changelog:
https://github.com/Kiau-Technologies-PBC/Kiau-Tech-monorepo/blob/main/mothership/README.md
That's the canonical history; don't duplicate it here — update this table's
"Status" column only when a deployment's live/offline state changes.
