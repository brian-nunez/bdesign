<p align="center">
  <img src="docs/brand/icon.svg" width="128" height="128" alt="bdesign icon: a white selection frame with corner handles on a green rounded square">
</p>

<h1 align="center">bdesign</h1>

<p align="center">
  <b>Design files; Brian Nunez's FigCraft designs, with SVG and PNG exports.</b>
</p>

<p align="center">
  Editable FigCraft sources, each with per-frame SVGs and a PNG preview, so you can look without installing anything.<br>
  <i>By Brian Nunez.</i>
</p>

<p align="center">
  <img alt="Made with FigCraft" src="https://img.shields.io/badge/made%20with-FigCraft-1A6E3B?style=flat-square">
  <img alt="Designs: 1" src="https://img.shields.io/badge/designs-1-2E8B4E?style=flat-square">
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-1A6E3B?style=flat-square">
  <br>
  <a href="https://www.linkedin.com/in/brianjnunez/"><img alt="LinkedIn: brianjnunez" src="https://img.shields.io/badge/LinkedIn-brianjnunez-0A66C2?style=flat-square"></a>
</p>

<p align="center">
  <a href="b8z-me/"><img alt="Browse the b8z.me design" src="https://img.shields.io/badge/Browse%20the%20b8z.me%20design-1A6E3B?style=for-the-badge" height="40"></a>
</p>

<p align="center">
  <a href="b8z-me/"><b>b8z.me redesign</b></a> ·
  <a href="https://www.b8z.me/">Current b8z.me</a> ·
  <a href="https://github.com/storytold/figcraft">FigCraft</a> ·
  <a href="https://www.linkedin.com/in/brianjnunez/">LinkedIn</a>
</p>

<br>

<p align="center">
  <img src="docs/images/hero.png" alt="The b8z.me redesign on desktop: a dark page with a green terminal-style logo, the headline &quot;I build accessible products and the systems that keep them running.&quot;, Email me and GitHub buttons, and a row of stats: 8+ years shipping, 300+ production applications, about 10 self-hosted services" width="100%">
  <br><sub><b>b8z.me redesign</b>: the desktop hero, exported from the FigCraft file at 2x.</sub>
</p>

> [!NOTE]
> **Design files only.** Nothing here is production code. Each design is a reviewable artifact; implementations live in their own repositories.

<p align="center">
  <a href="#designs">Designs</a> ·
  <a href="#b8zme-redesign">b8z.me redesign</a> ·
  <a href="#color-reference">Color reference</a> ·
  <a href="#opening-the-files">Opening the files</a> ·
  <a href="#documentation">Documentation</a> ·
  <a href="#license">License</a>
</p>

## Designs

Each design lives in its own folder with the editable source, an SVG per frame and a preview image.

| Design | Preview | Files (.figcraft, SVG, PNG) |
| ------ | ------- | ----- |
| **b8z.me redesign**<br>Personal site for a software engineer: a homelab architecture diagram, experience and projects, on desktop and mobile. | <a href="b8z-me/preview.png"><img src="b8z-me/preview.png" width="220" alt="b8z.me redesign, desktop and mobile frames side by side"></a> | [Source](b8z-me/b8z-redesign.figcraft)<br>[Desktop](b8z-me/svg/desktop-home.svg)<br>[Mobile](b8z-me/svg/mobile-home.svg)<br>[States](b8z-me/svg/states-and-annotations.svg)<br>[Preview](b8z-me/preview.png) |

## b8z.me redesign

A redesign of [b8z.me](https://www.b8z.me/) that keeps its green-on-black terminal identity and adds real proof: the homelab that hosts the site, drawn as an architecture diagram.

- **Three frames.** Desktop (1440 wide), mobile (390 wide), and a sheet of interaction states with handoff notes.
- **Homelab, shape only.** The diagram shows the request path from Cloudflare through a Linode edge and a Tailscale mesh into Proxmox, with no IP addresses, internal hostnames or ports.
- **Readable by default.** Grey text measures at least 8.6:1 against every surface it sits on, above WCAG AAA.
- **States drawn, not implied.** Default, hover, focus and pressed for buttons, nav links and project cards, with a visible 2px focus ring.

<p align="center">
  <a href="docs/images/states.png"><img src="docs/images/states.png" width="100%" alt="Interaction states sheet: primary and secondary buttons, nav links and project cards in default, hover, focus and pressed states, with four handoff notes"></a>
  <br><sub><b>States and annotations</b>: every interactive element in each state, plus notes on semantics, the diagram's text alternative, focus and open items.</sub>
</p>

## Color reference

The b8z.me palette. Every text colour is measured against every surface it sits on.

| Role | Hex |
| ---- | --- |
| Background | ![#070B08](https://dummyimage.com/10/070B08/070B08?text=+) `#070B08` |
| Surface | ![#0D140F](https://dummyimage.com/10/0D140F/0D140F?text=+) `#0D140F` |
| Surface, raised | ![#121B15](https://dummyimage.com/10/121B15/121B15?text=+) `#121B15` |
| Line | ![#223026](https://dummyimage.com/10/223026/223026?text=+) `#223026` |
| Text | ![#EEF3EE](https://dummyimage.com/10/EEF3EE/EEF3EE?text=+) `#EEF3EE` |
| Muted text | ![#AFBCB2](https://dummyimage.com/10/AFBCB2/AFBCB2?text=+) `#AFBCB2` |
| **Signal green** | ![#3DFF6E](https://dummyimage.com/10/3DFF6E/3DFF6E?text=+) `#3DFF6E` |
| Ink on green | ![#04130A](https://dummyimage.com/10/04130A/04130A?text=+) `#04130A` |

## Opening the files

Open a `.figcraft` file in the [FigCraft](https://github.com/storytold/figcraft) desktop app to edit it. The designs use Inter and Liberation Mono, which ship with FigCraft, so they look the same on any machine.

To export without opening the app, use `figcraft-cli`:

```sh
figcraft-cli export b8z-me/b8z-redesign.figcraft -o out/ --format svg    # one SVG per frame
figcraft-cli export b8z-me/b8z-redesign.figcraft -o out/ --scale 2       # one PNG per frame, at 2x
figcraft-cli render b8z-me/b8z-redesign.figcraft -o page.png             # the whole page in one image
```

The SVGs store text as outlines, so they render without the fonts installed. They display correctly in browsers and on GitHub; some librsvg-based viewers, such as GNOME's image viewer, cannot draw the glow filter on the green buttons and refuse to open them.

## Documentation

- [Decision records](docs/adr/README.md): why designs are FigCraft files, and future decisions.
- [Agent guide](AGENTS.md): layout, export commands and commit rules for anyone, human or agent, adding a design.

## License

bdesign is licensed under the [MIT License](LICENSE). Copyright (c) 2026 Brian Nunez.
