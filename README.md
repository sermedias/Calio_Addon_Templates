# Calio Template Library

Public catalog for the template library in Calio Free for Elementor.

## Structure

```text
manifest.json
templates/<slug>.json
pages/<slug>.json
sections/<slug>.json
screenshots/<slug>.webp
```

Add original, tested Elementor exports and actual screenshots before adding their entries to the manifest. ElementsKit is a UI reference; its templates and artwork are not included.

## Included templates

- **Forma Studio — Calio Free**: a responsive creative studio page, saved and exported from Elementor. It uses only Calio Free Advanced Heading, Advanced Button and Accordion widgets, with Elementor containers for layout. No Pro plugin, external images, custom CSS or paid fonts are required. Replace the demo copy and `hello@example.com` before using it for a business.
- **Accordion**: the original uploaded accordion section.

## Automatic Free / Pro classification

Calio reads each export's actual nested element tree when refreshing the catalog. Templates containing only Free widgets appear under **Free**. A single Calio Pro widget anywhere in that tree moves the entire template to **Pro**. You do not set a `tier` manually in this manifest; widget ownership comes from the widget catalog shipped with Calio Free, even when Pro is not installed.

Pro layouts remain previewable, but insertion requires an active, compatible and licensed Calio Pro plugin. The server re-downloads and re-checks the JSON before every import and rejects Pro content before importing any media. A stale or manually altered Free label cannot bypass this check. Other required widgets must also be installed and enabled. Unknown Calio widget names are locked conservatively until the Free plugin recognizes them.

## Add a template

1. Build the design with Elementor and enabled Calio widgets. Use only Free widgets for a Free template; including any Calio Pro widget makes it a Pro template automatically. Classic layouts and registered Elementor Atomic elements (including e-flexbox) are supported. The destination site must have every element and widget used by the design enabled. Calio preserves and remaps Atomic local style references during import.
2. Export the design as Elementor JSON. Place it in `templates/`, `pages/` or `sections/`.
3. Capture the actual design and add a PNG, JPG or WebP preview under `screenshots/`. Use a descriptive, versioned name when replacing an image, e.g. `agency-home-v2.webp`. Prefer optimized previews under 300 KB.
4. Add an entry to `manifest.json` and commit JSON, image and catalog together to `main`:

```json
{
  "version": 1,
  "items": [
    {
      "id": "agency-home",
      "title": "Agency Home",
      "type": "pages",
      "categories": ["Agency", "Business"],
      "file": "pages/agency-home.json",
      "thumbnail": "screenshots/agency-home-v1.webp"
    }
  ]
}
```

IDs must be unique lowercase slugs. Paths are repository-relative and may contain letters, numbers, hyphens, underscores and directory separators. Do not use full URLs, spaces, query strings or `..`. `type` is exactly `templates`, `pages` or `sections`.

Each item inserts a single Elementor layout into the current document. `templates` represents reusable layouts, not a full website kit installer. Import preserves the current page settings and global site styles. Calio generates new element IDs, imports media through Elementor and rejects missing widget dependencies. Editors can undo the insertion before saving the document. Imported media can remain in the Media Library after undo.

Imports require permission to edit the destination, upload files and use unfiltered HTML. No site URL, account details or credentials are sent in the GitHub catalog request. GitHub receives normal connection metadata; previews load directly from GitHub after the editor clicks Load library. Template content may reference media hosts, so use only public assets you have rights to distribute, with no localhost URLs or site-specific IDs.

Calio reads `https://raw.githubusercontent.com/sermedias/Calio_Addon_Templates/main/manifest.json`, caches successful catalogs for six hours, and can retain a last-known catalog for one week during network failures. Refresh bypasses the WordPress catalog cache; GitHub may still cache raw files briefly.

The repository contains data and images only, never executable PHP or JavaScript. Keep every template and bundled asset compatible with this repository's license and record any required third-party asset attribution. No GitHub token is required for a public catalog. Large libraries may later move to a dedicated CDN without changing the catalog format.
