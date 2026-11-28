# Arrival Email Generator

*Known as the **agent project**.*

Web tool for travel agents to prepare the new-member arrival email for The Grand Ho Tram.

- Fill in guest name, date of birth and arrival date/time (multiple guests supported)
- Guests arriving together share one group, so the arrival date and time are entered once
- Chinese, English and Vietnamese, switchable in the top right corner
- Preview the table, then send (opens the default mail app, table copied to clipboard)
- Download the table as a PNG image
- Representative Code is saved in the browser after first use

Current version: v1.25

Single static file (`index.html`), no build step. Host with GitHub Pages.

## Changelog

### v1.25

- **An AI side project library** was added. It lists projects that can earn
  money, with the region, the effort, the tools and the time to the first
  order for each one. The curated entries were checked by hand. A collector
  watches a set of feeds and puts new leads in a queue that waits for a
  review, and it runs on its own once a day.

### v1.24

- **The usage reporting is protected.** The server now checks a token before
  it accepts a report, and it allows at most thirty reports a minute from
  one address. A report over the limit is removed again straight away, so a
  flood cannot fill the database.

### v1.23

- **The recent records are paged.** The list shows ten rows at a time with
  previous and next buttons, and the row range and the total count sit
  between them. The paging happens on the server, so every row stays
  reachable no matter how many there are.

### v1.22

- **The refresh button on the dashboard works now.** The request asks for a
  fresh answer instead of reusing a cached one, the server sends a
  no-store header, and the button shows that it is working while it runs.

### v1.21

- The "统计已上报" note and the "诊断" button were removed from the page.
  The reporting itself is unchanged, and the dashboard still shows the cross
  check between the client side and the server side counts.

### v1.20

- **A second, independent counter.** The page reports the view to a separate
  endpoint that counts on the server, so the numbers do not depend on the
  page script at all.
- **The dashboard cross checks the two counts.** The client side figure and
  the server side figure sit next to each other with the gap between them
  and a coverage percentage. Any gap is usage the client side reporting
  missed.
- The server side count also gives the country and the referrer.

### v1.19

- **An action is no longer counted twice.** The report is sent with a plain
  fetch only, and the server ignores a repeat of the same device, event and
  guest count inside the same minute.
- **Every page open is counted as a visit**, not just the first one in a
  browser session.

### v1.18

- **Reports now go to every known address at once**, so one blocked host
  cannot swallow the statistics.
- **A "诊断" button in the footer** checks which reporting address answers
  and shows the result and the response time for each one.

### v1.17

- **The page now shows whether the usage report was delivered.** A small
  line in the footer reads "统计已上报" when the report reached the server,
  or "统计未送达" with the reason when it did not, so a broken report is
  visible instead of silent.

### v1.16

- **Fixed the usage reporting.** A dead host in the address list swallowed
  every report: a beacon sent to a name that does not resolve is dropped
  without an error. Only reachable addresses are listed now, and a plain
  fetch follows the beacon so a report is never lost silently.

### v1.15

- **Page visits are counted.** A visit is recorded once per browser session,
  separately from the generate and send actions.
- **The dashboard shows the total visit count** and the number of devices that
  have visited.
- **Week and month summaries** are shown as cards, with the start date, the
  action count, the people count, the device count and the number of devices
  that actually sent an email.
- Weekly and monthly history tables were added next to the daily trend.

### v1.14

- **Usage statistics.** Every preview and every send is reported to a small
  Cloudflare Worker backed by a D1 database. The record holds the device
  model plus a short random id kept in the browser, the interface language,
  the representative code, and the number of guests and groups. Reporting is
  fire-and-forget and never affects the tool.
- **The dashboard is a separate page**, `stats.html`. It asks for the admin
  password and then shows the totals, a 30 day trend, the split by interface
  language, the split by event, a row per device and the recent log.
- The reporting host is probed at load time, so the page keeps working if one
  of the two addresses is unreachable.

### v1.13

- The usage report is sent as a simple request, so no CORS preflight is
  needed and the report is not dropped by networks that block preflights.

### v1.12

- The reporting endpoint and the statistics dashboard were first added.

### v1.11

- **The generated email keeps its original English format** whichever
  interface language is selected. The subject still reads
  `VIE1040 Nguyen Van A new member on 13-Nov` and the body still opens with
  `Dear HTR team,`.
- The table header is fixed as well: English on top, Vietnamese underneath.
- Only the interface is translated.

### v1.10

- **Three languages.** Chinese (default), English and Vietnamese, with a
  switch in the top right corner. The choice is remembered in the browser.
- The whole interface is translated: labels, buttons, notes, group numbers,
  the day/month/year units and every validation message.
- **The generated email follows the language too**: the greeting, the subject
  wording and the table headers. The guest details the user types are not
  translated.
- The table header shows the second language on a second line only when it
  differs, so the Vietnamese version does not repeat the same words twice.

### v1.09

- The project is referred to as the **agent project** from now on.

### v1.08

- Name capitalisation simplified: guest names are typed in pinyin, so plain
  upper casing is enough.

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

### v1.01

- First release: guest rows, table preview, mailto: send with clipboard copy,
  PNG table download, representative code stored in the browser.
