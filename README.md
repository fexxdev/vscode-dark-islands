# Islands Dark

A custom VS Code theme with floating panels, rounded corners, glass borders, a pill-shaped activity bar, and subtle shadows — all built on a dark color palette with 342 workbench colors and 195 syntax scopes.

![Islands Dark Screenshot](assets/CleanShot%202026-02-19%20at%2019.37.59@2x.png)

## Features

- **Color theme** — dark palette with semantic highlighting for TypeScript, Python, Go, Rust, HTML/CSS, Markdown, JSON, YAML, and more
- **Custom CSS layer** — floating panels, rounded corners, glass borders, aurora animations, pill activity bar
- **Bear Sans UI fonts** — custom UI typography (optional, falls back to system sans-serif)

## Requirements

- VS Code **1.77+**
- [Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css) (recommended as an extension pack, installed automatically)

## Install

### Quick install (macOS/Linux)

```bash
git clone https://github.com/raaid3/vscode-dark-islands.git ~/vscode-dark-islands
cd ~/vscode-dark-islands
./install.sh
```

### Quick install (Windows)

```powershell
git clone https://github.com/raaid3/vscode-dark-islands.git $env:USERPROFILE\vscode-dark-islands
cd $env:USERPROFILE\vscode-dark-islands
.\install.ps1
```

### Manual install

1. Clone or download this repo somewhere permanent on your machine.

2. Install the [Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css) extension.

3. Install the `.otf` font files from `fonts/` (optional but recommended).

4. Add these to your VS Code `settings.json`, replacing the path with your actual location:

**macOS/Linux:**
```json
{
  "workbench.colorTheme": "Islands Dark",
  "vscode_custom_css.statusbar": true,
  "vscode_custom_css.imports": [
    "file:///Users/you/vscode-dark-islands/custom-css/islands-dark.css"
  ]
}
```

**Windows:**
```json
{
  "workbench.colorTheme": "Islands Dark",
  "vscode_custom_css.statusbar": true,
  "vscode_custom_css.imports": [
    "file:///C:/Users/you/vscode-dark-islands/custom-css/islands-dark.css"
  ]
}
```

5. Open the Command Palette (`Cmd+Shift+P` / `Ctrl+Shift+P`) and run **Enable Custom CSS and JS**.

6. Restart VS Code when prompted.

### Recommended settings

```json
{
  "editor.fontFamily": "IBM Plex Mono, Consolas, monospace",
  "terminal.integrated.fontFamily": "FiraCode Nerd Font Mono, Consolas, monospace",
  "editor.lineHeight": 1.8,
  "workbench.tree.indent": 16,
  "workbench.tree.renderIndentGuides": "always",
  "editor.minimap.showSlider": "always"
}
```

## The "corrupt installation" warning

VS Code will show a warning that your installation appears corrupt after enabling custom CSS. This is expected — the Custom CSS extension patches VS Code's internal HTML to inject the stylesheet. Click the gear icon on the notification and select **Don't Show Again**. Your installation is fine.

## Updating

After a VS Code update, the CSS patch gets removed. Run **Reload Custom CSS and JS** from the Command Palette and restart to re-apply.

## Uninstall

1. Run **Disable Custom CSS and JS** from the Command Palette.
2. Remove the `vscode_custom_css.imports` entry from your settings.
3. Switch to another color theme.
4. Restart VS Code.

Helper scripts are also available:

```bash
./uninstall.sh        # macOS/Linux
.\uninstall.ps1       # Windows
```

## What's included

```
themes/islands-dark.json     Color theme (342 workbench colors, 60 token rules, 25 semantic tokens)
custom-css/islands-dark.css  Workbench CSS (floating panels, glass borders, animations)
fonts/                       Bear Sans UI font family (.otf)
install.sh / install.ps1     Install helpers
uninstall.sh / uninstall.ps1 Uninstall helpers
```

## License

MIT
