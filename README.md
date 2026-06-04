# CloudConnect Releases

Signed Windows installers for the ZenControl CloudConnect desktop app.

## Latest release

**v1.0.67** — [`CloudConnect-1.0.67.msi`](CloudConnect-1.0.67.msi)

## Installation

1. Download the `.msi` file above.
2. Run it and follow the installer prompts.
3. Launch **Cloud Connect** from the Start menu.

## Changelog

### v1.0.67

- Fix cross-site data contamination when switching sites. On desktop, a race
  between persisting the newly selected site and refreshing the dashboards
  could briefly load the previous site's issues and uncommissioned devices;
  the site is now persisted before the refresh is triggered. On Android, the
  previous site's enrichment maps (floors, tenancies, fitting types, control
  system names) were reused after a switch; they are now cleared.
- Settings "Refresh All" now clears caches for the selected site only —
  other sites' cached data and the global product catalogs are left intact.
  Cached device test results are likewise deleted per-site.
- The Issues heading count now matches the tab counts (distinct affected
  devices, respecting the integrator filter) instead of counting raw issue
  rows, so the heading always equals the sum of the tabs.
- Rename the Emergency tab to "Predictive Maintenance (Beta)".

### v1.0.66

- Name exported PDF reports by site, test type, test name, and test start
  month (e.g. `Site-Emergency_Report-function-Monthly_Test-2026-03.pdf`)
  instead of the generic export date. Embedded PDF document titles match.
- Summary report filenames use the earliest running instance start date.
- New Settings toggle (BETA) to enable the Predictive Maintenance tab,
  persisted per platform.
- Hide the Emergency tab on sites with no emergency devices.
- Richer maintenance predictions: predicted date label, expected life,
  installed years.
- Refetch cached duration tests with incomplete results.
- Rate limiting: wait a full minute when the per-minute quota is exhausted.
- Desktop installer package renamed to "Cloud Connect".

### v1.0.20

- New Predictive Maintenance tab on the Emergency Testing screen uses linear
  regression on historical duration test results to predict when each
  device's battery will fall below the expected pass threshold.
- Predictions sorted by urgency: Critical (<3 months), Caution (3-6),
  Warning (6-12), OK (>12 months).
- No additional API calls — predictions computed from existing cached
  duration test data.

### v1.0.19

- Square corners on all UI elements — cards, buttons, dialogs, badges,
  progress bars, and bar charts all use sharp rectangular corners.
- Override Material3 shapes theme globally for consistent square styling.

### v1.0.17

- Deduplicate retested device tests so only the latest result per device is
  shown in both running and completed test views. Deduplication now groups
  by device address (csIdentifier.deviceIdentifier) instead of
  deviceLocationId for reliable matching across retests.
- Increase ECG endpoint timeout from 30s to 120s to prevent emergency device
  count from failing on large sites.
- Surface test instance load errors to the user instead of silently
  swallowing them.

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
