# TerraPULSE# TerraPULSE (Binary Releases) — Parameter Update Listing for Schema Evolution

---
![Platform](https://img.shields.io/badge/Platform-Windows-0078d4?logo=windows)
![Purpose](https://img.shields.io/badge/Terraform-Parameter%20Update%20Listing-7b42bc?logo=terraform)
![Terraform Docs](https://img.shields.io/badge/Terraform-Documentation-7b42bc?logo=terraform)
![Built with Nuitka](https://img.shields.io/badge/Built%20with-Nuitka-blue)
![PySide6](https://img.shields.io/badge/UI-PySide6-green)
![Maintained](https://img.shields.io/badge/Maintained-yes-green)
![Free to use](https://img.shields.io/badge/Free%20to%20use-yes-brightgreen)
---
![GitHub release](https://img.shields.io/github/v/release/Bilak-co-uk/TerraPULSE)
![GitHub downloads](https://img.shields.io/github/downloads/Bilak-co-uk/TerraPULSE/total)


TerraPULSE automates the tedious part of Terraform provider upgrades: finding exactly which resource arguments changed, were removed, renamed, or deprecated between two versions. Instead of reading through changelogs and raw markdown, you get a colour-coded diff table in seconds.

---

## Table of Contents

- [Three Comparison Modes](#three-comparison-modes)
- [Application Layout](#application-layout)
- [On-Demand Compare](#on-demand-compare)
- [Full Cache Compare](#full-cache-compare)
- [Local Scan](#local-scan)
- [GitHub Authentication](#github-authentication)
- [Understanding Results](#understanding-results)
- [Filtering, Sorting & Exporting](#filtering-sorting--exporting)
- [Parse Options](#parse-options)
- [Cache & Settings](#cache--settings)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Troubleshooting](#troubleshooting)

---

## Three Comparison Modes

| Mode | Best For |
|------|----------|
| 🟡 **On-Demand Compare** | Download and compare one specific resource directly from the Terraform Registry — no full download needed |
| 🔵 **Full Cache Compare** | Download an entire tagged release from GitHub, cache it permanently, compare any resource offline |
| 🟢 **Local Scan** | Compare two local documentation folders already on disk |

**What you get in every mode:**
- Colour-coded change table (removed, added, renamed…)
- Side-by-side markdown diff with word-level highlighting
- Parsed parameters view for both versions
- Standalone rendered document view
- CSV & Markdown export

---

## Application Layout

The window has two areas: the **Input Sources panel** on the left (select what to compare) and the **Results panel** on the right (see what changed).


<img width="1728" height="231" alt="layout" src="https://github.com/user-attachments/assets/0808b129-37da-4ec1-965a-5582826371d2" />



> **Tip:** Click the **◀** collapse arrow at the top-right of the Input Sources panel to hide it and maximise the results area. Click again to restore.

---

## On-Demand Compare

Download and compare one specific resource directly from the Terraform Registry. Best when you only need to check a particular resource quickly without downloading an entire release.


<img width="1728" height="958" alt="guide_od" src="https://github.com/user-attachments/assets/0e2cf877-121f-4399-8dd4-88c95909061a" />



### Step 1 Provider Repository

Select a provider from the dropdown (or type a custom `owner/repo` path such as `hashicorp/terraform-provider-azurerm`), then click **Load Provider**. Collapse Step 1 by clicking its header once loaded.

### Step 2 Select Versions

Choose **Version A** (your current version) and **Version B** (the version you are upgrading to). Use **Swap** to reverse them. Click **Load Versions** to fetch the resource list.

The summary shows how many resources are:
- **Matched** resource exists in both versions
- **Retired** resource only exists in Version A
- **Brand New** resource only exists in Version B

### Step 3 Select & Compare

Filter the resource list using **Search**, **Type**, or **Status**. Smart search is active — typing `logic app` finds `azurerm_logic_app_standard` automatically.

**Double-click** a resource to download and compare it immediately.
- 🟢 Brand New resources open in the Standalone Document viewer
- 🔴 Retired resources open in the Standalone Document viewer
- All others open the full side-by-side diff

> **Smart search:** Spaces, dashes, and underscores are treated the same, and provider prefixes like `azurerm_` are stripped automatically. Works on all three tabs.

---

## Full Cache Compare

Download a complete tagged release from GitHub, cache it permanently, then compare any resource instantly even when offline. Best for providers you compare regularly or when you need to browse many resources.


<img width="1728" height="959" alt="guide_fd" src="https://github.com/user-attachments/assets/8d404ed1-000d-4cee-ba40-821e128f760a" />



### Step 1 Select Provider Repository

Choose a provider from the dropdown or type a custom `owner/repo` path, then click **Load Tags**. TerraPULSE fetches the full release tag list via the GitHub API.

### Step 2 Choose Two Versions & Download

Select **Version A** (current) and **Version B** (new). The coloured dots show cache status:

| Dot | Meaning |
|-----|---------|
| 🟢 Green | Fully cached — ready for offline use |
| 🟡 Amber | Partially cached |
| ⚫ Grey | Not yet downloaded |

Click **Download & Cache Versions**. Downloads run 24 connections in parallel — typically under 30 seconds. Once cached, all comparisons are instant and work fully offline.

### Step 3 Browse, Filter & Open

After downloading, TerraPULSE automatically compares every matched resource pair in the background and colour-codes the results:

- 🟡 **Amber** Changed (resource has parameter differences)
- 🟢 **Green** Brand New (only exists in Version B)
- 🔴 **Red** Retired (only exists in Version A)

Filter by Search, Type, or Status (including **Changed** to see only resources with differences). **Double-click** any resource to open the full comparison.

> **Offline mode:** Once a version is fully cached (🟢 green), all comparisons read from disk with zero network calls.

---

## Local Scan

Compare two local copies of a provider's documentation — for example two cloned versions of a GitHub repo or two unzipped release archives already on your machine.


<img width="1728" height="960" alt="guide_ls" src="https://github.com/user-attachments/assets/9e4eff7a-727b-463c-b29b-158a13bc1622" />



### Step 1 Select Folders (or Files)

**Browse** for the current version folder and the new version folder. Use **Swap** to reverse current and new. You can also compare two individual `.md` files instead of whole folders.

TerraPULSE automatically finds the docs folder regardless of how deep it is nested — just point it at the repo root or any parent folder and it will locate the `r/`, `d/`, `resources/`, `data-sources/`, `ephemeral-resources/` and `list-resources/` subdirs automatically. You can also point it directly at a flat folder of `.md` files.

**Non-standard folder names:** If your folders do not follow the expected naming, TerraPULSE will still compare them as long as the same folder name exists in both versions. The resource type is inferred from each file's heading (`# Resource name`, `# Data Source: ...`, `# Ephemeral: ...`, `# List Resource: ...`). Folders that only exist on one side will be reported as retired or brand new.

### Step 2 Scan & Load Resources

Click **Scan & Load Resources**. A progress bar shows two phases:
1. Scanning the filesystem to match resources
2. Analysing every matched pair for changes

The resource list appears only when both phases are complete, with all statuses already coloured. If any non-standard folder names are detected a warning will list which folders were affected.

### Step 3 Browse & Open

Filter by **Search**, **Type** (Resource / Data Source / Ephemeral / List Resource), or **Status** (Matched / Changed / Retired / Brand New).

**Double-click** any resource to open it:
- Retired and Brand New resources → Standalone Document viewer
- Changed and Matched resources → side-by-side diff

---

## GitHub Authentication

### Why you need a token

GitHub allows **60 API requests/hour** without authentication. Loading a large provider easily exceeds this. With a Personal Access Token the limit rises to **5,000/hour**.

### Token security

- Encrypted with **Windows DPAPI** — tied to your Windows account
- Stored in `%APPDATA%\terrapulse` — never in plain text
- Only your Windows account can decrypt it
- Never logged or sent anywhere except GitHub API calls

### Setup

**Step 1 Create a token**
Go to [github.com/settings/tokens/new](https://github.com/settings/tokens/new), create a **classic** token. No scopes are required — leave all checkboxes unticked.

**Step 2 Add it to TerraPULSE**
Go to **Settings → GitHub Token** in the menu bar, paste the token and click **Save Token**. The token is validated immediately.

**Step 3 Done**
The token persists across sessions. Remove it via **Settings → GitHub Token → Remove Token** at any time.

---

## Understanding Results

### Change Type Colours

| Colour | Type | Meaning |
|--------|------|---------|
| 🔴 Red | **Removed** | Parameter no longer exists in the new version |
| 🟢 Green | **Added** | New parameter available in the new version |
| 🟡 Yellow | **Changed** | Requirement status changed (Required / Optional / Computed) |
| 🔵 Blue | **Renamed** | Parameter was renamed |
| 🟣 Purple | **Moved** | Parameter moved to a different block |
| 🟠 Orange | **Type Changed** | Inferred data type changed |
| 🟤 Tan | **Description Changed** | Description text was updated |
| ⚫ Grey | **Deprecated** | Deprecation notice added or changed |
| 🟡 Amber | **Resource Deprecated** | Entire resource is marked as deprecated |
| 🔵 Steel Blue | **Superseded** | Resource replaced by a newer resource |

### Results Tabs

#### Changed Parameters
Sortable, filterable table of all detected changes. Click any column header to sort. Use the text filter to search across all columns. Right-click a row to copy, filter by value, or jump directly to that location in the diff view.

#### Side-by-Side View
Raw markdown with line-level and **word-level** diff highlighting. Both panes scroll synchronised. Each pane has an independent search bar with next/previous navigation.

#### Parsed Parameters
The extracted parameter data for both versions shown side by side — useful for verifying that TerraPULSE parsed the document structure correctly.

#### Standalone Document
Fully rendered markdown with syntax highlighting, Terraform callout boxes, and clickable parameter pill-links. Right-click to copy the full document or only the parameter section.

### Badge Dashboard

Coloured count badges above the table show totals per change type. Click any badge to filter the table to that type only. Click **All** to reset.

---

## Filtering, Sorting & Exporting

| Action | How to do it |
|--------|-------------|
| Sort the table | Click any column header — arrow shows current direction |
| Filter by text | Type in the filter box above the table — searches all columns at once |
| Filter by change type | Use the type dropdown next to the filter box |
| Clear filter | `Escape` — first press clears the filter, second press clears all results |
| Export as CSV | `Ctrl+E` or **File → Export CSV** |
| Export as Markdown | `Ctrl+Shift+E` or **File → Export MD** |
| Copy to clipboard | **Edit → Copy Results** — tab-separated, pastes directly into Excel |
| Re-run last comparison | `Ctrl+R` or `F5` |

---

## Parse Options

### Parse Attributes Reference (Outputs)

Also parse the **Attributes Reference** / **Exports** section (read-only computed outputs), not just the Arguments Reference. Enable this if you need to track output changes.

### Detect Deprecation

Scan parameter descriptions for deprecation markers (`Deprecated:`, `Will be removed`…) and report them as a separate change type.

---

## Cache & Settings

**Settings → Clear Cache…** opens a dialog with per-category checkboxes:

| Cache | Contents |
|-------|----------|
| **Registry Cache** | Per-resource `.md` files and tree index `.json` files downloaded by the **On-Demand Compare** tab. Deleted files are re-downloaded automatically on demand. |
| **GitHub Versions Cache** | Complete tag folders used by **Full Cache Compare**, including pre-computed changed-resource lists. Location: `%APPDATA%\TerraPULSE\cache\versions` |

> ⚠️ Your GitHub token is **never** affected by any cache clear option.

### Auto Update

**Settings → Check for Updates on Startup** enables automatic update checks at launch. Use **Help → Check for Updates** to check manually. Choose **Update Now** or **Skip** — the installer downloads silently, closes TerraPULSE, and relaunches automatically.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+O` | Browse for current version file (Local Scan — file mode) |
| `Ctrl+Shift+O` | Browse for new version file (Local Scan — file mode) |
| `Ctrl+R` / `F5` | Re-run last comparison |
| `Ctrl+E` | Export results as CSV |
| `Ctrl+Shift+E` | Export results as Markdown |
| `Escape` | Clear filter (first press) / Clear all results (second press) |

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Rate limit exceeded | Configure a GitHub token — see [GitHub Authentication](#github-authentication) above |
| Can't find a resource | Type the name *without* the provider prefix: `windows_virtual_machine` not `azurerm_windows_virtual_machine` |
| Results seem incomplete | Check the file has an **Argument Reference** section. Enable **Parse Attributes** if outputs are missing. |
| Download slow (Full Cache Compare) | Add a GitHub token — unauthenticated requests are throttled server-side regardless of connection speed |
| Changed list empty after scan | The change analysis runs after scanning finishes. Wait for the progress bar to reach 100% before filtering by Changed. |
| Window size wrong on startup | Resize normally and close — the new size saves automatically. |

---

*TerraPULSE — Terraform Parameter Update Listing for Schema Evolution*
