# home-custom
tabby plugin

> **This plugin is an extended fork of [tabby-home](https://www.npmjs.com/package/tabby-home) by its original author. All core functionality belongs to them — this fork adds extra features on top.**

A connection manager home panel plugin for [Tabby](https://tabby.sh) — organize and manage all your SSH, Telnet, and Serial connections in one place.

## What's new in 1.3.0

- **Move to** — move a host to another group (or out of any group) from the card **⋮** menu. If several hosts are selected and the menu is opened on one of them, all selected hosts are moved.
- **Group colors** — give a group a color from an 8-color palette (Blue, Teal, Red, Amber, Purple, Pink, Green, Gray). The group card gets a colored folder icon and a colored stripe, and its hosts show a colored dot (Recent, search results, MultiExec chips). Colors adapt to light, dark, and colored themes.
- **Copy SSH command with jump host** — for hosts behind a jump host, the copied command now includes `-J` (including multi-hop chains), so it connects the same way the plugin does.
- **Card size restored** — grid cards are at least 280px wide again (as in 1.1.x) and stretch to fill the row; long names and addresses show the full text on hover.

## What's new in 1.2.0

- **No more empty tabs on startup** — Tabby Home no longer leaves a blank tab after restart, and stale empty tabs from previous sessions are cleaned up automatically. Only one Home tab is opened; the toolbar button and hotkey focus it instead of opening a duplicate.
- **Theme-aware colors** — all colors follow the active Tabby color scheme (light, dark, and colored themes like TokyoNight), with readable text, visible card borders, and host icons colored from the theme palette.
- **Checkboxes select hosts for real** — ticking a checkbox adds the host to the same selection used by `Cmd`/`Ctrl+Click` and MultiExec. `Shift+Click` on a checkbox selects a range.
- **Click empty space to clear the selection** — works like the **Cancel** button.
- **Sort order is remembered** — the selected sort mode is saved and restored across groups, Home reopening, and Tabby restarts.
- **Copy SSH command** — now also in the card **⋮** menu (it was previously only in the right-click menu).
- **Recent: Show more / Show less** — expand the Recent section to see up to 10 recent hosts.
- **`Cmd+F` / `Ctrl+F`** — focus the search box.
- **Status tooltips** — hover the status dot to see `online` / `offline` / `checking`.
- **Layout and accessibility** — cards fill the full window width, the header wraps on narrow windows, buttons show a visible keyboard focus ring, and icon buttons have labels.
- **MultiExec** — the **Add host…** field and the **×** remove buttons on host chips are easier to see and click.

## Features

All features from the original [tabby-home](https://www.npmjs.com/package/tabby-home), plus:

- **Multi-selection with keyboard modifiers** — select multiple hosts using `Ctrl+Click` (Windows/Linux), `Cmd+Click` (macOS), or `Shift+Click` for range selection
- **Checkbox selection** — in Selection mode, checkboxes and modifier clicks share one selection, which is exactly what MultiExec, Connect and bulk Edit act on
- **Jump Host support** — connect via a jump host (bastion): pick an existing host or configure one inline
- **Bulk credential editing** — when multiple hosts are selected, update username and/or password across all of them at once
- **Persistent sort order** — your sort choice survives restarts
- **Move to** — move one or several hosts to a group from the **⋮** menu
- **Group colors** — palette colors for groups, with a matching dot on their hosts
- **Copy SSH command** — a ready-to-paste `ssh` command, including `-J` for jump hosts
- **Theme-aware UI** — adapts to any Tabby color scheme

---

### Original features

- **Connection panel** — opens automatically on startup as a home tab
- **Groups** — organize hosts into color-coded groups with nested navigation
- **Smart search** — filter by name, host, username, tag, group, or connection type using query syntax
- **Sort** — sort by default order, alphabetical name, or most recently connected
- **Grid / List view** — toggle between card grid and compact list layout
- **Connection status** — ping all hosts to check online/offline status at a glance
- **Selection mode** — select multiple hosts to open tabs or launch MultiExec
- **MultiExec** — broadcast keystrokes to multiple SSH sessions simultaneously in a split-pane view
- **Drag & drop** — reorder hosts, move them between groups, or drop them into a MultiExec tab
- **Import / Export** — backup and restore connections as JSON
- **Hotkey** — configurable keyboard shortcut to jump to the connection panel
- **Vault integration** — credentials (password, private key, passphrase) stored securely in Tabby's vault

## Installation

Inside Tabby, go to **Settings → Plugins**, search for `tabby-home-custom`, then click **Install**.

Or install manually:

```bash
# Windows
cd %APPDATA%\tabby\plugins
npm install tabby-home-custom

# macOS
cd ~/Library/Application\ Support/tabby/plugins
npm install tabby-home-custom

# Linux
cd ~/.config/tabby/plugins
npm install tabby-home-custom
```

Restart Tabby after installation.

## Usage

### Selecting hosts

Use keyboard modifiers while clicking hosts to build a selection:

| Action | Behavior |
|--------|----------|
| `Ctrl + Click` *(Windows/Linux)* / `Cmd + Click` *(macOS)* | Toggle a single host in or out of the selection |
| `Shift + Click` | Select a range between the last selected host and the clicked host |
| Click a checkbox *(Selection mode)* | Toggle the host — same as `Ctrl`/`Cmd + Click` |
| `Shift + Click` a checkbox | Select a range — same as `Shift + Click` on a card |
| Click empty space | Clear the selection (same as **Cancel**) |
| `Ctrl/Cmd + A` | Select all hosts in the current view |
| `Enter` | Connect to the selected hosts |
| `Delete` | Delete the selected hosts |
| `Esc` | Clear the selection |

Checked checkboxes, highlighted cards, and the hosts passed to MultiExec are always the same set.

### Card menu and right-click menu

- **⋮ menu** on a host card: Connect, Duplicate, Copy SSH command, Move to, Edit, Delete
- **⋮ menu** on a group card: Color, Edit, Delete
- **Right-click** a host (or a selection): Connect, Open tabs, Export, Copy SSH command, Edit / Bulk edit, Duplicate, Delete

### Move to

Open **⋮** on a host card → **Move to** and pick a group (sorted alphabetically), or **No group** to move the host out of its group. The current group is marked and disabled.

- If several hosts are selected and you open **⋮** on one of them, all selected hosts are moved (the menu shows the count, e.g. *Move to (3)*).
- If you open **⋮** on a host that is not selected, only that host is moved.

Group counters and the open list update immediately, and the selection is cleared. Drag & drop and the group field in the host editor still work as before.

### Group colors

Open **⋮** on a group card → **Color** (or **Edit** on the group) and pick one of 8 palette colors, or **No color**:

- the group card gets a colored folder icon and a 3px colored stripe on the left;
- hosts of that group show a colored dot next to their name in **Recent**, search results, and MultiExec chips — hover the dot to see the group name.

Groups without a color look exactly as before. The color is stored as a palette key (e.g. `blue`), and the shade adapts to the current Tabby theme.

### Copy SSH command

Copies a ready-to-paste command, for example:

```bash
ssh user@10.1.2.230
ssh admin@db.example.com -p 2222
ssh -J jump@bastion.corp:2200 user@10.1.2.230
```

- Hosts behind a jump host get `-J` with the full chain (`-J 'hop1,hop2'` for multiple hops), matching how the plugin connects.
- Credentials are not included — `ssh` uses your own keys / agent or asks for a password.

### Jump Host

Open **New Host** or **Edit** on a host and set **Connection Type** to **Via Jump Host**:

- **Select existing jump host** — pick another host from your list as the bastion
- **Create inline jump host config** — enter the jump host address, port, username, and auth type directly

The jump host is used transparently when connecting, and it is included as `-J` in **Copy SSH command**.

### Bulk Credential Editing

1. Select two or more hosts (via Selection mode or keyboard modifiers)
2. Click **Edit** in the Hosts toolbar (tooltip: *Edit credentials for selected hosts*), or right-click → **Bulk edit**
3. Enter a **username** and/or **password** — only non-empty fields are applied; other values stay untouched

### Sorting

Click the sort button in the header to cycle through **Default → Name → Recent first**. The choice applies to the Hosts list and to hosts inside groups, and it is saved in Tabby's config. The **Recent** section is always ordered by last connection.

### Keyboard shortcuts in the panel

| Shortcut | Action |
|----------|--------|
| `Cmd + F` / `Ctrl + F` | Focus the search box |
| `↑` / `↓` + `Enter` in search | Pick a search result and connect |
| `Backspace` / mouse back button | Leave the current group |

## Search Query Syntax

Type in the search box to filter hosts. Supports:

| Syntax | Description |
|--------|-------------|
| `type:ssh` | Filter SSH connections |
| `type:telnet` | Filter Telnet connections |
| `type:serial` | Filter Serial connections |
| `name:web` | Filter by host name |
| `user:admin` | Filter by username |
| `tag:prod` | Filter by tag |
| `group:dc1` | Filter by group name |
| `web && prod` | Match ALL terms (AND) |
| `web \|\| db` | Match ANY term (OR) |

Type `/` at the end of your query to show the suggestion dropdown.

## MultiExec

MultiExec lets you work on multiple servers at the same time:

1. Open the connection panel → click **Select** → tick hosts (or use `Cmd`/`Ctrl`/`Shift + Click`) → click **MultiExec**
2. Or drag a host card and drop it into an open MultiExec tab
3. Or use the **Add host…** field in the MultiExec bar to add another host

In the MultiExec tab, click the **broadcast bar** and type — keystrokes are sent to all targeted panes at once. Use the host chips in the **Broadcast** row to toggle targets, **All** / **None** to select or clear them, and **×** on a chip to remove that host.

## Hotkey

Go to **Settings → Hotkeys** and assign a shortcut to **Tabby Home: Open** (`connection-manager-open`) to quickly switch back to the home panel from any tab.

## Credits

Based on [tabby-home](https://www.npmjs.com/package/tabby-home) — all core features and architecture are from the original plugin. This fork only extends it with additional functionality.

## License

MIT
