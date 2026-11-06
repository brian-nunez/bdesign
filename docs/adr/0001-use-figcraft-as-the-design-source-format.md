---
status: "accepted"
date: 2026-11-05
decision-makers: Brian Nunez
---

# Use FigCraft as the design source format

## Context and Problem Statement

bdesign holds Brian's designs for sites and products, starting with the b8z.me redesign. Every design needs one editable source of truth that lives in this repository, plus exports anyone can view on GitHub without installing anything. Designs are often built and revised by coding agents as well as by hand, so the source must be scriptable. Which format should be the source of truth for every design in this repository?

## Decision Drivers

* The source is a plain file in git, with no account or cloud workspace needed to open it.
* Agents can create, edit and export designs headlessly from scripts.
* Exports (SVG per frame, PNG previews) can be regenerated from the source by a command.
* Brian's tool preference: FigCraft is installed locally and is the tool he asked for.
* Designs are not trapped if the tool is ever replaced.

## Considered Options

* FigCraft (`.figcraft`)
* Figma
* Penpot
* HTML and CSS mockups

## Decision Outcome

Chosen option: "FigCraft (`.figcraft`)", because it is the only option that is both a local file committed to git and fully scriptable through `figcraft-cli`, which builds, edits and exports designs without a window. It is also the tool Brian chose.

### Consequences

* Good, because each design is one self-contained file in git, versioned with its exports.
* Good, because agents build and export designs through the same command API the app uses (`figcraft-cli run`, `export`, `render`), so exports are reproducible.
* Good, because FigCraft can write `.fig` and Penpot archives (`figcraft-cli export --format fig|penpot`), which keeps an exit path open.
* Bad, because viewers need FigCraft to edit a design; the committed SVG and PNG exports cover viewing only.
* Bad, because `.figcraft` is a binary zip archive, so git cannot diff or merge it; two people editing the same design must coordinate.
* Bad, because FigCraft is a young tool, and some of its exports trip stricter renderers: the SVG glow filter does not render in librsvg-based viewers.

### Confirmation

Every design folder contains a `.figcraft` source next to its `svg/` exports and `preview.png`. In review, check that no design is added as exports alone and that its exports were regenerated from the committed source with `figcraft-cli`.

## Pros and Cons of the Options

### FigCraft (`.figcraft`)

A desktop design editor whose files are plain archives on disk, with a CLI and MCP server that run the same 400+ commands as the UI.

* Good, because files are local and need no account.
* Good, because `figcraft-cli` scripts the whole lifecycle headlessly: build with `run`, then `export` to SVG, PNG or PDF.
* Good, because it exports to `.fig` and `.penpot` for migration.
* Neutral, because its built-in fonts (Inter, Liberation Mono, among others) keep renders identical across machines, but limit type choices unless system fonts are used.
* Bad, because it is new and less widely known than Figma.
* Bad, because the source file is binary and cannot be diffed.

### Figma

The industry-standard cloud design tool.

* Good, because collaborators and reviewers already know it.
* Good, because it has the largest plugin and community ecosystem.
* Bad, because the source of truth lives in a cloud workspace behind an account, not in this repository.
* Bad, because headless creation and editing from scripts is limited; the REST API reads files but cannot build designs.

### Penpot

An open-source design tool, self-hostable, with SVG-based files.

* Good, because it is open source and can be self-hosted, for example on Brian's homelab.
* Good, because its export archive is JSON and SVG, which is easier to inspect than a binary file.
* Bad, because using it means running and maintaining a Penpot server or depending on its cloud.
* Bad, because it has no headless CLI; building designs from scripts means its plugin or RPC API against a running server.

### HTML and CSS mockups

Designs written directly as web pages.

* Good, because they are text files that git diffs and merges, and they show real layout and interaction.
* Good, because they need no design tool to view.
* Bad, because they are code, not editable design documents; Brian asked for design files, and rejected an HTML mockup offered in place of a FigCraft design.
* Bad, because they blur the line between design and production implementation.

## More Information

* FigCraft: <https://github.com/storytold/figcraft>
* The b8z.me redesign in [`b8z-me/`](../../b8z-me/) was the first design built this way.
* Revisit this decision if FigCraft stops being maintained, or if designs need simultaneous multi-person editing that a binary file in git cannot support.
