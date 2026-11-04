# Kirtan Mellows Poster Maker

## Problem Statement

Creating a new Kirtan Mellows event poster currently requires manually editing graphic artwork. That makes updating the event information and sourcing replacement imagery harder than it needs to be. The supplied posters establish a recognizable series, but the workspace contains only flattened JPEGs; their text, marks, and artwork are not available as independently editable layers.

## Solution

Provide a public, static poster-making app that lets a poster maker choose one of four fixed compositions, enter event information, upload a background image and a separate featured image, select a curated color palette, and toggle selected minor decorations. The app previews the result and exports a square 1080×1080 PNG.

The app runs entirely in the browser, with no account, server-side image upload, cloud saving, or built-in background library. It must work on desktop and mobile and be compatible with static hosting on GitHub Pages.

## User Stories

1. As a poster maker, I want to open the app without creating an account, so that I can start making a poster immediately.
2. As a poster maker, I want to use the app on desktop or mobile, so that I can create a poster with the device I have available.
3. As a poster maker, I want to choose among four Kirtan Mellows compositions, so that I can select a layout suited to my event.
4. As a poster maker, I want the split composition to place a featured image on one side and event information on the other, so that the poster follows the reference layout.
5. As a poster maker, I want the scenic composition to place event information over an open area of a full-page background, so that the background remains visible without obscuring the copy.
6. As a poster maker, I want the portrait-led composition to give the featured image visual prominence, so that a portrait or other focal image anchors the poster.
7. As a poster maker, I want the centered-stack composition to group its title, supporting copy, and event information vertically, so that the result follows that layout family.
8. As a poster maker, I want each composition to retain its defined arrangement while I edit it, so that ordinary edits do not accidentally break the design.
9. As a poster maker, I want to upload a full-page background image, so that each event can have its own scene or texture.
10. As a poster maker, I want to upload a separate featured image, so that I can add a portrait, book, illustration, or other focal subject.
11. As a poster maker, I want to see a clear validation message when either required image is missing, so that I know what is preventing export.
12. As a poster maker, I want uploaded images to fill their designated frames automatically, so that images with different aspect ratios still fit the composition.
13. As a poster maker, I want to reposition and zoom each uploaded image within its fixed frame, so that I can keep the important subject visible without changing the layout.
14. As a mobile poster maker, I want image repositioning and zoom to work with touch input, so that I can crop images on a phone or tablet.
15. As a poster maker, I want to enter an event title, so that the poster identifies the event.
16. As a poster maker, I want to choose the event's calendar date, so that the displayed date is based on one unambiguous value.
17. As a poster maker, I want the weekday and ordinal date to update automatically from the selected date, so that the displayed weekday cannot accidentally disagree with the date.
18. As a poster maker, I want to add an optional subtitle, so that I can include a festival name or supporting description when needed.
19. As a poster maker, I want to add optional start and end times, so that attendees can see the event schedule when it is available.
20. As a poster maker, I want separate optional venue and address/postcode fields, so that a physical location can be presented in the same two-part style as the references.
21. As a poster maker, I want to add optional call-to-action copy, so that I can include a short invitation when appropriate.
22. As a poster maker, I want blank optional event fields to disappear from the poster, so that the result contains no empty labels or placeholders.
23. As a poster maker, I want the app to require an event title and date before export, so that each downloaded poster communicates its basic event identity.
24. As a poster maker, I want each composition to have a default color palette, so that a new design starts with coordinated colors.
25. As a poster maker, I want to choose from a small shared set of curated palettes, so that I can vary the appearance while retaining the series' visual character.
26. As a poster maker, I want a palette to affect poster typography, panels, and ornaments without tinting my uploaded photos, so that the source imagery remains intact.
27. As a poster maker, I want to show or hide selected minor decorative accents, so that I can adjust the ornamentation without rebuilding the composition.
28. As a poster maker, I want the Kirtan Mellows identity, mantra text, marks, and standard footer to remain consistent, so that different posters still belong to the same series.
29. As a poster maker, I want to preview my edits before downloading, so that I can review the finished composition.
30. As a poster maker, I want to download the finished design as a 1080×1080 PNG, so that it matches the square format used by the references.
31. As a poster maker, I want my uploaded images to remain in my browser rather than be sent to a service, so that I can make posters without uploading my images to a server.
32. As a poster maker, I want to use the app without cloud saving or an account, so that making and downloading a poster does not require a separate storage workflow.
33. As a poster maker, I want the editor controls to adapt to a mobile viewport while preserving the square poster preview, so that I can complete the same workflow on a phone.
34. As the Kirtan Mellows app maintainer, I want the app to run as static files, so that it can be hosted on GitHub Pages without a backend.

## Implementation Decisions

- Build a static, browser-only app with no server-side image processing, accounts, cloud storage, or upload endpoint.
- Provide four composition-only template families: split, scenic, portrait-led, and centered stack. The template defines element placement and hierarchy, not a preset background image or fixed color theme.
- Keep each composition fixed. Do not provide arbitrary drag-and-drop repositioning of text, branding, or decorations.
- Require both a poster maker-supplied background image and a separate featured image for every composition. The featured image's crop and shape are determined by the selected composition; it is not always circular.
- Use automatic image fitting with user-controlled repositioning and zoom constrained to each image's fixed frame. Support mouse and touch interaction.
- Require an event title and calendar date. Derive the displayed weekday and ordinal date from that calendar date. Treat subtitle, start/end times, venue, address/postcode, and call-to-action as optional fields; omit fields that are blank.
- Give each layout a default palette and provide a small shared palette selector. Palette changes apply to typography, panels, and ornaments, not uploaded images.
- Permit toggling selected minor accents only. Keep the composition, image frames, and core brand elements fixed.
- Keep the Kirtan Mellows identity, mantra text, associated marks, and standard footer consistent across templates and not editable by ordinary poster makers.
- Export one format only: square 1080×1080 PNG.
- Do not include a built-in background-image library in the first version. Backgrounds must be uploaded by the poster maker.
- Prefer original layered artwork, fonts, and clean brand assets if they are supplied. Otherwise reconstruct editable layers using the JPEGs as visual references; do not use a flattened reference JPEG as a background because its old text and artwork would remain visible.
- The current workspace contains eight flattened JPEG references: seven are 1080×1080 and one is 1254×1254. No app code, test harness, editable source layers, or separate brand assets are present.
- The design target is close fidelity in composition, typography, branding, and ornamental style. User-selected images and palettes naturally change the overall appearance; pixel-identical output is not promised without clean source assets.

## Testing Decisions

- Use one browser-level end-to-end seam through the public poster editor. Cover the four compositions and desktop and mobile viewports; validate behavior at the user-facing boundary rather than testing internal component structure.
- Exercise required-field validation, automatic weekday/date formatting, omission of blank optional fields, upload of both images, constrained reposition/zoom, palette changes, optional-accent toggles, preview updates, and PNG download.
- Verify the downloaded file is a readable 1080×1080 PNG and that the preview/export reflects the selected event information and images.
- Verify selected image contents are not sent to a server during editing or export.
- Review representative rendered outputs against the reference compositions for visible layout, branding, and typography fidelity. Do not require pixel-for-pixel equality against flattened references when user-supplied images and palettes differ.
- Good tests assert observable results, boundaries, and invariants: missing required fields block export; changing the selected calendar date changes the generated weekday; empty optional fields leave no blank labels; images stay inside their assigned frames; and export has the promised format and dimensions. Tests must not assert framework details, internal state shape, or incidental markup.
- Test the integrated editor and export flow as the highest available seam. The workspace currently has no app modules, test harness, or prior test examples; choose browser automation tooling when the app stack is established.

## Out of Scope

- User accounts, cloud storage, server-side image processing, or shared project saving.
- A built-in background gallery or preset background images in the first version.
- Saving and reopening an editable project file.
- Freeform canvas editing, arbitrary text placement, arbitrary resizing/rotation of elements, or user-uploaded stickers and decorations.
- Editing or removing the core Kirtan Mellows brand elements.
- Arbitrary color pickers or per-element custom colors beyond the curated palettes.
- Non-square, print, portrait, or other export formats.
- Pixel-identical reconstruction of the references when the original layered artwork, fonts, or brand assets are unavailable.

## Further Notes

- The supplied references vary substantially in background imagery and color while retaining a recognizable brand treatment and event-information hierarchy. The four templates therefore model composition, while poster makers supply the imagery and select a curated palette.
- The reference JPEGs are flattened; their event text and brand/art layers cannot be cleanly separated by treating them as editable source files.
- If clean original logos, fonts, or layered designs are available, they are needed to improve fidelity beyond a visual reconstruction.
