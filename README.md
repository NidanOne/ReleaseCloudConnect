# CloudConnect Releases

Signed Windows installers for the ZenControl CloudConnect desktop app.

## Latest release

**v1.0.12** — [`CloudConnect-1.0.12.msi`](CloudConnect-1.0.12.msi)

## Installation

1. Download the `.msi` file above.
2. Run it and follow the installer prompts.
3. Launch **CloudConnect** from the Start menu.

## Changelog

### v1.0.12

- Fix Device/CS/Emergency Issues & Faults showing wrong floor — the floor
  displayed was inherited from the control system, which is incorrect when a
  single CS manages devices across multiple floors. The per-device `floorId`
  now comes from the authoritative `/v2/sites/{siteId}/device-locations`
  endpoint instead of being derived from the CS.
- Widen the Floor column in Device/CS/Emergency Issues & Faults tables
  (+100dp, roughly 10 characters more) so longer floor names fit without
  truncation on desktop.
- Switch typography to bundled Roboto across all text styles on both desktop
  and Android. Desktop previously fell back to the JVM/Skia system sans-serif;
  Android was already using system Roboto. The font is now shipped with the
  app for consistent rendering on every platform.
- Consolidate logging into a new `CloudLog` module. Scattered
  `System.err.println("[CloudAPI] ...")` calls across the infrastructure,
  authentication, and app layers are replaced with concise, consistent
  `CloudLog.request/auth/error/rateLimit` calls. Cuts roughly 1000 lines of
  verbose debug output and quiets normal-operation logs.

### v1.0.11

- Add ZenControl logo branding to PDF report footers.

### v1.0.10

- Remove port 80 default to fix Windows installer permissions.

### v1.0.9

- Fix emergency device tally to use ECGs API.

### v1.0.8

- Fix Android print orientation to match PDF content.

### v1.0.7

- Add logout and retry buttons to site selection empty/error states.

### v1.0.6

- Descriptive PDF filenames, search improvements, pinch-to-zoom floor plan,
  and nav bar fix.

### v1.0.5

- Fix site-change loading bug, floor plan locate dialog, and UI improvements.

### v1.0.4

- Performance optimizations, release build support, and fix Android
  Change Site button.

### v1.0.3

- Brand installer and replace app icon with ZenControl logo.

### v1.0.2

- Remove hardcoded OAuth credentials and encrypt desktop tokens.

### v1.0.1

- Desktop MSI installer, PDF export, and issue detail reports.
