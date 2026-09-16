# Kerim Kfuri — Social Calendar

Local review build based on the approved design. Not published.

## Open the calendar

Serve this folder with a normal static web server and open `index.html`. No framework, package installation, compilation, or build step is required. The HTML embeds its CSS, JavaScript, logo, and photographs. Keep the small icon files and `site.webmanifest` beside it for home-screen installation.

The live calendar is requested directly from the supplied Google Apps Script endpoint on page load and when Refresh is selected. The endpoint redirects to Google’s content host and permits cross-origin reads. Availability is not hardcoded, stored in browser storage, or cached for offline use. While the page stays open, the displayed freshness and elapsed times are recalculated every minute; this is not an automatic network refresh.

## Label decision still awaiting confirmation

The current local build treats the supplied `open` array as the source of availability. `labels[].label` and `labels[].type` are displayed literally, using text nodes, without inferring category, destination, or event meaning. No date is blocked because of a label type. This follows the latest instruction to avoid interpreting types, but differs from the earlier instruction to block travel-labelled days even when open slots exist. The owner was asked to choose between showing supplied openings and blocking all labelled dates. The question remains unresolved at handoff.

Long labels may be shortened visually on compact calendar tiles. Their exact full text and type remain in the date’s accessible name, tooltip, and day-detail panel. Every label is present in the details. The page ignores booking counts and does not expose any other event fields.

## Included behavior

- All 60 consecutive dates are retained. Calendar-week alignment uses nine or ten rows as required.
- Each day opens its complete list of available times in a dialog. Closing returns focus and position to the same date.
- Times keep the feed’s timezone. Day-specific EDT/EST labels follow daylight saving; the page never switches to the visitor’s local timezone.
- Past times on the current feed-timezone date are no longer shown as future openings.
- A missing, invalid, incomplete, or unreachable feed produces an explicit unavailable state. A failed refresh retains the earlier loaded view with a visible warning.
- Source freshness is displayed. After 15 minutes, the page asks for a refresh rather than claiming the snapshot is current.
- Decorative icon motion, photo crossfades, pause control, reduced-motion preference, touch interaction, and keyboard date navigation are included.
- The overview fits when viewport height permits. Short screens, browser chrome, ten-row spans, or enlarged text may require scrolling so dates and controls remain readable.

## Home-screen app assets

The original Dual KK mark is used for:

- 16, 32, and 48 px PNG favicons and a multi-size `favicon.ico`.
- 152, 167, and 180 px Apple touch icons.
- 192 and 512 px app icons, plus a 512 px maskable icon.

The manifest contains the app name, short name, stable relative ID, start URL, scope, theme colour, background colour, and `standalone` display mode. Relative paths allow the whole folder to be hosted under a GitHub Pages project subpath. Apple standalone and title meta tags and viewport safe-area handling are included. The installation button provides a native install prompt when offered, or platform instructions.

These follow [Apple’s home-screen web app guidance](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html) and [web manifest guidance](https://web.dev/articles/add-manifest). Actual phone installation and standalone launch need verification from the eventual hosted HTTPS URL; no phone installation has been performed. There is no offline service worker, so offline availability is not promised.

## Validation and scope

Validated the live JSON response and cross-origin headers, the packaged JavaScript, 366 different 60-day start dates, DST labels and timestamp conversion, malformed feeds, literal labels, icon dimensions, and local asset references. Twelve validation groups pass. The local server returns the page successfully.

The in-app browser could not navigate directly to the Google endpoint (`ERR_BLOCKED_BY_CLIENT`), so the live response was retrieved and validated by an HTTP client after that attempt. An end-to-end interactive browser/phone test has not been completed. Do not claim on-device installation or full browser QA has passed.

Access control is intentionally not implemented, as requested. No repository or deployment was created. The site is an availability viewer only; it cannot book, modify, or write calendar events. The upstream classifier has not been changed. The supplied photographs were not retouched or regenerated.
