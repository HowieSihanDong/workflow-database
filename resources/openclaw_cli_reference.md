# Openclaw CLI Quick Reference

*All commands accept `--browser-profile <name>` to target a specific profile. All commands also accept `--json` for machine-readable output.*

## 1. Basics
```bash
openclaw browser status
openclaw browser start
openclaw browser stop
openclaw browser tabs
openclaw browser tab
openclaw browser tab new
openclaw browser tab select 2
openclaw browser tab close 2
openclaw browser open https://example.com
openclaw browser focus abcd1234
openclaw browser close abcd1234
```

## 2. Inspection (Snapshots & Analysis)
```bash
openclaw browser screenshot
openclaw browser screenshot --full-page
openclaw browser screenshot --ref 12
openclaw browser screenshot --ref e12
openclaw browser snapshot
openclaw browser snapshot --format aria --limit 200
openclaw browser snapshot --interactive --compact --depth 6
openclaw browser snapshot --efficient
openclaw browser snapshot --labels
openclaw browser snapshot --selector "#main" --interactive
openclaw browser snapshot --frame "iframe#main" --interactive
openclaw browser snapshot --interactive 2>/dev/null | grep -E "^\- (button|link|textbox|menuitem|tab|slider|radio)"
openclaw browser console --level error
openclaw browser errors --clear
openclaw browser requests --filter api --clear
openclaw browser pdf
openclaw browser responsebody "**/api" --max-chars 5000
```

## 3. Actions
```bash
openclaw browser navigate https://example.com
openclaw browser resize 1280 720
openclaw browser click 12 --double
openclaw browser click e12 --double
openclaw browser type 23 "hello" --submit
openclaw browser press Enter
openclaw browser hover 44
openclaw browser scrollintoview e12
openclaw browser drag 10 11
openclaw browser select 9 OptionA OptionB
openclaw browser download e12 report.pdf
openclaw browser waitfordownload report.pdf
openclaw browser upload /tmp/openclaw/uploads/file.pdf
openclaw browser fill --fields '[{"ref":"1","type":"text","value":"Ada"}]'
openclaw browser dialog --accept
openclaw browser wait --text "Done"
openclaw browser wait "#main" --url "**/dash" --load networkidle --fn "window.ready===true"
openclaw browser evaluate --fn '(el) => el.textContent' --ref 7
openclaw browser highlight e12
openclaw browser trace start
openclaw browser trace stop
```

## 4. State & Environment
```bash
openclaw browser cookies
openclaw browser cookies set session abc123 --url "https://example.com"
openclaw browser cookies clear
openclaw browser storage local get
openclaw browser storage local set theme dark
openclaw browser storage session clear
openclaw browser set offline on
openclaw browser set headers --headers-json '{"X-Debug":"1"}'
openclaw browser set credentials user pass
openclaw browser set credentials --clear
openclaw browser set geo 37.7749 -122.4194 --origin "https://example.com"
openclaw browser set geo --clear
openclaw browser set media dark
openclaw browser set timezone America/New_York
openclaw browser set locale en-US
openclaw browser set device "iPhone 14"
```

## 5. Wait Power-ups
Wait on more than just time/text:
```bash
openclaw browser wait --url "**/dash"
openclaw browser wait --load networkidle
openclaw browser wait --fn "window.ready===true"
openclaw browser wait "#main"
```

## 6. Snapshots and Refs Behavior
- **AI Snapshot** (`--format ai`): Uses numeric refs (`12`).
- **Role Snapshot** (`--interactive`, `--compact`, `--depth`): Uses role refs (`e12`).
- *Refs are not stable across navigations.* Re-run snapshot if an action fails to get fresh refs.

## 7. Debug Workflows
1. `openclaw browser snapshot --interactive`
2. Run action (`click <ref> / type <ref>`)
3. If it fails, use `openclaw browser highlight <ref>` to see target
4. If page behaves oddly:
   `openclaw browser errors --clear`
   `openclaw browser requests --filter api --clear`
5. Deep debugging: `openclaw browser trace start` -> reproduce -> `openclaw browser trace stop`
