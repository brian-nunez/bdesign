# bdesign

Brian Nunez's design files: editable FigCraft sources for sites and products, each committed with per-frame SVG exports and a PNG preview so anyone can view a design on GitHub. It holds design artifacts only, never production code. It currently contains one design, the b8z.me redesign, ready for review.

## Layout

- `<design>/`: one kebab-case folder per design (for example `b8z-me/`), named after the site or product.
  - `<design>/<name>.figcraft`: the editable source and the single source of truth.
  - `<design>/svg/`: one SVG per top-level frame, kebab-case names (`desktop-home.svg`).
  - `<design>/preview.png`: the main frames side by side on the design's background, for the README.
- `docs/images/`, `docs/brand/`: media used only by `README.md`.
- `docs/adr/`: decision records.

## Commands

FigCraft ships `figcraft-cli` inside its AppImage; it is not on `PATH` by default. Pass `--no-system-fonts` so renders match on every machine (the designs use FigCraft's built-in Inter and Liberation Mono).

```sh
figcraft-cli info <design>/<name>.figcraft                                   # list pages and frames
figcraft-cli export <design>/<name>.figcraft -o <design>/svg/ --format svg --no-system-fonts
figcraft-cli export <design>/<name>.figcraft --node "<frame name>" -o frame.png --scale 2 --no-system-fonts
```

`preview.png` is composed from the main frames exported at 1x, side by side on the design's background colour, with 96px gaps and margins:

```sh
magick -background '<bg hex>' desktop.png mobile.png -gravity north +smush 96 -bordercolor '<bg hex>' -border 96 <design>/preview.png
```

## Conventions

- FigCraft exports frames with their display names (`Desktop · Home.svg`); rename them to kebab-case before committing.
- Exported SVGs keep text as outlines. Check them in a browser: librsvg-based viewers cannot draw FigCraft's glow filter and refuse to open them, which is expected.
- A new design adds a row to the Designs table in `README.md` and increments the `designs` badge count.
- Design copy contains no em dashes.

## Commits

Every commit follows [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).

```text
<type>(<scope>): <summary>

<body>

<footers>
```

- **Type**: `feat` (new behavior), `fix` (corrected behavior), `docs`, `refactor` (no behavior change), `perf`, `test`, `build`, `ci`, `style` (formatting only), `chore`, `revert`. A new or changed design is `feat`; a corrected design is `fix`.
- **Scope**: the area changed, from this project's areas: the design folder name (`b8z-me`), `docs`, `repo`. Omit it only when the change spans the whole repository.
- **Summary**: imperative mood, lowercase, no trailing period, 72 characters or fewer. It names the change in behavior: `fix(b8z-me): raise muted text contrast to 8.6:1`, not `fix(b8z-me): update file`.
- **Body**: required unless the summary alone tells a reviewer everything. Wrap at 72 columns. State:
  - **Why**: the problem, bug or need that prompted the change.
  - **What**: the approach, and what now behaves differently.
  - **Impact**: anything a reader must know: follow-ups, trade-offs taken.

  Every sentence carries information a reviewer cannot get from the diff. A body with nothing to add is left out.
- **Footers**: `BREAKING CHANGE: <what breaks and how to migrate>` for incompatible changes (and `!` after the type or scope); `Refs: #<issue>` or `Closes: #<issue>` for tracked work.
- One logical change per commit.

## Decisions

Decision records live in [`docs/adr/`](docs/adr/README.md). Decisions costly to reverse get a MADR record before implementation, per [`docs/adr/README.md`](docs/adr/README.md).

## Boundaries

- Never hand-edit files in `<design>/svg/` or `<design>/preview.png`; regenerate them from the `.figcraft` source.
- Never add a design as exports alone; the `.figcraft` source is required ([ADR 0001](docs/adr/0001-use-figcraft-as-the-design-source-format.md)).
- Do not commit generator scripts, command scripts (`.json`) or scratch exports unless Brian asks for them.
- This repository is public: no IP addresses, internal hostnames, ports or secrets in designs or docs.
