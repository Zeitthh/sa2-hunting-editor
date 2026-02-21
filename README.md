# SA2 Hunting Editor

A web-based tool to create, organize, and export hunting sets for **Sonic Adventure 2: Battle (PC Version)**. Built as a companion to the [SA2 Hunting Helper created by starlitluna](https://starlitluna.github.io/sa2-hunting-helper).

---

## What is this?

The editor lets you build the `.ts` files that the Hunting Helper consumes. Each set defines a Piece 1 location, its associated Piece 2s, the Piece 3s for each P2, and the column where it will appear in the guide (Left / Center / Right).

**Supported levels:**

| Group | Levels |
|---|---|
| Hero | Pumpkin Hill · Pumpkin Hill NG · Aquatic Mine · Death Chamber · Meteor Herd |
| Dark | Dry Lagoon · Egg Quarters · Egg Quarters NG · Security Hall · Mad Space |

---

## Tech Stack

- [React](https://react.dev) + [TypeScript](https://www.typescriptlang.org/)
- [Vite](https://vitejs.dev/) as bundler
- SCSS for styles
- `useReducer` + Context API for state management
- `localStorage` for automatic persistence

---

## Getting Started

Requires **Node.js 18+** and any package manager (`npm`, `pnpm`, or `yarn`).

```bash
# Clone the repository
git clone https://github.com/your-username/sa2-hunting-editor.git
cd sa2-hunting-editor

# Install dependencies
npm install       # or pnpm install / yarn install

# Start development server
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

### Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start development server with HMR |
| `npm run build` | Production build output to `/dist` |
| `npm run preview` | Preview the production build locally |

---

## How to Use

1. **Pick a level** from the selector in the left sidebar (Hero / Dark groups).
2. **Create a set** with the `+ New Set` button or `Ctrl+N`.
3. **Select Piece 1** from the dropdown. Pumpkin Hill and Death Chamber have predefined lists grouped by zone; all other levels use free-text.
4. **Add P2 / P3 rows** with `+ P2/P3`. Each P2 row can have multiple P3s. Rows and individual P3s are reorderable by dragging the `≡` handle.
5. **Assign a column** (Left / Center / Right) by dragging the set in the sidebar to the corresponding section.
6. **Export** with the `Export` button or `Ctrl+E` to generate the `LevelName.ts` file.

### Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+Z` | Undo |
| `Ctrl+Y` / `Ctrl+Shift+Z` | Redo |
| `Ctrl+N` | New set |
| `Ctrl+E` | Export |
| `Ctrl+Delete` | Delete active set |

---

## Per-Level Settings

The **⚙ Level Settings** button in the sidebar opens a configuration panel for the active level:

- **Hide Reset Pieces** — mark P1 entries you don't want to appear in the selector. Pumpkin Hill and PH-NG have `La calavera indica el lugar.` marked as a reset piece by default. Users can uncheck it.
- In Pumpkin Hill and PH-NG, P1 entries in the dropdown are grouped by zone: **Church** (blues), **Ghost Train** (greens), **Pumpkin** (reds).

---

## Export Format

The exported file follows the format expected by the Hunting Helper:

```ts
// PumpkinHill.ts
export const SETS = [
  {
    p1: "Familia de calabazas.",
    column: "left",
    pieces: [
      {
        p2: "En una lápida en la ladera",
        p3s: ["Bajo las vías (P)", "Bad Wander", "Ladera Church"],
      },
    ],
  },
];
```

---

## Templates

From the home screen you can load preconfigured templates. The expected format is a `.json` file:

```json
{
  "level": "PumpkinHill",
  "sets": [
    {
      "p1Name": "Familia de calabazas.",
      "column": "left",
      "pieces": [...]
    }
  ]
}
```

The **Iden** template is intended for use in English as the original. The **Zeitthh** template is in Spanish. 

---

## Deployment

See [DEPLOY.md](./DEPLOY.md) for GitHub Pages instructions.

The project can be deployed to any static hosting provider (Netlify, Vercel, Surge, etc.) by pointing it at the `dist` folder after running `npm run build`.

---

## TO-DO

Features that are partially implemented in the UI but pending full functionality:

- **ENG / SPA language switch** — the toggle in Options saves the preference but does not yet translate any interface text. The state infrastructure (`language: 'spa' | 'eng'`) is in place; English hints are still in work in progress.

- **Iden and Zeitthh templates** — the buttons on the home screen are implemented and currently show "coming soon". The actual `.json` template files and their download URLs are still pending.

- **Import from TypeScript** — the Import button in the topbar accepts `.ts` files but currently only reliably parses files exported by the editor itself. Parsing arbitrary TypeScript files (such as those from the main Hunting Helper repo) is pending.

- **Predefined P1/P2/P3 data for most levels** — Aquatic Mine, Meteor Herd, Dry Lagoon, Egg Quarters, Egg Quarters NG, Security Hall, and Mad Space currently use free-text fields. Their curated piece lists have not yet been added to the project.

---
