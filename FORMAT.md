# Default Canvas Templates

These JSON files are seeded into `config/canvas-templates/` in the user data
directory on startup. They define the templates shown in the sidebar's
**New Canvas** submenu. Blank canvases are built into the app and do not have a
template file.

## Adding a custom template

Drop a JSON file into `config/canvas-templates/` next to the seeded templates.
It will be picked up on the next app launch. Format:

```json
{
  "id": "my-canvas",
  "name": "My Canvas",
  "icon": "layout-grid",
  "order": 100,
  "edgeDefaults": {
    "fromEnd": "none",
    "toEnd": "arrow",
    "edgeType": "orthogonal"
  },
  "seed": {
    "nodes": [],
    "edges": [],
    "x-clairvoyance": {
      "template": "my-canvas",
      "edgeDefaults": {
        "fromEnd": "none",
        "toEnd": "arrow",
        "edgeType": "orthogonal"
      }
    }
  }
}
```

| Field | Required | Notes |
|-------|----------|-------|
| `id` | yes | Unique identifier. |
| `name` | yes | Display name in the New Canvas submenu. |
| `seed` | yes | Valid JSON Canvas data with `nodes` and `edges` arrays. Unknown top-level keys are preserved. |
| `icon` | no | Icon name from `src/utils/iconResolver.ts`. Unknown or missing names use the generic fallback. |
| `order` | no | Sort key; unordered templates sort last by name. |
| `structure` | no | Structured renderer kind: `hierarchy`, `mindmap`, or `bands`. Omit for ordinary seed-only canvases. |
| `edgeDefaults` | no | Defaults for new edges: `fromEnd`, `toEnd`, and `edgeType`. |
| `version` | no | Bundled templates only: bumping it refreshes user copies of the same file on upgrade. |

Malformed files are skipped with a console warning and never prevent the app
from starting. Editing a seeded file works, but a future bundled version bump
will refresh its app-owned fields. Custom files are never touched by seeding.
