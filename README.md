# Human Atlas — KTM EduTech Edition

An interactive 3D anatomy explorer adapted and branded by **KTM EduTech**, built with React, Three.js, and shadcn/ui.

Explore the human body through an interactive 3D environment based on the **BodyParts3D 4.0 adult male reference anatomy**. The viewer provides **2,234 individually selectable meshes**, **15 anatomical systems**, and **3,432 searchable anatomical concepts**.

> **KTM EduTech Attribution**
>
> This project is a KTM EduTech adaptation and educational presentation of the original Human Atlas application. KTM EduTech has adapted, branded, configured, and extended the project for interactive educational use while retaining attribution to the original application and its third-party anatomy data.

## Explore

- Orbit, zoom, and select anatomical structures directly on the 3D model.
- Toggle individual anatomical systems.
- Use skeleton and organ presets for focused exploration.
- Move between assembled anatomy and an exploded inventory of visible structures.
- Search anatomical names and source identifiers.
- Select and isolate individual structures.
- Inspect structure information through the detail panel.
- Use compact controls and responsive information panels on mobile devices.
- Explore anatomy interactively without requiring an account or API key.

## KTM EduTech Edition

The KTM EduTech edition is designed as an educational anatomy exploration experience within the **KTM EduTech** ecosystem.

The adaptation focuses on:

- Interactive and student-centred learning.
- Clear visual exploration of anatomical structures.
- Responsive use across desktop, tablet, and mobile screens.
- Accessible controls for classroom and independent exploration.
- Educational presentation rather than clinical or diagnostic use.
- KTM EduTech branding and educational design.

**KTM EduTech**  
*Interactive learning through technology.*

## Live Demo

Explore the original/live Human Atlas deployment:

**[https://human-atlas-seven.vercel.app](https://human-atlas-seven.vercel.app)**

> If this fork has its own KTM EduTech deployment, replace the link above with the URL for the KTM EduTech edition.

## Run Locally

Requires **Node.js 22.13 or newer**.

No API keys or user accounts are required.

```sh
npm ci
npm run dev
```

Open:

```text
http://localhost:3016
```

To create a production build:

```sh
npm run build
```

The generated static site is placed in:

```text
dist/
```

## Validate

Run the project validation suite with:

```sh
npm run check
node scripts/validate-atlas.mjs
node scripts/validate-interactions.mjs
npm run build
```

Validation covers:

- Mesh buffers
- Anatomical names
- Concept membership
- Exploded-layout positioning
- Desktop and mobile aspect ratios
- Search behaviour
- Structure inspection
- Interaction contracts
- Tap-versus-drag handling
- Selection and isolation
- System controls
- Rotation
- Responsive layouts

Browser interaction checks have exercised selection, system controls, search, isolation, rotation, and the following layouts:

- `390 × 844`
- `320 × 568`
- `844 × 390`

Phone controls are designed to remain clear of the exploded inventory, while isolated structures are positioned to fit the available space above or beside the detail panel.

> **Testing note:** Physical-device performance and real multitouch hardware have not been fully tested.

## Anatomy Data and Attribution

The anatomy viewer uses **BodyParts3D 4.0**, an adult male reference anatomy dataset licensed under **CC BY 4.0**.

The anatomy data is a third-party resource and is **not owned by KTM EduTech**.

BodyParts3D does not represent every human anatomical structure, anatomical variation, or individual biological characteristic.

Individual source meshes and named anatomical concepts are not necessarily one-to-one. A single named concept may represent or group multiple meshes.

Geometry has been simplified for browser performance while retaining the source mesh collection used by the viewer.

The packaged model contains approximately:

- **2,234 selectable source meshes**
- **2,288,268 triangles**
- Approximately **33 MB of compressed geometry**
- **15 anatomical systems**
- **3,432 searchable concepts**

Full third-party credits, source information, licence details, and adaptation notes are available in:

[`public/ATTRIBUTION.md`](public/ATTRIBUTION.md)

When redistributing the anatomy data or a derivative work containing it, the applicable **CC BY 4.0 attribution requirements must be preserved**.

## Educational Disclaimer

This project is an **educational anatomy explorer**.

It is not intended to provide:

- Medical diagnosis
- Patient-specific medical advice
- Surgical guidance
- Clinical decision support
- Professional medical training or certification

The anatomical information should be treated as an educational representation rather than a complete clinical reference.

## How It Works

The viewer combines React, Three.js, and shadcn/ui to provide an interactive 3D anatomy experience.

Geometry is merged into rendering batches rather than being rendered as thousands of independent draw calls.

Per-structure GPU textures control properties such as:

- Translation
- Visibility
- Selection state

Component geometry supports accurate structure picking.

Exploded layouts are generated from the currently visible structures so that the viewer can separate anatomical pieces while maintaining usable spacing.

Rendering updates when the scene changes, while orbit controls remain responsive during camera interaction.

This architecture allows the application to display a large number of anatomical structures while keeping browser rendering practical.

## WebMCP Integration

The project includes optional WebMCP tools for anatomy search and inspection in compatible browsers.

These tools are optional.

The visible Human Atlas interface remains functional without WebMCP support.

## Rebuilding the Anatomy Geometry

The repository includes browser-ready anatomy geometry, so rebuilding the model is normally unnecessary.

If rebuilding is required, obtain the official **BodyParts3D OBJ archive** and the corresponding English metadata tables.

The general processing workflow is:

```text
BodyParts3D source data
        ↓
OBJ geometry + metadata
        ↓
Concept and system mapping
        ↓
scripts/convert-anatomy.py
        ↓
scripts/optimize-anatomy.mjs
        ↓
scripts/compress-models.mjs
        ↓
Browser-ready anatomy geometry
```

The geometry simplification process uses a **0.2% relative error limit per structure**.

Always verify the current BodyParts3D source terms and attribution requirements before rebuilding or redistributing the anatomy dataset.

## Deployment

The application can be deployed as a static Vite application.

### Vercel

Import the repository into Vercel as a Vite project.

The included [`vercel.json`](vercel.json) configures the project to use:

```text
npm ci
npm run build
```

with:

```text
dist/
```

as the output directory.

The application can also be hosted using other static hosting platforms capable of serving the generated Vite output.

## Technology Stack

- **React** — application interface
- **Three.js** — 3D rendering
- **shadcn/ui** — interface components
- **Vite** — development and production build tooling
- **WebMCP** — optional anatomy interaction tools
- **BodyParts3D 4.0** — third-party anatomy reference data

## Attribution

### KTM EduTech

**KTM EduTech** is responsible for this fork's educational adaptation, branding, interface presentation, configuration, and any original modifications contained in this edition.

**KTM EduTech**  
**Kyd Tantano Masong**

Website:

**[https://www.kydmasong.net](https://www.kydmasong.net)**

### Original Human Atlas Application

This repository is based on the original **Human Atlas** application.

The original application architecture, implementation, and associated contributions remain attributable to their respective original authors and contributors.

Please consult the repository history and original project documentation for detailed authorship and contribution information.

### BodyParts3D

The anatomy data is derived from **BodyParts3D 4.0** and is licensed under **CC BY 4.0**.

The BodyParts3D attribution and source information must be retained when the applicable anatomy data is redistributed or adapted.

See [`public/ATTRIBUTION.md`](public/ATTRIBUTION.md) for the complete attribution information.

## Licensing

The original application code is released under the **MIT License**, unless otherwise stated in the repository or in individual files.

The anatomy data has a **separate CC BY 4.0 licence**.

These licences apply differently:

- **Application source code:** MIT License
- **BodyParts3D anatomy data:** CC BY 4.0
- **Third-party dependencies:** Their respective licences
- **KTM EduTech original adaptations and branding:** Retain the applicable rights and notices associated with those contributions

> **Important:** Do not assume that the MIT licence applies to the third-party anatomy dataset.

When redistributing this project, preserve the relevant copyright, licence, and attribution notices.

## Contributions

Issues and pull requests are welcome.

When reporting an interaction or rendering problem, please include:

- Browser and version
- Operating system
- Device type
- Screen dimensions where relevant
- Steps required to reproduce the issue
- Expected behaviour
- Actual behaviour
- Console errors, if available

## Project Attribution

**Human Atlas — KTM EduTech Edition**

An educational adaptation of an interactive 3D anatomy explorer.

Built with **React, Three.js, shadcn/ui, and BodyParts3D**.

Adapted and branded for educational use by:

**KTM EduTech — Kyd Tantano Masong**

© 2026 KTM EduTech.

Original application and third-party anatomy data remain subject to their respective licences and attribution requirements.
