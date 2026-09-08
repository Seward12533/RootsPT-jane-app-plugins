---
name: jane-export-patient-list
description: "Export the full Patient List from Jane App (rootsmx.janeapp.com/admin) to Excel for ad hoc analysis."
---

# Export Jane App Patient List to Excel

Use this when the user asks to pull/export the patient list (or "all patients") from Jane App for analysis in Excel. Requires the Claude in Chrome browser tools, with the user's Jane App admin tab already open (or navigate to https://rootsmx.janeapp.com/admin).

## Steps

1. Click **Reports** in the top navigation bar.
2. Under the **Patients** section of the report list, click **Patient List**. Prefer the `find` tool (query: "Patient List report link in left sidebar") over hardcoded coordinates — the Reports menu re-orders itself to show whichever section was last used, so a fixed-coordinate click can land on the wrong report.
3. Wait for the report to load ("Please wait while your request is processed...").
4. Click the **All Patients** dropdown in the filter bar and select **All Patients** (not just Active or Inactive) so the export includes every record.
5. Click the **•••** (more options) icon at the right of the filter bar.
6. Click **Export to Excel**.
7. Jane opens a new browser tab titled "Your file is ready to view or download," showing a generated filename like `ROOTSPhysicalTherapyWellness_Patients_19270908_YYYYMMDD.xlsx` (the leading date is a fixed artifact of Jane's "all patients" range, not something you choose; the trailing `YYYYMMDD` is today's date).
8. On that tab, left-click the **Download XLSX File** button/link. This triggers a normal browser download to the user's default Downloads folder.
9. Open the Downloads folder and rename the downloaded file to `ROOTSPhysicalTherapyWellness_Patients_19270908_LATEST.xlsx`. A fixed "LATEST" filename means anything pointed at this file (dashboards, Excel queries) keeps working after future re-exports without needing an updated path. This session can't do the rename itself unless the `mcp__remote-devices__*` device-bridge tools are present (a linked desktop) — otherwise tell the user this step is needed and let them do it.
10. Copy/paste both this file and the companion Appointment History export (see the `jane-export-appointment-history` skill) into the shared **Roots/Jane Exports** folder on Andrew Seward's OneDrive — either by dragging the local files, or by uploading through [the Roots OneDrive folder link](https://1drv.ms/f/c/616916aab79088e0/IgCQTPV3AudtQaPYAticX-M-AV7MRPi3tqL-pPZF2bpy2xg). **Replace/overwrite** the existing files there rather than adding new copies — if a query or dashboard elsewhere isn't set up to auto-replace, it may need to be updated to point at the new filenames, or pointed instead at the local Downloads (or wherever) copies.
11. Open **Roots_Operations_Dashboard.xlsx** in the Excel desktop app (not a browser) from a Windows PC that has the OneDrive folder mapped as a local drive, so it picks up the newly uploaded data.

## Gotchas

- The download tab sometimes opens outside the Claude-in-Chrome controllable tab group (e.g. after a tab-group refresh). If `tabs_context_mcp` doesn't show a tab with a URL under `/downloads/.../preview`, ask the user to paste that tab's URL so you can navigate to it directly, or ask them to click **Download XLSX File** themselves — right-click "Save link as" is not reliably automatable since native OS context menus aren't visible to the browser tools.
- Downloads don't show a confirmation in the page screenshot (they land in the browser's download bar/Downloads folder, outside the page viewport) — ask the user to confirm the file arrived if uncertain.
- This session cannot open File Explorer/Finder, rename files, browse OneDrive, or open desktop Excel on the user's computer unless the `mcp__remote-devices__*` tools are present (a linked desktop). If they aren't, tell the user which manual step is needed rather than attempting it — never guess at OneDrive/Excel automation through the browser.
