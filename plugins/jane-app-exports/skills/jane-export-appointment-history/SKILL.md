---
name: jane-export-appointment-history
description: "Export Appointment History over a custom date range from Jane App (rootsmx.janeapp.com/admin) to Excel for ad hoc analysis."
---

# Export Jane App Appointment History to Excel

Use this when the user asks to pull/export appointment history from Jane App for analysis in Excel. Requires the Claude in Chrome browser tools, with the user's Jane App admin tab already open (or navigate to https://rootsmx.janeapp.com/admin).

## Steps

1. Click **Reports** in the top navigation bar.
2. Under the **Appointments** section of the report list, click **Appointments**. Prefer the `find` tool over hardcoded coordinates — the Reports menu re-orders to show whichever section was last active.
3. The Appointments Report loads with filters for Locations, Staff Members, Date Range, States, and Chart Statuses.
4. Click the **Date Range** dropdown to open the calendar picker (shows two side-by-side months with back `←` and forward `→` arrows — there is no direct type-in date field).
5. To set a start date in a past month: click the back arrow repeatedly until the desired month appears in the left calendar. Going back roughly N months takes N clicks — e.g. ~67 clicks to go from September 2026 back to January 2021. Batch these clicks (e.g. via `browser_batch`) rather than one at a time.
6. Click the specific start date (e.g. "1" for the 1st). The picker retains this as the range start even while you navigate the calendar elsewhere.
7. Click the forward arrow the same number of times to return to the current month.
8. Click the end date (typically today) to complete the range. The filter bar should now read something like "Jan 1, 2021 - Sep 8, 2026".
9. Wait for the report to (re)load — for multi-year ranges this can return thousands of rows.
10. Click the **•••** (more options) icon at the right of the filter bar.
11. Click **Export to Excel**.
12. Jane opens a new tab and processes the export ("Please wait while your request is processed..." — can take a minute or two for large ranges).
13. Once ready, the tab is titled "Your file is ready to view or download" showing a filename like `ROOTSPhysicalTherapyWellness_Appointments_<start>_<end>.xlsx`.
14. Left-click the **Download XLSX File** button/link to save it to the user's Downloads folder.
15. Open the Downloads folder and rename the file to `ROOTSPhysicalTherapyWellness_Appointments_<start>_LATEST.xlsx` (e.g. `..._20210101_LATEST.xlsx`). A fixed "LATEST" filename means anything pointed at this file (dashboards, Excel queries) keeps working after future re-exports. This session can't do the rename itself unless the `mcp__remote-devices__*` device-bridge tools are present (a linked desktop) — otherwise tell the user this step is needed and let them do it.
16. Copy/paste both this file and the companion Patient List export (see the `jane-export-patient-list` skill) into the shared **Roots/Jane Exports** folder on Andrew Seward's OneDrive — either by dragging the local files, or by uploading through the Roots OneDrive folder link **Replace/overwrite** the existing files there rather than adding new copies — if a query or dashboard elsewhere isn't set up to auto-replace, it may need to be updated to point at the new filenames, or pointed instead at the local Downloads (or wherever) copies.
17. Open **Roots_Operations_Dashboard.xlsx** in the Excel desktop app (not a browser) from a Windows PC that has the OneDrive folder mapped as a local drive, so it picks up the newly uploaded data.

## Gotchas

- The download tab can open outside the Claude-in-Chrome controllable tab group (e.g. after a tab-group refresh). If `tabs_context_mcp` doesn't show a tab with a URL under `/downloads/.../preview`, ask the user for that tab's URL or have them click **Download XLSX File** themselves.
- Right-click "Save link as" is not reliably automatable — native OS context menus don't render in browser screenshots. A plain left-click download (to the default Downloads location) is the reliable path.
- Downloads don't show a confirmation in the page screenshot — confirm with the user if uncertain.
- This session cannot open File Explorer/Finder, rename files, browse OneDrive, or open desktop Excel on the user's computer unless the `mcp__remote-devices__*` tools are present (a linked desktop). If they aren't, tell the user which manual step is needed rather than attempting it — never guess at OneDrive/Excel automation through the browser.
