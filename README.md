# Arrival Email Generator

Web tool for travel agents to prepare the new-member arrival email for The Grand Ho Tram.

- Fill in guest name, date of birth and arrival date/time (multiple guests supported)
- Preview the table, then send (opens the default mail app, table copied to clipboard)
- Download the table as a PNG image
- Representative Code is saved in the browser after first use

Current version: v1.08

Single static file (`index.html`), no build step. Host with GitHub Pages.

## Changelog

### v1.07

- **The subject now carries the first guest's name**, e.g.
  `VIE1040 Nguyen Van A new member on 13-Nov`.
- **Guest names are capitalised as you type**, so a name entered as
  `nguyen van a` becomes `NGUYEN VAN A` straight away. The caret stays where
  it was.

### v1.06

- **Dates now use English month names.** In the table and the clipboard the
  date of birth and the arrival date read `02-Nov-2026`; the subject uses the
  short form `13-Nov`.
- When several arrival dates are involved the subject lists them all, e.g.
  `VIE1040 new member on 13-Nov, 25-Dec`.

### v1.05

- **The mail body no longer repeats the guest details.** Opening the mail client
  now carries only a short greeting; the table is pasted from the clipboard
  instead, so it is not duplicated as plain text.
- The clipboard still holds the table twice: HTML for rich mail clients and a
  plain-text rendering as a fallback for clients that ignore HTML.
- The manual send panel shows the guest rows so they can be copied into
  WeChat or any other app.

### v1.04

- **Guests are now grouped.** Each arriving party gets its own boxed section
  with a numbered header (客人 1, 客人 2, ...).
- **The arrival date and time belong to the group**, so they are entered once
  and every guest in that group shares them.
- Adding a group creates a new box that **inherits the arrival date and time
  from the group above it**.
- "+ 再加一位客人" adds another guest inside the current group, for parties
  that arrive together.
- Validation messages now name the group (第 2 组) and, when a group has more
  than one guest, the guest within it.

### v1.03

- **Arrival date goes back to the native date picker.** The day / month / year
  boxes are now used for the date of birth only; the arrival date uses the
  browser's calendar control again.
- The arrival date picker is limited to today through one year from now.
- The table still shows both dates as dd/mm/yyyy.

### v1.02

- **Date inputs rebuilt**: day / month / year are three separate boxes instead of a
  native date picker. Digits only (typing and pasting), auto-advance to the next
  box, Enter moves on as well.
- **Real calendar validation**: month must be 1-12, the day must exist in that
  month for that year (leap years included), the year must be between 1900 and
  the current year + 10, and a date of birth cannot be today or in the future.
  Invalid fields turn red and show the reason underneath.
- **Preview lists every problem** instead of one generic message, and each guest
  is identified by position.
- **Fixed "send email" doing nothing**: the mailto: link no longer opens in a
  new tab (in-app browsers and mobile Chrome silently discarded it). Browsers
  without mailto: support (WeChat, DingTalk, QQ, Android without a mail app)
  now get a manual send panel with the text selected and a copy button.
- Arrival dates use the same component inputs.

### v1.01

- First release: guest rows, table preview, mailto: send with clipboard copy,
  PNG table download, representative code stored in the browser.
